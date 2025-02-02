---
title: Enter Parameter Value dialog box appears
description: Describes a problem that may occur when you try to run a query, a form, or a report in Access. The Enter Parameter Value dialog box may appear unexpectedly.
author: helenclu
manager: dcscontentpm
ms.custom: 
  - CI 111294
  - CSSTroubleshoot
search.appverid: 
  - MET150
audience: ITPro
ms.topic: troubleshooting
ms.author: luche
ms.reviewer: STECLEVE
appliesto: 
  - Access 2007
  - Access 2003
  - Access 2002
ms.date: 03/31/2022
---

# "Enter Parameter Value" dialog box appears when you run a query, a form, or a report

Moderate: Requires basic macro, coding, and interoperability skills.

This article applies only to a Microsoft Access database (.mdb).

## Symptoms

When you try to run a query, a form, or a report, the **Enter Parameter Value** dialog box may appear unexpectedly.

## Cause

This behavior occurs when a field, a criteria, an expression, or a control in a query, a form, or a report references a name that Access cannot find. For example, a name could be misspelled or a field may not be available within that scope. 

## Resolution

To resolve this behavior, rename the reference to a valid field name. If you don't know where the reference is located, run the Database Documenter for the object listed in the Enter Parameter Value dialog box, and then output the information to a text file. To do so, follow these steps:

- If you use Access 2002 and 2003, follow these steps:
  1. On the **Tools** menu, point to **Analyze**, and then select **Documenter**.
  2. Select the tab that corresponds to the type of database object that you're looking for, and then select the check box of the query, the form, or the report that you tried to run.

     **Note** If the object is a form or a report, include all source queries and subforms or subreports in your list of selections.
  3. Select **Options** to specify which feature of the selected object you want to print, and then select **OK**.
  4. Select **OK** to close the **Documenter** dialog box.
  5. On the **File** menu, select **Export**.
  6. In the **Save as type** list, select **Text Files**, and then complete the remainder of the information as needed.   
  7. Open the exported file in Microsoft Word, and then search for the parameter requested in the **Enter Parameter Value** dialog box.
- If you use Access 2007 or a later version, follow these steps:
  1. On the **Database Tools** tab, select **Database Documenter** in the **Analyze** group.
  2. Select the tab that corresponds to the type of database object that you're looking for, and then select the check box of the query, the form, or the report that you tried to run.

     **Note** If the object is a form or a report, include all source queries and subforms or subreports in your list of selections.
  3. Select **Options** to specify which feature of the selected object you want to print, and then select **OK**.
  4. Select **OK** to close the **Documenter** dialog box.
  5. In **Data** group, select **Text File**, and then complete the remainder of the information as needed.
  6. Open the exported file in Microsoft Word, and then search for the parameter requested in the **Enter Parameter Value** dialog box.

If you can't run the Database Documenter, check to see if there's a missing reference. The most common missing reference in this case is to the Utility.mda. To check for this reference, follow these steps:

1. In the Database window, select **Modules** under **Objects**.

   **Note** If you use Access 2007 or a later version, on the Database Tools tab, select **Visual Basic**, and then go to step 3.
2. Select any existing module, and then select Design or insert a new module to start the Visual Basic Editor.
3. On the Tools menu, select References.
4. In the Available References list, look for any reference that has "MISSING: " in front of the name. Clear the check box.

   **NOTE** If you don't need a reference to Utility.mda, skip to step 8.
5. Select Browse.
6. In the Files of type list, select Add-ins (`*.mda`).
7. Browse to the folder that contains Utility.mda, select it, and then select Open. By default, this file is in the folder C:\Program Files\Microsoft Office\Office\1033.
8. Select OK.
9. On the Debug menu, select Compile **database name**.
10. On the File menu, select **Close and Return to Microsoft Access**.

## More information

### Steps to reproduce the behavior in Access 2002 or in Access 2003

> [!CAUTION]
> If you follow the steps in this example, you modify the sample database Northwind.mdb. You may want to back up the Northwind.mdb file and follow these steps on a copy of the database.

1. Open the sample database Northwind.mdb.
2. Open the Order Subtotals query in **Design view**.
3. Rename the **OrderID** field to **OrderIDNumber**.
4. Close the query, and then select Yes to save the changes.
5. Run the Order Subtotals query.

Note that the **Enter Parameter Value** dialog box appears.
