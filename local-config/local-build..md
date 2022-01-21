### Follow these steps, you will make it.
- VM Options
```shell
-Des.path.conf=/Users/andyni/dev/projects/andy/es_home/config
-Des.path.home=/Users/andyni/dev/projects/andy/es_home
-Dlog4j2.disable.jmx=true
-Djava.security.policy=/Users/andyni/dev/projects/andy/es_home/config/java.policy
```

- Add java.policy file in config directory
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