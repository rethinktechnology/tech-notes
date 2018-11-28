#### Different types of classloader
```
Bootstrap ClassLoader (native one, we can't see from java APIs like ClassLoder.getSystemClassLoader())
      |
Extension ClassLoader (ClassLoader.getSystemClassLoader() returns this as always)
      |
App/System ClassLoader (YourClass.class.getClassLoader())
```


#### Getting jars loaded from application/system classloader

    URLClassLoader urlClassLoader = (URLClassLoader) Main.class.getClassLoader().getParent();
		Arrays.stream(urlClassLoader.getURLs())
			.forEach(System.out::println);

#### Trying to see the amount memory taken in classloader based on the jar/zip files loaded in JVM's classloader
		long sum = Arrays.stream(urlClassLoader.getURLs())
			.map(url -> {
				try {
					return Paths.get(url.toURI());
				} catch (URISyntaxException e1) {
					return null;
				}
			})
			.map(path -> {
				try {
					long size = Files.size(path);
					System.out.println(size + " : " + path);
					return size;
				} catch (IOException e) {
					return 0L;
				}
			}).reduce(0L, Long::sum);
		float jarSize = (float)sum/(8 * 1024 * 1024);
		System.out.println("Size : " + jarSize);
    
#### Trying to load Spring API and see what classes loaded in JVM's Classloader
		AnnotationConfigApplicationContext springConfigContext = new AnnotationConfigApplicationContext(SpringConfig.class);
		try {
			Field f = ClassLoader.class.getDeclaredField("classes");
			f.setAccessible(true);

			ClassLoader cl = Thread.currentThread().getContextClassLoader();
			Vector<Class> classes =  (Vector<Class>) f.get(cl);
			classes.forEach(System.out::println);
		} catch (NoSuchFieldException | SecurityException | IllegalArgumentException | IllegalAccessException e) {
			e.printStackTrace();
		}
