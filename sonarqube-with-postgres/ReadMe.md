SonarQube

SonarQube is an essential tool for maintaining code quality and ensuring adherence to coding standards. By integrating it with a PostgreSQL database in a Docker container, you can efficiently analyze your code and gain valuable insights into potential issues. This guide will walk you through the step-by-step process of setting up SonarQube with a Postgres database using Docker, allowing for quick code quality analysis.

Issues:
1. ElasticSearch will not come up in WSL 2. 
    ```
    sonarqube   | 2024.04.24 12:57:39 INFO  es[][o.e.b.BootstrapChecks] explicitly enforcing bootstrap checks
    sonarqube   | 2024.04.24 12:57:39 ERROR es[][o.e.b.Elasticsearch] node validation exception
    sonarqube   | [1] bootstrap checks failed. You must address the points described in the following [1] lines before starting Elasticsearch. For more information see [https://www.elastic.co/guide/en/elasticsearch/reference/8.11/bootstrap-checks.html]
    sonarqube   | bootstrap check failure [1] of [1]: max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]; for more information see [https://www.elastic.co/guide/en/elasticsearch/reference/8.11/_maximum_map_count_check.html]
    sonarqube   | ERROR: Elasticsearch did not exit normally - check the logs at /opt/sonarqube/logs/sonarqube.log
    sonarqube   | 2024.04.24 12:57:39 WARN  es[][o.e.n.Node] unexpected exception while waiting for http server to close
    sonarqube   | java.util.concurrent.ExecutionException: java.lang.IllegalStateException: Can't move to stopped state when not started
    sonarqube   |   at java.util.concurrent.FutureTask.report(Unknown Source) ~[?:?]
    sonarqube   |   at java.util.concurrent.FutureTask.get(Unknown Source) ~[?:?]
    sonarqube   |   at org.elasticsearch.node.Node.prepareForClose(Node.java:1776) ~[elasticsearch-8.11.0.jar:?]
    sonarqube   |   at org.elasticsearch.bootstrap.Elasticsearch.shutdown(Elasticsearch.java:468) ~[elasticsearch-8.11.0.jar:?]
    sonarqube   |   at java.lang.Thread.run(Unknown Source) ~[?:?]
    sonarqube   | Caused by: java.lang.IllegalStateException: Can't move to stopped state when not started
    sonarqube   |   at org.elasticsearch.common.component.Lifecycle.canMoveToStopped(Lifecycle.java:128) ~[elasticsearch-8.11.0.jar:?]
    sonarqube   |   at org.elasticsearch.common.component.AbstractLifecycleComponent.stop(AbstractLifecycleComponent.java:73) ~[elasticsearch-8.11.0.jar:?]
    sonarqube   |   at org.elasticsearch.node.Node.lambda$prepareForClose$59(Node.java:1768) ~[elasticsearch-8.11.0.jar:?]
    sonarqube   |   at java.util.concurrent.FutureTask.run(Unknown Source) ~[?:?]
    sonarqube   |   ... 1 more
    ```
    Here are the steps on how to increase vm.max_map_count in WSL2:
    Open a command prompt or PowerShell window.
    Create a .wslconfig file in your %userprofile% directory if it doesn't exist.
    Add the following line to the .wslconfig file:
    ```
    [wsl2]
    kernelCommandLine = "sysctl.vm.max_map_count=262144"
    ```
    Save the .wslconfig file and Restart your WSL2 distribution.
   
    To verify that the change has been made, you can run the following command in a WSL2 terminal:
    ```
    sysctl vm.max_map_count
    ```
    This should output the value 262144.

    Note: You may need to increase the value of vm.max_map_count even higher if you are running a large number of Docker containers or if you are using Elasticsearch
    * Here are some additional tips for increasing vm.max_map_count in WSL2:
        * If you are using Docker Desktop, you can also increase the value of vm.max_map_count by editing the Docker Desktop settings. To do this, open the Docker Desktop settings and go to the Resources tab. Under the WSL Integration section, increase the value of the Max map count setting.
        * If you are using a different WSL distribution, such as Ubuntu or Debian, you can increase the value of vm.max_map_count by editing the /etc/sysctl.conf file. To do this, open the /etc/sysctl.conf file in a text editor and add the following line:
          ```
          vm.max_map_count=262144
          ```
          Save the file and restart your WSL distribution.
