
# Sample Properties for Kafka

By default, Kafka support in RHPAM is actually disabled.  To enable the feature,  
set the **org.kie.kafka.server.ext.disabled** property to **false**.  


The property **org.kie.server.jbpm-kafka.ext.topics.ExampleMessage** shows  
how you can map a Kafka topic to a Message name in your BPM Process.  
In this case, we want to map a topic called **my-kafka-topic1** to  
a BPM message called **ExampleMessage**.  In the **Start Message** task of your process,  
you need to specify the **Message** property as **ExampleMessage**

```
<!-- ========================== Kafka- Related Configuration Properties ============================== -->

<property name="org.kie.kafka.server.ext.disabled" value="false" />
<property name="org.kie.server.jbpm-kafka.ext.bootstrap.servers" value="BOOTSTRAP_SERVER_HOSTNAMES_AND_PORT" />
<property name="org.kie.server.jbpm-kafka.ext.group.id" value="YOUR_GROUP_ID" />
<!-- 
  In the following property, we are mapping the Kafka topic 'my-kafka-topic1' to a Message in our Start Event
   the Message attribute of your start event should be set to 'ExampleMessage'
 -->
<property name="org.kie.server.jbpm-kafka.ext.topics.ExampleMessage" value="my-kafka-topic1"/>

<property name="org.kie.server.jbpm-kafka.ext.auto.offset.reset" value="latest" />

<!-- SSL Config needed if you are connecting to a Broker over SSL -->
<property name="org.kie.server.jbpm-kafka.ext.ssl.keystore.location" value="" />
<property name="org.kie.server.jbpm-kafka.ext.ssl.keystore.password" value="" />

<property name="org.kie.server.jbpm-kafka.ext.ssl.truststore.location" value="" />
<property name="org.kie.server.jbpm-kafka.ext.ssl.truststore.password" value="" />
<property name="org.kie.server.jbpm-kafka.ext.security.protocol" value="SSL" />
<!-- End of SSL Config -->
```

# Sample Properties for Invoking Restful Service over SSL

Setting the **org.kie.workitem.rest.useSystemProperties** to **true** is quite important.  
Without it, all the system properties will be ignored by the KIE Server.

```
<!-- ========================== Restful over SSL Configuration Properties ============================== -->
<property name="org.kie.workitem.rest.useSystemProperties" value="true" />
<property name="javax.net.ssl.trustStore" value="" />
<property name="javax.net.ssl.trustStorePassword" value="" />
<property name="javax.net.ssl.trustStoreType" value="JKS" />

<property name="javax.net.ssl.keyStore" value="" />
<property name="javax.net.ssl.keyStorePassword" value="" />
<property name="javax.net.ssl.keyStoreType" value="JKS" />
```