---
layout: wiki
title: Redis常用命令
categories: Redis
keywords: Redis
---

Redis的一些常用命令

---

## string
* set key value 设置key的值, 成功的话，返回OK
* get key  获取key的值，成功的话，返回值，不成功的话，返回nil，0的意思
* del key 删除key的值 返回1，删除成功，返回0，删除失败

## list
* rpush listKey item 从列表右端，插入一个值
* lpush listKey item2 从列表左端，插入一个值
* lrange listKey 0 -1  
	* 0: 起始索引
	* -1： 结束索引
* lindex listKey 1  获取指定位置的值，获取位置是1的值
* lpop listKey  从左端弹出一个元素，并返回被弹出元素的值
* rpop listKey  从右端弹出一个元素，并返回被弹出元素的值
* lrem listKey 1 zhangsan  从左边开始找，删除value=zhangsan的所有元素
* lrem listKey -1 zhangsan  从右边开始找，删除value=zhangsan的所有元素


## set
* sadd setKey value 给setKey插入一个值，是无序的
* smembers setKey 获取setKey所有的值
* sismember setKey value 检查value值是否在setKey中存在，返回1，存在，返回0，不存在
* srem setKey value 删除setKey中得value，返回1，删除成功，返回0，删除失败

## hash
* hset user_1 name kyle ->true:1, false:0
* hset user_1 sex man ->true:1, false:0
* hgetall user_1
* hget user_1 name  ->kyle
* del user_2
* del user_2 name

## zset
* zadd zsetKey 701 member1
* zadd zsetKey 703 member2
* zadd zsetKey 702 member3
* del zsetKey
* zrange zsetKey 0 -1 withscores