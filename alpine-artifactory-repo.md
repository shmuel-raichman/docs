# B"H
# Setup
To create alpine repo in artifactory there is a need of using a plugin that make it possible.
More info here: https://www.jfrog.com/jira/browse/RTFACT-9985
Download the groovy script: `expireFilesMetadata.groovy`
From here:
https://github.com/jfrog/artifactory-user-plugins/tree/master/metadata/expireFilesMetadata
Create a file named: `expireFilesMetadata.json'
```json
{
    "repositories": {
        "alpine-remote": {
            "delay": 600,
            "patterns": ["**/*/APKINDEX*.tar.gz"]
        }
    }
}
```
Artifactory HOME: 
The default configs are located in: `/etc/opt/jfrog/artifactory/default`
Opening that file shows ARTIFACTORY_HOME is `/var/opt/jfrog/artifactory`
https://stackoverflow.com/questions/39839342/where-is-artifactory-home-directory


Reload plugins:  
```bash
curl -X POST -I -u {username}:{password} http://${artifactory-host}:${port}/artifactory/api/plugins/reload
```
here are API doc: https://www.jfrog.com/confluence/display/RTF/Artifactory+REST+API#ArtifactoryRESTAPI-ReloadPlugins


In alpine:
```bash
sed -i -e 's/http:\/\/dl-cdn\.alpinelinux\.org/http:\/\/${artifactory-host}:${port}\/artifactory\/alpine-remote/g' /etc/apk/repositories

apk update
apk add {your_package}
```


APK UPDATE ISSUE
https://unix.stackexchange.com/questions/478182/alpine-linux-ignoring-apkindex-bad-file-descriptor
```bash
rm -rf /var/cache/apk
mkdir /var/cache/apk
```
