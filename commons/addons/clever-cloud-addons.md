---
title: Clever Cloud Add-ons
position: 3
---

# Clever Cloud Add-ons

Clever Cloud provides internally the following add-ons:

* MySQL
* PostgreSQL
* MongoDB
* FS bukets


## MySQL plans

<table class="table table-bordered table-striped dataTable"><caption>MySQL pricing plans</caption>
<tr>
<th>Name</th>
<th>Cache (Memory)</th>
<th>Disk</th>
<th>Conn. limit</th>
<th>Price /mo</th>
</tr> 
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">DEV</span></td>
<td>SHARED</td>
<td>10 MB</td>
<td>5</td>
<td>Free</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">S</span></td>
<td>SHARED</td>
<td>256 MB</td>
<td>10</td>
<td>15 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">M</span></td>
<td>1 GB</td>
<td>10 GB</td>
<td>75</td>
<td>45 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">L</span></td>
<td>2 GB</td>
<td>200 GB</td>
<td>500</td>
<td>300 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">XL</span></td>
<td>8 GB</td>
<td>500 GB</td>
<td>750</td>
<td>1600 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">XXL</span></td>
<td>16 GB</td>
<td>900 GB</td>
<td>2000</td>
<td>2200 €</td>
</tr>
</table>

### Migrating from an old database

Some applications require a populated database to run properly.  
If you want to import your **SQL** dump, you can use several methods:

1. <a href="https://dbms-pma.clever-cloud.com/">our WebGUI (PHP My Admin)</a>
2. command line tool for MySQL administration
3. any MySQL client such as MySQL Workbench.


<br/><br/>If you need to import a very large dump, please send an email to <support@clever-cloud.com>.


## PostgreSQL plans

<table class="table table-bordered table-striped dataTable"><caption>PostgreSQL pricing plans</caption>
<tr>
<th>Name</th>
<th>Cache (Memory)</th>
<th>Disk</th>
<th>Conn. limit</th>
<th>Price /mo</th>
</tr> 
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">DEV</span></td>
<td>SHARED</td>
<td>256 MB</td>
<td>10</td>
<td>Free</td>
</tr>

<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">S</span></td>
<td>SHARED</td>
<td>1 GB</td>
<td>10</td>
<td>10 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">M</span></td>
<td>1 GB</td>
<td>100 GB</td>
<td>75</td>
<td>30 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">L</span></td>
<td>8 GB</td>
<td>450 GB</td>
<td>500</td>
<td>240 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">XL</span></td>
<td>32 GB</td>
<td>600 GB</td>
<td>750</td>
<td>700 €</td>
</tr>
<tr>
<td class="cc-col__price "><span class="label cc-label__price label-info">XXL</span></td>
<td>64 GB</td>
<td>900 GB</td>
<td>1000</td>
<td>1200 €</td>
</tr>
</table>

### Migrating from an old database

Some applications require a populated database to run properly.  
If you want to import your **SQL** dump, you can use several methods:

1. <a href="https://dbms-adminer.clever-cloud.com/adminer/">our WebGUI (Adminer)</a>
2. command line tool for PostgreSQL administration like `psql`
3. any PostgreSQL client such as pgAdmin 3.



## FS Buckets: file system with persistance <span class="cc-beta pull-right" title="Currently in Beta version"></span>

<div class="alert alert-hot-problems">
  <h5>Note for Beta Version</h5>
  <div>FS Buckets are free during the beta period. No credits will be charged.</div>
</div>

When you deploy an application on any PaaS, a new application is created, the previous is deleted. If your application generates data, for example if you let users upload pictures and you do not store it on external services like S3, you will loose data.

The Git deployment does not allow you to keep generated data files between deployments. To avoid the loss of your data, you have to mount a persistent filesystem. This is why we created File System Buckets.

You will be able to retrieve generated data between two deployments.

### Creating a FS Bucket

[This article](/addons/clever-cloud-addons/) describes the process to add a File System Bucket on Clever Cloud.


### Configuring your application

To configure your application to use buckets, use the
`clevercloud/buckets.json` file.

The `clevercloud` folder must be located at the root of your application.

The `buckets.json` file must contain the following structure:

```javascript
[
  {
    "bucket" : "bucketId",
    "folder" : "/myFolder",
    "apps"   : ["app_id"]

  },
  {
    "bucket" : "bucketId2",
    "folder" : "/myotherFolder",
    "apps"   : ["app_id_2"]
  }
]
```


It's a json array containing objects with two fields:

<table id="nodedeps" class="table table-bordered table-striped">
<thead>
<tr>
<th>Usage</th>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><span class="label label-important">Required</span></td>
<td>bucket</td>
<td>The bucket id you can find in the console. It begins with `bucket_`</td>
</tr>
<tr>
<td><span class="label label-important">Required</span></td>
<td>folder</td>
<td>The folder you want the bucket to be mounted in. Should start with `/`. Using the example
*myFolder*, you can access your buckets via the *myFolder* folder at
the root of your application or via */app/myFolder*</td>
</tr>
<tr>
<td class="cc-depusage"><span class="label label-inverse">Optional</span></td>
<td>apps</td>
<td>Whitelist of the applications allowed to mount this bucket. It's helpful if you need
to deploy a *preprod* app and a *prod* app using the exact same codebase but different
buckets</td>
</tr>
</tbody>
</table>

<div class="alert alert-hot-problems">
<h5>Important note about target folder</h5>
<p>
The folder must not exists in your repository (or it needs to be empty). Otherwise, the mount of your bucket will be ignored.
</p>
<p>
You can mount the same bucket in different folders, but they will share the same
content, so it's not the solution. You should prefer to mount the bucket in only one
folder and then manage multiple subfolders in it.
</p>
</div>

<div class="alert alert-hot-problems">
<h5>Other things you *must* know</h5>
<p>
You cannot mount two buckets in the same folder for the same app.
</p>
<p>
If you put the same "folder" value for two entries in the *buckets.json* array, **you better
make sure** that the "apps" fields make the two buckets mutually exclusive upon deployment!
</p>
</div>

### Accessing your data inside the FS Bucket

The "configuration" tab of your FS Bucket add-on displays the information you need to connect to
your bucket using FTP.

## Cellar <span class="cc-beta pull-right" title="Currently in Beta version"></span>
<div class="alert alert-hot-problems">
  <h5>Note for Beta Version</h5>
  <div>Cellar is free during the beta period. No credits wil be charged.</div>
</div>
Cellar

Cellar is S3-compatible online file storage web service. You can use it with
your favorite S3 client.

Do manually manage the files, you can use [s3cmd](http://s3tools.org/s3cmd).
You can download a s3cmd configuration file from the add-on configuration
page.

### Creating a bucket

In Cellar, files are stored in buckets. When you create a Cellar addon, no
bucket is created yet.

To create a bucket, you can use s3cmd:

    s3cmd mb s3://bucket-name

You can list files

    s3cmd ls s3://bucket-name

You can upload files (`--acl-public` makes the file readable by everyone).

    s3cmd put --acl-public image.jpg s3://bucket-name

<div class="alert alert-hot-problems">
  <h5>S3 signature algorithm</h5>
  <div>Cellar doesn't support the `v4` signature algorithm from S3. Please make sure
       your client is configured to use the `v2` signature algorithm. The
      s3cmd configuration file provided on the add-on configuration page already has it.
  </div>
</div>

## MongoDB <span class="cc-beta pull-right" title="Currently in Beta version"></span>
<div class="alert alert-hot-problems">
  <h5>Note for Beta Version</h5>
  <div>MongoDB is free during the beta period. No credits wil be charged.</div>
</div>
MongoDB is an open source NoSQL document-oriented database.

