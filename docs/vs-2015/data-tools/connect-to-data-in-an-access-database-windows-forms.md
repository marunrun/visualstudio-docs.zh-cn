---
title: 连接到 Access 数据库中的数据（Windows 窗体） |Microsoft Docs
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
- databases, connecting to
- databases, Access
- data [Visual Studio], connecting
- connecting to data, from Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
caps.latest.revision: 32
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8426e9fcaa29bef36b6701c78d622f6f42fd1171
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651131"
---
# <a name="connect-to-data-in-an-access-database-windows-forms"></a>连接到 Access 数据库中的数据（Windows 窗体）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用 Visual Studio 连接到 Access 数据库（.mdf 文件或 .accdb 文件）。 在定义此连接后，数据会显示在“数据源”窗口中。 可从该位置将表或视图拖动到窗体上。

## <a name="prerequisites"></a>Prerequisites
 若要使用这些过程，需要一个 Windows 窗体应用程序项目，并使用 Access 数据库（.accdb 文件）或 Access 2000 –2003数据库（.mdb 文件）。 按照与你的文件类型对应的过程操作。

## <a name="creating-the-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集
 你可以使用以下过程连接到通过 Access 2013、Office 365、Access 2010 或 Access 2007 创建的数据库。

#### <a name="to-create-the-dataset"></a>创建数据集

1. 打开要将数据连接到的 Windows 窗体应用程序。

2. 在 "**视图**" 菜单上，选择 "**其他 Windows**  > **数据源**"。

     ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png "ViewDataSources")

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”** 。

     ![添加新数据源](../data-tools/media/dataaddnewdatasource.png "dataAddNewDataSource")

4. 选择 "**选择数据源类型**" 页上的 "**数据库**"，然后选择 "**下一步**"。

5. 选择 "**选择数据库模型**" 页上的 "**数据集**"，然后选择 "**下一步**"。

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

7. 将**数据源**更改为**OLE DB 的 .NET Framework 数据提供程序**。

     ![将数据访问接口更改为 OLE DB](../data-tools/media/datachangedatasourceoledb.png "dataChangeDataSourceOLEDB")

    > [!IMPORTANT]
    > 尽管**Microsoft Access 数据库文件（OLE DB）** 的数据源可能看起来像是正确的选择，但将该数据源类型仅用于 .mdb 数据库文件。

8. 在**OLE DB 提供程序**中，选择**Microsoft Office 12.0 访问数据库引擎 OLE DB 提供程序**。

     ![OLE DB 提供程序 Microsoft Office 12.0 访问](../data-tools/media/dataoledbprovideroffice12access.png "dataOLEDBProviderOffice12Access")

9. 在 "**服务器或文件名**" 中，指定要连接到的 .accdb 文件的路径和名称，然后选择 **"确定"** 。

    > [!NOTE]
    > 如果数据库文件有用户名和密码，请在选择 **"确定"** 之前指定。

10. 选择 "**选择您的数据连接**" 页上的 "**下一步**"。

11. 在 "将**连接字符串保存到应用程序配置文件**" 页上选择 "**下一步**"。

12. 在“选择数据库对象”页面上展开“表”节点。

13. 选择数据集中所需的任何表或视图，然后选择 "**完成**"。

     数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

## <a name="creating-the-dataset-for-an-mdb-file"></a>为 .mdb 文件创建数据集
 通过运行“数据源配置向导”创建数据集。

#### <a name="to-create-the-dataset"></a>创建数据集

1. 打开要将数据连接到的 Windows 窗体应用程序。

2. 在 "**视图**" 菜单上，选择 "**其他 Windows**  > **数据源**"。

     ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png "ViewDataSources")

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”** 。

4. 选择 "**选择数据源类型**" 页上的 "**数据库**"，然后选择 "**下一步**"。

5. 选择 "**选择数据库模型**" 页上的 "**数据集**"，然后选择 "**下一步**"。

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。

7. 如果数据源不是**Microsoft Access 数据库文件（OLE DB）** ，请选择 **"更改**" 以打开 "**更改数据源**" 对话框，然后选择 " **Microsoft Access 数据库文件**"，然后选择 **"确定"** 。

8. 在 "**数据库文件名**" 中，指定要连接到的 .mdb 文件的路径和名称，然后选择 **"确定"** 。

     ![添加连接访问数据库文件](../data-tools/media/dataaddconnectionaccessmdb.png "dataAddConnectionAccessMDB")

9. 选择 "**选择您的数据连接**" 页上的 "**下一步**"。

10. 在 "将**连接字符串保存到应用程序配置文件**" 页上选择 "**下一步**"。

11. 在“选择数据库对象”页面上展开“表”节点。

12. 选择数据集中所需的任何表或视图，然后选择 "**完成**"。

     数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。

## <a name="security"></a>安全
 存储敏感信息（如密码）会影响应用程序的安全性。 若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。 有关详细信息，请参阅[保护连接信息](https://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4)。

## <a name="next-steps"></a>后续步骤
 刚刚创建的数据集现在可在 "**数据源**" 窗口中找到。 现在可以执行以下任何任务：

- 在 "**数据源**" 窗口中选择项，然后将其拖到窗体上（请参见将[Windows 窗体控件绑定到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)）。

- 在数据集设计器中打开数据源，以添加或编辑组成数据集的对象。

- 将验证逻辑添加到数据集中的数据表 <xref:System.Data.DataTable.ColumnChanging> 或 <xref:System.Data.DataTable.RowChanging> 事件（请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)）。

## <a name="see-also"></a>请参阅

 [准备应用程序以接收数据](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)将[控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)[验证数据](https://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)[数据演练](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)