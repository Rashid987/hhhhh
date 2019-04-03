weather-proxy
=============
#### 1.install packages
    npm install
#### 2.Create the table using scripts/ip2location_ip2location_db11.sql
#### 3.Get the weatherData.tar.gz from s3://cassandra-securifi/weatherData/weatherData.tar.gz.
#### 4.Untar the file and put weatherData.csv in the scritps.
#### 5.Insert the data using scripts/dataPopulation.sql.
#### 6.Add configs/db.json.
#### 7.run node scripts/migrationScript.js for migrating the data.
#### 8.start background with command
  ENV=BACKGROUND node background.js
#### 9.start the weather server with command.
  node background.js
