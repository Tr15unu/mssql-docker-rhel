# mssql-server-rhel
# Maintainers: Takayoshi Tanaka (tanaka-takayoshi on GitHub)
# GitRepo: https://github.com/tanaka-takayoshi/mssql-docker-rhel

# Base OS layer: latest RHEL 7
FROM registry.access.redhat.com/rhel7/rhel:latest

# For environment variables list, see https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-configure-environment-variables
ARG SA_PASSWORD='StrongP@ssW0rd'
ARG TCP_PORT=1433
ARG PID=Developer
ENV ACCEPT_EULA=Y MSSQL_PID=$PID MSSQL_SA_PASSWORD=$SA_PASSWORD MSSQL_TCP_PORT=$TCP_PORT

# Install latest mssql-server package
# You don't have to register subscription if you build docker image on registered RHEL machine.
# If you build on other machines, please fill in Red Hat subscription name and password and uncomment the below command.
#RUN subscription-manager register --username <your_username> --password <your_password> --auto-attach

RUN curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo && curl https://packages.microsoft.com/config/rhel/7/prod.repo > /etc/yum.repos.d/msprod.repo && yum install -y mssql-server mssql-server-agent mssql-server-fts && yum install -y mssql-tools unixODBC-devel

# Default SQL Server TCP/Port
EXPOSE $TCP_PORT

ENV PATH $PATH:/opt/mssql-tools/binTH $PATH:/opt/mssql-tools/bin

CMD /opt/mssql/bin/sqlservr
