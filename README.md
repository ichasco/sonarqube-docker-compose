https://github.com/gabrie-allaigre/sonar-gitlab-plugin

git clone https://github.com/andrejpetras/sonarqube-community-branch-plugin.git
git checkout sonarqube82
docker run -it --rm -v $PWD:/home/gradle gradle:jdk11 bash
./gradlew assemble
./gradlew check
gradle build


mv sonarqube-community-branch-plugin/build/libs/sonarqube-community-branch-plugin-1.4.0-SNAPSHOT.jar .



https://github.com/mc1arke/sonarqube-community-branch-plugin/files/4396080/sonarqube-community-branch-plugin-1.4.0-SNAPSHOT.jar.zip

Copiar el plugin en:
extensions/plugins/
lib/common/