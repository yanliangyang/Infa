单元测试：
测试用例目录：src/test/java
测试用例资源目录：src/test/resources
测试用例名称格式：*Test.java
Maven执行插件：surefire
用例框架：junit


接口测试：
测试用例目录：src/integration-test/java
测试用例资源目录：src/integration-test/resources
测试用例名称格式：IT*.java
Maven执行插件：failsafe
用例框架：junit


用例执行命令标准格式：
单元测试：mvn clean test
接口测试：mvn clean verify -P integration-test
单元测试+接口测试：mvn clean verify -P all-tests


PS：
1、因为我们的接口测试单独运行在某个服务器上，需要取到服务数据的话，请修改工程样例的POM文件
<!--
Prepares the property pointing to the JaCoCo runtime agent which
is passed as VM argument when Maven the Failsafe plugin is executed.
-->
<execution>
<id>pre-integration-test</id>
<phase>pre-integration-test</phase>
<goals>
	<goal>prepare-agent</goal>
</goals>
<configuration>
	<!-- Sets the path to the file which contains the execution data. -->
	<destFile>${jacoco.it.execution.data.file}</destFile>
	<!--
		Sets the name of the property containing the settings
		for JaCoCo runtime agent.
	-->
	<propertyName>failsafeArgLine</propertyName>
</configuration>
</execution>


修改为：
<!--
Prepares the property pointing to the JaCoCo runtime agent which
is passed as VM argument when Maven the Failsafe plugin is executed.
-->
<execution>
<id>pre-integration-test</id>
<phase>pre-integration-test</phase>
<goals>
	<goal>dump</goal>
</goals>
<configuration>
	<!-- Sets the path to the file which contains the execution data. -->
	<destFile>${jacoco.it.execution.data.file}</destFile>
	<!--
		Sets the address for JaCoCo runtime agent where the service run.
	-->
	<address>172.27.20.26</address>
</configuration>
</execution>

同时删除maven-failsafe-plugin插件的configuration下面的<argLine>${failsafeArgLine}</argLine>


2、集成测试运行规则，不允许用例失败，如果用例失败，会导致任务失败，如果需要调试，请添加控制项(maven-failsafe-plugin插件的configuration下面)
<testFailureIgnore>true</testFailureIgnore>

