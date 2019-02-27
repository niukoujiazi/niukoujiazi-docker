FROM ubuntu:18.04
MAINTAINER clip "niukoujiazi@gmail.com"
#设置时区为亚洲上海 
#安装python依赖 python3.6.7 postgresql10.6 pip3 django2.1.7 tornado5.1.0 twisted18.9.0 redis4.0.9
#复制配置文件进镜像
RUN apt-get -y  update \
		&& export DEBIAN_FRONTEND=noninteractive \
		&& apt-get -y  install tzdata \
		&& ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
		&& dpkg-reconfigure -f noninteractive tzdata \
		&& apt-get -y  install build-essential checkinstall \
			libreadline-gplv2-dev libncursesw5-dev libssl-dev \
			libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev \
		&& apt-get -y  install python3.6 \
		&& ln -s /usr/bin/python3.6 /usr/bin/python \
		&& apt-get -y  install postgresql-client postgresql \
		&& apt-get -y  install python3-pip \
		&& apt-get -y install redis-server \
		&& pip3 install django --no-cache-dir \ 
		&& pip3 install twisted --no-cache-dir \
		&& pip3 install tornado --no-cache-dir \
		&& pip3 install redis --no-cache-dir \
        && pip3 install crccheck --no-cache-dir \
        && pip3 install sqlalchemy --no-cache-dir \
        && pip3 install psycopg2 --no-cache-dir \
        && pip3 install djangorestframework --no-cache-dir \
        && pip3 install markdown --no-cache-dir \
        && pip3 install django-filter --no-cache-dir \
        && pip3 install django-cors-headers --no-cache-dir \
        && pip3 install django-crispy-forms --no-cache-dir \
		&& pip3 install psycopg2-binary --no-cache-dir \
		&& rm -rf /var/lib/apt/lists/* \
		&& rm -rf /root/.cache/ \
		&& apt-get -y  purge -y --auto-remove $buildDeps \
		&& mkdir -p /var/run/postgresql/10-main.pg_stat_tmp \
		&& chown -R postgres:postgres /var/run/postgresql/10-main.pg_stat_tmp 
#COPY pg_hba.conf /etc/postgresql/10/main/pg_hba.conf 
#修改配置文件访问权限及所有者，并重启服务
#RUN chmod 777 /etc/postgresql/10/main/pg_hba.conf \
#		&& chown -R postgres:postgres /etc/postgresql/10/main/pg_hba.conf \
#RUN chown -R redis:redis /etc/redis/redis.conf \
#		&& /etc/init.d/postgresql restart \
#		&& service redis-server restart \
#		&& mkdir -p /var/run/postgresql/10-main.pg_stat_tmp \
#		&& chown -R postgres:postgres /var/run/postgresql/10-main.pg_stat_tmp 
USER postgres
RUN /etc/init.d/postgresql restart \
		&& psql --command " ALTER USER postgres WITH PASSWORD '123456';" \
		&& /etc/init.d/postgresql stop
COPY --chown=postgres:postgres pg_hba.conf /etc/postgresql/10/main/pg_hba.conf
COPY --chown=postgres:postgres postgresql.conf /etc/postgresql/10/main/postgresql.conf
COPY --chown=redis:redis redis.conf /etc/redis/
