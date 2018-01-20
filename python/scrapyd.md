# Deploy scrapy

## scrapy.cfg

```
[deploy]
url = http://192.168.1.243:6801/
project = toutiao
```

## scrapyd

> It provides a server with HTTP API, capable of running and monitoring Scrapy spiders.

安装

```
pip install scrapyd
```

运行服务

```
scrapyd
```

执行爬虫

```
curl http://192.168.1.243:6801/schedule.json -d project=toutiao -d spider=hnpatent
```

## scrapyd-deploy

> To deploy spiders to Scrapyd, you can use the scrapyd-deploy tool provided by the [scrapyd-client](https://github.com/scrapy/scrapyd-client) package.

```
scrapyd-deploy
```

If you have more than one target to deploy, you can deploy your project in all targets with one command:

```
scrapyd-deploy -a -p <project>
```

scrapyd 只是爬虫服务，通过 scrapyd-deploy deploy your project to a Scrapyd server.




