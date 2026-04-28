# ServiceNow CMDB Bulk Import: Windows Server CI Records and CI Relationships

This repository documents a practical ServiceNow CMDB data loading exercise. The project demonstrates how Windows Server CI records can be prepared in Excel, loaded into an import set table, mapped to the correct CMDB target table, transformed, and then validated in the Windows Server and CI Relationship tables.

> **Note:** This project was completed in a ServiceNow Developer Instance for learning and portfolio purposes.

---

## Project Objective

The aim of this project was to practise a real CMDB data import workflow using ServiceNow Import Sets and Transform Maps.

The work covers:

- Preparing Windows Server CI data in Excel
- Loading spreadsheet data into ServiceNow
- Creating an import set table
- Creating and configuring a Transform Map
- Mapping source fields to the Windows Server CMDB class
- Running the transform process
- Validating inserted CI records
- Reviewing bulk-created CI relationships

---

## Tools and Platform Used

- ServiceNow Developer Instance
- ServiceNow CMDB
- Import Sets
- Transform Maps
- Mapping Assist
- Microsoft Excel
- Windows Server CMDB class: `cmdb_ci_win_server`
- CI Relationship table: `cmdb_rel_ci`

---

## Source Data

The source file was prepared in Excel with sample Windows Server records. Each row represented one server CI.

Example source fields:

| Source Field | Example Value | Purpose |
|---|---:|---|
| `name` | `ABC123` | Unique server name / CI name |
| `manufacturer` | `Lenovo` | Hardware manufacturer |
| `os` | `Windows 2000` | Operating system value |

![Source Excel Data](assets/01-source-excel-data.png)

---

## Step 1: Load the Excel File into ServiceNow

The Excel file was uploaded through **System Import Sets > Load Data**.

A new import set table was created for the uploaded spreadsheet.

Example import set table:

```text
u_ritm1234_windows_server_create
```

![Load Data Screen](assets/02-load-data-screen.png)

---

## Step 2: Create the Transform Map

A Transform Map was created to move the data from the staging/import set table into the correct CMDB target table.

Target table used:

```text
Windows Server [cmdb_ci_win_server]
```

![Transform Map Target Table](assets/05-transform-map-target-table.png)

---

## Step 3: Map Source Fields to Target Fields

Using **Mapping Assist**, the Excel source columns were mapped to the correct fields in the Windows Server CMDB table.

| Source Field | Target Field |
|---|---|
| `name` | `Name` |
| `manufacturer` | `Manufacturer` |
| `os` | `Operating System` |

![Mapping Assist](assets/03-mapping-assist.png)

---

## Step 4: Select the Transform Map and Run Transform

After creating the Transform Map, it was selected from the available transform maps and run against the import set.

![Selected Transform Map](assets/06-selected-transform-map.png)

The transform completed successfully.

![Transform Complete](assets/04-transform-complete.png)

---

## Step 5: Import Processor Result

The import processor completed with a success status.

In this run, ServiceNow showed:

```text
Processed: 284
Inserts: 284
Updates: 0
Errors: 0
Empty and ignored: 0
Ignored errors: 0
```

![Import Processor Success](assets/07-import-processor-success.png)

---

## Step 6: Validate Created Windows Server Records

After the transform, the records were validated in the **Windows Servers** table.

The imported records showed the expected values:

- Name: `ABC123`, `ABC124`, `ABC125`, etc.
- Operating System: `Windows 2000`
- Manufacturer: `Lenovo`

![Windows Server Records Created](assets/09-windows-server-records-created.png)

---

## CI Relationship Bulk Load Validation

The CI Relationship table was also reviewed to confirm relationship records created through bulk loading.

Example relationship details visible in the list:

| Parent | Relationship Type | Child | Connection Strength |
|---|---|---|---|
| `ABC123` | `Receives data from::Sends data to` | `Storage Area Network 002` | `Always` |
| `ABC124` | `Receives data from::Sends data to` | `Storage Area Network 002` | `Always` |

![CI Relationship Bulk Load](assets/08-ci-relationship-bulk-load.png)

---

## What I Practised

Through this project, I practised:

- Creating import set tables
- Loading Excel data into ServiceNow
- Creating Transform Maps
- Mapping source fields to CMDB fields
- Transforming staged data into CMDB records
- Validating inserted records
- Understanding parent-child CI relationships
- Reviewing CI relationship data in `cmdb_rel_ci`
- Troubleshooting data loading and mapping outcomes

---

## Key Learning Points

### 1. Import Set Table

An import set table acts as a temporary staging table. Data is first loaded here before being transformed into the final ServiceNow table.

### 2. Transform Map

A Transform Map defines how data moves from the import set table into the target table.

In this project:

```text
Source table: u_ritm1234_windows_servers
Target table: cmdb_ci_win_server
```

### 3. Field Mapping

Field mapping ensures that each spreadsheet column updates the correct ServiceNow field.

For example:

```text
Excel column `os` → ServiceNow field `Operating System`
```

### 4. Target Table Selection

Choosing the correct target table is important. For Windows Server CIs, the correct CMDB class is:

```text
cmdb_ci_win_server
```

### 5. Validation

After transformation, the imported records should be checked in the target table to confirm that the data was inserted correctly.

---

## Portfolio Summary

This project demonstrates practical ServiceNow CMDB data management skills, including import sets, transform maps, CMDB class selection, field mapping, data transformation, and CI relationship validation.

It is relevant to roles such as:

- CMDB Analyst
- IT Asset Analyst
- IT Support Analyst
- ServiceNow Administrator Trainee
- ITSM Analyst
- Configuration Management Analyst

---

## Skills Demonstrated

- ServiceNow CMDB
- Import Sets
- Transform Maps
- Data Mapping
- Excel Data Preparation
- CI Record Creation
- CI Relationship Validation
- ITSM Data Management
- Configuration Management
- Attention to Data Quality
