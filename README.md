<p align="center">
  <img title="Redash" src='https://redash.io/assets/images/logo.png' width="200px"/>
</p>

[![Documentation](https://img.shields.io/badge/docs-redash.io/help-brightgreen.svg)](https://redash.io/help/)
[![Datree](https://s3.amazonaws.com/catalog.static.datree.io/datree-badge-20px.svg)](https://datree.io/?src=badge)
![Build Status](https://circleci.com/gh/getredash/redash.png?circle-token=8a695aa5ec2cbfa89b48c275aea298318016f040)

**_Redash_** is our take on freeing the data within our company in a way that will better fit our culture and usage patterns.

Prior to **_Redash_**, we tried to use traditional BI suites and discovered a set of bloated, technically challenged and slow tools/flows. What we were looking for was a more hacker'ish way to look at data, so we built one.

**_Redash_** was built to allow fast and easy access to billions of records, that we process and collect using Amazon Redshift ("petabyte scale data warehouse" that "speaks" PostgreSQL).
Today **_Redash_** has support for querying multiple databases, including: Redshift, Google BigQuery, PostgreSQL, MySQL, Graphite, Presto, Google Spreadsheets, Cloudera Impala, Hive and custom scripts.

**_Redash_** consists of two parts:

1. **Query Editor**: think of [JS Fiddle](https://jsfiddle.net) for SQL queries. It's your way to share data in the organization in an open way, by sharing both the dataset and the query that generated it. This way everyone can peer review not only the resulting dataset but also the process that generated it. Also it's possible to fork it and generate new datasets and reach new insights.
2. **Visualizations and Dashboards**: once you have a dataset, you can create different visualizations out of it, and then combine several visualizations into a single dashboard. Currently Redash supports charts, pivot table, cohorts and [more](https://redash.io/help/user-guide/visualizations/visualization-types).

<img src="https://raw.githubusercontent.com/getredash/website/8e820cd02c73a8ddf4f946a9d293c54fd3fb08b9/website/_assets/images/redash-anim.gif" width="80%"/>

## Getting Started

* [Setting up Redash instance](https://redash.io/help/open-source/setup) (includes links to ready made AWS/GCE images).
* [Documentation](https://redash.io/help/).

## Supported Data Sources

Redash supports more than 35 [data sources](https://redash.io/help/data-sources/supported-data-sources). 

## Getting Help

* Issues: https://github.com/getredash/redash/issues
* Discussion Forum: https://discuss.redash.io/

## Reporting Bugs and Contributing Code

* Want to report a bug or request a feature? Please open [an issue](https://github.com/getredash/redash/issues/new).
* Want to help us build **_Redash_**? Fork the project, edit in a [dev environment](https://redash.io/help-onpremise/dev/guide.html), and make a pull request. We need all the help we can get!

## Security

Please email security@redash.io to report any security vulnerabilities. We will acknowledge receipt of your vulnerability and strive to send you regular updates about our progress. If you're curious about the status of your disclosure please feel free to email us again. If you want to encrypt your disclosure email, you can use [this PGP key](https://keybase.io/arikfr/key.asc).

## License

BSD-2-Clause.

# python3版本Fork

这个版本只是修改了其后天,从python2.7迁移到了python3,依赖在:

+ requirements-run.txt 运行需要的依赖
+ requirements-else.txt hive,mysql,influxdb,elasticsearch相关的依赖

## 外部依赖

需要pg 10以上和redis,默认的数据库连接为:postgresql://postgres:123123@localhost/redash和redis://localhost:6379/0

## 前端部分编译

+ npm install
+ npm run build

结果会在client/dist中

## 后端部分

+ 使用虚拟环境

```
python -m venv env

env/bin/python -m pip install -r requirements-run.txt
env/bin/python -m pip install -r requirements-else.txt
```

+ 初始化数据库
```
env/bin/python manage.py database create-tables
```

+ 启动worker和scheduler

```
bash entrypoint worker
bash entrypoint scheduler
```
+ 测试环境使用manage.py启动服务

```
env/bin/python manage.py run
```
在端口5000启动

+ 正式启动

```
bash entrypoint server
```
在端口8222启动


## 已知的bug

+ celery[有一处bug](https://github.com/celery/celery/pull/5500/files)会引起无法识别错误,可以按这个pr来修改
+ csv/excel文件下载默认文件名是bytes的字符串