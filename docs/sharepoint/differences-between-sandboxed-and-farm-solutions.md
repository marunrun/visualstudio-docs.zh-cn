---
title: 区别沙盒解决方案与场解决方案 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62967541"
---
# <a name="differences-between-sandboxed-and-farm-solutions"></a>区别沙盒解决方案与场解决方案
  编译 SharePoint 解决方案时，它将部署到 SharePoint 服务器，并附加调试器来调试它。 用于调试解决方案的过程取决于沙盒解决方案属性的设置： 沙盒解决方案或场解决方案。

 有关详细信息，请参阅[沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)。

## <a name="farm-solutions"></a>场解决方案
 场解决方案，承载于 IIS 工作进程 (W3WP.exe) 中，运行可能会影响整个服务器场的代码。 当调试其沙盒解决方案属性设置为"场解决方案"的 SharePoint 项目时，系统的 IIS 应用程序池回收之前 SharePoint 收回或部署功能，以便释放锁定 IIS 工作进程的任何文件。 仅提供 SharePoint 项目的站点 URL 的 IIS 应用程序池被回收。

## <a name="sandboxed-solutions"></a>沙盒解决方案
 沙盒解决方案，托管在 SharePoint 用户代码解决方案工作进程 (SPUCWorkerProcess.exe) 中，运行只会影响解决方案的网站集的代码。 因为未在 IIS 工作进程中运行沙盒解决方案，既不 IIS 应用程序池，也不在 IIS 服务器必须重新启动。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将调试器附加到 SharePoint 中的 SPUserCodeV4 服务会自动触发的 SPUCWorkerProcess 过程和控件。 不需要为 SPUCWorkerProcess 进程回收加载解决方案的最新版本。

## <a name="either-type-of-solution"></a>任一类型的解决方案
 无论使用哪一类解决方案，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]还会将调试器附加到浏览器，启用客户端脚本调试。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 使用的脚本调试引擎实现此目的。 若要启用脚本调试，必须更改默认浏览器设置，当系统提示。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将调试器附加到运行当前站点的 W3WP 或 SPUCWorkerProcess 进程仅。 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 此外会将附加的托管 COM Plus 和工作流调试引擎。

## <a name="see-also"></a>请参阅
- [调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)
- [生成和调试 SharePoint 解决方案](../sharepoint/building-and-debugging-sharepoint-solutions.md)
- [沙盒解决方案注意事项](../sharepoint/sandboxed-solution-considerations.md)
