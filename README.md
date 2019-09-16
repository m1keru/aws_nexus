# MVN:
* Copy dot_m2 to ~/.m2/settings.xml
* Run 
```bash
mvn dependency:get  -DgroupId=org.apache.commons -DartifactId=commons-lang3 -Dversion=3.6 -Dtransitive=false
```
OR 
```bash
mvn dependency:get -DremoteRepositories=http://localhost:8081/repository/maven-public -DgroupId=org.apache.commons -DartifactId=commons-lang3 -Dversion=3.6 -Dtransitive=false
```

![SCHEMA](https://github.com/mtiurin-ias/awsdevops/raw/master/custom_stack-designer.png)

