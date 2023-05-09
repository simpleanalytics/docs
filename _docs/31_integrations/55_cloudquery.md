---
title: Export Simple Analytics Data to a Database or Data Warehouse with CloudQuery
menu: CloudQuery
category: integrations
permalink: /export-to-data-warehouse-with-cloudquery
created_at: 2023-02-22
last_modified_at: 2023-02-22
---

## Introduction

This guide will show you how to export Simple Analytics data to your own database, data warehouse or data lake using [CloudQuery](https://www.cloudquery.io/). CloudQuery is an open source ELT platform that can load Simple Analytics data and send it to dozens of different destinations, including PostgreSQL, SQLite, BigQuery, S3, Snowflake, and [many more](https://www.cloudquery.io/docs/plugins/destinations/overview). With your data exported, you can then do more advanced analysis or use the data in other systems.

We will show you how to export your Simple Analytics data with two examples:

1.  a [SQLite database](#example-1-exporting-to-sqlite),
2.  a [BigQuery Data Warehouse](#example-2-exporting-to-bigquery) running on Google Cloud.

This should give you the general idea for any supported database, data warehouse or data lake. The same steps can applied with slight modifications for any other destination supported by CloudQuery. Authentication steps specific to each destination are documented in the CloudQuery documentation for the destination.

## Prerequisites

To follow along with the examples, you will need:

- a Simple Analytics API key and user ID. You can create a key in your [account settings](https://simpleanalytics.com/account). The user ID is also shown there.
- the CloudQuery CLI installed. CloudQuery is distributed as a cross-platform CLI tool, with pre-built binaries for different platforms. You can follow the installation instructions for your desired platform on the CloudQuery website by following the links below:
  - [MacOS](https://www.cloudquery.io/docs/quickstart/macOS)
  - [Linux](https://www.cloudquery.io/docs/quickstart/linux)
  - [Windows](https://www.cloudquery.io/docs/quickstart/windows)

When the installation is complete, you should be able to run the `cloudquery --help` command in your terminal and see information about the available commands.

## Example 1: Exporting to SQLite

The CloudQuery CLI uses configuration files to define the data sources and destinations. In this example, we will create configuration files that sync Simple Analytics data to a local SQLite database.

### Step 1. Create the Source Configuration File

First, let's create a source configuration file named `simpleanalytics.yml` with the following contents:

```yaml
kind: source
spec:
  name: "simpleanalytics"
  path: "simpleanalytics/simpleanalytics"
  version: "v1.0.0"
  tables: ["*"]
  destinations:
    - "sqlite"
  spec:
    # plugin spec section
    user_id: "${SA_USER_ID}"
    api_key: "${SA_API_KEY}"
    period: 7d
    websites:
      - hostname: <your-website.com>
        # metadata_fields: 
          # - fieldname_text
          # - fieldname_int
          # - ... 
```

This configuration file defines a source named `simpleanalytics` that will sync data from Simple Analytics to a SQLite database. You can find the latest `version` on the [releases page](https://github.com/simpleanalytics/cq-source-simpleanalytics/releases).

The inner plugin spec section defines the configuration specific to the Simple Analytics plugin. Here are a few of the highlights:

- The `user_id` and `api_key` values are set to environment variables, which we will set in the next step.
- The `period` value defines the time period for which data will be synced. We chose `7d` here to fetch only the last 7 days, but you can also choose `1m` for the last month, `1y` for the last year, and so on, or omit this setting to fetch all your historical data.
- The `websites` section defines the websites for which data will be synced. You should replace `<your-website.com>` with the website as defined can add multiple websites to this list.
- The `metadata_fields` is an optional list of metadata fields to sync, e.g. ["fieldname_text", "fieldname_int"]. If not specified, no metadata fields will be synced.

All the available options for the Simple Analytics CloudQuery plugin are documented in the [plugin repository README](https://github.com/simpleanalytics/cq-source-simpleanalytics).

### Step 2. Create the Destination Configuration File

Next, let's create a destination configuration file named `sqlite.yml` with the following contents:

```yaml
kind: destination
spec:
  name: sqlite
  path: cloudquery/sqlite
  version: "v1.2.1"
  spec:
    connection_string: ./db.sql
```

This configuration file defines a destination named `sqlite` that will sync data to a SQLite database. This must be the same as the value we have in the `destinations` setting in the source config.

The example uses the plugin version 1.2.1, but you can find the latest `version` on the [CloudQuery website](https://www.cloudquery.io/docs/plugins/destinations/sqlite/overview).

The `connection_string` value defines the path to the SQLite database file. In this example, we will create a file named `db.sql` in the current directory.

### Step 3. Set Environment Variables

Next, we need to set the `SA_USER_ID` and `SA_API_KEY` environment variables. You can do this by running the following commands in your terminal:

```bash
export SA_USER_ID=<your-user-id>
export SA_API_KEY=<your-api-key>
```

### Step 4. Run CloudQuery

With the configuration files and environment variables in place, we can run CloudQuery to sync the data. Run the following command in your terminal:

```bash
cloudquery sync simpleanalytics.yml sqlite.yml
```

You will see a progress bar as CloudQuery syncs the data. It might take a few minutes, depending on how much data you have. When it's done, it should look something like this:

```text
➜ playground cloudquery sync simpleanalytics.yml sqlite.yml
Loading spec(s) from simple-analytics.yml
Starting migration with 2 tables for: simple-analytics (v1.0.0) -> [sqlite (v1.2.1)]
Migration completed successfully.
Starting sync for: simple-analytics (v1.0.0) -> [sqlite (v1.2.1)]
Sync completed successfully. Resources: 105666, Errors: 0, Panics: 0, Time: 41s
```

If anything goes wrong, you can inspect the `cloudquery.log` file to look for error messages.

### Step 5. Query the data

We can now open the SQLite database file to see the data (you will need have [SQLite installed](https://www.sqlite.org/download.html) for this step):

```bash
sqlite3 db.sql
```

To render results nicely, we can turn on the `column` mode and show headers:

```text
sqlite> .mode column
sqlite> .headers on
```

The sync created two tables: `simple_analytics_page_views` and `simple_analytics_events`. Let's query the `simple_analytics_page_views` table to see the top pages for the last 7 days:

```text
sqlite> select path, count(*) as count from simple_analytics_page_views group by path order by count desc limit 3;
path                       count
-------------------------  ------
/                          123456
/docs                      78910
/blog/simple-analytics     11121
```

What you do with the data from here is up to you. You can use it to create reports, dashboards, or other visualizations.

## Example 2: Exporting to BigQuery

For our second example, we will sync Simple Analytics data to [BigQuery](https://cloud.google.com/bigquery). BigQuery is a completely serverless and cost-effective enterprise data warehouse.

### Prerequisites

To follow this example, you will need to have a Google Cloud Platform account and a project with BigQuery enabled. You can follow the [Quickstart guide](https://cloud.google.com/bigquery/docs/quickstarts/quickstart-web-ui) to create a project and enable BigQuery.

You will also need to have the `gcloud` command-line tool installed. See the official documentation for [installing the gcloud CLI](https://cloud.google.com/sdk/docs/install).

### Step 1. Create an Empty BigQuery Dataset

On the [BigQuery Cloud Console](https://console.cloud.google.com/bigquery), expand the project menu and select your project. Then, click the `Create dataset` button to create a new dataset.

<img class="border" src="https://assets.simpleanalytics.com/docs/cloudquery/001-create-bigquery-dataset.png" alt="Create BigQuery Dataset" />

Give the dataset a name and click `Create`.

<img class="border" src="https://assets.simpleanalytics.com/docs/cloudquery/002-create-bigquery-dataset.png" alt="Create BigQuery Dataset" />

### Step 2. Log in to Google Cloud using gcloud

Next, we need to log in to Google Cloud using the [gcloud command-line tool](https://cloud.google.com/sdk/gcloud). The CloudQuery plugin will use the same credentials to write to BigQuery. Run the following command in your terminal:

```bash
gcloud auth application-default login
```

### Step 3. Create the Source Configuration File

Let's create a source configuration file named `simpleanalytics.yml` with the following contents:

```yaml
kind: source
spec:
  name: "simpleanalytics"
  path: "simpleanalytics/simpleanalytics"
  version: "v1.0.0"
  tables: ["*"]
  destinations:
    - "bigquery" # <-- this is the only change from the SQLite example
  spec:
    # plugin spec section
    user_id: "${SA_USER_ID}"
    api_key: "${SA_API_KEY}"
    period: 7d
    websites:
      - hostname: <your-website.com>
        # metadata_fields: 
```

The only change from the SQLite example is the `destinations` setting, which now uses `bigquery` instead of `sqlite`.

### Step 4. Create the Destination Configuration File

Next, let's create a destination configuration file named `bigquery.yml` with the following contents:

```yaml
kind: destination
spec:
  name: bigquery
  path: cloudquery/bigquery
  version: "v2.1.3"
  write_mode: "append"
  spec:
    project_id: ${PROJECT_ID}
    dataset_id: ${DATASET_ID}
```

Like with SQLite, see the [CloudQuery BigQuery Plugin page](https://www.cloudquery.io/docs/plugins/destinations/bigquery/overview) for the latest version and details on the available configuration options.

### Step 5. Set Environment Variables

Next, we need to set the `SA_USER_ID`, `SA_API_KEY`, `PROJECT_ID` and `DATASET_ID` environment variables. Run the following commands in your terminal, replacing the placeholders with your values:

```bash
export SA_USER_ID=<your-user-id>
export SA_API_KEY=<your-api-key>
export PROJECT_ID=<your-project-id>
export DATASET_ID=<your-dataset-id>
```

### Step 6. Run CloudQuery

With the configuration files and environment variables in place, we can run CloudQuery to sync the data. Run the following command in your terminal:

```bash
cloudquery sync simpleanalytics.yml bigquery.yml
```

It should run for a few minutes, depending on how much data you have. When it's done, it should look something like this:

```text
➜ playground cloudquery sync simpleanalytics.yml bigquery.yml
Loading spec(s) from simpleanalytics.yml
Starting migration with 2 tables for: simpleanalytics (v1.0.0) -> [bigquery (v2.1.3)]
Migration completed successfully.
Starting sync for: simpleanalytics (v1.0.0) -> [bigquery (v2.1.3)]
Sync completed successfully. Resources: 105666, Errors: 0, Panics: 0, Time: 2m 10s
```

If anything goes wrong, you can inspect the `cloudquery.log` file to look for error messages.

### Step 7. Query the data

Now that the data is in BigQuery, we can query it using the [BigQuery web console](https://console.cloud.google.com/bigquery). Click the dataset in the sidebar to open it. Then click on the newly created `simple_analytics_page_views` table, and click the `Query` button:

<img class="border" src="https://assets.simpleanalytics.com/docs/cloudquery/003-query-bigquery-dataset.png" alt="BigQuery Query" />

Now we can run any query we like. In this example we simply explore 100 rows from the table:

<img class="border" src="https://assets.simpleanalytics.com/docs/cloudquery/004-query-bigquery-dataset.png" alt="BigQuery Query" />
