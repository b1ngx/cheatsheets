# Elasticsearch


## 安装

- [Install Elasticsearch with .zip or .tar.gz](https://www.elastic.co/guide/en/elasticsearch/reference/current/zip-targz.html)
- [Configuring system settings](https://www.elastic.co/guide/en/elasticsearch/reference/current/setting-system-settings.html)

Running as a daemon

```
./bin/elasticsearch -d -p pid
```

Shutdown

```
kill `cat pid`
```

Elasticsearch 不能以 `root` 权限运行，先添加组和用户，然后赋予权限

```
useradd es
chown -R  es:es /home/es/elasticsearch-6.1.2
```

配置文件 `config/elasticsearch.yml


## 语法

#### 搜索

```
GET _search
{
  "query": {
    "match_all": {}
  }
}

```

#### 索引

```
# 查看索引
GET _all
GET _settings
GET toutiao
GET toutiao/_settings

# 创建索引
PUT toutiao

# 修改索引
PUT toutiao/_settings
{
   "number_of_replicas": 2
}

# 删除索引
DELETE toutiao
```

#### 文档
```
# 保存文档
PUT toutiao/article/1
{
  "title":"关于对河南省企业研发费用财政补助审核结果的公示",
  "site": "zznet",
  "site_name": "郑州科技局",
  "publish_date": "2017-12-15"
}

# 修改文档
POST toutiao/article/1/_update
{
  "doc": {
    "site_name": "科技局"
  }
}

# 查看文档
GET toutiao/article/1
GET toutiao/article/1?_source=title,site

# 删除文档
DELETE toutiao/article/1
```

## 插件

[elasticsearch-head](https://github.com/mobz/elasticsearch-head) 需要修改 `elasticsearch.yml` 配置

```
network.host: 0.0.0.0
http.cors.enabled: true
http.cors.allow-origin: "*"
```

[elasticsearch-analysis-ik](https://github.com/medcl/elasticsearch-analysis-ik)

如果没有对应的版本，可尝试 `pom.xml` 文件，例如下载的是 6.1.1 版本，修改为 6.1.2 版本

```
<properties>
    <elasticsearch.version>6.1.2</elasticsearch.version>
    ...       
</properties>
```

