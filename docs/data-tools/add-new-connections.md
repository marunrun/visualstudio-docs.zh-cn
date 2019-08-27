---
title: 添加新连接
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b01af2aa269cbaddbd84d24827b1a77e97d52d8a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62818453"
---
# <a name="add-new-connections"></a>添加新连接

可以测试连接到数据库或服务，并浏览数据库内容和架构，通过使用**服务器资源管理器**，**云资源管理器**，或**SQL Server 对象资源管理器**. 某种程度上重叠的这些 windows 功能。 基本区别如下：

- 服务器资源管理器

   默认情况下，在 Visual Studio 中安装。 可用来测试连接和查看 SQL Server 数据库、 已安装，ADO.NET 提供程序的任何其他数据库和某些 Azure 服务。 此外显示了系统性能计数器、 事件日志和消息队列等低级别对象。 如果数据源不具有任何 ADO.NET 提供程序，它不会显示在此处，但您仍可以使用它从 Visual Studio 通过以编程方式连接。

- Cloud Explorer

   手动安装此窗口，以从 Visual Studio 扩展[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.CloudExplorerForVS)。 提供浏览和连接到 Azure 服务的专用的功能。

- SQL Server 对象资源管理器

   安装了 SQL Server Data Tools 和下可见**视图**菜单。 如果看不到它存在，请转到**程序和功能**控制面板中，找到 Visual Studio 中，并选择**更改**以 SQL Server Data tools 中选中的复选框后重新运行安装程序。 使用**SQL Server 对象资源管理器**到视图 SQL 数据库 （如果他们有 ADO.NET 提供程序），创建新的数据库、 修改架构、 创建存储的过程、 检索连接字符串、 查看数据，并提供更多信息。 SQL 数据库，以安装任何 ADO.NET 提供程序不会显示在此处，但你仍然可以连接到它们以编程方式。

## <a name="add-a-connection-in-server-explorer"></a>在服务器资源管理器中添加连接

若要创建与数据库的连接，请单击**添加连接**中的图标**服务器资源管理器**，或在右键单击**服务器资源管理器**上**数据连接**节点，然后选择**添加连接**。 在这里，您可以还连接到另一台服务器、 SharePoint 服务或 Azure 服务上的数据库。

![服务器资源管理器的新连接图标](../data-tools/media/raddata-server-explorer-new-connection-icon.png)

这将显示**添加连接**对话框。 在这里，我们已经输入的 SQL Server LocalDB 实例的名称。

![添加新连接](../data-tools/media/raddata-add-new-connection-dialog.png)

## <a name="change-the-provider"></a>更改提供程序

如果数据源不是你想要请单击**更改**按钮以选择新的数据源和/或新的 ADO.NET 数据提供程序。 新的提供程序可能会要求输入凭据，具体取决于具体的配置。

![更改 AD0.NET 数据提供程序](../data-tools/media/raddata-change-ad0.net-data-provider.png)

## <a name="test-the-connection"></a>测试连接

选择数据源后，单击**测试连接**。 如果不成功，您需要进行故障排除基于供应商的文档。

![测试连接](../data-tools/media/raddata-test-connection.png)

如果测试成功，已准备好创建*数据源*，这是真正含义的 Visual Studio 术语*数据模型*基于基础数据库或服务。

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
