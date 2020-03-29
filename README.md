# deley-task

## 介绍

业务想自己实现一个延迟任务的轮子

## 方案选型

### 方案一：存储在数据库中，定时轮询扫描
#### 优点：
1. 横向扩展方便，可以用已有的数据分片方案（sharding-sphere、mycat等）
#### 缺点：
1. 轮询间隔不好确定（间隔大，时效性就会降低，间隔小对数据库压力较大） 
2. 单表数据量较多的话，轮询效率会比较低
### 方案二：JDK DelayQueue
#### 优点：
1. 简单易用，JDK已经封装好了api
#### 缺点：
1. 存储在内存，当延迟任务比较多的时候，容易OOM
2. down机无法恢复
3. 没法天然支持分布式，扩容不方便
### 方案三：RocketMQ等mq方案
#### 优点：
1. 天然支持分布式场景，不需要考虑扩展性和高可用问题
2. 简单易用，大佬们已经封装好了api
#### 缺点：
1. 不支持任意的时间精度，RocketMQ的时间精度：5s、10s、1m等
### 方案四：基于redis
#### 优点：
1. 也是这个项目的目的，准备参考一些方案自己实现一个延迟队列轮子     
