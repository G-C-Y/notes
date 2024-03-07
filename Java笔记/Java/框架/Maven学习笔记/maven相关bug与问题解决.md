## maven导入不成功刷新没用的时候
更新代码之后有了新的包，导致项目无法启动成功，排查问题过程中maven有个包能查到但是无法导入，刚开始采用网上传统的办法，刷新maven之后在lifestyle之下clean install，没有用。然后把不正常模块下生成的.iml文件删除掉重新生成，但是maven总是更新到一般就自动停止。 查了很多大部分是说 刷新一下Maven Project就会自动生成.iml文件但是我试了几次后还是不可以。下载同事项目启动了，所以我就在想应该是idea项目配置的原因导致项目无法启动。
然后就查了一些关于idea的问题  历经苦难 知道了一些 maven idea的命令。

生成.ipr文件: mvn idea:project
生成.iws文件: mvn idea:workspace
生成.iml文件: mvn idea:module
在项目模块目录下执行   mvn idea:module  问题完美解决！！！
## springboot项目启动失败，加载不到类
maven 设置中，Runner选项里面去掉Delegate IDE build/run actions to Maven选项。
项目启动失败的原因找到了：不要随便改pom文件
 
