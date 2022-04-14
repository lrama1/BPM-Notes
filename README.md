
# Installing Required Softwares for Developing BPM

1.  Download the Zip installation of "Red Hat JBoss Enterprise Application Platform"
2.  Unzip the file into a directory.
3.  Download the Zip installation of "Red Hat Process Automation Manager v.x.x Business Central Deployable for EAP 7".
4.  Unzip the file into the same directory as the JBoss EAP.  To verify if you installed the PAM correctly,  go to the   
    **<JBOSS Install>/standalone/deployments** directory and verify that a **business-central.war** folder exists.  
5.  Download the Zip installation of the "Red Hat Process Automation Manager v.x.x Process Server for All Supported EE8 Containers".
6.  Unzip it into a temporary folder.
7.  Copy the **kie-server.war** folder to the **<JBOSS Install>/standalone/deployments** directory.
8.  Copy the contents of **SecurityPolicy** directory into **<JBOSS Install>/bin**.  
    NOTE: The operating system should prompt you if you want to overwrite the same files.  At this point,  
	click 'Yes to All'	



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
<property name="org.kie.server.jbpm-kafka.ext.ssl.keystore.location" value="KEYSTORE_FILE_FULL_PATH" />
<property name="org.kie.server.jbpm-kafka.ext.ssl.keystore.password" value="KEYSTORE_PASSWORD" />

<property name="org.kie.server.jbpm-kafka.ext.ssl.truststore.location" value="TRUSTSTORE_FILE_FULL_PATH" />
<property name="org.kie.server.jbpm-kafka.ext.ssl.truststore.password" value="TRUSTSTORE_PASSWORD" />
<property name="org.kie.server.jbpm-kafka.ext.security.protocol" value="SSL" />
<!-- End of SSL Config -->
```

# Sample Properties for Invoking Restful Service over SSL

Setting the **org.kie.workitem.rest.useSystemProperties** to **true** is quite important.  
Without it, all the system properties will be ignored by the KIE Server.

```
<!-- ========================== Restful over SSL Configuration Properties ============================== -->
<property name="org.kie.workitem.rest.useSystemProperties" value="true" />
<property name="javax.net.ssl.trustStore" value="TRUSTSTORE_FILE_FULL_PATH" />
<property name="javax.net.ssl.trustStorePassword" value="TRUSTSTORE_PASSWORD" />
<property name="javax.net.ssl.trustStoreType" value="JKS" />

<property name="javax.net.ssl.keyStore" value="KEYSTORE_FILE_FULL_PATH" />
<property name="javax.net.ssl.keyStorePassword" value="KEYSTORE_PASSWORD" />
<property name="javax.net.ssl.keyStoreType" value="JKS" />
```