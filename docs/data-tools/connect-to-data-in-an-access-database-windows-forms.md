---
title: 连接到 Access 数据库中的数据
ms.date: 07/18/2019
ms.topic: how-to
helpviewer_keywords:
- data [Visual Studio], connecting
- connecting to data, Access databases
- Access databases, connecting
ms.assetid: 4159e815-d430-4ad0-a234-e4125fcbef18
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 03c92476e8083106a0d301655be3a1779709c1c1
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282730"
---
# <a name="connect-to-data-in-an-access-database"></a>连接到 Access 数据库中的数据

您可以使用 Visual Studio 连接到 Access 数据库（ *.mdb*文件或 *.accdb*文件）。 在定义此连接后，数据会显示在“数据源”窗口中****。 您可以从此处将表或视图拖动到设计图面上。

## <a name="prerequisites"></a>先决条件

若要使用这些过程，您需要 Windows 窗体或 WPF 项目以及 Access 数据库（*.accdb*文件）或 access 2000-2003 数据库（*.mdb*文件）。 按照与你的文件类型对应的过程操作。

## <a name="create-a-dataset-for-an-accdb-file"></a>为 .accdb 文件创建数据集

使用以下过程连接到使用 Office 365、Access 2013、Access 2010 或 Access 2007 创建的数据库。

1. 在 Visual Studio 中打开 Windows 窗体或 WPF 应用程序项目。

2. 若要打开 "**数据源**" 窗口，请在 "**视图**" 菜单上选择 "**其他 Windows**  >  **数据源**"。

   ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png)

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

   "**数据源配置向导**" 将打开。

4. 选择 "**选择数据源类型**" 页上的 "**数据库**"，然后选择 "**下一步**"。

5. 选择 "**选择数据库模型**" 页上的 "**数据集**"，然后选择 "**下一步**"。

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接********。

   随即会打开“添加连接”对话框****。

7. 如果**数据源**未设置为 " **Microsoft Access 数据库文件**"，请选择 "**更改**" 按钮。

   此时将打开 "**更改数据源**" 对话框。 在数据源列表中，选择 " **Microsoft Access 数据库文件**"。 在 "**数据访问接口**" 下拉 .NET Framework 中，选择**OLE DB 的 "数据提供程序**"，然后选择 **"确定"**。

8. 选择 "**数据库文件名**" 旁边的 "**浏览**"，然后导航到 *.accdb*文件，然后选择 "**打开**"。

9. 输入用户名和密码（如有必要），然后选择 **"确定"**。

10. 选择 "**选择您的数据连接**" 页上的 "**下一步**"。

    你可能会看到一个对话框，告知你当前项目中没有数据文件。 选择 **"是" 或 "** **否**"。

11. 在 "将**连接字符串保存到应用程序配置文件**" 页上选择 "**下一步**"。

12. 在“选择数据库对象”页面上展开“表”节点********。

13. 选择要包含在数据集中的表或视图，然后选择 "**完成**"。

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图****。

## <a name="create-a-dataset-for-an-mdb-file"></a>为 .mdb 文件创建数据集

使用以下过程连接到使用 Access 2000-2003 创建的数据库。

1. 在 Visual Studio 中打开 Windows 窗体或 WPF 应用程序项目。

2. 在 "**视图**" 菜单上，选择 "**其他 Windows**  >  **数据源**"。

   ![查看其他 Windows 数据源](../data-tools/media/viewdatasources.png)

3. 在 **“数据源”** 窗口中，单击 **“添加新数据源”**。

    "**数据源配置向导**" 将打开。

4. 选择 "**选择数据源类型**" 页上的 "**数据库**"，然后选择 "**下一步**"。

5. 选择 "**选择数据库模型**" 页上的 "**数据集**"，然后选择 "**下一步**"。

6. 在“选择数据连接”页面上选择“新建连接”，配置一个新的数据连接********。

7. 如果数据源不是**Microsoft Access 数据库文件（OLE DB）**，请选择 **"更改**" 以打开 "**更改数据源**" 对话框，然后选择 " **Microsoft Access 数据库文件**"，然后选择 **"确定"**。

8. 在 "**数据库文件名**" 中，指定要连接到的 *.mdb*文件的路径和名称，然后选择 **"确定"**。

   ![添加连接访问数据库文件](../data-tools/media/add-connection-access-db.png)

9. 选择 "**选择您的数据连接**" 页上的 "**下一步**"。

10. 在 "将**连接字符串保存到应用程序配置文件**" 页上选择 "**下一步**"。

11. 在“选择数据库对象”页面上展开“表”节点********。

12. 选择数据集中所需的任何表或视图，然后选择 "**完成**"。

    数据集将添加到项目中，并且“数据源”窗口中将显示表和视图****。

## <a name="next-steps"></a>后续步骤

您刚刚创建的数据集将出现在 "**数据源**" 窗口中。 现在可以执行以下任何任务：

- 在 "**数据源**" 窗口中选择项，然后将其拖到窗体或设计图面上（请参见将[Windows 窗体控件绑定到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)或[WPF 数据绑定概述](/dotnet/desktop-wpf/data/data-binding-overview)）。

- 在数据集设计器中打开数据源，以便添加或编辑组成数据集的对象****。

- 将验证逻辑添加到 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 数据集中数据表的或事件（请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)）。

## <a name="see-also"></a>另请参阅

- [添加连接](../data-tools/add-new-connections.md)
- [WPF 数据绑定概述](/dotnet/framework/wpf/data/data-binding-overview)
- [数据绑定 Windows 窗体](/dotnet/framework/winforms/data-binding-and-windows-forms)
