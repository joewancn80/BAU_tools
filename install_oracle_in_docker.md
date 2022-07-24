
 ```
 
 docker login container-registry.oracle.com
 
 
-- docker pull  container-registry.oracle.com/database/enterprise:latest
 docker pull  container-registry.oracle.com/database/enterprise:19.3.0.0
-- docker pull  container-registry.oracle.com/database/enterprise:21.3.0.0
 
 
docker run -d --name oracle19c3 -e ORACLE_SID=ora19c3 -e ORACLE_PDB=PDB_19c3 -e ORACLE_PWD=redhat -e INIT_SGA_SIZE=1000M -e INIT_PGA_SIZE=800M -e ENABLE_ARCHIVELOG=true  container-registry.oracle.com/database/enterprise:19.3.0.0
 
 
 [root@master ~]# docker logs oracle19   <<< 这里看整个数据库的安装情况
[2022:07:24 13:26:08]: Acquiring lock .ORA19C3.create_lck with heartbeat 30 secs
[2022:07:24 13:26:08]: Lock acquired
[2022:07:24 13:26:08]: Starting heartbeat
[2022:07:24 13:26:08]: Lock held .ORA19C3.create_lck
ORACLE EDITION: ENTERPRISE

LSNRCTL for Linux: Version 19.0.0.0.0 - Production on 24-JUL-2022 13:26:08

Copyright (c) 1991, 2019, Oracle.  All rights reserved.

Starting /opt/oracle/product/19c/dbhome_1/bin/tnslsnr: please wait...

TNSLSNR for Linux: Version 19.0.0.0.0 - Production
System parameter file is /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
Log messages written to /opt/oracle/diag/tnslsnr/fa10c2b6d2e8/listener/alert/log.xml
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))

Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=IPC)(KEY=EXTPROC1)))
STATUS of the LISTENER
------------------------
Alias                     LISTENER
Version                   TNSLSNR for Linux: Version 19.0.0.0.0 - Production
Start Date                24-JUL-2022 13:26:09
Uptime                    0 days 0 hr. 0 min. 0 sec
Trace Level               off
Security                  ON: Local OS Authentication
SNMP                      OFF
Listener Parameter File   /opt/oracle/product/19c/dbhome_1/network/admin/listener.ora
Listener Log File         /opt/oracle/diag/tnslsnr/fa10c2b6d2e8/listener/alert/log.xml
Listening Endpoints Summary...
  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1)))
  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=0.0.0.0)(PORT=1521)))
The listener supports no services
The command completed successfully
[WARNING] [DBT-06208] The 'SYS' password entered does not conform to the Oracle recommended standards.
   CAUSE:
a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
b.The password entered is a keyword that Oracle does not recommend to be used as password
   ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
[WARNING] [DBT-06208] The 'SYSTEM' password entered does not conform to the Oracle recommended standards.
   CAUSE:
a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
b.The password entered is a keyword that Oracle does not recommend to be used as password
   ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
[WARNING] [DBT-06208] The 'PDBADMIN' password entered does not conform to the Oracle recommended standards.
   CAUSE:
a. Oracle recommends that the password entered should be at least 8 characters in length, contain at least 1 uppercase character, 1 lower case character and 1 digit [0-9].
b.The password entered is a keyword that Oracle does not recommend to be used as password
   ACTION: Specify a strong password. If required refer Oracle documentation for guidelines.
Prepare for db operation
8% complete
Copying database files

 
 
 
 
 ```
 
 
 ```
 docker run -d --name <container_name> \
 -p <host_port>:1521 -p <host_port>:5500 \
 -e ORACLE_SID=<your_SID> \
 -e ORACLE_PDB=<your_PDBname> \
 -e ORACLE_PWD=<your_database_password> \
 -e INIT_SGA_SIZE=<your_database_SGA_memory_MB> \
 -e INIT_PGA_SIZE=<your_database_PGA_memory_MB> \
 -e ORACLE_EDITION=<your_database_edition> \
 -e ORACLE_CHARACTERSET=<your_character_set> \
 -e ENABLE_ARCHIVELOG=true \
 -v [<host_mount_point>:]/opt/oracle/oradata \
container-registry.oracle.com/database/enterprise:21.3.0.0

Parameters:
 --name:                 The name of the container (default: auto generated
 -p:                     The port mapping of the host port to the container port.
                         Two ports are exposed: 1521 (Oracle Listener), 5500 (OEM Express)
 -e ORACLE_SID:          The Oracle Database SID that should be used (default:ORCLCDB)
 -e ORACLE_PDB:          The Oracle Database PDB name that should be used (default: ORCLPDB1)
 -e ORACLE_PWD:          The Oracle Database SYS, SYSTEM and PDBADMIN password (default: auto generated)
 -e INIT_SGA_SIZE:       The total memory in MB that should be used for all SGA components (optional)
 -e INIT_PGA_SIZE:       The target aggregate PGA memory in MB that should be used for all server processes attached to the instance (optional)
 -e ORACLE_EDITION:      The Oracle Database Edition (enterprise/standard, default: enterprise)
 -e ORACLE_CHARACTERSET: The character set to use when creating the database (default: AL32UTF8)
 -e ENABLE_ARCHIVELOG:   To enable archive log mode when creating the database (default: false). Supported 19.3 onwards.
 -v /opt/oracle/oradata
                         The data volume to use for the database. Has to be writable by the Unix "oracle" (uid: 54321) user inside the container
                         If omitted the database will not be persisted over container recreation.
 -v /opt/oracle/scripts/startup | /docker-entrypoint-initdb.d/startup
                         Optional: A volume with custom scripts to be run after database startup.
                         For further details see the "Running scripts after setup and on
                         startup" section below.
 -v /opt/oracle/scripts/setup | /docker-entrypoint-initdb.d/setup
                         Optional: A volume with custom scripts to be run after database setup.
                         For further details see the "Running scripts after setup and on startup" section below.
 ```
 


