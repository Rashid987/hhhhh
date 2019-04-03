weather-Server
=============
#### 1.add configs/db.json and configs/local.json
#### 2.execute following commands.
      cd scripts
      sudo bash installation.sh
####   or to add data from mysql instance execute following.
      cd scripts 
      sudo bash addDataOnMysql.sh <mysql_user> <mysql_host> <mysql_password>
#### 3.start background with command
      ENV=BACKGROUND node background.js
#### 4.start the weather server with command.
      node background.js
