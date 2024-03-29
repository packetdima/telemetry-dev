# Network telemetry
Network telemetry software consists of two major components:<br>
`Data collectors` is a software which installed on network switches, routers & firewalls and are used to communicate/send data to centralized analytics service<br>
`Analytics engine` is a service, which consists of queuing/load-balancing software, noSQL database, analytics software, visualization frameworks. 
  
`Data collectors` are implemented by different vendors in the same way. Here is the comparison:
|vendor		       |encoding & encap          |data model          |dial-out<br>push<br>transport protocol|dial-in<br>pull<br>subscription protocol|       
|----------------|--------------------------|--------------------|--------------------------------------|----------------------------------------|
|microsoft(SONiC)|`protobufs` `json`        |`yang`              |`grpc`                                |`grpc`                                  |
|cisco    	     |`protobufs` `json`        |`yang` `native` `OC`|`grpc` `udp`                          |`netconf` `cli`                         |
|arista    	     |`protobufs` `json`        |`yang`              |`gprc` `netconf`                      |`netconf` `cli`                         |
|juniper   	     |`protobufs` `json` `avro` |`yang`              |`grpc` `udp`                          |`netconf` `cli`                         |
|huawei   	     |`protobufs` `json`        |`yang` `json` `xml` |`grpc` `IPFIX` `udp`                  |`grpc` `netconf` `cli`                  |
  
### Telemetry analytics service
Telemetry data in large infrastrcuture could be `1-5 Tb per day.`
Network vendors fork open-source software and pack it into their telemetry brand products. Here is the comparison:
  
|vendor		        |brand                    |data lake                              |queuing   |analytics	     |dashboards         |
|-----------------|-------------------------|---------------------------------------|----------|---------------|-------------------|
|micrisoft (SONiC)|none                     |`redis`                                |`none`    |`none`         |`none`             |
|cisco			      |tetration                |`druid` `mongodb` `hdfs`               |`kafka`   |`spark`        |`proprietary`      |
|cisco			      |nexus dashboard          |`elastic search`                       |`kafka`   |`flink` `spark`|`proprietary`      |
|cisco			      |DNA center               |`influxdb`                             |`kafka`   |`spark`        |`proprietary`      |
|cisco			      |pipeline                 |`influx` `elastic search` `prometheous`|`kafka`   |`?`            |`grafana`          |
|arista			      |cloud vision             |`hbase` `elastic search` `hdfs`        |`kafka`   |`proprietary`  |`proprietary`      |
|arista			      |go arista                |`influx` `elastic search`              |`kafka`   |`?`            |`?`                |                         
|juniper		      |jti mon                  |`prometheous` `influx`                 |`kafka`   |`none`         |`none`             |
|juniper		      |open NTI                 |`influx`                               |`?`       |`none`         |`grafana`          |
|huawei 		      |iMaster                  |`druid` `hdfs`                         |`kafka`   |`spark`        |`proprietary`      |

We are also seeing many new open source projects related to streaming telemetry, such as: Pipeline (backed by Cisco), OpenNTI (backed by Juniper), GoArista (backed by Arista)


### Popular open-source software for network telemetry  
|function                 |software                                                                                                       |
|-------------------------|---------------------------------------------------------------------------------------------------------------|
|time-series databases    |`influxDB` `kdb+` `promotheus` `RRDTool` `timescaleDB` `graphite` `openTSDB` `victoria metrics` `warp10`       |
|other databases used     |`cassandra` `counchDB` `elastic search` `mongoDB` `hbase` `redis` `kudu` `druid`                               |
|analytics                |`spark` `flink` `kapacitor` `storm` `heron`                                                                    |
|queing                   |`kafka` `rabbitMQ` `zeroMQ` `activeMQ`                                                                         |
|dashboard                |`graphana` `kibana` `chronograf`                                                                               |
|data collectors          |`telegraf` `fluentd` `logstash` `metricbeat` `logstash` `collectd` `statsd` `beats` `promtail` `node-exporter` |

### Databases for telemetry comparison
We tested the following databases functionality (not performance) as telemetry data storage. Here are our findings:

|database                 |remarks                                                                                                        |
|-------------------------|---------------------------------------------------------------------------------------------------------------|
|influx    |`many plugins for telegraf` `beautiful UI analogue to kibana & graphana` `easy to install` `many succcess stories` `queing is integraded` `replication/backup function is not free` `joining data is pain with CPU 100% utilization`| 
|promotheus|`works with pull data gathering model` `not suitable if  network devices are behind NAT` `need to install aditional push-server`| 
|openTSDB|`no ecosystem` `hard to install`| 
|victoria metrics|`no success stories` `political`| 
|warp10|`has great UI` `has ecosystem`| 
|elastic search|`has great ecosystem` `well-known product` `breaks when indices more than 50M entries` | 
