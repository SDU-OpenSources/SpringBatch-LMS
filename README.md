# SpringBatch-LMS

## Spring Batch
Spring Batch is a open source framework for enterprise batch processing. This basically means execution of various steps in pipeline. It is a flexible framework where a job is executed which consists of several steps and each step consists of READ-PROCESS-WRITE process(or a tasklet).

## Steps
Each step in Spring Batch consists of Read-Process-Write process for which we need to implement ItemReader, ItemProcessor and ItemWriter respectively.
JobLauncher is responsible for starting the job and executing all the Steps chained together.

## Project
In this repository, a basic implementation of Spring Batch is created where a simple job of updating host system status is implemented.

| Class | Description |
| --- | --- |
| [App.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/App.java) | Application Driving Class with Job Launcher |
| [BatchConfiguration.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/BatchConfiguration.java) | Spring Batch Configuration class with ItemReader, ItemProcessor, ItemWriter and DataSource Beans |
| [HostSystemStatusItemReader.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/HostSystemStatusItemReader.java) | Custom Reader Class with list of POJOs to be processed |
| [HostSystemStatusItemProcessor.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/HostSystemStatusItemProcessor.java) | Custom Processor where any massaging can be done over input data |
| [HostSystemStatusItemWriter.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/HostSystemStatusItemWriter.java) | Custom Writer Class which can be used to perform any user defined operations for write phase |
| [HostSystemStatusPojo.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/HostSystemStatusPojo.java) | Typical Pojo class |

## Steps to get it up and running.
### Import
Import the project as an existing maven project in Eclipse.
1. Download project source code and unzip it into a folder location.
2. From Eclipse, Project Explorer -> Right click -> Select Import Menu and Import.
3. Expand Maven menu.
4. And click Existing Maven Projects. Enter the project source code path from #1.

#### Fixing ojdbc7.jar Dependency
If maven build gives missing artifact exception for OJDBC Library :

Download [ojdbc7.jar](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/ojdbc7.jar) and execute following command by providing path to the download jar in command prompt.

```
mvn install:install-file -Dfile="Path/To/ojdbc7.jar" -DgroupId=com.oracle -DartifactId=ojdbc7 -Dversion=12.1.0.2 -Dpackaging=jar
```

### Configuration
Enter Oracle Database Details for LMS Schema in class [BatchConfiguration.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/0de077aef05aa43fefdc328cac533579052bf837/LMS_BatchProcessing/src/main/java/main/BatchConfiguration.java#L108-L110)(lines 108-110) inside DataSource Bean.

### Execution
Run [App.java](https://github.com/SDU-OpenSources/SpringBatch-LMS/blob/master/LMS_BatchProcessing/src/main/java/main/App.java).
#### Before Execution
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Before%20Batch.JPG">
</p>

#### After Execution
FLG_GLSTATUS and FLG_GLSUBSTATUS is updated from "ONLINE" to "BATCH" and "EOD STARTED" respectively.
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/After%20Batch.JPG">
</p>

### Spring Batch Tables
Spring Batch automatically creates several meta-data tables in DB Schema during Batch execution for tracking purposes.
To Learn more about these Meta-Data Tables, Please refer to this concise official doc [here](https://docs.spring.io/spring-batch/trunk/reference/html/metaDataSchema.html).

#### Table BATCH_JOB_INSTANCE
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Table_BATCH_JOB_INSTANCE.JPG">
</p>

#### Table BATCH_JOB_EXECUTION
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Table_BATCH_JOB_EXECUTION.JPG">
</p>

#### Table BATCH_JOB_EXECUTION_PARAMS
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Table_BATCH_JOB_EXECUTION_PARAMS.JPG">
</p>

#### Table BATCH_JOB_EXECUTION_CONTEXT
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Table_BATCH_JOB_EXECUTION_CONTEXT.JPG">
</p>

#### Table BATCH_STEP_EXECUTION
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Table_BATCH_STEP_EXECUTION.JPG">
</p>

#### Table BATCH_STEP_EXECUTION_CONTEXT
<p align="center"> 
<img src="https://raw.githubusercontent.com/SDU-OpenSources/SpringBatch-LMS/master/Illustrations/Table_BATCH_STEP_EXECUTION_CONTEXT.JPG">
</p>

## Read More?
Please find official Spring Batch documentation [here](https://docs.spring.io/spring-batch/4.1.x/reference/html/index-single.html).
