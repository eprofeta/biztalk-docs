---
title: "Message Schemas for the Basic Insert, Update, Delete, and Select Operations on Tables and Views | Microsoft Docs"
ms.custom: ""
ms.date: "06/08/2017"
ms.prod: "biztalk-server"
ms.reviewer: ""

ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "operations on tables, message actions for"
  - "table operations, message actions for"
  - "table operations, message structure for"
  - "operations on tables, message schemas for"
  - "table operations, message schemas for"
  - "operations on tables, message structure for"
ms.assetid: 8228d5e6-14af-49e0-b34b-be03aea59189
caps.latest.revision: 4
author: "MandiOhlinger"
ms.author: "mandia"
manager: "anneta"
---
# Message Schemas for the Basic Insert, Update, Delete, and Select Operations on Tables and Views
The [!INCLUDE[adapteroracle](../../includes/adapteroracle-md.md)] surfaces basic Insert, Update, Delete, and Select operations for each table and view in the Oracle database. These operations perform the appropriate SQL statement qualified by a WHERE clause. The [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] uses strongly-typed records and record sets in these operations.  
  
## Message Structure for Basic Table Operations  
 The following table shows the XML message structure for the basic table operations exposed by the [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] on Oracle database tables. The target table for an operation is specified in the message action and also appears in the target namespace.  

### Insert  
There are the following types of Insert operations. A message can contain only one kind of Insert operation.

- Multiple Record Insert inserts the supplied record set of strongly-typed data into the target table.
- For each record in a multiple record insert, you can specify value for an optional attribute called **InlineValue**. If specified, it overrides the value of the element.
- Bulk Insert inserts the record set returned by a SELECT query specified in the QUERY element into the target table. This is done by using the comma-separated list of columns specified in the COLUMN_NAMES element.

#### XML message  

**Multiple record insert**  
```
<Insert xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<RECORDSET>     
<[TABLE_NAME]RECORDINSERT>       
<[FIELD1_NAME InlineValue="value"]>value1</[FIELD1_NAME]>       
<[FIELD2_NAME InlineValue="value"]>value2</[FIELD2_NAME]>       
…     
</[TABLE_NAME]RECORDINSERT>       
<[TABLE_NAME]RECORDINSERT >       
<[FIELD1_NAME InlineValue="value"]>value1</[FIELD1_NAME]>       
<[FIELD2_NAME InlineValue="value"]>value2</[FIELD2_NAME]>       
…     
</[TABLE_NAME]RECORDINSERT>     
…   
</RECORDSET> 
</Insert>
```

SQL executed by the adapter: `INSERT INTO TABLE_NAME (FIELD1_NAME, FIELD2_NAME, …)VALUES (value1, value2, …);`


**Bulk Insert**  
```
<Insert xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">
<COLUMN_NAMES>[COLUMN_list]</COLUMN_NAMES>
<QUERY>[SELECT_query]</QUERY>
</Insert>
```

SQL executed by the adapter: `INSERT INTO TABLE_NAME (COLUMN_list) SELECT_query;`

### Insert Response
The number of rows inserted is returned in the InsertResult element.

#### XML message  

```
<InsertResponse xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<InsertResult>[rows inserted]</InsertResult> 
</InsertResponse>
```

### Select
A SELECT query is performed on the target table using the WHERE clause specified in the FILTER element. The result set contains the columns in the comma-separated list of column names specified in the COLUMN_NAMES element.

#### XML message  
```
<Select xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<COLUMN_NAMES>[COLUMN_list]</COLUMN_NAMES>   
<FILTER>WHERE_clause</FILTER> 
</Select>
```

SQL executed by the adapter: `SELECT COLUMN_list FROM TABLE_NAME WHERE WHERE_clause;`

### Select Response
The result set generated by the SELECT query.

#### XML message  
```
<SelectResponse xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<SelectResult>     
<[TABLE_NAME]RECORDSELECT>       
<[FIELD1_NAME]>value1</[FIELD1_NAME]>       
<[FIELD2_NAME]>value2</[FIELD2_NAME]>       
…     
</[TABLE_NAME]RECORDSELECT>   
</SelectResult> 
</SelectResponse>
``` 

### Update
Rows that match the where clause specified in the FILTER element are updated to the values specified in the RECORDSET. Only the columns that are specified in the RECORDSET are updated in each matching row.

#### XML message  
```
<Update xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<RECORDSET>     
<[FIELD1_NAME]>value1</[FIELD1_NAME]>     
<[FIELD2_NAME]>value2</[FIELD2_NAME]>       
…   
</RECORDSET>   
<FILTER>WHERE_clause</FILTER> </Update>
```

SQL executed by the adapter: `UPDATE [TABLE_NAME] SET [FIELD1_NAME] = value1, [FIELD2_NAME] = value2, … WHERE WHERE_clause;`

### Update Response
The number of rows updated is returned in the UpdateResult element.

#### XML message  
```
<UpdateResponse xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<UpdateResult>[rows inserted]</UpdateResult> 
</UpdateResponse>
```

### Delete
Rows matching the WHERE clause specified by the FILTER element are deleted.

#### XML message 
```
<Delete xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<FILTER>WHERE_clause</FILTER> 
</Delete>
```

SQL executed by the adapter: `DELETE FROM [TABLE_NAME] WHERE WHERE_clause;`

### Delete Response
The number of rows deleted is returned in the DeleteResult element.

#### XML message 
```
<DeleteResponse xmlns="[VERSION]/[SCHEMA]/Table/[TABLE_NAME]">   
<DeleteResult>[rows inserted]</DeleteResult> 
</DeleteResponse>
```
  
  | Placeholder value| Description |
  | --- | --- |
  | [VERSION] | The message version string; for example, `http://Microsoft.LobServices.OracleDB/2007/03`|
  | [SCHEMA] | Collection of Oracle artifacts; for example, `SCOTT`|
  | [TABLE_NAME] | Name of the table; for example, `EMP`|
  | [FIELD1_NAME] | Table field name; for example, `EMPNAME`|
  | [COLUMN_list] | Comma-separated list of columns; for example, `NAME`|
  | [SELECT_query] | A SQL SELECT statement specified in the QUERY element of a Bulk Insert operation; for example, `SELECT * from MyTable`|
  | [WHERE_clause] | WHERE_clause for the SELECT statement used for the operation; for example, `ID > 10`|
  
> [!IMPORTANT]
>  The message structure for the basic table operations on views is the same as that on tables, but the namespace for the operation specifies a view rather than a table: `<Insert xmlns ="[VERSION]/[SCHEMA]/``View``/[VIEW_NAME]">`.  
  
## Message Actions for Basic Table Operations  
 The following table shows the message actions that are used by the [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] for the basic table operations on tables. The [!INCLUDE[adapteroracle_short](../../includes/adapteroracle-short-md.md)] uses the table name specified in the message action to determine the target table of the operation.  
  
|Operation|Message Action|Example|  
|---------------|--------------------|-------------|  
|Insert|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Insert|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Insert|  
|Insert Response|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Insert/response|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Insert/response|  
|Select|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Select|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Select|  
|Select Response|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Select/response|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Select/response|  
|Update|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Update|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Update|  
|Update Response|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Update/response|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Update/response|  
|Delete|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Delete|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Delete|  
|Delete Response|[VERSION]/[SCHEMA]/Table/[TABLE_NAME]/Delete/response|http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/Table/EMP/Delete/response|  
  
 [VERSION] = The message version string; for example, http://Microsoft.LobServices.OracleDB/2007/03.  
  
 [SCHEMA] = Collection of Oracle artifacts; for example, SCOTT.  
  
 [TABLE_NAME] = Name of the table; for example, EMP.  
  
> [!IMPORTANT]
>  The message action for an operation on a view is the same as that for a table except that "View" replaces "Table"; for example, `http://Microsoft.LobServices.OracleDB/2007/03/SCOTT/``View``/EMPVIEW/Insert`.  
  
## See Also  
 [Messages and Message Schemas for BizTalk Adapter for Oracle Database](../../adapters-and-accelerators/adapter-oracle-database/messages-and-message-schemas-for-biztalk-adapter-for-oracle-database.md)