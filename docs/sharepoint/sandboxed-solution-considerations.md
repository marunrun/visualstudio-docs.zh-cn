---
title: 沙盒解决方案注意事项 |Microsoft Docs
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
ms.openlocfilehash: 3f6345e7627549c672aa28fac8cba5f6d9658a23
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435445"
---
# <a name="sandboxed-solution-considerations"></a>沙盒解决方案注意事项
  *沙盒解决方案*是使站点集合用户上传自己的自定义代码的解决方案的 Microsoft SharePoint 2010 中的功能。 常见的沙盒解决方案是将 Web 部件添加其自己的用户。

 在有权访问有限 Web 场的一部分的安全、 受监视进程中运行沙盒 SharePoint 应用程序。 Microsoft SharePoint 2010 使用功能、 解决方案库、 监视、 解决方案和验证框架的组合实现沙盒解决方案。

## <a name="specify-project-trust-level"></a>指定项目的信任级别
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 支持通过布尔项目属性的沙盒解决方案称为*沙盒解决方案*。 可以随时在项目中，设置此属性或可以指定当您创建的项目中**SharePoint 自定义向导**。

> [!NOTE]
> 更改*沙盒解决方案*属性在创建后的项目可能会导致验证错误。

 该解决方案被视为场范围的解决方案，如果*沙盒解决方案*属性设置为**false**或者选择**部署为场解决方案**选项。 但是，该解决方案不会被视为场解决方案如果*沙盒解决方案*属性设置为**true**或者选择**部署为沙盒解决方案**在向导中的选项。

## <a name="sharepoint-site-hierarchy"></a>SharePoint 站点层次结构
 若要了解如何沙盒解决方案的工作，它有助于了解作用域中的 SharePoint 站点是层次结构。 顶级元素被称为 Web 场和其他元素都从属于它：

 Web 场

 Web 应用程序 A

 站点集合 A1

 站点 A1a

 Web 应用程序 B

 站点集合 B1

 站点 B1a

 站点 B1b

 站点集合 B2

 站点 B2a

 如您所见，Web 场可包含一个或多个 Web 应用程序，它又可以包含一个或多个站点集合，其中可以具有子站点，等等。 对一个站点集合产生哪些影响仅站点集合进行和任何其他更改。 但是，在 Web 场级别所做的更改会影响对场的所有站点集合。

 Windows SharePoint Services (WSS) 3.0，可将解决方案部署到的场级别，仅但[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]允许您将部署到服务器场级别 （场解决方案） 或网站集级别 （沙盒解决方案）。

## <a name="why-sandboxed-solutions"></a>为什么沙盒解决方案？
 在 WSS 3.0 中，可以仅向场级别部署解决方案。 这意味着整个 Web 场和其他网站集和其下运行的应用程序的所有受影响的无法部署可能有害或不稳定的解决方案。 但是，通过使用沙盒解决方案，可以将你的解决方案部署的场，在特定站点集合的子区域。 若要提供额外的保护，解决方案的程序集不是加载到主[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)]进程 (*w3wp.exe*)。 相反，加载到一个单独的进程 (*SPUCWorkerProcess.exe*)。 此过程受到监视，实施配额和限制，以防止场执行有害活动，如运行消耗 CPU 周期的紧密循环的沙盒解决方案中。

## <a name="site-collection-solution-gallery"></a>网站集解决方案库
 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 2010 包含一项名为“网站集解决方案库”的功能。 您可以访问此功能从 SharePoint 2010 管理中心页或通过打开**站点操作**菜单中，选择**站点设置**，然后选择**解决方案**链接下**库**SharePoint 站点中。 解决方案库是存储库的解决方案，使网站集管理员来管理其站点集合中的解决方案。

 解决方案库是存储在根 SharePoint 站点的站点中的文档库。 解决方案库替换站点模板，并支持解决方案包。 当 SharePoint 解决方案包 (*.wsp*) 上传文件，它被处理为沙盒解决方案。

## <a name="sandboxed-solution-limitations"></a>沙盒解决方案的限制
 沙盒解决方案部署时，向其提供的 SharePoint 功能的数组是限制以减少可能会有任何安全漏洞。 其中某些限制包括：

- 沙盒解决方案已部署的解决方案元素提供给他们的受限的子集。 可能有漏洞的 SharePoint 项目模板，如站点定义和工作流，将不可用。

- SharePoint 在进程中运行沙盒解决方案代码 (*SPUCWorkerProcess.exe*) 独立于主[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)]应用程序池 (*w3wp.exe*) 过程。

- 无法将映射的文件夹添加到项目。

- 中的类型[!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]Microsoft.Office.Server 不能使用沙盒解决方案中的程序集。 此外，仅在类型[!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)]可以沙盒解决方案中使用 Microsoft.SharePoint 程序集。

  务必要注意该指定 SharePoint 解决方案作为沙盒解决方案; 的 SharePoint 服务器上不产生任何影响它只确定如何将 SharePoint 项目部署到 SharePoint 从[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]和它到绑定的程序集。 它不会影响生成 *.wsp*文件，并 *.wsp*文件没有直接关联到任何数据*沙盒解决方案*属性。

## <a name="capabilities-and-elements-in-sandboxed-solutions"></a>功能和沙盒解决方案中的元素
 沙盒解决方案支持以下功能和元素：

- 内容的类型字段

- 自定义操作

- 声明性工作流

- 事件接收器

- 功能标注

- 列表定义

- 列表实例

- 模块/文件

- 导航

- *Onet.xml*

- SPItemEventReceiver

- SPListEventReceiver

- SPWebEventReceiver

- 对派生的所有 Web 部件的支持 `System.Web.UI.WebControls.WebParts.WebPart`

- Web 部件

- WebTemplate 功能元素 (而不是*Webtemp.xml*)

- 可视 Web 部件

  沙盒解决方案不支持以下功能和元素：

- 应用程序页

- 自定义操作组

- 服务器场范围的功能

- `HideCustomAction` 元素

- Web 应用程序范围的功能

- 使用代码的工作流

## <a name="see-also"></a>请参阅
- [区别沙盒解决方案与场解决方案](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
