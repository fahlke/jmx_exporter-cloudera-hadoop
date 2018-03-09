# jmx_exporter-cloudera-hadoop

Prometheus jmx_exporter configurations for Cloudera Hadoop.

## Cloudera Hadoop Metrics

For Cloudera Hadoop I enabled jmxremote for each service via the extra java options and used jmxterm to get all beans I needed. Don't forget to remove the jmxremote settings after you are finished.

## Exporter ports and configuration files

The table is sorted alphabetically by service name.

| Service   | Role                    | JMX port  | Exporter port | Configuration file                          |
|:----------|:------------------------|:----------|:--------------|:--------------------------------------------|
| HDFS      | NameNode                | 18000     | 19000         | [cdh-hdfs-namenode.yaml][1]                 |
| HDFS      | SecondaryNameNode       | 18001     | 19001         | [cdh-hdfs-secondarynamenode.yaml][2]        |
| HDFS      | JournalNode             | 18002     | 19002         | [cdh-hdfs-journalnode.yaml][3]              |
| HDFS      | Failover Controller     | 18003     | 19003         | [cdh-hdfs-failover-controller.yaml][4]      |
| HDFS      | HttpFS                  | 18004     | 19004         | [cdh-hdfs-httpfs.yaml][5]                   |
| HDFS      | Balancer                | 18005     | 19005         | [cdh-hdfs-balancer.yaml][6]                 |
| HDFS      | NFS Gateway             | 18006     | 19006         | [cdh-hdfs-nfs-gateway.yaml][7]              |
| HDFS      | DataNode                | 18007     | 19007         | [cdh-hdfs-datanode.yaml][8]                 |
| Hive      | HiveServer2             | 18020     | 19020         | [cdh-hive-hiveserver2.yaml][9]              |
| Hive      | Hive Metastore Server   | 18021     | 19021         | [cdh-hive-metastore-server.yaml][10]        |
| Hive      | WebHCat Server          | 18022     | 19022         | [cdh-hive-webhcat-server.yaml][11]          |
| Hue       | Hue Server              | 18040     | 19040         | [cdh-hue-server.yaml][12]                   |
| Hue       | Kerberos Ticket Renewer | 18041     | 19041         | [cdh-hue-kerberos-ticket-renewer.yaml][13]  |
| Hue       | Loadbalancer            | 18042     | 19042         | [cdh-hue-loadbalancer.yaml][14]             |
| Kafka     | Kafka Broker            | 18090     | 19090         | [cdh-kafka-broker.yaml][15]                 |
| Kafka     | Kafka MirrorMaker       | 18091     | 19091         | [cdh-kafke-mirrormaker.yaml][16]            |
| Oozie     | Oozie Server            | 18050     | 19050         | [cdh-oozie-server.yaml][17]                 |
| Sentry    | Sentry Server           | 18060     | 19060         | [cdh-sentry-server.yaml][18]                |
| Solr      | Solr Server             | 18100     | 19100         | [cdh-solr-server.yaml][19]                  |
| Spark     | History Server          | 18070     | 19070         | [cdh-spark-history-server.yaml][20]         |
| Spark 2   | History Server          | 18080     | 19080         | [cdh-spark2-history-server.yaml][21]        |
| YARN      | ResourceManager         | 18010     | 19010         | [cdh-yarn-resourcemanager.yaml][22]         |
| YARN      | JobHistory Server       | 18011     | 19011         | [cdh-yarn-jobhistory-server.yaml][23]       |
| YARN      | NodeManager             | 18012     | 19012         | [cdh-yarn-nodemanager.yaml][24]             |
| ZooKeeper | Server                  | 18030     | 19030         | [cdh-zookeeper-server.yaml][25]             |

## JMX configuration for getting MBeans

### Enable jmxremote

Example for configuring the DataNode:

    HADOOP_DATANODE_OPTS=<DEFAULT OPTIONS PROVIDED BY CLOUDERA> \
    -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=18007 \
    -Dcom.sun.management.jmxremote.local.only=true \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false

### Get MBeans with jmxterm

    $ java -jar jmxterm.jar --url localhost:18007
    $>beans
    #domain = Hadoop:
    Hadoop:name=DataNodeInfo,service=DataNode
    Hadoop:name=UgiMetrics,service=DataNode
    Hadoop:name=JvmMetrics,service=DataNode
    Hadoop:name=MetricsSystem,service=DataNode,sub=Control
    Hadoop:name=MetricsSystem,service=DataNode,sub=Stats
    Hadoop:name=RpcActivityForPort50020,service=DataNode
    Hadoop:name=RpcDetailedActivityForPort50020,service=DataNode
    ....

[1]: configuration/cdh-hdfs-namenode.yaml
[2]: configuration/cdh-hdfs-secondarynamenode.yaml
[3]: configuration/cdh-hdfs-journalnode.yaml
[4]: configuration/cdh-hdfs-failover-controller.yaml
[5]: configuration/cdh-hdfs-httpfs.yaml
[6]: configuration/cdh-hdfs-balancer.yaml
[7]: configuration/cdh-hdfs-nfs-gateway.yaml
[8]: configuration/cdh-hdfs-datanode.yaml
[9]: configuration/cdh-hive-hiveserver2.yaml
[10]: configuration/cdh-hive-metastore-server.yaml
[11]: configuration/cdh-hive-webhcat-server.yaml
[12]: configuration/cdh-hue-server.yaml
[13]: configuration/cdh-hue-kerberos-ticket-renewer.yaml
[14]: configuration/cdh-hue-loadbalancer.yaml
[15]: configuration/cdh-kafka-broker.yaml
[16]: configuration/cdh-kafke-mirrormaker.yaml
[17]: configuration/cdh-oozie-server.yaml
[18]: configuration/cdh-sentry-server.yaml
[19]: configuration/cdh-solr-server.yaml
[20]: configuration/cdh-spark-history-server.yaml
[21]: configuration/cdh-spark2-history-server.yaml
[22]: configuration/cdh-yarn-resourcemanager.yaml
[23]: configuration/cdh-yarn-jobhistory-server.yaml
[24]: configuration/cdh-yarn-nodemanager.yaml
[25]: configuration/cdh-zookeeper-server.yaml