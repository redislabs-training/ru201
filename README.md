# Redis University RU201, RediSearch

## Course Retired

**This course has been retired, and replaced with RU203, Querying, Indexing, and Full-Text Search.  [Sign up for RU203](https://university.redislabs.com/courses/ru203/).**

---

## Introduction

This repo contains the sample data and Node.js load script for RU201, [RediSearch](https://university.redislabs.com/courses/ru201/) at [Redis University](https://university.redislabs.com/).

## Setup

### Redis

* You will need to [download and install Redis](https://redis.io/download).  Use version 5.0.3 or higher.
* You will also need to [download and install RediSearch](https://oss.redislabs.com/redisearch/Quick_Start/).  Use version 1.4.2 or higher.

### Node.js

To install the script that loads the sample data into RediSearch, you'll need `npm` and Node.js 8.11+. To get the dependencies use:

```
$ npm install
```

in this directory.

## Configuration

First, you will need to create a simple JSON file for your connection credentials. This connection file is based on the node_redis config object allowing you specify host, password, port, etc. In the most basic configuration you would have just these:

```
{
  "host"  : "localhost",
  "port"  : 6379
}
```

Remember: don't commit your copy of this file to your fork of this repo if it contains sensitive credentials.

## Running

The `index.js` script will create the schema and database for you from a CSV file (provided). 

When running you'll need to specify:

- `source` **Required.** _The CSV file which will be ingested. `General_Building_Permits.csv` is included_
- `connection` **Required.** _The path to your configuration file._
- `drop` **Optional.** _This will drop the existing permits schema._
- `totaldocs` **Optional.** _This will give you an accurate progress bar. The provided CSV has 121,828 docs_

Example:

```
$ node index.js --source ./General_Building_Permits.csv --connection ./connection.json --drop --totaldocs 121828
```

The output should look something like this:

```
Created index. Starting ingest.
Ingested: 121828 documents.
Ingested 121828 documents in 15 seconds. Average rate 8122 docs/sec.
```

## Confirmation

You can check you have the right data by trying the following search from the redis-cli

```
127.0.0.1:6379> ft.search permits garage limit 0 0
1) (integer) 49488
```

## Data

The data file provided (`General_Building_Permits.csv`) is pulled from the [Edmonton Open Data Portal](https://data.edmonton.ca) and is the [General Building Permits](https://data.edmonton.ca/Sustainable-Development/General-Building-Permits/24uj-dj8v) dataset pulled on May 16, 2018. This dataset is frequently updated, however we've frozen the data set in this course to provided a consistent course experience. 

### Subscribe to our YouTube Channel

We'd love for you to [check out our YouTube channel](https://youtube.com/redislabs), and subscribe if you want to see more Redis videos!
