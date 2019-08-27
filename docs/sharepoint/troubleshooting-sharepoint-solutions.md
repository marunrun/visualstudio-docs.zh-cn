---
title: SharePoint 解决方案疑难解答 |Microsoft Docs
ms.date: 02/22/2017
ms.topic: conceptual
f1_keywords:
- Microsoft.VisualStudio.Tools.SharePoint.Errors.Debugging
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, troubleshooting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bab7f45824def7a4b5a385381a4789b7adc276d0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63008075"
---
# <a name="troubleshoot-sharepoint-solutions"></a>对 SharePoint 解决方案进行故障排除
  当使用调试 SharePoint 解决方案时，可能出现以下问题或警报[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]调试器。 有关详细信息，请参阅[调试 SharePoint 2007 工作流解决方案](https://msdn.microsoft.com/3a5392f3-66f3-48be-956e-02de23fa6247)。

## <a name="token-restrictions-in-sandboxed-visual-web-parts"></a>沙盒可视 web 部件中的标记限制
 沙盒解决方案中的可视 Web 部件无法处理标准标记，例如 SharePoint 运行时支持的 $SPUrl。 因此不会解析 URL，并且如果您直接在脚本元素中引用 URL，则无法在可视 Web 部件设计器的“设计”视图中预览内容：

```xml
<script src="<% $SPUrl:~site/SiteAssets/ListOperations.js %>"></script>
```

 若要解决此限制并解析标记，请使用以下文本引用标记：

```xml
<asp:literal ID="Literal1" runat="server" Text="<script src='" />
<asp:literal ID="Literal2" runat="server" Text="<% $SPUrl:~site/SiteAssets/ListOperations.js %>" />
<asp:literal ID="Literal3" runat="server" Text="' type='text/javascript' ></script>" />
```

## <a name="character-restrictions-in-names-of-projects-and-project-items"></a>在名称中的项目和项目项的字符限制
 在 SharePoint 2010 中，项目和项目项名称只能包含部署路径中有效的字符。 不允许使用任何其他字符。

### <a name="error-message"></a>错误消息
 "无效字符"错误消息。

### <a name="resolution"></a>解决方法
 对于 SharePoint 项目和项目项名称，仅使用以下字符：

- 字母数字 ASCII 字符

- 空格

- 句点 （.）

- 逗号 （，）

- 下划线 (_)

- 短划线 （-）

- 反斜杠 (\\)

  在打包项目时，验证规则将验证要部署的每个文件的部署路径属性是否只包含上述有效字符。

## <a name="errors-when-creating-custom-fields"></a>创建自定义字段时出错
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的自定义字段是使用 XML 定义的。 如果未使用特定格式定义或引用字段，则会出错。

### <a name="error-message"></a>错误消息
 在打包时"无效字符"错误消息。

### <a name="resolution"></a>解决方法
 如下面的示例所示，字段定义的 ID 必须是大括号括起来的 GUID：

```xml
<Field ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Type="Note"
    Name="PatientName"
    DisplayName="Patient Name"
    Group="A Custom Group">
</Field>.
```

 如下面的示例所示，必须通过使用空元素格式定义内容类型中的字段引用 (\<FieldRef / >)，不能通过使用开始/结束元素 (\<FieldRef >\</FieldRef >):

```xml
<FieldRef ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Name="PatientName"
    DisplayName="Patient Name"
    Required="TRUE"/>
```

 如果字段的源 XML 格式不正确、不是有效的 XML 文件或出现一些其他问题，则会出现“无法分析文件”错误。

## <a name="new-non-english-site-definitions-do-not-appear-in-site-creation-page-after-deployment"></a>新的非英语站点定义不会出现在站点创建页中部署后
 创建并使用非英语版本的部署站点定义后[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)](即，具有区域设置的版本[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]不是 1033年)，则**SharePoint 自定义**选项卡不会显示在**模板选择**框和新的站点模板不会出现在**新的 SharePoint 站点**页。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 由于不正确的值中会发生此问题**路径**属性为 webtemp 站点定义配置文件，如*webtemp_SiteDefinitionProject1.xml*。 在**路径**webtemp 文件，位于属性**部署位置**，为相应的区域设置更改 1033年[!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，若要使用日文区域设置将值更改为 1041年。 有关详细信息，请参阅[由 Microsoft 分配的区域设置 Id](http://go.microsoft.com/fwlink/?LinkID=165561)。

## <a name="error-appears-when-a-workflow-project-is-deployed-on-a-clean-system"></a>在干净系统上部署工作流项目时，会出现错误
 如果在干净系统上部署 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的工作流项目，则会发生此问题。 干净系统是指以全新方式安装了 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 SharePoint 但未部署工作流项目的计算机。

### <a name="error-message"></a>错误消息
 找不到 SharePoint 列表：工作流历史记录。

### <a name="resolution"></a>解决方法
 由于缺少工作流历史记录列表会发生此错误。 由于开发环境是干净的系统，部署任何工作流，并且尚不存在工作流历史记录列表。 若要解决此问题，重新打开工作流向导中，这会导致要创建的工作流历史记录列表。

##### <a name="to-reenter-the-workflow-wizard"></a>若要重新输入工作流向导

1. 在中**解决方案资源管理器**，选择工作流节点。

2. 在中**属性**窗口中，选择具有省略号按钮的任何属性的省略号 （...） 按钮。

## <a name="user-must-refresh-application-page-in-browser-while-debugging-to-view-updated-image"></a>若要查看更新的映像进行调试时，用户必须刷新浏览器中的应用程序页上
 如果正在调试 SharePoint 解决方案，其中包含与控件用于显示图像，如应用程序页[!INCLUDE[TLA2#tla_html](../sharepoint/includes/tla2sharptla-html-md.md)]图像控件，必须刷新页面，在浏览器显示的图像所做的任何更改。

## <a name="error-the-site-location-is-not-valid"></a>错误：站点位置无效
 如果出现此问题[!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]未安装。 如果你还没有到中指定的 SharePoint Web 站点的管理员访问权限也可能发生**SharePoint 自定义向导**。

### <a name="error-message"></a>错误消息

- SharePoint 站点位置无效。

### <a name="resolution"></a>解决方法

- 安装 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]。

- 确保有 SharePoint 网站管理员访问权限。 有关详细信息，请参阅[!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)]在线文章[分配或删除 SharePoint Server 中的服务应用程序管理员](https://docs.microsoft.com/sharepoint/administration/assign-or-remove-administrators-of-service-applications)。

## <a name="site-deletion-web-event-does-not-occur-in-event-receiver-project"></a>事件接收方项目中不会发生站点删除 web 事件
 当你创建事件接收器项目，并且您选择某些 Web 事件，如"正在删除网站"时，永远不会发生该事件。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 因为功能作用域必须是"站点"以处理站点级别的事件，但事件接收方项目的默认功能作用域是"Web"，将发生此问题。 受影响的 Web 事件是：

- 正在为站点删除 (WebDeleting)

- 已删除网站 (WebDeleted)

- 正在将站点移 (WebMoving)

- 已移动网站 (WebMoved)

  若要解决此问题，请按如下所示更改事件接收器，功能的范围。

##### <a name="to-change-the-feature-scope-of-the-event-receiver"></a>若要更改的事件接收器的功能范围

1. 在中**解决方案资源管理器**，打开事件接收器 *.feature*文件中**功能设计器**通过双击该文件或打开其快捷菜单，然后选择**打开**。

2. 选择箭头旁边**作用域**，然后选择**站点**中显示的列表。

## <a name="deployment-error-appears-after-the-name-of-an-identifier-in-a-business-data-connectivity-model-project-is-changed"></a>业务数据连接模型项目中的标识符的名称更改后，会出现部署错误
 如果更改业务数据连接 (BDC) 模型中的实体的标识符名称，然后尝试部署解决方案，将发生此问题。

### <a name="error-messages"></a>错误消息

- \<*模型名称*> 具有以下外部内容类型激活错误...

- 名称的 IMetadataObject '\<*模型名称*> 字段 name 的重复中有一个值...

### <a name="resolution"></a>解决方法
 若要解决此问题，手动删除该模型，然后再次部署该解决方案。  可以使用以下工具之一来删除模型：

- SharePoint 2010 管理中心。 有关详细信息，请参阅[BDC 模型管理](http://go.microsoft.com/fwlink/?LinkID=181472)Microsoft TechNet 网站上。

- Windows PowerShell。 可以通过在命令提示符下键入以下命令来删除模型：**删除 SPBusinessDataCatalogModel**。 有关详细信息，请参阅[常规 cmdlet (SharePoint Server 2010)](http://go.microsoft.com/fwlink/?LinkID=182375) Microsoft TechNet 网站上。

## <a name="an-error-appears-when-you-try-to-view-a-visual-web-part-in-sharepoint"></a>当您尝试查看 SharePoint 中的可视 web 部件时，会出现错误
 发生此问题时**路径**用户控件的属性不会开始替换的字符串"controltemplates 设置样式\\"。

### <a name="error-messages"></a>错误消息

- 文件 /_CONTROLTEMPLATES/*\<项目名称 >*/*\<Web 部件名称 >*/*\<用户控件名称 >*.ascx 不存在。

- '/' 应用程序中的服务器错误。

### <a name="resolution"></a>解决方法

##### <a name="to-resolve-this-issue"></a>若要解决此问题

1. 在中**解决方案资源管理器**，选择用户控件文件，其文件扩展名是 *.ascx*。

2. 在菜单栏上依次选择**视图** > **属性窗口**。

3. 在中**属性**窗口中，展开**部署位置**节点。

4. 确保的值**路径**属性以使用字符串"controltemplates 设置样式\\"。

## <a name="error-appears-when-an-imported-reusable-workflow-that-contains-a-task-form-field-is-run"></a>包含任务窗体字段的导入可重用工作流运行时，会出现错误
 如果你导入包含有一个字段的任务窗体的工作流，然后运行从中导入它的同一系统上的新工作流，会发生此问题。

### <a name="error-message"></a>错误消息
 部署步骤激活功能中出现错误：Id 字段 [*Guid*] 功能中定义 [*Guid*] 在当前站点集合或子站点中找到。

### <a name="resolution"></a>解决方法
 此错误是发生的原因导入可重用工作流项目中的字段 ID 冲突的结果[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]不会更改任务窗体字段 Id。 如果部署包含原始工作流在同一服务器上的导入工作流时，会发生字段 ID 冲突。

 若要解决此问题，请使用查找和替换功能中的所有导入工作流文件的字段 ID 属性值更改。

## <a name="error-appears-when-a-renamed-imported-list-instance-is-run"></a>出现错误时重命名导入运行列表实例
 如果重命名导入的列表实例，然后在中运行，会发生此问题[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

### <a name="error-message"></a>错误消息
 生成错误：部署步骤激活功能中出现错误：文件 Template\Features\\[*导入项目*<em>功能</em>*名称*] \Files\Lists\\[*旧*<em>列表名称</em>] \Schema.xml 不存在。

### <a name="resolution"></a>解决方法
 导入的列表实例时，名为 CustomSchema 的属性添加到列表实例的 Elements.xml 文件中。 Elements.xml 包括列表实例自定义 schema.xml 的路径。 当您重命名中的列表实例[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]、 自定义 schema.xml 的部署路径发生变化，但不是更新 CustomSchema 属性的路径值。 因此，列表实例找不到*schema.xml*旧时激活该功能由 CustomSchema 特性指定的路径中的文件。

 若要解决此问题，更新的部署位置的路径*schema.xml* CustomSchema 属性中的文件。

## <a name="sharepoint-debugging-session-terminated-by-iis"></a>SharePoint 在调试会话 IIS 终止
 如果在中设置断点，会发生此问题[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SharePoint 解决方案中，选择**F5**键以运行它，然后保持在 90 秒以上的断点处。

### <a name="error-message"></a>错误消息
 正在进行调试的 Web 服务器进程已终止由 Internet 信息服务 (IIS)。 您可通过在 IIS 中配置应用程序池 Ping 设置来避免此问题。 请参阅有关更多详细信息的帮助。

### <a name="resolution"></a>解决方法
 默认情况下，IIS 应用程序池等待 90 秒，获取应用程序响应之前关闭应用程序。 此过程称为"执行 ping 操作的"应用程序。 若要解决此问题，可以增加的等待时间或禁用应用程序完全执行 ping 操作。

##### <a name="to-access-the-iis-app-pool-settings"></a>若要访问 IIS 应用程序池设置

1. 打开 IIS 管理器。

2. 在中**连接**窗格中，展开 SharePoint 服务器节点，然后再选择**应用程序池**节点。

3. 上**应用程序池**页上，选择 SharePoint 应用程序池 (通常"SharePoint-80")，然后在**操作**窗格中，选择**高级设置**链接。

4. 若要增加 IIS 超时前的等待时间，更改的值**Ping 最大响应时间 （秒）** 大于 90 秒的值。

5. 若要禁用 IIS 执行 ping 操作，设置**启用 Ping**到**False**。

## <a name="auto-retract-leaves-orphaned-list-instance-in-sharepoint"></a>在 SharePoint 中自动收回离开孤立的列表实例
 如果执行以下步骤，将发生此问题。

1. 创建具有列表实例中的列表定义[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 选择**F5**键以运行该解决方案。

3. 停止调试，或关闭 SharePoint 站点。

4. 重新打开 SharePoint 站点，打开列表实例。

### <a name="error-message"></a>错误消息
 '/' 应用程序中的服务器错误。

### <a name="resolution"></a>解决方法
 这是因为关闭 SharePoint 解决方案的调试会话后自动收回功能，收回该解决方案。 收回从 SharePoint 删除列表定义，但不会删除列表实例。 列表实例需要的基础列表定义。

 若要解决此问题，以部署解决方案，在菜单栏中选择**构建** > **部署**。 (不调试解决方案，通过选择**F5**键。)然后，删除在 SharePoint 中的列表实例。

## <a name="original-sharepoint-solution-is-replaced-by-an-exported-version"></a>导出版本替换原始的 SharePoint 解决方案
 如果导出 SharePoint 解决方案时，导入到解决方案[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，和回复到同一站点从其导出然后部署该解决方案，将替换原始的 SharePoint 解决方案。 如果将解决方案部署到不具有在其上激活的原始解决方案的服务器不会出现此问题。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 若要避免覆盖与从中导出的站点上的解决方案，更改的解决方案 Id 的 Guid 和功能 Id 中的所有导入功能[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]项目。

## <a name="error-appears-when-debugging-starts"></a>启动调试时，会出现错误
 在 Visual Studio 中开始调试 SharePoint 解决方案时出现错误，表明由于字典中没有给定键，Visual Studio 无法加载 Web.config 文件。

### <a name="error-message"></a>错误消息
 无法加载 Web.config 配置文件。 检查文件中的任何格式不正确的 XML 元素，然后重试。 发生下列错误：不在字典中存在给定的键的。

### <a name="resolution"></a>解决方法
 若要解决此问题，请确保 Visual Studio 中的 SharePoint 项目的“站点 URL”属性值与分配给 Web 应用程序的备用访问映射的默认区域的 URL 一致。 对 URL 使用其他区域（如 Intranet）将无法解决此错误。 项目的站点 URL 与默认区域中的 URL 必须一致。 若要访问备用访问映射，打开 SharePoint 2010 管理中心实用工具中，选择**应用程序管理**链接，然后在**Web 应用程序**，选择**配置备用访问映射**链接。 有关详细信息，请参阅[创建 Web 应用程序的区域](http://go.microsoft.com/fwlink/?LinkId=192274)。

## <a name="see-also"></a>请参阅

- [SharePoint 打包和部署进行故障排除](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [在 Visual Studio 中进行调试](../debugger/debugging-in-visual-studio.md)