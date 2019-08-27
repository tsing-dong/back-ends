# 1. 即使对象属性的值为null 也不会报错:
```java
    @Test
	public void function01() {
		User u1 = new User();
		u1.setId(1L);
		u1.setName("用户1");
		u1.setAge(20);

		User u2 = new User();
		u2.setId(2L);
		u2.setAge(30);

		List<User> list = new ArrayList<User>();
		list.add(u1);
		list.add(u2);

		// 如果 name 没值也不会报错
		for (User user : list) {
			Optional<User> u = Optional.ofNullable(user);
			System.out.println(u.map(User::getName).orElse("其他值"));
		}
	}
```

# 2. 将对象中符合条件的数据过滤出来:
```java
    @Test
	public void function02() {
		User u1 = new User();
		u1.setId(1L);
		u1.setName("用户1");
		u1.setAge(20);

		User u2 = new User();
		u2.setId(2L);
		u2.setAge(30);

		List<User> list = new ArrayList<User>();
		list.add(u1);
		list.add(u2);

		// 将 name 中包含 1 的过滤出来
		for (User user : list) {
			Optional<User> result = Optional.ofNullable(user)
					.filter(u -> u.getName() != null && u.getName().contains("1"));
			System.out.println(result.get());
		}
	}

```