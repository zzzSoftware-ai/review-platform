# 黑马点评 · 点评类 App 后端

仿大众点评的点评类 App 后端项目,重点实践 Redis 在高并发场景下的应用:缓存问题治理、分布式锁、秒杀等。个人学习项目。

## 技术栈

- Spring Boot、MyBatis-Plus
- MySQL、Redis、Lombok

## 核心亮点

### 1. 商户查询缓存 —— 缓存三兄弟解决方案

- **缓存穿透**:空值缓存 + 布隆过滤器过滤无效请求
- **缓存击穿**:互斥锁重建缓存 / 逻辑过期方案
- **缓存雪崩**:TTL 随机化避免集中过期

### 2. 优惠券秒杀 —— 高并发下单

- Redis 原子操作扣减库存,解决**超卖**问题
- Redisson 分布式锁保证**一人一单**(可重入锁 + 看门狗自动续期)
- Redis + Lua 脚本将判断与扣减合并为原子操作,减少网络往返

### 3. 短信验证码登录与会话共享

- 验证码写入 Redis 并设置 TTL
- 登录后签发 token 存 Redis 实现会话共享
- 双拦截器方案:登录校验 + token 有效期自动刷新

### 4. 其他模块

- 探店笔记发布与评论
- 好友关注(共同关注、Feed 流)

## 快速启动

依赖:JDK 8+、MySQL、Redis

1. 建库:执行 `src/main/resources/db/` 下的 SQL 脚本
2. 修改 `src/main/resources/application.yaml` 中的 MySQL 密码与 Redis 地址
3. 启动 `HmDianPingApplication`

## 配置说明

- `application.yaml` 中的数据库密码已脱敏,需自行填写本地 MySQL 密码
