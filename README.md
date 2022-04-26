# Network telemetry technological stack comparison:
The collection of telemetry data is carried out by different vendors in the same way and with _same_ computer programs:
|vendor		  |encoding                      |data model                    |protocol                           |subscription protocol           |       
|-----------|------------------------------|------------------------------|-----------------------------------|--------------------------------|
|open-souce	|xml<br>json<br>protobuf<br>gpb|yang                          |gprc(gnmi)<br>netconf<br>restconf  |netconf<br>openconfig rpc       |
|cisco    	|gpb=protobufs,json            |yang (openconfig)             |grpc,udp, http                     |netconf<br>cli                  |
|arista    	|gpb=protobufs                 |yang (openconfig)             |gprc(gnmi)<br>netconf              |netconf<br>cli                  |
|juniper   	|gpb=protobufs                 |yang (openconfig)             |grpc<br>udp                        |netconf<br>cli<br>openconfig rpc|
|huawei   	|gpb=protobufs                 |yang (openconfig)<br>json<xml>|grpc<br>udp                        |netconf<br>cli                  |
Well-known open source data collectors are Telegraf, Fluentd, and Logstash.

Telemetric data processing is carried out by different vendors in the same way, but using _different_ computer programs.
|vendor		  |key-value database	(data lake)                              |queuing system  |analytics pipeline	    |visualization                 |               
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
