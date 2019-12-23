## Welcome to Kent's NLP analysis of Crunchbase's 2013 Snapshot!

To get started, install a virtual environment using the requirements.txt file.

`pip install -r requirements.txt`

### Accessing the Data - Setting up MySQL

The Crunchbase 2013 snapshot is available [here](https://data.crunchbase.com/docs/2013-snapshot) after registering for a free account. It is available for download through their api upon receiving a key. As it's in MySQL format, I also installed the MySQL v5.7.28 community edition [here](https://dev.mysql.com/downloads/mysql/) following instructions [here](https://dev.mysql.com/doc/refman/5.7/en/osx-installation-pkg.html). MySQL v8.0.11+ is incompatible with some of the options that [have since been deprecated and removed](https://dev.mysql.com/doc/relnotes/mysql/8.0/en/news-8-0-11.html#mysqld-8-0-11-deprecation-removal), namely SQL_MODE='NO_AUTO_VALUE_ON_ZERO,POSTGRESQL', so be sure to install the correct version.

For me (after adding export PATH=/usr/local/mysql/bin:$PATH to my environment), the command for starting mysql is `sudo -u root mysqld --datadir /usr/local/mysql/data --user=_mysql &` and stopping it is `mysqladmin -u root -p shutdown`. There is also a MySQL gui under preferences that can do the same. Test that the server is running with `mysqladmin -u root -p version`.

Concatenate all the sql files to execute in mysql shell. (Use different extension to avoid possible infinite loop.) `cat *.sql > all_cb.sql1`. 

Start the mysql shell with `mysql -u root -p --binary-mode=1` then create a database and select it. **NOTE: binary mode is necessary for parsing data in python.** `create database crunchdb; use crunchdb;`. Finally execute the data migration. `\. all_cb.sql1`.

Alternatively, you can skip the data ingestion and pick up where I load in pickle files.