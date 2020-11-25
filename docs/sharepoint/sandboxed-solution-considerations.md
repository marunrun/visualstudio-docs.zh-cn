---
title: 沙盒解决方案注意事项 |Microsoft Docs
description: 探索沙盒解决方案，这是 Microsoft SharePoint 中的一项功能，使网站集用户可以上传自己的自定义代码解决方案。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SandboxedSolutions
- VS.SharePointTools.Security.SandboxedSolutions
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 17b310a3f992f80b04ad14bb6e038e05b009a4af
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2020
ms.locfileid: "95970458"
---
# <a name="sandboxed-solution-considerations"></a>沙盒解决方案注意事项
  *沙盒解决方案* 是 Microsoft SharePoint 2010 的一项功能，它使网站集用户可以上传自己的自定义代码解决方案。 常见的沙盒解决方案是用户上传自己的 Web 部件。

 沙盒中的 SharePoint 应用程序在安全的、受监视的进程中运行，该进程可以访问部分 Web 场。 Microsoft SharePoint 2010 使用功能、解决方案库、解决方案监视和验证框架的组合来启用沙盒解决方案。

## <a name="specify-project-trust-level"></a>指定项目信任级别
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 支持通过名为 *沙盒解决方案* 的布尔项目属性使用沙盒解决方案。 此属性可以在项目中随时设置，也可以在 **SharePoint 自定义向导** 中创建项目时指定。

> [!NOTE]
> 在项目创建后更改其 " *沙盒解决方案* " 属性可能会导致验证错误。

 如果 " *沙盒解决方案* 属性" 设置为 " **false** " 或选择 " **部署为场解决方案** " 选项，则该解决方案将被视为场范围的解决方案。 但是，如果将 " *沙盒解决方案* " 属性设置为 " **true** " 或在向导中选择 " **部署为沙盒解决方案** " 选项，则解决方案的处理方式不同于场解决方案。

## <a name="sharepoint-site-hierarchy"></a>SharePoint 站点层次结构
 若要了解沙盒解决方案的工作原理，有助于了解 SharePoint 站点在范围内是分层的。 顶部元素称为 Web 场，其他元素是其从属元素：

 Web 场

 Web 应用程序 A

 网站集 A1

 站点 A1a

 Web 应用程序 B

 网站集 B1

 站点 B1a

 站点 B1b

 网站集 B2

 站点 B2a

 正如您所看到的，Web 场可以包含一个或多个 Web 应用程序，而这些 Web 应用程序又可以包含一个或多个网站集，这些网站集可以有子网站等。 对一个网站集所做的更改只会影响该网站集，而不会影响其他网站集。 但是，在 Web 场级别所做的更改将影响场中的所有网站集。

 Windows SharePoint Services (WSS) 3.0 使你可以仅将解决方案部署到场级别，但 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 允许部署到场级别 (场解决方案) 或网站集级别 (沙盒解决方案) 。

## <a name="why-sandboxed-solutions"></a>为什么是沙盒解决方案？
 在 WSS 3.0 中，解决方案只能部署到场级别。 这意味着可能会对可能有害或破坏的解决方案进行部署，这些解决方案会影响整个 Web 场以及在其下运行的所有其他网站集和应用程序。 但是，通过使用沙盒解决方案，可以将解决方案部署到场的子区域，即特定的网站集。 为了提供额外的保护，解决方案的程序集不会加载到主 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 进程中， (*w3wp.exe*) 。 相反，它将加载到单独的进程中 (*SPUCWorkerProcess.exe*) 。 此过程受到监视并实现了配额和限制，以便保护场免遭执行有害活动的沙盒解决方案（例如，运行占用 CPU 周期的紧密循环）。

## <a name="site-collection-solution-gallery"></a>网站集解决方案库
 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 2010 包含一项名为“网站集解决方案库”的功能。 你可以从 SharePoint 2010 管理中心页面访问此功能，或通过打开 "**网站操作**" 菜单，选择 **"站点设置**"，然后选择 SharePoint 站点中 "**库**" 下的 "**解决方案**" 链接。 解决方案库是解决方案的存储库，使网站集管理员可以在其网站集中管理解决方案。

 解决方案库是存储在 SharePoint 站点的根网站中的文档库。 解决方案库取代了站点模板并支持解决方案包。 当上载 SharePoint 解决方案包 (*.wsp*) 文件时，它将作为沙盒解决方案进行处理。

## <a name="sandboxed-solution-limitations"></a>沙盒解决方案限制
 部署沙盒解决方案时，可供其使用的 SharePoint 功能的数组将受到限制，以帮助减少它可能具有的任何安全漏洞。 其中一些限制包括：

- 沙盒解决方案具有可供他们使用的可部署解决方案元素的有限子集。 可能存在漏洞的 SharePoint 项目模板，如站点定义和工作流。

- SharePoint 在进程 (*SPUCWorkerProcess.exe*) 独立于主 [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] 应用程序池 (*w3wp.exe*) 过程中运行沙盒解决方案代码。

- 无法将映射的文件夹添加到项目。

- [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]程序集中的类型不能在沙盒解决方案中使用。 此外，在 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] 沙盒解决方案中只能使用程序集中的类型。

  需要特别注意的是，将 SharePoint 解决方案指定为沙盒解决方案对 SharePoint 服务器没有影响;它仅确定如何从 sharepoint 项目部署到 SharePoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 以及它所绑定到的程序集。 它不会影响生成的 *.wsp* 文件，并且 *.wsp* 文件没有直接与 *沙盒解决方案* 属性关联的数据。

## <a name="capabilities-and-elements-in-sandboxed-solutions"></a>沙盒解决方案中的功能和元素
 沙盒解决方案支持以下功能和元素：

- 内容类型/字段

- 自定义操作

- 声明性工作流

- 事件接收器

- 功能标注

- 列出定义

- 列出实例

- 模块/文件

- 导航

- *Onet.xml*

- SPItemEventReceiver

- SPListEventReceiver

- SPWebEventReceiver

- 支持派生自的所有 Web 部件 `System.Web.UI.WebControls.WebParts.WebPart`

- Web 部件

- WebTemplate 功能元素 (而不是 *Webtemp.xml*) 

- 视觉对象 Web 部件

  沙盒解决方案不支持以下功能和元素：

- 应用程序页

- 自定义操作组

- 场作用域内功能

- `HideCustomAction` 元素

- Web 应用程序范围的功能

- 包含代码的工作流

## <a name="see-also"></a>另请参阅
- [沙盒解决方案与场解决方案之间的差异](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
