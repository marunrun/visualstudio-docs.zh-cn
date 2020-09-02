---
title: 沙盒解决方案与场解决方案之间的差异 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
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
ms.openlocfilehash: 073e62b473ebfcec5f71ae1907e8f9e385333411
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62967541"
---
# <a name="differences-between-sandboxed-and-farm-solutions"></a>沙盒解决方案与场解决方案之间的差异
  编译 SharePoint 解决方案时，该解决方案将部署到 SharePoint 服务器上，并附加调试器以对其进行调试。 用于调试解决方案的过程取决于沙盒解决方案属性的设置：沙盒解决方案或场解决方案。

 有关详细信息，请参阅 [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="farm-solutions"></a>场解决方案
 在场解决方案（托管在 IIS 工作进程 ( # A0) 中）运行可能影响整个场的代码。 调试其沙盒解决方案属性设置为 "场解决方案" 的 SharePoint 项目时，该系统的 IIS 应用程序池会在 SharePoint 收回之前回收或部署该功能，以便释放由 IIS 工作进程锁定的任何文件。 仅回收为 SharePoint 项目的网站 URL 提供服务的 IIS 应用程序池。

## <a name="sandboxed-solutions"></a>沙盒解决方案
 沙盒解决方案在 SharePoint 用户代码解决方案工作进程中承载 ( # A0) ，运行只能影响解决方案网站集的代码。 由于沙盒解决方案不在 IIS 工作进程中运行，因此 IIS 应用程序池和 IIS 服务器都不能重启。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将调试器附加到 Spucworkerprocess.exe 进程，SharePoint 中的 SPUserCodeV4 服务会自动触发和控制。 Spucworkerprocess.exe 进程回收以加载最新版本的解决方案并不是必需的。

## <a name="either-type-of-solution"></a>任一类型的解决方案
 对于任一解决方案类型， [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 还会将调试器附加到浏览器以启用客户端脚本调试。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 出于此目的使用脚本调试引擎。 若要启用脚本调试，您必须在出现提示时更改默认浏览器设置。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 仅将调试器附加到运行当前站点的 W3WP.EXE 或 Spucworkerprocess.exe 进程。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 还附加托管 COM Plus 和工作流调试引擎。

## <a name="see-also"></a>另请参阅
- [调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)
