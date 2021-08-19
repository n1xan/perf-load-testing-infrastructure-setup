# graphana-influxdb-reports-setup
# Pull and start the influxDB docker image
`docker pull influxdb:1.8`
# Download influx config 
Download from [https://openplant.b-cdn.net/wp-content/uploads/influxdb.conf](https://openplant.b-cdn.net/wp-content/uploads/influxdb.conf) and save at location: `C:\ProgramData\InfluxDB`

`docker run -p 8086:8086 --name influxdb2 -v C:/ProgramData/InfluxDB:/var/lib/influxdb influxdb:1.8`

`docker exec -it influxdb bash`

# Create the webpagetest database
`influx`

`CREATE DATABASE webpagetest`

# Access influxdb instance

Navigate to [http://localhost:8086/](http://localhost:8086/) - 404 error IS EXPECTED

Navigate to [http://localhost:8086/query?pretty=true&q=SELECT%20*%20FROM%20%22webpagetest%22&db=webpagetest](http://localhost:8086/query?pretty=true&q=SELECT%20*%20FROM%20%22webpagetest%22&db=webpagetest) to query the newly created Database

# Pull and run the graphana docker image 
`docker run -d -p 3000:3000 --name graphana grafana/grafana`

# Add InfluxDB Datasource
* Access graphana by visiting [http://localhost:3000/](http://localhost:3000/)
* Login using admin/admin
* Set new password
* Open Settings/Add Datasource InfluxDB
* Fill in DataSource name, url: http://localhost:8086/, for Access Select type "Browser"
* Click on Save & Test

# WebPageTest integration [https://github.com/n1xan/webpagetest-nodejs-runner](https://github.com/n1xan/webpagetest-nodejs-runner)
# Google Page Speed integration [https://github.com/n1xan/psi-report](https://github.com/n1xan/psi-report)
# JMeter integration [https://jmeter.apache.org/usermanual/realtime-results.html](https://jmeter.apache.org/usermanual/realtime-results.html)
# Telegraf Server monitoring
* Download `https://dl.influxdata.com/telegraf/releases/telegraf-1.16.2_windows_amd64.zip`
* Unzip
* Edit telegraf.config
* Set database name /should be created/
* Save
* cmd `telegraf.exe --config telegraf.conf`
* debug `telegraf.exe --config telegraf.conf --debug`
