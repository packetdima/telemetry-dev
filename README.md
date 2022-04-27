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
|vendor		  |encoding                      |data model       |transport protocol           |subscription protocol        |       
|-----------|------------------------------|-----------------|-----------------------------|-----------------------------|
|open-souce	|xml<br>json<br>protobuf<br>gpb|yang             |gprc<br>netconf<br>restconf  |netconf<br>openconfig        |
|cisco    	|protobufs<br>json             |yang             |grpc<br>udp<br>http          |netconf<br>cli               |
|arista    	|protobufs                     |yang             |gprc<br>netconf              |netconf<br>cli               |
|juniper   	|protobufs                     |yang             |grpc<br>udp                  |netconf<br>cli<br>openconfig |
|huawei   	|protobufs                     |yang<br>json<xml>|grpc<br>udp                  |netconf<br>cli               |
  
Well-known open source data collectors are Telegraf, Fluentd, and Logstash.

### Telemetry analytics service
Telemetry data in large infrastrcuture is a lot of data, for example 1-3Tb per day. Software developers, who works with Big Data ecosystem is familiar with data analytics pipeline, which can process several terabytes of data per day. 
Network vendors fork open-source sofrware to build their telemetry products. Here is the comparison:
  
|vendor		  |NoSQL                                                       |queuing system  |analytics pipeline	    |visualization                 |               
|-----------|------------------------------------------------------------|----------------|-----------------------|------------------------------|
|open-souce	|hbase<br>cassanda<br>kudu<br>prometheus<br>druid<br>influxdb|kafka<br>MQ		  |Spark<br>Storm<br>Heron|Kibana<br>Graphana            |
|cisco			|elastic search<br>postgres<br>redis                         |kafka  			    |CloudVision Turbines	  |Cisco DNA Center, DCNM        |
|arista			|hbase				                                               |kafka 		      |CloudVision Turbines	  |Cloud Vision Telemetry Viewers|
|juniper		|     				                                               |     			      |                       |                              |
|huawei 		|     				                                               |     			      |                       |iMaster NCE-FabricInsight     |

  
We are also seeing many new open source projects related to streaming telemetry, such as:
Pipeline (backed by Cisco)
OpenNTI (backed by Juniper)
GoArista (backed by Arista)
