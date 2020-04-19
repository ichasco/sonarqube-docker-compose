Sonarqube
==========

Setup
------
Create `.env` file and add values


```
cp .env.sample .env
```

Start container

```
docker-compose up
```

Add branch plugin
-------------------


```
wget https://github.com/mc1arke/sonarqube-community-branch-plugin/files/4396080/sonarqube-community-branch-plugin-1.4.0-SNAPSHOT.jar.zip
docker cp sonarqube-community-branch-plugin-1.4.0-SNAPSHOT.jar.zip sonarqube:/opt/sonarqube/extensions/plugins/
docker cp sonarqube-community-branch-plugin-1.4.0-SNAPSHOT.jar.zip sonarqube:/opt/sonarqube/lib/common/
docker restart sonarqube
```

Add to Gitlab CI
-------------------

In the `.gitlab-ci.yml`

```
code_quality:
  stage: code_quality
  image:
    name: sonarsource/sonar-scanner-cli:latest
    entrypoint: [""]
  variables:
    GIT_DEPTH: 0
    SONAR_HOST_URL: https://sonar.example.com
    SONAR_TOKEN: <SECRET_TOKEN>
  allow_failure: true
  script:
    - sonar-scanner
      -Dsonar.qualitygate.wait=true
      -Dsonar.projectKey=${CI_PROJECT_ID}
      -Dsonar.projectName=${CI_PROJECT_TITLE}
      -Dsonar.branch.name=${CI_COMMIT_REF_NAME}
      -Dsonar.projectVersion=${CI_COMMIT_TAG}
      -Dsonar.sourceEncoding=UTF-8
      -Dsonar.sources=./
      -Dsonar.links.ci=${CI_PROJECT_URL}/pipelines
      -Dsonar.links.homepage=${CI_PROJECT_URL}
  only:
    - merge_requests
    - master
```

