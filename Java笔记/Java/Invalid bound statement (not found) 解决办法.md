**网上已经有很多文章说明可能导致这个报错的原因，无非是以下几种：**
1.检查xml文件的namespace是否正确
2.Mapper.java的方法在Mapper.xml中没有，然后执行Mapper的方法会报此
3.xxxMapper.java的方法返回值是List,而select元素没有正确配置ResultMap,或者只配置ResultType
4.如果你确认没有以上问题,请任意修改下对应的xml文件,比如删除一个空行,保存.问题解决
5.看下mapper的XML配置路径是否正确

**如果全部检查了一遍，还发现没有问题，最好看下自己的配置文件，那时候很有可能是配置少了扫描mapper的东西：**
在创建SqlSessionFactory的时候，加了以下配置：
sqlSessionFactoryBean.setMapperLocations(new PathMatchingResourcePatternResolver().getResources("classpath:mapper/*.xml"));
sqlSessionFactoryBean.setTypeAliasesPackage("com.thingshub.ifactory.tmom.entity");
而且注意sqlSessionFactoryBean.setTypeAliasesPackage参数不支持通配符*,如果有多个包可以通过","等分割
如果需要加载依赖传递过来的jar包中的mapper目录下的xml，classpath:mapper/*.xml 修改为classpath*:mapper/*.xml
![image.png](https://images.cherryfloris.eu.org/2022/1648455722907-edfcdf48-a146-451a-96a3-987676a22748.png)

