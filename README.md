# Brooklyn JMeter

Provides [Apache Brooklyn](https://brooklyn.apache.org/) entites for invoking
[Apache JMeter](http://jmeter.apache.org/).


## Installing

Clone the repository and use the [Brooklyn CLI](https://brooklyn.apache.org/v/latest/ops/cli/)
to add entities to the catalogue:

    git clone git@github.com:brooklyncentral/brooklyn-jmeter.git
    cd brooklyn-jmeter/catalog
    br catalog add .


## Using

Two entities and one template are provided.

**jmeter**

A generic entity that must be configured with a plan for JMeter to execute.

*Configuration*

| Name              | Description                                   | Type   | Default |
|-------------------|-----------------------------------------------|--------|---------|
| plan              | A URL for the plan JMeter should execute      | String |         |
| shutdownPort      | The port JMeter should listen on to shut down | Port   | 4445+   |
| jmeter.properties | Command line properties                       | Map    | {}      |

`jmeter.properties` is a map intended for use with JMeter's
[`__P`](http://jmeter.apache.org/usermanual/functions.html#__P) property function.
Values in the map are transformed into `key=value` pairs and are set on the command
line to parameterise the plan when launching JMeter.


**jmeter-app**

Configures `jmeter` with a plan that is parameterised with values for host, port and path,
and the load to send to that destination. The plan runs until stopped.

*Configuration*

| Name         | Description                                                              | Type    | Default |
|--------------|--------------------------------------------------------------------------|---------|---------|
| host         | Domain name or IP address of the host JMeter should target               | String  |         |
| port         | The port JMeter should target                                            | Port    | 80      |
| path         | The path JMeter should target                                            | String  | /       |
| numThreads   | The number of threads JMeter should use                                  | Integer | 10      |
| requestDelay | The time in milliseconds each JMeter thread should wait between requests | Integer | 100     |

Throughput can be reconfigured post-deployment with an effector named `changeLoad` and 
paused with an effector named `pause`.


**jmeter-app-template**

A template packaging `jmeter-app`. Configuration is as previously described.
