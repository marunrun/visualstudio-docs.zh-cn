---
title: 生成和调试 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, building and debugging
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: e91c1433fde85a9ec828a6a018bee986fdc7aa5c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62988141"
---
# <a name="build-and-debug-sharepoint-solutions"></a>生成和调试 SharePoint 解决方案
  一般情况下，生成和调试 SharePoint 解决方案是生成和调试其他类型中的项目的相同[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 本部分的主题介绍存在的差异。

## <a name="project-output-for-sharepoint-solutions"></a>SharePoint 解决方案的的项目输出
 构建 SharePoint 解决方案创建程序集和解决方案包 ( *.wsp*) 文件。 下表显示在生成期间这些文件的位置。

|生成项|输出文件夹|
|----------------|-------------------|
|程序集、 程序数据库 ( *.pdb*)，并 *.wsp*文件。|*\<项目名称 > \bin\debug*或 *\<项目名称 > \bin\release*|
|SharePoint 项目项文件。|*\<项目名称 > \pkg\debug*或 *\<项目名称 > \pkg\release*|
|生成中间文件。|*\<项目名称 > \obj\debug*或 *\<项目名称 > \obj\release*|
|包中间文件。|*\<项目名称 > \pkgobj\debug*或 *\<项目名称 > \pkgobj\release*|

## <a name="build-sharepoint-solutions"></a>构建 SharePoint 解决方案
 若要生成 SharePoint 解决方案，在开发计算机必须安装 SharePoint 服务器的正确版本。 否则，构建 SharePoint 解决方案是与生成其他类型中的项目的相同[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。 有关详细信息，请参阅[如何：构建 SharePoint 解决方案](../sharepoint/how-to-build-sharepoint-solutions.md)。

## <a name="debug-and-test-sharepoint-solutions"></a>调试和测试 SharePoint 解决方案
 在调试时前,[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]副本 *.wsp*包到 SharePoint 服务器激活的站点和 Web 范围的功能，并在某些情况下，将启动项目。 在某些情况下，您可能必须手动打开项目。 有关详细信息，请参阅[进行故障排除 SharePoint 解决方案](../sharepoint/troubleshooting-sharepoint-solutions.md)并[调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)。

## <a name="debug-and-verify-sharepoint-solutions-by-using-azure-devops-services-features"></a>调试和使用 Azure DevOps 服务功能来验证 SharePoint 解决方案
 Azure DevOps 服务功能，例如单元测试和 IntelliTrace，您在 SharePoint 解决方案中的更多准确地查明问题。 通过分析，您可以查找并确定 SharePoint 解决方案中的性能问题区域。 有关详细信息，请参阅[验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)并[分析 SharePoint 应用程序性能](../sharepoint/profiling-the-performance-of-sharepoint-applications.md)。

## <a name="security-during-the-build-process"></a>在生成过程中的安全
 若要打包或部署 SharePoint 解决方案[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]必须有权将文件复制到 SharePoint 服务器。 您必须运行[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]提升的进程，以及你的用户帐户必须是 SharePoint 服务器上的站点集合管理员。 此外，必须指定你的项目是沙盒解决方案或场解决方案。 有关详细信息，请参阅[Differences Between Sandboxed 和场解决方案](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)。

## <a name="using-the-clean-command"></a>使用清理命令
 对于调试，在 SharePoint 服务器上安装 SharePoint 解决方案时**清理**命令不会卸载该解决方案。 相反，您必须先停用的功能通过 SharePoint 配置。

## <a name="see-also"></a>请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [浏览 SharePoint 连接使用服务器资源管理器](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
