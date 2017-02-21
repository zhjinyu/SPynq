# SPynq: Spark on Pynq

###Description

Spynq is a framework for the efficient deployment of data analytics on embedded systems that are based on the heterogenous MPSoC FPGA called Pynq. The mapping of Spark on Pynq allows that fast deployment of embedded and cyber-physical systems that are used in edge and fog computing. Below we will describe the configuration steps for the deployment of Spark on Pynq as well as the actions needed to access the built-in Xilinx libraries from PySpark.

###Deploying Apache Spark

Besides the Zynq FPGA, Pynq hosts a dual-core ARM Cortex-A9 32-bit processor and 512MB of DDR3 memory. It is obvious that building Spark from source on Pynq could take too long or even end up failing since its resources are limited enough. For that reason, a pre-built version of Spark is used for the deployment. After connecting with Pynq through ssh protocol and extracting Spark to the directory of your choice, we need to follow certain steps in order for it to work.

First of all, we need to edit the following three files under the conf/ dir of Spark. 

1. **spark-defaults.conf**  _(Add or edit the following lines)_

  ```shell
  spark.eventLog.enabled           true  
  spark.eventLog.dir               {path/to/the/dir/where/log/files/will/be/stored}  
  spark.driver.memory              475M  
  spark.executor.memory            475M 
  ```
  
2. **spark-env.sh**  _(Add or edit the following lines)_  

  ```shell
  export PYSPARK_PYTHON        = python3  
  export SPARK_EXECUTOR_MEMORY = 475m  
  export SPARK_DRIVER_MEMORY   = 475m
  ```
  
  Xilinx libraries for accessing Pynq's modules, are built using python3. Not adding the first line to the configuration, would prevent applciations using those libraries from running.

3. **log4j.properties**  
Should look something like the file uploaded to the current project. (this one is optional and doesn't affect Spark execution, is used in order to hide unwanted log lines from the console)

After these configurations are made, Spark is ready to be run on Pynq. Of course, before running a Spark application, jdk has to be present and JAVA_HOME to be set properly.

 _(Under the project's conf dir you can find all of the three files mentioned above.)_
 
###Xilinx libraries for python applications
In order to use Pynq's board peripherals or the PL, always remember to append the path to Xilinx's pre-built libraries. Every python application should include the following two lines:
  ```python
  import sys
  sys.path.append('/home/xilinx')
  ```

**Contact Details:**
Christoforos Kachris

Microprocessors and Digital Systems Lab (Microlab)
School of Electrical & Computer Engineering 
National Technical University of Athens (NTUA)
Athens 
Greece

**Contributions:**
Ioannis Stamelos
Elias Koromilas


