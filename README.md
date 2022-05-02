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
|juniper   	     |`protobufs` `json`        |`yang`              |`grpc` `udp`                          |`netconf` `cli`                         |
|huawei   	     |`protobufs` `json`        |`yang` `json` `xml` |`grpc` `IPFIX` `udp`                  |`grpc` `netconf` `cli`                  |
  
### Telemetry analytics service
Telemetry data in large infrastrcuture could be `1-5 Tb per day.`
Network vendors fork open-source software and pack it into their telemetry brand products. Here is the comparison:
  
|vendor		        |brand                                 |data lake                 |queuing          |analytics	    |dashboards           |
|-----------------|--------------------------------------|--------------------------|-----------------|---------------|---------------------|
|micrisoft (SONiC)|none                                  |`redis`                   |`none`           |`none`         |`none                |
|cisco			      |tetration                             |`kafka`  			            |`?`              |`?`            |`?`                  |
|cisco			      |nexus dashboard                       |`kafka`                   |`spark` `flink`  |`?`            |`?`                  |
|cisco			      |DNA center                            |`influxdb`                |`kafka`  		    |`spark`        |`?`                  |
|arista			      |cloud vision                          |`hbase`                   |`kafka` 		      |               |                     |                         
|juniper		      |junos telemetry interface             |`influx`                  |`none`           |`kapacitor`    |`juniper graphana`   |                        
|huawei 		      |iMaster                               |`druid` `hdfs`            |`kafka`   	      |`spark`        |`proprietary`        |

### Popular open-source software for network telemetry  
|function                 |software                                                                                       |
|-------------------------|-----------------------------------------------------------------------------------------------|
|time-series databases    |`influxDB` `kdb+` `promotheus` `RRDTool` `timescaleDB` `graphite` `openTSDB` `victoria metrics`|
|other databases used     |`cassandra` `counchDB` `elastic search` `mongoDB` `hbase` `redis` `kudu` `druid`               |
|analytics                |`spark` `flink` `kapacitor` `storm` `heron`                                                    |
|queing                   |`kafka` `rabbitMQ` `zeroMQ` `activeMQ`                                                         |
|dashboard                |`graphana` `kibana` `chronograf`                                                               |
|data collectors          |`telegraf` `fluentd` `logstash` `metricbeat` `logstash` `collectd` `statsd`                    |
  
We are also seeing many new open source projects related to streaming telemetry, such as: Pipeline (backed by Cisco), OpenNTI (backed by Juniper), GoArista (backed by Arista)
