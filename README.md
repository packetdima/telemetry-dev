# Network telemetry
Network telemetry software consists of two major components:
<li> Agents, which are installed on network switches, routers & firewalls and are used to communicate/send data to centralized analytics service
<li> Telemetry analytics service, which consists of queuing/load-balancing software, noSQL database, analytics software, visualization frameworks 

### Agents (or data collectors)
The collection of telemetry data from switches, routers and firewalls is done by so called agents. Agent is a collection of software, which does the following things:
<li> Gather data from network devices using data model (configuration file a.k.a. device config)
<li> Squizze and encode data
<li> Send data to centralized analytics server using transport protocol
<li> Receive commands (subscribe to data etc..) from centralized analytics server 
  
Agents are implemented by different vendors in the same way. Here is the comparison of telemetry agents:
|vendor		       |encoding/encapsulation        |data model          |transport protocol<br>dial-out<br>push|subscription protocol<br>dial-in<br>pull|       
|----------------|------------------------------|--------------------|--------------------------------------|----------------------------------------|
|microsoft(SONiC)|protobufs<br>json             |yang                |grpc                                  |grpc                                    |
|cisco    	     |protobufs<br>json             |yang<br>native<br>OC|grpc<br>udp<br>http                   |netconf<br>cli                          |
|arista    	     |protobufs<br>json             |yang                |gprc<br>netconf                       |netconf<br>cli                          |
|juniper   	     |protobufs<br>json             |yang                |grpc<br>udp                           |netconf<br>cli                          |
|huawei   	     |protobufs<br>json             |yang<br>json<xml>   |grpc<br>IPFIX<br>udp                  |grpc<br>netconf<br>cli                  |

### Telemetry analytics service
Telemetry data in large infrastrcuture could be 1-5 Tb per day.
Network vendors fork open-source software and pack it into their telemetry brand products. Here is the comparison:
  
|vendor		        |brand                        |NoSQL                              |queuing system  |analytics pipeline	  |dashboards                 |               
|-----------------|-----------------------------|-----------------------------------|----------------|----------------------|---------------------------|
|micrisoft (SONiC)|no final product             |redis                              |none?           |none?                 |none?                      |
|cisco			      |DNA center<br>nexus dashboard<br>tetration|openTSDB<br>elastic search<br>postgres<br>redis<br>prometheus<br>influx|kafka  			   |spark<br>flink                      |graphana <br>kibana                  |
|arista			      |cloud vision                 |hbase	                            |kafka 		       |                      |                           |                         
|juniper		      |junos telemetry interface    |influx   	                        |none? 			     |none?                 |juniper graphana           |                        
|huawei 		      |iMaster                      |druid<br>hdfs                      |kafka   	       |spark                 |proprietary Fabric Insight |

### Popular open-source software for network telemetry
<li> Time-series databases: cassandra, counchDB, elastic search, influxDB, MongoDB, Promotheus, RRDTool, TimescaleDB, OpenTSDB.
<li> Analytics: spark, flink.
<li> Dashboard: graphana, kibana, chronograf
<li> Data collectors are Telegraf (Cisco IOS XR), Fluentd, and Logstash.

<li> We are also seeing many new open source projects related to streaming telemetry, such as: Pipeline (backed by Cisco), OpenNTI (backed by Juniper), GoArista (backed by Arista)
