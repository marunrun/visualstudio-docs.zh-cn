---
title: 演练：通过使用单表继承 （O-R 设计器） 中创建 LINQ to SQL 类 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 63bc6328-e0df-4655-9ce3-5ff74dbf69a4
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: aa33d13623e1f7222eb831571d60d25404465dc4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65702981"
---
# <a name="walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-or-designer"></a>演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)支持单表继承中，通常是在关系数据库管理系统中实现。 本演练中提供的通用步骤进行了扩展[如何：通过使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)主题，并提供一些真实数据演示了如何使用中的继承[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。  
  
 在本演练中，你将要执行以下任务：  
  
- 创建一个数据库表，并向其中添加数据。  
  
- 创建一个 Windows 窗体应用程序。  
  
- 将一个 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 文件添加到项目。  
  
- 创建新的实体类。  
  
- 配置实体类使用继承。  
  
- 查询继承类。  
  
- 在 Windows 窗体上显示数据。  
  
## <a name="create-a-table-to-inherit-from"></a>创建要从中继承的表  
 为了解继承的工作方式，您将创建一个小的 Person 表用作基类，然后创建一个从该表继承的 Employee 对象。  
  
#### <a name="to-create-a-base-table-to-demonstrate-inheritance"></a>创建基表以演示继承  
  
1. 在中**服务器资源管理器**/**数据库资源管理器**，右键单击**表**节点，然后单击**添加新表**。  
  
    > [!NOTE]
    > 可以使用 Northwind 数据库或其他任何可添加表的数据库。  
  
2. 在表设计器中，向该表中添加以下列：  
  
    |列名|数据类型|允许为 Null|  
    |-----------------|---------------|-----------------|  
    |**ID**|**int**|**False**|  
    |**Type**|**int**|**True**|  
    |**FirstName**|**nvarchar(200)**|**False**|  
    |**LastName**|**nvarchar(200)**|**False**|  
    |**Manager**|**int**|**True**|  
  
3. 将 ID 列设置为主键。  
  
4. 保存该表并将其命名为 Person。  
  
## <a name="add-data-to-the-table"></a>向表中添加数据  
 为了验证对继承的配置是否正确，表对于单表继承中的每个类都需要一些数据。  
  
#### <a name="to-add-data-to-the-table"></a>向表中添加数据。  
  
1. 在数据视图中打开该表。 (右键单击**Person**表中**服务器资源管理器**/**数据库资源管理器**然后单击**显示表数据**。)  
  
2. 将下面的数据复制到表中。 （您可以将其复制，然后，通过在结果窗格中选择整行，将其粘贴到表。）  
  
    ||||||  
    |-|-|-|-|-|  
    |**ID**|**Type**|**FirstName**|**LastName**|**Manager**|  
    |**1**|**1**|**Anne**|**Wallace**|**NULL**|  
    |**2**|**1**|**Carlos**|**Grilo**|**NULL**|  
    |**3**|**1**|**Yael**|**Peled**|**NULL**|  
    |**4**|**2**|**Gatis**|**Ozolins**|**1**|  
    |**5**|**2**|**Andreas**|**Hauser**|**1**|  
    |**6**|**2**|**Tiffany**|**Phuvasate**|**1**|  
    |**7**|**2**|**Alexey**|**Orekhov**|**2**|  
    |**8**|**2**|**Michał**|**Poliszkiewicz**|**2**|  
    |**9**|**2**|**Tai**|**Yee**|**2**|  
    |**10**|**2**|**Fabricio**|**Noriega**|**3**|  
    |**11**|**2**|**Mindy**|**Martin**|**3**|  
    |**12**|**2**|**Ken**|**Kwok**|**3**|  
  
## <a name="create-a-new-project"></a>创建新项目  
 至此，表已经创建完毕，下面创建一个新项目演示对继承的配置。  
  
#### <a name="to-create-the-new-windows-application"></a>创建新的 Windows 应用程序  
  
1. 从**文件**菜单中，创建一个新项目。  
  
2. 将项目命名**InheritanceWalkthrough**。  
  
    > [!NOTE]
    > Visual Basic 和 C# 项目中都支持 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。 请使用这些语言之一创建新项目。  
  
3. 单击**Windows 窗体应用程序**模板，然后单击**确定**。 有关详细信息，请参阅[客户端应用程序](https://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68)。  
  
4. InheritanceWalkthrough 项目即被创建并添加到**解决方案资源管理器**。  
  
## <a name="add-a-linq-to-sql-classes-file-to-the-project"></a>将 LINQ to SQL 类文件添加到项目  
  
#### <a name="to-add-a-linq-to-sql-file-to-the-project"></a>将 LINQ to SQL 文件添加到项目  
  
1. 在 **“项目”** 菜单上，单击 **“添加新项”**。  
  
2. 单击“LINQ to SQL 类”模板，然后单击“添加”。  
  
     .dbml 文件即添加到项目，[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]打开。  
  
## <a name="create-the-inheritance-by-using-the-or-designer"></a>使用 O/R 设计器创建继承  
 通过将“继承”对象从“工具箱”拖动到设计图面来配置继承。  
  
#### <a name="to-create-the-inheritance"></a>创建继承  
  
1. 在中**服务器资源管理器**/**数据库资源管理器**，导航到**人员**前面创建的表。  
  
2. 拖动**Person**表拖动到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]设计图面。  
  
3. 将另一个**Person**表拖动到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]和其名称更改为**员工**。  
  
4. 从“Person”对象删除“Manager”属性。  
  
5. 从“Employee”对象删除“Type”、“ID”、“FirstName”和“LastName”属性。 （即删除“Manager”以外的所有属性。）  
  
6. 从“工具箱”的“对象关系设计器”选项卡上，在“Person”和“Employee”对象之间创建“继承”。 为此，请单击“工具箱”中的“继承”项，然后松开鼠标按钮。 接下来，单击**员工**对象，然后**人员**对象中[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。 继承连线上的箭头将指向**人员**对象。  
  
7. 单击设计图面上的“继承”连线。  
  
8. 将“鉴别器属性”属性设置为“Type”。  
  
9. 将“派生类鉴别器值”属性设置为“2”。  
  
10. 将“基类鉴别器值”属性设置为“1”。  
  
11. 将“继承默认值”属性设置为“Person”。  
  
12. 生成项目。  
  
## <a name="query-the-inherited-class-and-display-the-data-on-the-form"></a>查询继承类并在窗体上显示数据  
 你将向窗体中添加一些代码，用于在对象模型中查询特定的类。  
  
#### <a name="to-create-a-linq-query-and-display-the-results-on-the-form"></a>创建一个 LINQ 查询并在窗体上显示结果  
  
1. 拖动**ListBox**拖到 Form1 上。  
  
2. 双击窗体以创建 `Form1_Load` 事件处理程序。  
  
3. 将以下代码添加到 `Form1_Load` 事件处理程序中：  
  
    ```vb  
    Dim dc As New DataClasses1DataContext  
    Dim results = From emp In dc.Persons _  
        Where TypeOf emp Is Employee _  
        Select emp  
  
    For Each Emp As Employee In results  
        ListBox1.Items.Add(Emp.LastName)  
    Next  
    ```  
  
    ```csharp  
    NorthwindDataContext dc = new DataClasses1DataContext();  
    var results = from emp in dc.Persons  
                  where emp is Employee  
                  select emp;  
  
    foreach(Employee Emp in results)  
    {  
        listBox1.Items.Add(Emp.LastName)  
    }  
    ```  
  
## <a name="test-the-application"></a>测试应用程序  
 运行应用程序并检验列表框中显示的记录是否全为员工（“Type”列值为 2 的记录）。  
  
#### <a name="to-test-the-application"></a>测试应用程序  
  
1. 按 F5。  
  
2. 检验是否仅显示了“Type”列值为 2 的记录。  
  
3. 关闭窗体。 （在“调试”菜单上，单击“停止调试”。）  
  
## <a name="see-also"></a>请参阅  
 [LINQ to SQL 工具在 Visual Studio 中](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [如何：添加 LINQ to SQL 类到项目 （O-R 设计器）](https://msdn.microsoft.com/library/7bb184ab-ec54-4cda-b706-604b2b4a3ed6)   
 [演练：创建 LINQ to SQL 类 （O-R 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [如何：分配存储的过程以便执行更新、 插入和删除操作 （O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [如何：在 Visual Basic 或 C# 中生成对象模型](https://msdn.microsoft.com/library/a0c73b33-5650-420c-b9dc-f49310c201ee)
