PostGIS plugin for Dokku
------------------------

Project: https://github.com/progrium/dokku

**Warning: This plugin is under development and still only tested with the below dependencies**

Requirements
------------
* Docker version `0.7.2` or higher
* Dokku version `0.2.1` or higher

Installation
------------
```
cd /var/lib/dokku/plugins
git clone https://github.com/fermuch/dokku-pg-plugin.git postgis
dokku plugins-install
```


Commands
--------
```
$ dokku help
    postgis:console <db>                        Open a PostGIS console
    postgis:create <db>                         Create a PostGIS container
    postgis:delete <db>                         Delete specified PostGIS container
    postgis:dump <db> > dump_file.sql           Dump database data
    postgis:info <db>                           Display database informations
    postgis:link <app> <db>                     Link an app to a PostGIS database
    postgis:list                                Display list of PostGIS containers
    postgis:logs <db>                           Display last logs from PostGIS container
    postgis:restore <db> < dump_file.sql        Restore database data from a previous dump
```

Simple usage
------------

Create a new DB:
```
$ dokku postgis:create foo            # Server side
$ ssh dokku@server postgis:create foo # Client side

-----> PostGIS container created: postgis/foo

       Host: 172.17.42.1
       User: 'root'
       Password: 'RDSBYlUrOYMtndKb'
       Database: 'db'
       Public port: 49187
```

Deploy your app with the same name (client side):
```
$ git remote add dokku git@server:foo
$ git push dokku master

```

Link your app to the database
```bash
dokku postgis:link app_name database_name
```


Advanced usage
--------------

Inititalize the database with SQL statements:
```
cat init.sql | dokku postgis:create foo
```

Open a PostGIS console for specified database:
```
dokku postgis:console foo
```

Deleting databases:
```
dokku postgis:delete foo
```

Linking an app to a specific database:
```
dokku postgis:link foo bar
```

postgis logs (per database):
```
dokku postgis:logs foo
```

Database information:
```
dokku postgis:info foo
```

List of containers:
```
dokku postgis:list
```

Dump a database:
```
dokku postgis:dump foo > foo.sql
```

Restore a database:
```
dokku postgis:restore foo < foo.sql
```

In case Dokku says `pg_dump not found` when dumping or restoring database:
```
sudo apt-get install postgresql-client-9.3
```
