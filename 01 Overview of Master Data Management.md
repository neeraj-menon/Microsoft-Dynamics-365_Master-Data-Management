# Overview

The current version of **Microsoft Dynamics 365** varies depending on the specific application and module. For example, the latest version of **Dynamics 365 Sales Enterprise** is **9.0.24104.10001**, scheduled for release in December 2024. Similarly, **Dynamics 365 Customer Service** is at version **9.0.24102.1002**, with updates expected in November 2024.
## MDM Features

MDM provides several standard features that you can use to tune your MDM implementation:

- **Single-master or multi-master record modification** – You can configure a single-master environment, where only one AX 2012 instance can push updated data to SQL MDS, and all other instances are read-only. Alternatively, you can configure a multi-master environment, where all AX 2012 instances can update master data records.
    
- **Synchronization scheduling** – You can schedule entities to sync with the master database every hour, day, or week. Synchronization groups permit you to more easily schedule entities that you want to sync at the same time.
    
- **Data filtering** – You can limit the records that are pulled from the master data store to a AX 2012 instance by defining a view that retrieves a specified subset of data. For example, if you have subsidiaries in multiple geographic locations, you might want the instance in each location to pull down only products that are sold in that region. You can also limit the records that are pushed to the master data store from a AX 2012 instance by defining a query that similarly narrows the data that is selected. For example, if your vendors must meet specific requirements before they can be used in all geographic locations, you might want to synchronize only vendor records that are approved for use across the company.
    
- **Conflict identification and resolution** – When two instances make different updates to the same record, this conflict is recognized, and the conflicting records are flagged in the master data store. The conflict is reported to MDM so that you are alerted. You can then use the SQL Server Master Data Services Add-In for Microsoft Excel to manually resolve the conflict.
    
- **Customization support** – You can extend your master data coverage by adding or customizing Data Import/Export Framework entities that are used with MDM.


![Flow Diagram](./Images/Pasted%20image%2020241104123016.png)

This diagram illustrates the **MDM (Master Data Management) topology and workflow** for Microsoft Dynamics AX, showcasing how data is imported, managed, synchronized, and updated across different systems. Here’s a breakdown of each component in the diagram:

1. **Dynamics AX Instance 1**:
   - This represents a Microsoft Dynamics AX instance where data is stored and managed.

2. **Data Import/Export Framework**:
   - This is the framework within Dynamics AX that handles data import and export activities.
   - **Subscribed Entities**: Specific data entities, such as *Customers* and *Global Address Book*, are set up for MDM. These entities are subscribed to receive updates.
   - **Import/Export Job**: Jobs that handle the import or export of master data. Data changes in these entities trigger updates.

3. **Data Flow (Green and Blue Arrows)**:
   - **Green Arrows**: Represent data updates and transfers between different components.
      - For example, when entities (like Customers or Global Address Book) are updated, changes are sent to **Staging Tables**.
   - **Blue Arrows**: Represent synchronization processes and data exchanges with **SQL Server Master Data Services (MDS)**, where master data is managed.

4. **Staging Tables**:
   - Temporary storage for data changes before they are finalized in the master data system.
   - The staging tables hold data that’s imported or updated, allowing verification or transformation before it's sent to the next stage.

5. **Master Data Management (MDM)**:
   - This section is responsible for managing, synchronizing, and finalizing master data.
   - **Synchronization Job**: This job keeps master data consistent across systems, ensuring changes in Dynamics AX are reflected in SQL Server MDS and vice versa.
   - **MDM Tools**: Tools used for configuring and provisioning MDM, like:
     - **Client Configuration**: Sets up clients with the correct master data configurations.
     - **Provisioning**: Handles initial setup and updates for MDM.

6. **SQL Server Master Data Services (MDS)**:
   - A centralized repository that stores master data records, managed independently of Dynamics AX.
   - **Dynamics AX Entity Master Records**: These are the actual records maintained in SQL Server MDS, which serve as the "single source of truth" for master data.
   - **Data Flow to and from MDS**: 
      - Data updates are pushed from Dynamics AX to SQL MDS when changes occur.
      - Conversely, SQL MDS sends master data back to Dynamics AX to ensure consistency.

---

**Key Workflow Steps:**

1. **Data Updates in Dynamics AX**:
   - When subscribed entities (like customers or the global address book) are updated, these changes are pushed to the **Staging Tables** within the **Data Import/Export Framework**.

2. **Synchronization and Validation**:
   - The **Synchronization Job** in MDM retrieves updated data from the staging tables, validates it, and synchronizes it with SQL Server MDS.

3. **Master Data Management in SQL Server MDS**:
   - SQL Server MDS maintains the master data records and sends any changes back to Dynamics AX as needed, keeping data consistent across the system.

---

This diagram highlights the **importance of staging and synchronization** in managing master data, ensuring data consistency across Dynamics AX and SQL Server MDS, and illustrates how Dynamics AX uses the Data Import/Export Framework to manage data flow. Including this in your presentation can help demonstrate the technical workflow of MDM in Dynamics and its role in maintaining accurate, consistent master data.



