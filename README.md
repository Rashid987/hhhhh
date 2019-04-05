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

#### Code flow.
#### 1.Background.js
 - 1.set() will call the scan function.
 - 2.scan will return array of all the cityids stored in redis. 
 - 3.all the cityids are sorted and depending on the no. of server running and the serverNo a subarray of cityids will be update.  
 - eq. if 5 servers are running and this is 4th servers and no fo cityids are 100. then this server will update the cityid from index 60 to 79. 
 -4.In this subarray for each cityid openweather request will be made and data will be stored in redis.
#### 2.migration.sh
 - 1.download the cassandra-data depending on the filename.
 - 2.file is processed and ips.json file is created with.
 - 3.migrationScript.js is run for populating the data.

#### 3.migrationScript.js
  - 1.ips from ips.json files are converted to ipNumbers and sorted.
  - 2.out off this sorted list subarray of 500 ips are used to call getIpData which will get the  
  - city for this ip from mysql and will store the ip to city mapping in redis and cityIds array is created and on callback next 500 ips will be called.
  - 3.for each cityid in array, openweather is called which will store the city data in redis.

 #### 4.ipLookup.js
  - 1.first ip to cityid mapping is checked in redis for the ip.
  - 2.if cityid is found then getCityData is called.
  - 3.if cityid is not  present then getIpData is called
  - 4.getIpData will check the ip to cityid mapping in mysql,will store the data in redis and getCityData is called.
  - 5.getCityData will check the cityData in redis.
  - 6.if data is found then data is formated and response is send.
  - 7.if data is not present then openWeather is called with id.
  - 8.openWeather will make the request to openweather server depending on the cityid and responseData is stored in redis.
  - 9.after getting the data from openweather data is formated and response is send.

   
