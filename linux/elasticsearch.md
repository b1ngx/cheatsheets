# Elasticsearch


## 安装

#### 手动安装

[Install Elasticsearch with .zip or .tar.gz](https://www.elastic.co/guide/en/elasticsearch/reference/current/zip-targz.html)

下载最新包

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.1.2.tar.gz
tar -xzf elasticsearch-6.1.2.tar.gz
cd elasticsearch-6.1.2/
```

由于 Elasticsearch 不能以 `root` 权限运行，先添加用户组，然后赋予权限

```
useradd es
chown -R  es:es /home/es/elasticsearch-6.1.2

chown -R elasticsearch:elasticsearch /var/lib/elasticsearch
```

运行 Running as a daemon

```
su es
cd $ES_HOME
./bin/elasticsearch -d -p pid
```

Shutdown

```
kill `cat pid`
```

配置文件位置 `$ES_HOME/config/elasticsearch.yml`

运行中的系统参数设置参照 [Configuring system settings](https://www.elastic.co/guide/en/elasticsearch/reference/current/setting-system-settings.html) 进行配置

#### RPM 安装

导入 PGP key

```
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```
配置 RPM 源

```
[elasticsearch-6.x]
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```
安装

```
yum install elasticsearch
```

通过 `systemd` 运行

```
systemctl daemon-reload
systemctl enable elasticsearch
systemctl start/stop/status elasticsearch
```

配置文件位置

```
/etc/elasticsearch
```

$ES_HOME 位置在

```
/usr/share/elasticsearch
```

## 语法

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

#### 搜索

```
# 返回 20 条结果
GET _search
{
  "query": {
    "match_all": {}
  },
  "from": 0,
  "size": 20
}

# match 查询，对关键词分词，并进行大小写转换
GET toutiao/_search
{
  "query": {
    "match": {
      "title": "大数据 "
    }
  }
}

# term 查询，完全匹配，不做大小写转换
#GET toutiao/_search
{
  "query": {
    "term": {
      "site_name": "河南科技网"
    }
  }
}

# terms 多个关键字查询
GET toutiao/_search
{
  "query": {
    "terms": {
      "title": ["河南", "企业"]
    }
  }
}

# 短语查询，满足所有词，并指定词间的最大距离
GET toutiao/_search
{
  "query": {
    "match_phrase": {
      "title": {
        "query": "河南企业",
        "slop": 6
      }
    }
  }
}

# 多字段查询
GET toutiao/_search
{
  "query": {
    "multi_match": {
      "query": "河南企业",
      "fields": ["title", "site_name"]
    }
  }
}

# 指定返回的字段
GET toutiao/doc/_search
{
  "stored_fields": ["site_name", "url_fingerprint"],
  "query": {
    "match": {
      "title": "大数据 "
    }
  }
}

# 排序
GET toutiao/doc/_search
{
  "query": {
    "match": {
      "title": "大数据 "
    }
  },
  "sort": [{ "publish_date": { "order": "desc" } }]
}

# 范围查询
GET toutiao/_search
{
  "query": { 
    "range": { "publish_date": { "gte": "2017-01-23" } } 
  }
}

# bool查询，must, filter, should, must_not
"bool": {
  "must": [],
  "filter": [],  
  "should": [],
  "must_not": []
}

# bool 组合查询
GET toutiao/_search
{
  "query": {
    "bool": {
      "filter": [
        { "range": { "publish_date": { "gte": "2017-01-23" } } }
      ],
      "must": [{ "match": { "title": "大数据" } }]
    }
  },
  "sort": [{ "publish_date": { "order": "desc" } }]
}
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





