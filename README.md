# buildrun-emqx-backend-mysql
EMQX  client connection and message save to MySQL

emqx for mysql

### erlang 


### bianyifabu

1、clone emqx-rel  tag  v4.1.2

``` bash
git clone https://github.com/emqx/emqx-rel.git
cd emqx-rel
git checkout v4.1.2
make
```

 `_build/emqx/rel/emqx/bin/emqx console`  emqx

### make plugin

2.rebar.config 

```erl
{deps,
   [ {buildrun_emqx_backend_mysql, {git, "https://github.com/goBuildRun/buildrun-emqx-backend-mysql.git", {branch, "master"}}}
   , ....
   ....
   ]
}

```

3.rebar.config

```erl
{relx,
    [...
    , ...
    , {release, {emqx, git_describe},
       [
         {buildrun_emqx_backend_mysql, load},
       ]
      }
    ]
}
```
4.make

> make

surf `localhost:18083`  `buildrun_emqx_backend_mysql`

### config

File: etc/buildrun_emqx_backend_mysql.conf

```
# mysql 
mysql.server = 127.0.0.1:3306

# pool
mysql.pool_size = 8

# mysql admin
mysql.username = buildrun

# mysql pwd
mysql.password = buildrun

# database name
mysql.database = mqtt

# timeout
mysql.query_timeout = 10s

```

### mqtt_client.sql, mqtt_msg.sql

[mqtt_client.sql](./sql/mqtt_client.sql), [mqtt_msg.sql](./sql/mqtt_msg.sql)。

### load

> ./bin/emqx_ctl plugins load buildrun_emqx_backend_mysql

or make

data/loaded_plugins

>  {buildrun_emqx_backend_mysql, true}.

