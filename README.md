# Oracle Connect Neo4j graph database with JDBC

## NEO4J.CONF
![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/0abc56cf-1fc6-4dda-bf87-a947d9cde95d)

    # Configuration
    dbms.security.procedures.unrestricted=apoc.*,gds.*,bloom.*
    dbms.security.procedures.allowlist=apoc.*,gds.*,bloom.*
    apoc.import.file.enabled=true
    apoc.import.file.use_neo4j_config=true
    dbms.default_listen_address=0.0.0.0
    dbms.default_advertised_address=192.168.18.209
    
    # JDBC Oracle
    #apoc.jdbc.oracle.url=jdbc:oracle:thin:[username]/[password]@[hostname]:[port]/[service_name]
    apoc.jdbc.oracle.url=jdbc:oracle:thin:webuser/ddi123@centos7:1521/xepdb1
    apoc.jdbc.oracle.url=jdbc:oracle:thin:system/APP100897app@centos7:1521

## EDIT BASH_PROFILE
    vi ~/.bash_profile
User specific environment and startup programs

    PATH=$PATH:/opt/oracle/product/21c/dbhomeXE/bin
    export ORACLE_SID=XE
    export ORAENV_ASK=NO
    export ORACLE_HOME=/opt/oracle/product/21c/dbhomeXE
    export ORACLE_BASE=/opt/oracle
    export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.20.0.8-1.el7_9.x86_64/bin/java
    export PATH
    
If not, the listener will fail to start add 
    
    export ORACLE_HOSTNAME=myserver.example.com

Add Java Home
    
    JAVA_HOME=/usr/lib/jvm/java-11-openjdk-11.0.20.0.8-1.el7_9.x86_64/bin/java

![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/ce541b92-336b-48d5-bea0-2ee994a525c5)

## NEO4J PLUGINS

![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/beb8dafd-0181-498c-9ded-98e4f60c4285)

## LISTENER
    lsnrctl status
    vi /opt/oracle/homes/OraDBHome21cXE/network/admin/listener.ora

### Config file listener.ora

![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/2e234069-a52c-441d-90c9-02d20d8da578)

    lsnrctl start
    lsnrctl stop

## LOGIN SQLPLUS 

    sqlplus system/APP100897app@centos7:1521/XE
    sqlplus system/APP100897app@centos7:1521
    sqlplus system/APP100897app@centos7
    
    sqlplus webuser/ddi123@centos7:1521/XEPDB1
    
    sqlplus c##orcusr01/ddi123@centos7:1521/XE
    
    sqlplus / as sysdba
    startup

## CYPHER NEO4J 

    CALL apoc.load.jdbc("jdbc:oracle:thin:webuser/ddi123@centos7:1521/xepdb1", "select * from customer") YIELD row
    RETURN count(*);
    //RETURN row;
![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/f9e79907-40dc-4688-a490-077528ca0d33)

    CALL apoc.load.jdbc("jdbc:oracle:thin:webuser/ddi123@centos7:1521/xepdb1", "select * from customer") YIELD row
    RETURN row.CUSTOMER_ID, row.FIRST_NAME, row.EMAIL, row.PHONE_NUMBER
![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/45b447b1-b871-4171-bdc2-ef5a00767656)

    CALL apoc.load.jdbc("jdbc:oracle:thin:webuser/ddi123@centos7:1521/xepdb1", "select * from customer") YIELD row
    merge (c:Customer{customer_id:row.CUSTOMER_ID})
    on create set
    c.first_name = row.FIRST_NAME,
    c.email = row.EMAIL,
    c.phone_number = row.PHONE_NUMBER
    RETURN c;

## LOAD CYPHER JDBC ORACLE DI NEO4J BROWSER

### CHECK AND START LISTENER
lsnrctl status
lsnrctl start

### LOGIN SQLPLUS
sqlplus webuser/ddi123@centos7:1521/XEPDB1

Pastiin langsung connect tanpa tanda error kaya gambar ini 
![image](https://github.com/arliputraa/oracle-connect-neo4j-with-jdbc/assets/110078907/d611e96b-4234-4356-87b9-146f4ab49233)

### LOAD CYPHERNYA 
CALL apoc.load.jdbc("jdbc:oracle:thin:webuser/ddi123@centos7:1521/xepdb1", "select * from customer") YIELD row
RETURN row

