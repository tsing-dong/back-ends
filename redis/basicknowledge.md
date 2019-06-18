# redis 数据库基础知识

## 1. redis 分布式事物锁 之 setnx:

     设置 key对应的值为 string类型的 value。 如果key 已经存在，返回 0，nx 是not exist 的意思。

        // 使用redis做分布式锁定
        String redisLookKey = "order:createtborder:" + entity.getMobileNum();
        String redisLookValue = "create_tborder_" + System.currentTimeMillis();
        try {
        // 添加锁
            while (RedisUtil.setnx(redisLookKey, redisLookValue, 5) == 0) {
                log.debug("创建团建游精确询价添加分布式锁失败:" + redisLookKey + ":" + redisLookValue);
                Thread.sleep(50);
            }
            log.debug("创建团建游精确询价添加分布式锁成功:" + redisLookKey + ":"redisLookValue);
            // 创建团建游模糊询价
            return tbHelper.createTeambuildingOrder(entity, header, userId);
        } catch (InterruptedException e) {
            log.error("睡眠失败", e);
        } finally {
            // 释放锁
            String redisValue = RedisUtil.get(redisLookKey);
            if (redisValue != null && redisValue.equals(redisLookValue)) {
                RedisUtil.del(redisLookKey);
                log.debug("释放询价分布式锁:" + redisLookKey + ":" + redisValue);
            }
        }
        return null;

