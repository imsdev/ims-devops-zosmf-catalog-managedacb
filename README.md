## Setup IMS catalog with managed ACBs

**Overview**

With the IMS catalog and managed ACBs workflow you can rapidly provision the catalog with [managed ACBs](https://www.ibm.com/support/knowledgecenter/en/SSEPH2_14.1.0/com.ibm.ims14.doc.sdg/ims_catalog_acb_mgmt.htm) using the IBM® z/OS® Management Facility (z/OSMF) 

IMS can manage the runtime application control blocks (ACBs) for databases and program views for you. When IMS manages ACBs, IMS no longer requires DBD, PSB, and ACB libraries

The workflow will provision the catalog with managed ACBs to an existing IMS with these steps:
* Create the catalog database.
* Create the IMS DFSDFxxx proclib members to enable IMS catalog with managed ACBs.
* Load the catalog database.
* Build the IMS catalog directory data sets.

The workflow will also optionally take an image copy of the HALDB catalog database.

**Pre-requisites**
* An SMP/E installation of IMS is done and the IMS load libraries are available.
* Identify the z/OS system parameters
* IMS SVC modules are installed on the system
* The Common Service Layer must be started.
* z/OSMF must be started. Both the angel and server z/OSMF address spaces must be started. 

**Security requirements**  
To run the workflow, you need the following authority:
* RACF read authority on SMP/E installed IMS libraries
* RACF update authority on the high level qualifiers (HLQs) you are using for the IMS instance libraries
* Authority to ADD/DELETE APF authorizations

**Package structure**  
The repository includes the following files:
* setupCatalogManagedACB.xml
  * This is the file that provisions the catalog with managed ACBs. You should not modify the workflow XML.
* workflow_variables.properties
  * This properties file contains values from the variables referenced in the setupCatalogManagedACB.xml workflow. Edit the workflow_variables.properties file to specify the system specific information for the variables in the file. 

**Installation**  
* FTP the setupCatalogManagedACB.xml workflow and the workflow_variables.properties file to the z/OS host USS in binary mode.
* The files need to be made visible to the z/OSMF application.  Do this by changing the access permissions of the files using the chmod command
* Examples: 
```Java
chmod 755 setupCatalogManagedACB.xml
```
* Or if the file is in a folder with the name of workflows:
```Java 
chmod -R 755 workflows
```

**Common errors**
* IZUWF0105E   Workflow property file file-name is either not found or cannot be accessed
  * Typically this error comes from the file not existing at the path given, or the file exists, and chmod needs to be done on this file.

**z/OSMF documentation**
https://www.ibm.com/support/knowledgecenter/search/IBM%20z%2FOS%20Management%20Facility?scope=SSLTBW_2.2.0
