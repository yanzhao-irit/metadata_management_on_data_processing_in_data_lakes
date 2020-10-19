# metadata_management_on_data_processing_in_data_lakes

## Abstract

Data Lake (DL) is known as a Big Data analysis solution. A data lake stores not only data but also the processes that were carried out on these data. It is commonly agreed that data preparation/transformation takes most of the data analyst's time. To improve the efficiency of data processing in a DL, we propose a framework which includes a metadata model and algebraic transformation operations. The metadata model ensures the findability, accessibility, interoperability and reusability of data processes as well as data lineage of processes. Moreover, each process is described through a set of coarse-grained data transforming operations which can be applied to different types of datasets. We illustrate and validate our proposal with a real medical use case implementation.

## Exploitation of the Metadata

To illustrate that our metadata model of data processing can help users find the relevant processes or datasets to improve the efficiency and efficacy of data preparation, we have implemented a graph database by Neo4j. The choice of a graph database is motivated by the scalability and flexibility as well as the interconnections of this NoSql storage system. We choose the Neo4j platform for its maturity. 

We emphasize that the process metadata should at least help users on the following stages:

- **When creating a new dataset from existing source**, data wranglers can find all other datasets created from the same source and their corresponding  processes. So that data wranglers may find code or programs that they can reuse, which saves them time and efforts.
- **When working on existing dataset**, data wranglers can find the history of the different types processes that were executed on this dataset. For example, by accessing the process of filtering the dataset, users have more confidence on the origin of transformations. In addition, if some data need to be modified or updated, users can reference the existing processes.
- **While manipulating process**, data wranglers need to reuse a data process or if they want to modify or update a process for further use, they can find all the source code and execution information.


To validate our implementation and present its application on data preparation, we introduce two examples on searching data processing metadata.

### Example 1

Another team has a project that has objective to improve the exchange and interoperability of the medical data by implementing a dataset with applied FHIR (Fast Healthcare Interoperability Resources) standard. They have planned to extract and map clinical and terminology data from the EHR database for the reason that they did not know the program EHDEN existed. Thanks to the implanted metadata of the data lake, this team can search if there are projects that have already worked on extracting clinical terminologies.



With the result, users find out the project 'EHDEN' including its sub-process 'EHDEN terminologies' and they can take advantage of its first phases on extracting clinical data and terminologies.

Before the implementation of the data lake as well as the applied metadata, different teams do their work in silos. Each team has performed the data transformation for their projects, and these processes may have already been completed by another team. With the implemented metadata, users can save lots of time and effort by finding and reusing existing processes.
 

### Example 2

A head trauma doctor wants to analyze all the medical history of his patients to have more information and to improve the effectiveness of his medical treatment. A part of his project concerns the analysis of various medical reports. He annotated a few keywords of three types of reports (paper version): hospitalization reports, neuropsychological assessments and neuropsychological examinations. The team who works on the project needs to extract the electronic version of these reports from the EHR, annotate what he marked and analyze these reports. The first step of this project is to extract the three types of reports. For the reason that the EHR database is not well documented, the team does not know where to find the corresponding data and how to restructure the reports. Therefore, they use the metadata system to check if the three types of reports are already extracted. The used query is presented below and the result is in the following figure. 


With the result, the team discovers that hospitalization reports are already extracted for the EBERS project. Although they cannot find the other two types of reports, they study the different reports that EBERS is retrieving and they are aware that all reports with their field are stored in three tables in the EHR database. They get information from EBERS queries and they contact the person who worked on EBERS to request more experiences on extracting medical reports. The effectiveness of their work is much improved by the experience from the project EBERS.