Core Java Section
Packages and Contents:

DAO Class (caseDAO) – Case Queries, Customer & Transaction DAO, Customer & Transaction DAO Implementations
Domain Class(caseModel) – Customer Details, Transactions, Connections, Getters & Setters
Main Class(caseRunner) – Customer Runner, Transaction Runner, JDBC Main

File Location: 2.1.0_Core_Java

Launch Eclipse and Import mmarshall_java.zip file

RDBMS/MYSQL Section
CDW_SAPP database 
   1. Added last updated timestamp columns to Branch and Customer
   2. Inserted records into Customer, Branch and Credit Card tables for append. Time table is updated as changes are made to Credit Card table.

File Location: 2.1.1_Customer_Transaction_Detail_Module
Execute  - Import database by running CDW_SAPP.sql using MySQL

Hadoop-HDFS-Data Warehousing Section 
All sqoop commands for Data Extraction and Transportation  from MySQL into HDFS are included in this section. The target directories for each table are listed below:
   /user/mack_sqoop/Credit_Card_System/Branch
  /user/mack_sqoop/Credit_Card_System/Credit
  /user/mack_sqoop/Credit_Card_System/Customer
  /user/mack_sqoop/Credit_Card_System/Time

File location: 2.2.1_Data_Extraction_Transportation_UsingSqoop
Execute - Enter each sqoop command found in SqoopCaseQueries.txt at command line and run to create jobs. Launch Ambari Sandbox using Hortonworks. Go to Files View to see directories. 

Hive Partitions Sections 

All Hive statements and commands for creating partitioned tables stored in HDFS and hive warehouse are included in this section. The Hive tables are listed below:

Internal table: int_BRANCH
External table: EXT_CDW_BRANCH Partition(BRANCH_STATE)
Internal table: int_CREDIT
External table: EXT_CDW_CREDIT Partition(TRANSACTION_TYPE)
Internal table: int_CUSTOMER
External table: EXT_CDW_CUSTOMER Partition(CUST_STATE)
Internal table: int_Time
External table: EXT_CDW_TIME Partition(MONTH)

File location:  2.2.2 Loading Data
Execute - Open Ambari Sandbox and go to Hive View. Enter each HiveQL command into Query Editor from Hive_data.txt and execute the query.

Oozie Section 
All actions performed using Hive, Sqoop, Oozie and RDBMS are combined to automate the process using a coordinator. All files used for this process are listed below in their respective tables:
Oozie Sqoop Jobs – OozieSqoopJobs.txt
Branch Folder 
branchQuery2.txt (Sqoop job found in OozieSqoopJobs.txt)
pre_branch.hive
cdw_branch1.hive
copyDatabranch1.hql
job.properties
workflowbranch.xml

CreditCard Folder 
creditcardQuery.txt (sqoop job found in OozieSqoopJobs.txt)
pre_credit.hive
cdw_creditcard.hive
Copydatacredit.hql
job.properties
workflow.xml

Customer Folder 
customerQuery.txt (sqoop job found in OozieSqoopJobs.txt)
pre_customer.hive
cdw_customer.hive
Copydatacustomer.hql
job.properties
workflow.xml

Time Folder 
timeQuery.txt (sqoop job found OozieSqoopJobs.txt)
pre_time.hive
cdw_time.hive
Copydatatime.hql
job.properties
workflow.xml

Coordinator Folder 
AllInOneWorkflow2.xml
Coordinator.xml
job.properties

File location: 2.2.3 Automation Process using Oozie in OozieFiles.zip
To begin this process open VMWare player, WinSCP, Ultra VNC Viewer, and Ambari. Login to shell and type sqoop-metastore to connect to metastore. Open an additional shell. Enter each sqoop job found in OozieSqoopJobs.txt at command line to create the jobs to be stored in the metastore. Upload the job.properties file in WinSCP under /root/Documents/coordinator. At the command line type oozie job -oozie http://localhost:11000/oozie -config /root/Documents/coordinator/job.properties -run to execute coordinator workflow. To monitor the process. Open a browser and enter IP address:11000/oozie to open Oozie Web Console. You can also enter “oozie job -oozie http://localhost:8080/oozie -info “job id” at the command line.

Oozie Optimized Section
This process uses a coordinator that only imports updated records in relation to the stated check values and last modified dates.  Additional sqoop jobs and workflows were created for the incremental append. All files used for this process are listed below:

Optimized Files 
OptimSqoopBranch.txt (sqoop job found in OptimizedOozieSqoopJobs.txt)
Optim_InsertTo_ExternBranch.hql
OptimSqoopCreditCard.txt (sqoop job found in OptimizedOozieSqoopJobs.txt)
Optim_InsertTo_ExternCredit.hql
OptimSqoopCustomer.txt (sqoop job found in OptimizedOozieSqoopJobs.txt)
Optim_InsertTo_ExternCustomer.hql
OptimSqoopTime.txt (sqoop job found OptimizedOozieSqoopJobs.txt)
Optim_InsertTo_ExternTime.hql

File location: 2.2.4 Optimization Append in OptimizationAppendCoord.zip
Execute - To begin this process open VMWare player, WinSCP, Ultra VNC Viewer, and Ambari. Login to shell and type sqoop-metastore to connect to metastore. Open an additional shell. Enter each sqoop job found in OptimizedOozieSqoopJobs.txt at command line to create the jobs to be stored in the metastore. Upload the Optimjob.properties file in WinSCP under /root/Documents/coordinator. At the command line type oozie job -oozie http://localhost:11000/oozie -config /root/Documents/coordinator/Optimjob.properties -run to execute coordinator workflow. To monitor the process. Open a browser and enter IP address:11000/oozie to open Oozie Web Console. You can also enter “oozie job -oozie http://localhost:8080/oozie -info “job id” at the command line.

Visualization Section 
This section uses hive queries and tools with tables created in Hive from CDW_SAPP database.
The contents are listed below:

Visualization Folder 
 Top 20 zip codes by Transaction value – Top20ZipTrans.jpg
Total Transaction by quarter in 2018- TotalTransQuart18.jpg
Visualization_Of_Data.txt

File location: Visualization in Visualization.zip
