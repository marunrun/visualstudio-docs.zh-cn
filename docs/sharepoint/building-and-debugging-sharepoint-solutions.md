---
title: 生成和调试 SharePoint 解决方案 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: overview
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
ms.openlocfilehash: e4b34df23c8cb612d72fed108a6c0aecbf57875c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016368"
---
# <a name="build-and-debug-sharepoint-solutions"></a>生成和调试 SharePoint 解决方案
  通常，生成和调试 SharePoint 解决方案与在中生成和调试其他类型的项目相同 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 本部分的主题介绍存在的差异。

## <a name="project-output-for-sharepoint-solutions"></a>SharePoint 解决方案的项目输出
 生成 SharePoint 解决方案将创建程序集和解决方案包（*.wsp*）文件。 下表显示了生成期间这些文件的位置。

|生成项|输出文件夹|
|----------------|-------------------|
|程序集、程序数据库（*.pdb*）和 *.wsp*文件。|* \<ProjectName> \bin\debug*或* \<ProjectName> \bin\release*|
|SharePoint 项目项文件。|* \<ProjectName> \pkg\debug*或* \<ProjectName> \pkg\release*|
|生成中间文件。|* \<ProjectName> \obj\debug*或* \<ProjectName> \obj\release*|
|打包中间文件。|* \<ProjectName> \pkgobj\debug*或* \<ProjectName> \pkgobj\release*|

## <a name="build-sharepoint-solutions"></a>生成 SharePoint 解决方案
 若要生成 SharePoint 解决方案，开发计算机必须安装了正确版本的 SharePoint server。 否则，生成 SharePoint 解决方案与在中生成其他类型的项目相同 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 。 有关详细信息，请参阅[如何：生成 SharePoint 解决方案](../sharepoint/how-to-build-sharepoint-solutions.md)。

## <a name="debug-and-test-sharepoint-solutions"></a>调试和测试 SharePoint 解决方案
 调试之前，会 [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 *.wsp*包复制到 SharePoint 服务器，激活站点和 Web 范围的功能，在某些情况下，会启动项目。 在某些情况下，您可能必须手动打开项目。 有关详细信息，请参阅[sharepoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)和[调试 sharepoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)。

## <a name="debug-and-verify-sharepoint-solutions-by-using-azure-devops-services-features"></a>使用 Azure DevOps Services 功能调试和验证 SharePoint 解决方案
 通过使用单元测试和 IntelliTrace Azure DevOps Services 功能，您可以更准确地查明 SharePoint 解决方案中的问题。 通过分析，您可以查找并确定 SharePoint 解决方案中的性能问题区域。 有关详细信息，请参阅[验证和调试 Sharepoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)和[分析 sharepoint 应用程序的性能](../sharepoint/profiling-the-performance-of-sharepoint-applications.md)。

## <a name="security-during-the-build-process"></a>生成过程中的安全性
 若要打包或部署 SharePoint 解决方案， [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 必须具有将文件复制到 sharepoint 服务器的权限。 您必须以 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 提升的进程运行，并且您的用户帐户必须是 SharePoint 服务器上的网站集管理员。 此外，你必须指定你的项目是沙盒解决方案还是场解决方案。 有关详细信息，请参阅[沙盒解决方案与场解决方案之间的差异](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)。

## <a name="using-the-clean-command"></a>使用 "清除" 命令
 在 SharePoint 服务器上安装 SharePoint 解决方案以便进行调试时，"**清理**" 命令不会卸载解决方案。 相反，您必须通过 SharePoint 配置停用功能。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
