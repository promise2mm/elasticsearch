### Follow these steps, you will make it.
- Gradle
  - choose the right version of gradle and java version
  - setting repository mirror(`$GRADLE_HOME/init.d/init.gradle`)
  ```shell
    allprojects{
        repositories {
            def ALIYUN_REPOSITORY_URL = 'https://maven.aliyun.com/repository/public/'
            def ALIYUN_GRADLE_PLUGIN_URL = 'https://maven.aliyun.com/repository/gradle-plugin/'
            all { ArtifactRepository repo ->
                if(repo instanceof MavenArtifactRepository){
                    def url = repo.url.toString()
                    if (url.startsWith('https://repo1.maven.org/maven2/')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                        remove repo
                    }
                    if (url.startsWith('https://jcenter.bintray.com/')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_REPOSITORY_URL."
                        remove repo
                    }
                    if (url.startsWith('https://plugins.gradle.org/m2/')) {
                        project.logger.lifecycle "Repository ${repo.url} replaced by $ALIYUN_GRADLE_PLUGIN_URL."
                        remove repo
                    }
                }
            }
            maven { url ALIYUN_REPOSITORY_URL }
            maven { url ALIYUN_GRADLE_PLUGIN_URL }
        }
  } 
  ```
- VM Options
```shell
-Des.path.conf=/Users/andyni/dev/elasticsearch-6.2.3/elasticsearch-6.2.3-single/config
-Des.path.home=/Users/andyni/dev/elasticsearch-6.2.3/elasticsearch-6.2.3-single
-Dlog4j2.disable.jmx=true
-Didea.no.launcher=true
-Djava.security.policy=/Library/Java/JavaVirtualMachines/jdk-9.0.4.jdk/Contents/Home/conf/security/java.policy
```

- Add java.policy file in config directory
  - (or your system java security config file: `/Library/Java/JavaVirtualMachines/jdk-9.0.4.jdk/Contents/Home/conf/security/java.policy`)
```shell
grant {
    permission java.lang.RuntimePermission "createClassLoader";
};
```

- Copy es modules(download a specific .zip release version and unzip.) to `es_home`
  - get from here: https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.2.3.zip
  - or get it from [huaweicloud](https://repo.huaweicloud.com/elasticsearch/6.2.3/elasticsearch-6.2.3.tar.gz)

- Add dependencies with "provided" scope to classpath
<img src="https://cdn.jsdelivr.net/gh/promise2mm/pics/yiming/md/20220121011043.png" style="zoom:30%;" />

- You may modify the current version in `org.elasticsearch.Version.CURRENT` if you met some problems like:
  - `plugin version is not compatible with Elasticsearch`
