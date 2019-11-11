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
ms.openlocfilehash: fcb30056021a865d0b0e605de462ff72ced5a383
ms.sourcegitcommit: 77ef1dcc71057cd5fdc4733ff0cb6085bd6113e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2019
ms.locfileid: "73661887"
---
# <a name="troubleshoot-sharepoint-solutions"></a>SharePoint 解决方案疑难解答
  使用 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 调试器调试 SharePoint 解决方案时，可能会出现以下问题或警报。 有关详细信息，请参阅[调试 SharePoint 2007 工作流解决方案](https://msdn.microsoft.com/3a5392f3-66f3-48be-956e-02de23fa6247)。

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

## <a name="character-restrictions-in-names-of-projects-and-project-items"></a>项目和项目项名称中的字符限制
 在 SharePoint 2010 中，项目和项目项名称只能包含部署路径中有效的字符。 不允许使用任何其他字符。

### <a name="error-message"></a>错误消息
 "无效字符" 错误消息。

### <a name="resolution"></a>解决方法
 对于 SharePoint 项目和项目项名称，仅使用以下字符：

- 字母数字 ASCII 字符

- 空格

- Period （.）

- 逗号（，）

- 下划线（_）

- 短划线（-）

- 反斜杠 (\\)

  在打包项目时，验证规则将验证要部署的每个文件的部署路径属性是否只包含上述有效字符。

## <a name="errors-when-creating-custom-fields"></a>创建自定义字段时出错
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的自定义字段是使用 XML 定义的。 如果未使用特定格式定义或引用字段，则会出错。

### <a name="error-message"></a>错误消息
 打包时出现 "无效字符" 错误消息。

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

 如下面的示例所示，内容类型中的字段引用必须使用空元素格式（\<f/>）定义，而不能使用 start/end 元素（\<f >\</FieldRef >）来定义：

```xml
<FieldRef ID="{5744d18c-305e-4632-8bd1-09d134f4830d}"
    Name="PatientName"
    DisplayName="Patient Name"
    Required="TRUE"/>
```

 如果字段的源 XML 格式不正确、不是有效的 XML 文件或出现一些其他问题，则会出现“无法分析文件”错误。

## <a name="new-non-english-site-definitions-do-not-appear-in-site-creation-page-after-deployment"></a>部署后，新的非英语网站定义不会出现在站点创建页面中
 使用非英语版本的 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] （即，区域设置 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)] 不是1033）创建和部署站点定义之后，" **SharePoint 自定义**" 选项卡不会显示在 "**模板选择**" 框和新站点中。模板不会显示在 "**新建 SharePoint 网站**" 页中。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 出现此问题的原因是 webtemp 站点定义配置文件的**路径**属性中的值不正确，如*webtemp_SiteDefinitionProject1*。 在 webtemp 文件（位于**部署位置**下）的 "**路径**" 属性中，将1033更改为相应的区域设置 [!INCLUDE[TLA2#tla_id](../sharepoint/includes/tla2sharptla-id-md.md)]。 例如，若要使用日语区域设置，请将值更改为1041。 有关详细信息，请参阅[Microsoft 分配的区域设置 id](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c)。

## <a name="error-appears-when-a-workflow-project-is-deployed-on-a-clean-system"></a>在干净系统上部署工作流项目时出现错误
 如果在干净系统上部署 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的工作流项目，则会发生此问题。 干净系统是指以全新方式安装了 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 和 SharePoint 但未部署工作流项目的计算机。

### <a name="error-message"></a>错误消息
 找不到 SharePoint 列表：工作流历史记录。

### <a name="resolution"></a>解决方法
 发生此错误的原因是缺少工作流历史记录列表。 由于开发环境是一个干净的系统，因此不会部署工作流，并且工作流历史记录列表尚不存在。 若要解决此问题，请重新打开工作流向导，这将导致创建工作流历史记录列表。

##### <a name="to-reenter-the-workflow-wizard"></a>重新输入工作流向导

1. 在**解决方案资源管理器**中，选择 "工作流" 节点。

2. 在 "**属性**" 窗口中，选择具有省略号按钮的任何属性上的省略号（"..."）按钮。

## <a name="user-must-refresh-application-page-in-browser-while-debugging-to-view-updated-image"></a>调试时，用户必须在浏览器中刷新应用程序页面以查看更新的映像
 如果正在调试的 SharePoint 解决方案包含的应用程序页包含显示图像的控件（如 [!INCLUDE[TLA2#tla_html](../sharepoint/includes/tla2sharptla-html-md.md)] 图像控件），则必须刷新浏览器中的页面，以显示对图像所做的任何更改。

## <a name="error-the-site-location-is-not-valid"></a>错误：站点位置无效
 如果未安装 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]，则可能出现此问题。 如果你没有管理员访问**Sharepoint 自定义向导**中指定的 sharepoint 网站的权限，也可能会发生这种情况。

### <a name="error-message"></a>错误消息

- SharePoint 网站位置无效。

### <a name="resolution"></a>解决方法

- 安装 [!INCLUDE[moss_14_short](../sharepoint/includes/moss-14-short-md.md)]。

- 确保你拥有对 SharePoint 网站的管理员访问权限。 有关详细信息，请参阅 [!INCLUDE[TLA2#tla_office](../sharepoint/includes/tla2sharptla-office-md.md)] Online 文章[在 SharePoint Server 中分配或删除服务应用程序的管理员](/sharepoint/administration/assign-or-remove-administrators-of-service-applications)。

## <a name="site-deletion-web-event-does-not-occur-in-event-receiver-project"></a>在事件接收器项目中不发生站点删除 web 事件
 当你创建事件接收器项目并选择某些 Web 事件（如 "正在删除网站"）时，事件永远不会发生。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 之所以出现此问题，是因为功能范围必须是 "Site" 才能处理站点级事件，但事件接收器项目的默认功能范围为 "Web"。 受影响的 Web 事件如下：

- 正在删除网站（WebDeleting）

- 已删除站点（WebDeleted）

- 正在移动站点（WebMoving）

- 已移动站点（WebMoved）

  若要解决此问题，请按如下所示更改事件接收器的功能范围。

##### <a name="to-change-the-feature-scope-of-the-event-receiver"></a>更改事件接收器的功能范围

1. 在**解决方案资源管理器**中，双击文件或打开其快捷菜单，然后选择 "**打开**"，在**功能设计器**中打开事件接收器的 *. 功能*文件。

2. 选择 "**作用域**" 旁边的箭头，然后在显示的列表中选择 "**站点**"。

## <a name="deployment-error-appears-after-the-name-of-an-identifier-in-a-business-data-connectivity-model-project-is-changed"></a>更改业务数据连接模型项目中的标识符名称后，将显示部署错误
 如果在业务数据连接（BDC）模型中更改实体的标识符名称，然后尝试部署解决方案，则会出现此问题。

### <a name="error-messages"></a>错误消息

- \<*模型名称*> 具有以下外部内容类型激活错误 。

- 名称为 "\<*型号*>" 的 IMetadataObject 在 "名称" 字段中有一个重复的值 。

### <a name="resolution"></a>解决方法
 若要解决此问题，请手动删除该模型，然后重新部署该解决方案。  您可以使用下列任一工具删除该模型：

- SharePoint 2010 管理中心。 有关详细信息，请参阅 Microsoft TechNet 网站上的[BDC 模型管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14)#delete-a-bdc-model)。

- Windows PowerShell。 您可以通过在命令提示符下键入以下命令来删除该模型： **SPBusinessDataCatalogModel**。 有关详细信息，请参阅 Microsoft TechNet 网站上的[常规 cmdlet （SharePoint Server 2010）](/powershell/module/sharepoint-server) 。

## <a name="an-error-appears-when-you-try-to-view-a-visual-web-part-in-sharepoint"></a>尝试在 SharePoint 中查看可视 web 部件时出现错误
 如果用户控件的**Path**属性不以字符串 "CONTROLTEMPLATES\\" 开头，则会出现此问题。

### <a name="error-messages"></a>错误消息

- 文件 "/_CONTROLTEMPLATES/ *\<项目名称 >* / *\<Web 部件名称*/\<*用户控件名称 >* " 不存在。

- "/" 应用程序中出现服务器错误。

### <a name="resolution"></a>解决方法

##### <a name="to-resolve-this-issue"></a>解决此问题

1. 在**解决方案资源管理器**中，选择文件扩展名为 *.ascx*的用户控件文件。

2. 在菜单栏上，选择 "**查看** > **属性" 窗口**。

3. 在 "**属性**" 窗口中，展开 "**部署位置**" 节点。

4. 确保**Path**属性的值以字符串 "CONTROLTEMPLATES\\" 开头。

## <a name="error-appears-when-an-imported-reusable-workflow-that-contains-a-task-form-field-is-run"></a>当包含任务窗体域的导入可重用工作流运行时出现错误
 如果导入的工作流包含包含字段的任务窗体，然后在从中导入该工作流的同一系统上运行新工作流，则会出现此问题。

### <a name="error-message"></a>错误消息
 部署步骤 "激活功能" 中出错：在当前网站集或子网站中找到了在功能 [*guid*] 中定义的 Id 为 [*guid*] 的字段。

### <a name="resolution"></a>解决方法
 之所以出现此错误，是因为在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中的 "导入可重用工作流" 项目不会更改任务窗体字段 Id，导致出现字段 ID 冲突。 如果在包含原始工作流的同一服务器上部署导入的工作流，则会发生字段 ID 冲突。

 若要解决此问题，请使用 "查找和替换" 功能更改所有导入的工作流文件中 "字段 ID" 属性的值。

## <a name="error-appears-when-a-renamed-imported-list-instance-is-run"></a>当重命名导入的列表实例运行时出现错误
 如果重命名导入的列表实例，然后在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中运行该实例，则会出现此问题。

### <a name="error-message"></a>错误消息
 生成错误：部署步骤 "激活功能" 中发生错误：文件 Template\Features\\[*导入项目*<em>功能</em>*名称*] \Files\Lists\\[*旧*<em>列表名称</em>] \Schema.xml 不存在。

### <a name="resolution"></a>解决方法
 导入列表实例时，会将名为 CustomSchema 的属性添加到该列表实例的元素 .xml 文件。 元素 .xml 包含列表实例的自定义 schema 的路径。 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中重命名列表实例时，自定义架构 .xml 的部署路径会更改，但不会更新 CustomSchema 属性的路径值。 因此，当激活功能时，列表实例找不到由 CustomSchema 属性指定的旧路径中的*架构 .xml*文件。

 若要解决此问题，请在 CustomSchema 属性中更新*schema .xml*文件的部署位置的路径。

## <a name="sharepoint-debugging-session-terminated-by-iis"></a>IIS 终止了 SharePoint 调试会话
 如果你在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint 解决方案中设置断点，然后选择**F5**键运行它，然后在超过90秒的断点处保留，则会出现此问题。

### <a name="error-message"></a>错误消息
 Internet Information Services （IIS）终止了正在调试的 Web 服务器进程。 您可通过在 IIS 中配置应用程序池 Ping 设置来避免此问题。 有关更多详细信息，请参阅 "帮助"。

### <a name="resolution"></a>解决方法
 默认情况下，IIS 应用程序池会等待90秒，应用程序在关闭应用程序之前将做出响应。 此过程称为 "ping" 该应用程序。 若要解决此问题，可以增加等待时间或完全禁用应用程序 ping。

##### <a name="to-access-the-iis-app-pool-settings"></a>访问 IIS 应用程序池设置

1. 打开 IIS 管理器。

2. 在 "**连接**" 窗格中，展开 SharePoint server 节点，然后选择 "**应用程序池**" 节点。

3. 在 "**应用程序池**" 页上，选择 SharePoint 应用程序池（通常为 "sharepoint-80"），然后在 "**操作**" 窗格中选择 "**高级设置**" 链接。

4. 若要增加 IIS 超时前的等待时间，请将 " **Ping 最大响应时间（秒）** " 的值更改为大于90秒的值。

5. 若要禁用 IIS ping，请将 "**启用 Ping** " 设置为 " **False**"。

## <a name="auto-retract-leaves-orphaned-list-instance-in-sharepoint"></a>自动收回在 SharePoint 中离开孤立的列表实例
 如果执行以下步骤，则会出现此问题。

1. 在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中创建一个包含列表实例的列表定义。

2. 选择**F5**键以运行解决方案。

3. 停止调试或关闭 SharePoint 站点。

4. 重新打开 SharePoint 站点并打开 "列表实例"。

### <a name="error-message"></a>错误消息
 "/" 应用程序中出现服务器错误。

### <a name="resolution"></a>解决方法
 发生这种情况的原因是，在关闭 SharePoint 解决方案的调试会话之后，自动收回功能将收回解决方案。 收回操作会从 SharePoint 中删除列表定义，但不会删除列表的实例。 列表实例需要基础列表定义。

 若要解决此问题，请通过在菜单栏上选择 "**生成** > **部署**" 来部署解决方案。 （不要通过选择**F5**键调试解决方案。）然后，在 SharePoint 中删除列表实例。

## <a name="original-sharepoint-solution-is-replaced-by-an-exported-version"></a>原始 SharePoint 解决方案替换为导出版本
 如果导出 SharePoint 解决方案，则将解决方案导入到 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中，然后将该解决方案部署回其导出到的同一站点，原始 SharePoint 解决方案将被替换。 如果将解决方案部署到的服务器上未激活原始解决方案，则不会出现此问题。

### <a name="error-message"></a>错误消息
 无。

### <a name="resolution"></a>解决方法
 若要避免在导出解决方案的站点上覆盖解决方案，请更改 "SolutionID" 和 "[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 项目中所有已导入功能的功能 Id。

## <a name="error-appears-when-debugging-starts"></a>调试开始时出现错误
 在 Visual Studio 中开始调试 SharePoint 解决方案时出现错误，表明由于字典中没有给定键，Visual Studio 无法加载 Web.config 文件。

### <a name="error-message"></a>错误消息
 未能加载 web.config 配置文件。 检查文件中是否存在格式错误的 XML 元素，然后重试。 出现以下错误：字典中不存在给定的键。

### <a name="resolution"></a>解决方法
 若要解决此问题，请确保 Visual Studio 中的 SharePoint 项目的“站点 URL”属性值与分配给 Web 应用程序的备用访问映射的默认区域的 URL 一致。 对 URL 使用其他区域（如 Intranet）将无法解决此错误。 项目的站点 URL 与默认区域中的 URL 必须一致。 若要访问备用访问映射，请打开 SharePoint 2010 管理中心实用工具，选择 "**应用程序管理**" 链接，然后在 " **Web 应用程序**" 下选择 "**配置备用访问映射**" 链接。 有关详细信息，请参阅[为 Web 应用程序创建区域](/previous-versions/office/sharepoint-2007-products-and-technologies/cc263087(v=office.12))。

## <a name="see-also"></a>请参阅

- [SharePoint 打包和部署疑难解答](../sharepoint/troubleshooting-sharepoint-packaging-and-deployment.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [在 Visual Studio 中进行调试](../debugger/debugger-feature-tour.md)