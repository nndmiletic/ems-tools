# Bulk Loader

[TOC]

Bulk Loader is a system that automates the process of uploading a large number of Creo, SolidWorks, Unigraphics, and AutoCAD models and other document types to Windchill. The core of this system is EMS database which contains all metadata required for the transfer of models to Windchill. The transfer is done by the EMS Bulk Loader application, which is using the data from the EMS Database, such as: Target Context, Target Directory, Target Version etc., to successfully upload/check in the models to the Windchill. So, the most important parts of the Bulk Loader system are the EMS Database and EMS Bulk Loader.

**EMS Database** contains tables that provide mapping between existing data in SPDMS (Source PDM System) and target data in TPDMS (Target PDM System), and the basic information about the models, such as: model name, location on the local disk, source and target (Windchill) version, model dependencies, model attributes, etc.

The preparation of EMS Database is done as follows:

1. Initialize EMS Database using the init xml file. Init xml file contains the following information:
   - Information about Windchill system that is used
   - Mapping between Source/Target Revisions
   - Mapping between source lifecycle state and target lifecycle state
   - Authoring application and version
   - Global settings that will be used for uploading models to Windchill

2. Load data from the dependency xml files into the database. Dependency xml files represent the structure of the models that will be used by Bulk Loader to create identical model structure during the upload process to Windchill.

3. Perform additional tasks which should be run on database before migration starts:
   - Setting the Target Versions
   - Setting the MVO (Model Version Order column in database)
   - Analyze Data – Identify problematical data
   - Prepare Data - Set flags in database for uploading

The second most important component of Bulk Loader system is the **EMS Bulk Loader** which is used to transfer models using the data from the EMS Database. When the EMS Database is prepared for transfer, EMS Bulk Loader picks the models from the local disk and starts the upload/check in process. It communicates with EMS Windchill server component that provides EMS Bulk Loader with various services, such as document status retrieve, check-in etc. 

## Installation

Run the provided installation file and follow the installation steps in order to set the installation options and install the EMS Bulk Loader.

During the installation process, user can set the installation directory where the application will be installed. The default location is on root of the system partition.

![Figure](Figures\img001.png)

Figure 1‑1 Setting EMS Bulk Loader installation directory

*NOTE: If the appropriate version of Microsoft .NET Framework is not present on the system, the installation wizard will abort the installation process and notify the user to download and install it (a system restart might be needed after that).*