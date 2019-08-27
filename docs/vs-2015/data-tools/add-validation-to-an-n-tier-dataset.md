---
title: 向 n 层数据集添加验证 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- n-tier applications, validating
- validation [Visual Basic], n-tier data applications
- validating n-tier data applications
ms.assetid: 34ce4db6-09bb-4b46-b435-b2514aac52d3
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 4b9b4f77045732bc61fa8aa8e4496eebf86f890a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65683224"
---
# <a name="add-validation-to-an-n-tier-dataset"></a>向 n 层数据集添加验证
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

向被分隔为 n 层解决方案的数据集添加验证基本上是将验证添加到单个文件数据集 （单个项目中的数据集） 相同。 对数据执行验证的建议的位置是期间<xref:System.Data.DataTable.ColumnChanging>和/或<xref:System.Data.DataTable.RowChanging>数据表的事件。  
  
数据集设计器提供用于创建分部类可向其中添加功能到列和行的用户代码更改在数据集中数据表的事件。 有关将代码添加到在 n 层解决方案中的数据集的详细信息，请参阅[将代码添加到 n 层应用程序中的数据集](../data-tools/add-code-to-datasets-in-n-tier-applications.md)，并[n 层应用程序中将代码添加到 Tableadapter](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)。 有关分部类的详细信息，请参阅[如何：将类拆分为分部类 （类设计器）](../ide/how-to-split-a-class-into-partial-classes-class-designer.md)或[分部类和方法](https://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1)。  
  
> [!NOTE]
> 当你分离数据集与 Tableadapter (通过设置**数据集项目**属性)，将不会自动移动项目中的现有数据集分部类。 向数据集项目，必须手动移动现有数据集分部类。  
  
> [!NOTE]
> 数据集设计器不会自动创建事件处理程序在 C# 中为<xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.RowChanging>事件。 您必须手动创建事件处理程序，并挂接到基础事件的事件处理程序。 以下过程介绍如何在 Visual Basic 和 C# 中创建必需的事件处理程序。  
  
## <a name="validatechanges-to-individual-columns"></a>Validatechanges 到各个列  
 通过处理验证中的单个列的值<xref:System.Data.DataTable.ColumnChanging>事件。 <xref:System.Data.DataTable.ColumnChanging>修改列中的值时引发事件。 创建事件处理程序<xref:System.Data.DataTable.ColumnChanging>通过双击所需的列的数据集上的事件。  
  
 第一次双击某一列，该设计器生成的事件处理程序<xref:System.Data.DataTable.ColumnChanging>事件。 `If…Then`语句还会创建一个测试的特定列。 例如，双击 Northwind 订单表上的 RequiredDate 列时，则会生成以下代码：  
  
```vb  
Private Sub OrdersDataTable_ColumnChanging(ByVal sender As System.Object, ByVal e As System.Data.DataColumnChangeEventArgs) Handles Me.ColumnChanging  
    If (e.Column.ColumnName = Me.RequiredDateColumn.ColumnName) Then  
        ' Add validation code here.  
    End If  
End Sub  
```  
  
> [!NOTE]
> 在 C# 项目中，数据集设计器仅创建数据集和数据集中的各个表的分部类。 数据集设计器不会自动创建的事件处理程序<xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.RowChanging>中 C# 类似它在 Visual Basic 中执行的操作的事件。 在 C# 项目中，必须手动构造用于处理事件和方法挂钩到基础事件的方法。 以下过程提供了 Visual Basic 和 C# 中创建必需的事件处理程序的步骤。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-add-validation-during-changes-to-individual-column-values"></a>若要将更改过程中的验证添加到各列的值  
  
1. 在设计器中打开数据集，通过双击 **.xsd**中的文件**解决方案资源管理器**。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。  
  
2. 双击你想要验证的列。 此操作将创建<xref:System.Data.DataTable.ColumnChanging>事件处理程序。  
  
    > [!NOTE]
    > 数据集设计器不会自动创建 C# 事件的事件处理程序。 需要处理 C# 中的事件的代码包含在下一节中。 `SampleColumnChangingEvent` 创建并将其然后挂接<xref:System.Data.DataTable.ColumnChanging>中的事件<xref:System.Data.DataTable.EndInit%2A>方法。  
  
3. 添加代码以验证`e.ProposedValue`包含满足要求的应用程序的数据。 如果建议的值是不可接受，设置该列以指示其包含一个错误。  
  
     下面的代码示例验证**数量**列包含多个 0。 如果**数量**小于或等于为 0，将列设置为错误。 `Else`子句中，如果清除该错误**Quantity**大于 0。 中的列更改事件处理程序的代码应如下所示：  
  
    ```vb  
    If (e.Column.ColumnName = Me.QuantityColumn.ColumnName) Then  
        If CType(e.ProposedValue, Short) <= 0 Then  
            e.Row.SetColumnError(e.Column, "Quantity must be greater than 0")  
        Else  
            e.Row.SetColumnError(e.Column, "")  
        End If  
    End If  
    ```  
  
    ```csharp  
    // C#  
    // Add this code to the DataTable   
    // partial class.  
  
        public override void EndInit()  
        {  
            base.EndInit();  
            // Hook up the ColumnChanging event  
            // to call the SampleColumnChangingEvent method.  
            ColumnChanging += SampleColumnChangingEvent;  
        }  
  
        public void SampleColumnChangingEvent(object sender, System.Data.DataColumnChangeEventArgs e)  
        {  
            if (e.Column.ColumnName == QuantityColumn.ColumnName)  
            {  
                if ((short)e.ProposedValue <= 0)  
                {  
                    e.Row.SetColumnError("Quantity", "Quantity must be greater than 0");  
                }  
                else  
                {  
                    e.Row.SetColumnError("Quantity", "");  
                }  
            }  
        }  
    ```  
  
## <a name="validatechanges-to-whole-rows"></a>对整个行 Validatechanges  
 通过处理验证中整个行的值<xref:System.Data.DataTable.RowChanging>事件。 <xref:System.Data.DataTable.RowChanging>提交中的所有列的值时引发事件。 需要在验证<xref:System.Data.DataTable.RowChanging>事件时将一个列中的值依赖于另一个列中的值。 例如，考虑订购日期和 RequiredDate Northwind 中的 Orders 表中。  
  
 当输入订单时，验证可确保不使用位于或早于订购日期 RequiredDate 输入订单。 在此示例中，要求日期和订购日期列的值需要进行比较，以便验证单个列更改是没有意义。  
  
 创建事件处理程序<xref:System.Data.DataTable.RowChanging>通过双击表名的表的标题栏中的事件。  
  
#### <a name="to-add-validation-during-changes-to-whole-rows"></a>若要添加到整个行的过程中更改的验证  
  
1. 在设计器中打开数据集，通过双击 **.xsd**中的文件**解决方案资源管理器**。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。  
  
2. 双击设计器上的数据表的标题栏。  
  
     分部类创建与`RowChanging`事件处理程序并在代码编辑器中打开。  
  
    > [!NOTE]
    > 数据集设计器不会自动创建的事件处理程序<xref:System.Data.DataTable.RowChanging>C# 项目中的事件。 您必须创建一个方法来处理<xref:System.Data.DataTable.RowChanging>要挂接表的初始化方法中的事件的事件和运行的代码。  
  
3. 添加用户代码的分部类声明。  
  
4. 下面的代码演示在何处添加用户代码来验证期间<xref:System.Data.DataTable.RowChanging>适用于 Visual Basic 的事件：  
  
    ```vb  
    Partial Class OrdersDataTable  
        Private Sub OrdersDataTable_OrdersRowChanging(ByVal sender As System.Object, ByVal e As OrdersRowChangeEvent) Handles Me.OrdersRowChanging  
            ' Add logic to validate columns here.  
            If e.Row.RequiredDate <= e.Row.OrderDate Then  
                ' Set the RowError if validation fails.  
                e.Row.RowError = "Required Date cannot be on or before the OrderDate"  
            Else  
                ' Clear the RowError when validation passes.  
                e.Row.RowError = ""  
            End If  
        End Sub  
    End Class  
    ```  
  
5. 下面的代码演示如何创建`RowChanging`事件处理程序以及在何处添加用户代码，以验证期间<xref:System.Data.DataTable.RowChanging>适用于 C# 事件：  
  
    ```csharp  
    partial class OrdersDataTable  
    {  
        public override void EndInit()  
        {  
            base.EndInit();  
            // Hook up the event to the  
            // RowChangingEvent method.  
            OrdersRowChanging += RowChangingEvent;  
        }  
  
        public void RowChangingEvent(object sender, OrdersRowChangeEvent e)  
        {  
            // Perform the validation logic.  
            if (e.Row.RequiredDate <= e.Row.OrderDate)  
            {  
                // Set the row to an error when validation fails.  
                e.Row.RowError = "Required Date cannot be on or before the OrderDate";  
            }  
            else  
            {  
                // Clear the RowError if validation passes.  
                e.Row.RowError = "";  
            }  
        }  
    }  
    ```  
  
## <a name="see-also"></a>请参阅  
 [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)   
 [演练：创建 N 层数据应用程序](../data-tools/walkthrough-creating-an-n-tier-data-application.md)   
 [验证数据集中的数据](../data-tools/validate-data-in-datasets.md)
