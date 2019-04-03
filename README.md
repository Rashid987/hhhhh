weather-proxy
=============

1.Create the table using scripts/ip2location_ip2location_db11.sql
2.Get the weatherData.tar.gz from s3://cassandra-securifi/weatherData/weatherData.tar.gz.
3.Untar the file and put weatherData.csv in the scritps.
4.Insert the data using scripts/dataPopulation.sql.
5.Add configs/db.json.
5.run node scripts/migrationScript.js for migrating the data.
6.start background with command
  sudo ENV=BACKGROUND node background.js
7.start the weather server with command.
  sudo node background.js
