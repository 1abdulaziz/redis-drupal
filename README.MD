# HOW TO USE REDIS ON DRUPAL WITH LANDO 

1- Edit the .lando.yml file and add the following a cache server to the services section.
```yml
services:
...
  cache:
    type: redis:4.0
    portforward: 6380
    persist: true
```
2- In the tooling section add access to the redis-cli command.
```yml
tooling:
...
  redis-cli:
    service: cache
```
3- Install the module [redis](https://www.drupal.org/project/redis) and Enable.
4- go to seetings.php and set:
```php
$settings['redis.connection']['interface'] = 'PhpRedis';
$settings['redis.connection']['host'] = 'cache';
$settings['redis.connection']['port'] = 6379;
$settings['cache']['default'] = 'cache.backend.redis';
$settings['cache']['bins']['render'] = 'cache.backend.redis';
$settings['container_yamls'][] = 'modules/contrib/redis/example.services.yml';
$settings['redis_compress_length'] = 100;
```
5- go to this link /admin/reports/redis to check is connected or not.
