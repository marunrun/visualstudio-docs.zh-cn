---
title: 添加新连接 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 8a93c287-2834-4a83-a590-bdc3fe8d293f
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 44146613fb43b6fc4269741ba09b94629f888d5f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72673076"
---
# <a name="add-new-connections"></a>添加新连接
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以使用**服务器资源管理器**、 **Cloud Explorer**或**SQL Server 对象资源管理器**测试与数据库或服务的连接，并浏览数据库内容和架构。 这些窗口的功能与某个范围重叠。 基本差异如下：

 默认情况下，服务器资源管理器安装在 Visual Studio 中。 可用于测试连接并查看 SQL Server 数据库、安装了 ADO.NET 提供程序的任何其他数据库以及某些 Azure 服务。 还显示低级别对象，如系统性能计数器、事件日志和消息队列。 如果数据源没有 ADO.NET 提供程序，则它将不会显示在此处，但仍可通过编程方式连接从 Visual Studio 中使用它。

 Cloud Explorer 通过选择 "**工具**"  >  "**扩展和更新**"  > **联机** > **visual studio 库**，手动安装此窗口。 为浏览和连接到 Azure 服务提供了专用功能。

 SQL Server 对象资源管理器随 SQL Server Data Tools 安装并且在 "**视图**" 菜单下可见。 如果看不到该文件，请转到控制面板中的 "**程序和功能**"，查找 Visual Studio，然后选择 "**更改**" 以在选中 "SQL Server Data Tools" 复选框后重新运行安装程序。 使用**SQL Server 对象资源管理器**可以查看 SQL 数据库（如果它们具有 ADO.NET 提供程序）、创建新数据库、修改架构、创建存储过程、检索连接字符串、查看数据等。 未安装 ADO.NET 提供程序的 SQL 数据库将不会显示在此处，但仍可通过编程方式连接到这些数据库。

## <a name="add-a-connection-in-server-explorer"></a>在服务器资源管理器中添加连接
 若要创建与数据库的连接，请单击 "**服务器资源管理器**中的"**添加连接**"图标，或在"**数据连接**"节点上右键单击**服务器资源管理器**，然后选择"**添加连接**"。 在这里，你还可以连接到另一台服务器、SharePoint 服务或 Azure 服务上的数据库。

 ![服务器资源管理器新建连接 "图标](../data-tools/media/raddata-server-explorer-new-connection-icon.png "raddata 服务器资源管理器新建连接图标")

 此时将打开 "**添加连接**" 对话框。 在这里，我们输入了 SQL Server LocalDB 实例的名称。

 ![添加新连接](../data-tools/media/raddata-add-new-connection-dialog.png "raddata "添加新连接" 对话框")

## <a name="change-the-provider"></a>更改提供程序
 如果数据源不是所需的数据源，请单击 "**更改**" 按钮，选择新的数据源和/或新的 ADO.NET 数据提供程序。 新的提供程序可能要求提供凭据，具体取决于您的配置方式。

 ![更改 AD0.NET 数据提供程序](../data-tools/media/raddata-change-ad0-net-data-provider.png "raddata 更改 AD0.NET 数据提供程序")

## <a name="test-the-connection"></a>测试连接
 选择数据源后，单击 "**测试连接**"。 如果未成功，你将需要根据供应商的文档进行故障排除。

 ![测试连接](../data-tools/media/raddata-test-connection.png "raddata 测试连接")

 如果测试成功，您就可以创建一个*数据源，该数据源*是一个 Visual Studio 术语，它真正表示基于基础数据库或服务的*数据模型*。

## <a name="see-also"></a>请参阅
 [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
