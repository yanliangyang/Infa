#####**Requirement：**
###### 1、Jenkins、SonarQube Installed
###### 2、SonarQube jenkins plugin installed

##### **Do：**
###### 1、 add build step "Execute SonarQube Scanner"
![add sonarqube scanner step](https://github.com/yanliangyang/Infa/blob/master/image/2016-08-03_151326.png)

###### 2、set "Analysis properties" below this
<pre><code>sonar.projectKey=YYL::ALL
sonar.projectName=YYL::ALL
sonar.projectVersion=1.0
sonar.sources=.
sonar.java.binaries=target/classes
sonar.jacoco.reportPath=target/coverage-reports/jacoco-ut.exec
sonar.jacoco.itReportPath=target/coverage-reports/jacoco-it.exec
</code></pre>

###### *3、if u want know what the Parameters mean, pls see* [Analysis+Parameters](http://docs.sonarqube.org/display/SONAR/Analysis+Parameters "Analysis+Parameters").
`sonar.jacoco.reportPath`:Set the property to the path of the JaCoCo UT coverage report.
`sonar.jacoco.itReportPath`:The path to the pre-generated JaCoCo IT coverage report.

##### **Result:**
###### 1、It will show the UT and IT Coverage Report on Sonarqube
![sonarqube show ut and it coverage report](https://github.com/yanliangyang/Infa/blob/master/image/2016-08-05_155733.png) 