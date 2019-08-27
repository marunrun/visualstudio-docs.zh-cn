---
title: 连接到 Access 数据库 （Windows 窗体） 中的数据 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 120297a7e1b3c1e973f1775d769ab6deb8c2902a
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705563"
---
# <a name="connect-to-data-in-an-access-database-windows-forms"></a>连接到 Access 数据库中的数据（Windows 窗体）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过使用 Visual Studio 连接到 Access 数据库 （.mdf 文件或.accdb 文件）。 在定义此连接后，数据会显示在“数据源”窗口中。 可从该位置将表或视图拖动到窗体上。  
  
## <a name="prerequisites"></a>系统必备  
 若要使用这些过程，需要一个 Windows 窗体应用程序项目，和 Access 数据库 （.accdb 文件） 或 Access 2000 – 2003年数据库 （.mdb 文件）。 按照与你的文件类型对应的过程操作。  
  
## <a name="creating-the-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集  
 你可以连接到 Access 2013 和 Office 365 或访问 2010 Access 2007 通过使用以下过程创建的数据库。  
  
#### <a name="to-create-the-dataset"></a>创建数据集  
  
1. 打开要将数据连接到的 Windows 窗体应用程序。  
  
2. 上**视图**菜单中，选择**其他 Windows** > **数据源**。  
  
     ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png "ViewDataSources")  
  
3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。  
  
     ![添加新数据源](../data-tools/media/dataaddnewdatasource.png "dataAddNewDataSource")  
  
4. 选择**数据库**上**选择数据源类型**页，，然后选择**下一步**。  
  
5. 选择**数据集**上**选择数据库模型**页，，然后选择**下一步**。  
  
6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。  
  
7. 更改**数据源**到**OLE DB 的.NET Framework 数据提供程序**。  
  
     ![将数据提供程序更改为 OLE DB](../data-tools/media/datachangedatasourceoledb.png "dataChangeDataSourceOLEDB")  
  
    > [!IMPORTANT]
    > 尽管数据源的**Microsoft Access 数据库文件 (OLE DB)** 似乎是正确的选择，只能为.mdb 数据库文件使用该数据源类型。  
  
8. 在中**OLE DB 访问接口**，选择**Microsoft Office 12.0 Access 数据库引擎 OLE DB 访问接口**。  
  
     ![OLE DB 提供程序 Microsoft Office 12.0 Access](../data-tools/media/dataoledbprovideroffice12access.png "dataOLEDBProviderOffice12Access")  
  
9. 在中**服务器或文件名**，指定的路径和你想要连接，，然后选择.accdb 文件的名称**确定**。  
  
    > [!NOTE]
    > 如果数据库文件的用户名和密码，请指定它们之后再选择**确定**。  
  
10. 选择**下一步**上**选择您的数据连接**页。  
  
11. 选择**下一步**上**将连接字符串保存到应用程序配置文件**页。  
  
12. 在“选择数据库对象”页面上展开“表”节点。  
  
13. 选择任何表或视图也想在你的数据集，并选择**完成**。  
  
     数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。  
  
## <a name="creating-the-dataset-for-an-mdb-file"></a>创建.mdb 文件的数据集  
 通过运行“数据源配置向导”创建数据集。  
  
#### <a name="to-create-the-dataset"></a>创建数据集  
  
1. 打开要将数据连接到的 Windows 窗体应用程序。  
  
2. 上**视图**菜单中，选择**其他 Windows** > **数据源**。  
  
     ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png "ViewDataSources")  
  
3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。  
  
4. 选择**数据库**上**选择数据源类型**页，，然后选择**下一步**。  
  
5. 选择**数据集**上**选择数据库模型**页，，然后选择**下一步**。  
  
6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接。  
  
7. 如果数据源不是**Microsoft Access 数据库文件 (OLE DB)**，选择**更改**以打开**更改数据源**对话框，选择**Microsoft访问数据库文件**，然后选择**确定**。  
  
8. 在中**数据库文件的名称**，指定的路径和你想要连接，，然后选择的.mdb 文件的名称**确定**。  
  
     ![添加连接 Access 数据库文件](../data-tools/media/dataaddconnectionaccessmdb.png "dataAddConnectionAccessMDB")  
  
9. 选择**下一步**上**选择您的数据连接**页。  
  
10. 选择**下一步**上**将连接字符串保存到应用程序配置文件**页。  
  
11. 在“选择数据库对象”页面上展开“表”节点。  
  
12. 选择任何表或视图也想在你的数据集，并选择**完成**。  
  
     数据集将添加到项目中，并且“数据源”窗口中将显示表和视图。  
  
## <a name="security"></a>安全性  
 存储敏感信息（如密码）会影响应用程序的安全性。 若要控制对数据库的访问，一种较为安全的方法是使用 Windows 身份验证（也称为集成安全性）。 有关详细信息，请参阅[保护连接信息](https://msdn.microsoft.com/library/1471f580-bcd4-4046-bdaf-d2541ecda2f4)。  
  
## <a name="next-steps"></a>后续步骤  
 你刚刚创建的数据集现已推出**数据源**窗口。 现在可以执行以下任何任务：  
  
- 选择中的项**数据源**窗口并将其拖到窗体上 (请参阅[绑定 Windows 窗体控件添加到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md))。  
  
- 在要添加或编辑组成数据集的对象的数据集设计器中打开数据源。  
  
- 添加验证逻辑<xref:System.Data.DataTable.ColumnChanging>或<xref:System.Data.DataTable.RowChanging>数据表中数据集事件 (请参阅[验证数据集中](../data-tools/validate-data-in-datasets.md))。  
  
## <a name="see-also"></a>请参阅

 [准备应用程序以接收数据](https://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [验证数据](https://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [数据演练](https://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)