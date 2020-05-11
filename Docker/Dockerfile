FROM registry.access.redhat.com/ubi7/ubi:latest

LABEL name: Name: "PostgreSQL" \
			vendor: "OpenTestLabs" \
			version: "9.6" \
			release: "1.0" \
			summary: PostgreSQL \
			description: "PostgreSQL is an advanced Object-Relational database management system (DBMS). The image contains the client and server programs that you'll need to create, run, maintain and access a PostgreSQL DBMS server."


COPY licenses /licenses

RUN yum -y install sudo epel-release; yum clean all

RUN yum install https://download.postgresql.org/pub/repos/yum/9.6/redhat/rhel-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm -y

RUN yum install postgresql96 postgresql96-server postgresql96-contrib postgresql96-libs -y

RUN sed -i 's/.*requiretty$/#Defaults requiretty/' /etc/sudoers

ENV USER_NAME postgres 

RUN mkdir -p /var/lib/pgsql/data

RUN chown -R postgres /var/lib/pgsql

RUN ln -s /var/lib/pgsql/bin/* /usr/bin/.

USER $USER_NAME

RUN cd /usr/pgsql-9.6/bin && \
     ./initdb -E UTF8 -D /var/lib/pgsql/data && \
	 ./pg_ctl -D /var/lib/pgsql/data start
     

ENV PATH /var/lib/pgsql/bin:$PATH

ENV PGDATA /var/lib/pgsql/data

RUN echo "listen_addresses='*'" >> /var/lib/pgsql/data/postgresql.conf

RUN echo "host    all             all             0.0.0.0/0               md5" >> /var/lib/pgsql/data/pg_hba.conf

EXPOSE 5432

ENTRYPOINT ["/usr/pgsql-9.6/bin/postgres"]
