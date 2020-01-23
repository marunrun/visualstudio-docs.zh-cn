---
title: 如何：添加、更新或删除 WCF 数据服务引用
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: c60dffc7bb47336ae36e64a366def3c4dce06213
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586579"
---
# <a name="how-to-add-update-or-remove-a-wcf-data-service-reference"></a>如何：添加、更新或删除 WCF 数据服务引用
*服务引用*允许项目访问一个或多个 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]。 使用 "**添加服务引用**" 对话框可以在本地、局域网或 Internet 上搜索当前解决方案中的 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-a-service-reference"></a>添加服务引用

### <a name="to-add-a-reference-to-an-external-service"></a>添加对外部服务的引用

1. 在**解决方案资源管理器**中，右键单击要向其添加服务的项目的名称，然后单击 "**添加服务引用**"。

     此时将显示 "**添加服务引用**" 对话框。

2. 在 "**地址**" 框中，输入服务的 URL，然后单击 "**开始**" 搜索服务。 如果服务实施用户名和密码安全，系统可能会提示你输入用户名和密码。

    > [!NOTE]
    > 应仅从受信任源引用服务。 从不受信任的源添加引用可能会危及安全性。

     你还可以从 "地址" 列表中选择 URL，该**地址**将存储找到了有效服务元数据的前15个 url。

     执行搜索时，将显示一个进度栏。 您可以随时通过单击 "**停止**" 来停止搜索。

3. 在 "**服务**" 列表中，展开要使用的服务的节点，然后选择实体集。

4. 在 "**命名空间**" 框中，输入要用于引用的命名空间。

5. 单击 **"确定"** 以添加对该项目的引用。

     将生成服务客户端（代理），并将描述服务的元数据添加到*app.config*文件中。

### <a name="to-add-a-reference-to-a-service-in-the-current-solution"></a>在当前解决方案中添加对服务的引用

1. 在**解决方案资源管理器**中，右键单击要向其添加服务的项目的名称，然后单击 "**添加服务引用**"。

    此时将显示 "**添加服务引用**" 对话框。

2. 单击 "**发现**"。

    当前解决方案中的所有服务（[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 和 WCF 服务）都将添加到**服务**列表中。

3. 在 "**服务**" 列表中，展开要使用的服务的节点，然后选择实体集。

4. 在 "**命名空间**" 框中，输入要用于引用的命名空间。

5. 单击 **"确定"** 以添加对该项目的引用。

    将生成服务客户端（代理），并将描述服务的元数据添加到*app.config*文件中。

## <a name="update-a-service-reference"></a>更新服务引用
[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 的实体数据模型有时会发生变化。 如果发生这种情况，则必须更新服务引用。

### <a name="to-update-a-service-reference"></a>更新服务引用

- 在**解决方案资源管理器**中，右键单击服务引用，然后单击 "**更新服务引用**"。

     当引用从其原始位置更新时，将显示一个进度对话框，然后重新生成服务客户端以反映元数据中的任何更改。

## <a name="remove-a-service-reference"></a>删除服务引用
如果不再使用服务引用，则可以将其从解决方案中删除。

### <a name="to-remove-a-service-reference"></a>删除服务引用

- 在**解决方案资源管理器**中，右键单击服务引用，然后单击 "**删除**"。

     将从解决方案中删除服务客户端，并将从*app.config*文件中删除描述该服务的元数据。

    > [!NOTE]
    > 引用服务引用的任何代码都必须手动删除。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
