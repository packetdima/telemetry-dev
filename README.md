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
|vendor		       |encoding                      |data model       |transport protocol           |subscription protocol        |       
|----------------|------------------------------|-----------------|-----------------------------|-----------------------------|
|open-souce	     |xml<br>json<br>protobuf<br>gpb|yang             |gprc<br>netconf<br>restconf  |netconf<br>openconfig        |
|microsoft(SONiC)|protobufs<br>json             |yang             |grpc                         |grpc-server                  |
|cisco    	     |protobufs<br>json             |yang             |grpc<br>udp<br>http          |netconf<br>cli               |
|arista    	     |protobufs                     |yang             |gprc<br>netconf              |netconf<br>cli               |
|juniper   	     |protobufs<br>json             |yang             |grpc<br>udp                  |netconf<br>cli               |
|huawei   	     |protobufs                     |yang<br>json<xml>|grpc<br>udp                  |netconf<br>cli               |
  
Well-known open source data collectors are Telegraf, Fluentd, and Logstash.

### Telemetry analytics service
Telemetry data in large infrastrcuture is a lot of data, for example 1-3Tb per day. Software developers, who works with Big Data ecosystem is familiar with data analytics pipeline, which can process several terabytes of data per day. 
Network vendors fork open-source software and pack it into their telemetry brand products. Here is the comparison:
  
|vendor		        |brand                      |NoSQL                              |queuing system  |analytics pipeline	  |visualization              |               
|-----------------|---------------------------|-----------------------------------|----------------|----------------------|---------------------------|
|micrisoft (SONiC)|no final product           |redis                              |none?           |none?                 |none                       |
|cisco			      |DNA Center, Nexus Dashboard|elastic search<br>postgres<br>redis<br>prometheus<br>influx|kafka  			   |                      |graphana                   |
|arista			      |cloud vision               |hbase	                            |kafka 		       |                      |                           |                         
|juniper		      |junos telemetry interface  |influx   	                        |none? 			     |none?                 |juniper graphana           |                        
|huawei 		      |iMaster                    |druid<br>hdfs                      |kafka   	       |spark                 |proprietary Fabric Insight |


We are also seeing many new open source projects related to streaming telemetry, such as:
Pipeline (backed by Cisco)
OpenNTI (backed by Juniper)
GoArista (backed by Arista)
