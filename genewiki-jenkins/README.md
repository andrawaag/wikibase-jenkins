# genewiki-jenkins
These are tools for setting up a Jenkins instance for running Wikibase bots and associated tools

**Dockerfile**

Pulls the default jenkins:lts image, installs the recommended plugins (plugins.txt), plus several others we need.
Then it installs python3 and several python packages. Then copies over two example jobs

Build using:
`docker build -t genewiki-jenkins .`

Run using:
`docker run -p 8080:8080 -p 50000:50000 genewiki-jenkins:latest`

**docker-compose.yml**

This is the ([wikibase-docker](https://github.com/wmde/wikibase-docker)) [docker-compose file](https://raw.githubusercontent.com/wmde/wikibase-docker/master/docker-compose.yml),
with the customized jenkins image and volume.


### Notes

**To create backup**

`docker run --rm --volumes-from genewiki-jenkins_jenkins_1 -v $(pwd):/backup ubuntu tar cvf /backup/backup.tar /var/jenkins_home`

**Building the jenkins jobs**

I made them manually, and then copy over the config.xml files using

```
docker cp 575fb6ef3fe7:/var/jenkins_home/jobs/Disease_Ontology_Trigger/config.xml jenkins_home/jobs/Disease_Ontology_Trigger/
docker cp 575fb6ef3fe7:/var/jenkins_home/jobs/Disease_Ontology/config.xml jenkins_home/jobs/Disease_Ontology/
```
