#  运行实例
docker build -t dockerregistry:30290/myduckserver:latest -f docker/Dockerfile .

docker run -p 13306:3306 -p 15432:5432 apecloud/myduckserver:latest

# 
# main 中运行
# 支持的主要数据库版本：MySQL >= 8.0 和 PostgreSQL >= 13。除了默认设置外，对于 PostgreSQL，必须通过设置 wal_level=logical 启用逻辑复制。对于 MySQL，建议使用基于 GTID 的复制（ gtid_mode=ON 和 enforce_gtid_consistency=ON ），但不是强制要求的。
docker run -d --name myduck \
-p 13306:3306 \
-p 15432:5432 \
--env=SETUP_MODE=REPLICA \
--env=SOURCE_DSN="<postgres|mysql>://<user>:<password>@<host>:<port>/<dbname>"
apecloud/myduckserver:latest

# 开发者指南
https://blog.csdn.net/gitblog_00176/article/details/147160294