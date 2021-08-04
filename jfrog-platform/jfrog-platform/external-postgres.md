## psql --host=mydb.xyz.eu-central-1.rds.amazonaws.com -U postgres --password --dbname=postgres
```bash
CREATE USER "artifactory" WITH PASSWORD 'password';
CREATE USER "xray" WITH PASSWORD 'password';
CREATE USER "distribution" WITH PASSWORD 'password';
CREATE USER "mc" WITH PASSWORD 'password';

CREATE DATABASE artifactory ENCODING='UTF8';
CREATE DATABASE xray ENCODING='UTF8';
CREATE DATABASE distribution ENCODING='UTF8';
CREATE DATABASE mission_control ENCODING='UTF8';

GRANT ALL PRIVILEGES ON DATABASE artifactory TO artifactory;
GRANT ALL PRIVILEGES ON DATABASE xray TO xray;
GRANT ALL PRIVILEGES ON DATABASE distribution TO distribution;
GRANT ALL PRIVILEGES ON DATABASE mission_control TO mc;
```

## psql  --host=mydb.xyz.eu-central-1.rds.amazonaws.com -U mc --password --dbname=mission_control 
```bash
CREATE SCHEMA IF NOT EXISTS jfmc_server AUTHORIZATION mc;
GRANT ALL ON SCHEMA jfmc_server TO mc;
CREATE SCHEMA IF NOT EXISTS insight_server AUTHORIZATION mc;
GRANT ALL ON SCHEMA insight_server TO mc;
CREATE SCHEMA IF NOT EXISTS insight_scheduler AUTHORIZATION mc;
GRANT ALL ON SCHEMA insight_scheduler TO mc;
```
