---
title: 如何：添加、更新或移除 WCF 数据服务引用
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- service references [Visual Studio]
- WCF Data Service reference
- WCF data service references
- ADO.NET service references
- ADO.NET Data Service reference
ms.assetid: 892ebf37-3af4-472e-8744-92837677d611
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: f5f5a1e14a6eab7537c8ce64636f0f34378ad7f0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85282366"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>如何：添加、更新或删除 WCF 数据服务引用

::: moniker range="vs-2017"
*服务引用*允许项目访问一个或多个 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 。 使用 " **添加服务引用** " 对话框可以在本地 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 、在本地网络或 Internet 上搜索当前解决方案。
::: moniker-end
::: moniker range=">=vs-2019"
您可以使用**解决方案资源管理器**中的 "**连接的服务**" 节点访问**Microsoft WCF Web Service Reference Provider**，这使您可以管理 Windows Communication Foundation (WCF) 数据服务引用。
::: moniker-end

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-wcf-service-reference"></a>添加 WCF 服务引用

### <a name="to-add-a-reference-to-an-external-service"></a>添加对外部服务的引用

::: moniker range="vs-2017"

1. 在 **解决方案资源管理器**中，右键单击要向其添加服务的项目的名称，然后单击 " **添加服务引用**"。

   此时将出现“添加服务引用”对话框****。

1. 在 " **地址** " 框中，输入服务的 URL，然后单击 " **开始** " 搜索服务。 如果服务实施用户名和密码安全，系统可能会提示你输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     你还可以从 "地址" 列表中选择 URL，该 **地址** 将存储找到了有效服务元数据的前15个 url。

     执行搜索时，将显示一个进度栏。 您可以随时通过单击 " **停止**" 来停止搜索。

1. 在 " **服务** " 列表中，展开要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间****。

1. 单击“确定”将参考添加到项目中****。

     将生成服务客户端 (代理) ，并将描述服务的元数据添加到 *app.config* 文件中。
::: moniker-end
::: moniker range=">=vs-2019"
1. 在 **解决方案资源管理器**中，双击或点击 " **连接的服务** " 节点。

   此时将打开 " **配置服务** " 选项卡。

1. 选择 **Microsoft WCF Web Service Reference Provider**。

   此时将显示 " **配置 WCF Web 服务引用** " 对话框。

   !["WCF Web 服务提供程序" 对话框的屏幕截图](media/vs-2019/configure-wcf-web-service-reference-dialog.png)


1. 在 " **URI** " 框中，输入服务的 URL，然后单击 " **开始** " 搜索服务。 如果服务实施用户名和密码安全，系统可能会提示你输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     你还可以从 **URI** 列表中选择 URL，其中存储了以前15个 url，其中找到了有效的服务元数据。

     执行搜索时，将显示一个进度栏。 您可以随时通过单击 " **停止**" 来停止搜索。

1. 在 " **服务** " 列表中，展开要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间****。

1. 单击 " **完成** "，将引用添加到项目。

     将生成服务客户端 (代理) ，并将描述服务的元数据添加到 *app.config* 文件中。

::: moniker-end

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>在当前解决方案中添加对服务的引用

::: moniker range="vs-2017"

1. 在 **解决方案资源管理器**中，右键单击要向其添加服务的项目的名称，然后单击 " **添加服务引用**"。

    此时将出现“添加服务引用”对话框****。

1. 单击 " **发现**"。

    [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]当前解决方案中 (和 WCF 服务) 的所有服务都将添加到**服务**列表中。

1. 在 " **服务** " 列表中，展开要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间****。

1. 单击“确定”将参考添加到项目中****。

    ) 生成服务客户端 (代理，并将描述服务的元数据添加到 *app.config* 文件中。
::: moniker-end
::: moniker range=">=vs-2019"
1. 在 **解决方案资源管理器**中，双击或点击 " **连接的服务** " 节点。 

   此时将打开 " **配置服务** " 选项卡。

1. 选择 **Microsoft WCF Web Service Reference Provider**。

   此时将显示 " **配置 WCF Web 服务引用** " 对话框。

1. 单击 " **发现**"。

    [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]当前解决方案中 (和 WCF 服务) 的所有服务都将添加到**服务**列表中。

1. 在 " **服务** " 列表中，展开要使用的服务的节点，然后选择实体集。

1. 在“命名空间”框中，输入要用于参考的命名空间****。

1. 单击 " **完成** "，将引用添加到项目。

    ) 生成服务客户端 (代理，并将描述服务的元数据添加到 *app.config* 文件中。

::: moniker-end

## <a name="update-a-service-reference"></a>更新服务引用

有时更改的实体数据模型 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 。 如果发生这种情况，则必须更新服务引用。

### <a name="to-update-a-service-reference"></a>更新服务引用

- 在 **解决方案资源管理器**中，右键单击服务引用，然后单击 " **更新服务引用**"。

     当引用从其原始位置更新时，将显示一个进度对话框，然后重新生成服务客户端以反映元数据中的任何更改。

## <a name="remove-a-service-reference"></a>删除服务引用

如果不再使用服务引用，则可以将其从解决方案中删除。

### <a name="to-remove-a-service-reference"></a>删除服务引用

- 在 **解决方案资源管理器**中，右键单击服务引用，然后单击 " **删除**"。

     将从解决方案中删除服务客户端，并将从 *app.config* 文件中删除描述该服务的元数据。

    > [!NOTE]
    > 引用服务引用的任何代码都必须手动删除。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
