# Network telemetry technological stack comparison:

|vendor		  |encoding                      |data model         |protocol                           |subscription protocol           |       
|-----------|------------------------------|-------------------|-----------------------------------|--------------------------------|
|open-souce	|xml<br>json<br>protobuf<br>gpb|yang               |gprc(gnmi)<br>netconf<br>restconf  |netconf<br>cli<br>openconfig rpc|
|cisco    	|                              |yang (open config)            |grpc                               ||
|arista    	|                              |                   |                                   ||
|juniper   	|gpb                           |yang               |grpc                               ||
|huawei   	|                              |                   |                                   ||



|vendor		  |key-value database	                                         |queuing system  |analytics pipeline	 |visualization                 |               
|-----------|------------------------------------------------------------|----------------|---------------------|------------------------------|
|open-souce	|hbase<br>cassanda<br>kudu<br>prometheus<br>druid<br>influxdb|kafka<br>MQ		  |Spark<br>Storm<br>Heron|Kibana<br>Graphana            |
|arista			|hbase				      |     			     |CloudVision Turbines	 |Cloud Vision Telemetry Viewers|
|cisco			|     				      |     			     |CloudVision Turbines	 |Cloud Vision Telemetry Viewers|
