---
title: 生成和调试 SharePoint 解决方案 | Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "86016368"
---
# <a name="build-and-debug-sharepoint-solutions"></a>生成和调试 SharePoint 解决方案
  通常情况下，生成和调试 SharePoint 解决方案与在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 中生成和调试其他类型的项目相同。 本部分的主题介绍存在的差异。

## <a name="project-output-for-sharepoint-solutions"></a>SharePoint 解决方案的项目输出
 生成 SharePoint 解决方案时会创建程序集和解决方案包 (.wsp) 文件。 下表显示了生成期间这些文件的位置。

|生成项|输出文件夹|
|----------------|-------------------|
|程序集、程序数据库 (.pdb) 和 .wsp 文件 。|\<ProjectName>\bin\debug 或 \<ProjectName>\bin\release |
|SharePoint 项目项文件。|\<ProjectName>\pkg\debug 或 \<ProjectName>\pkg\release |
|生成中间文件。|\<ProjectName>\obj\debug 或 \<ProjectName>\obj\release |
|打包中间文件。|\<ProjectName>\pkgobj\debug 或 \<ProjectName>\pkgobj\release |

## <a name="build-sharepoint-solutions"></a>生成 SharePoint 解决方案
 若要生成 SharePoint 解决方案，开发计算机必须安装正确版本的 SharePoint 服务器。 否则，生成 SharePoint 解决方案与在 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]中生成其他类型的项目相同。 有关详细信息，请参阅[如何：生成 SharePoint 解决方案](../sharepoint/how-to-build-sharepoint-solutions.md)。

## <a name="debug-and-test-sharepoint-solutions"></a>调试并测试 SharePoint 解决方案
 在调试之前，[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将 .wsp 包复制到 SharePoint 服务器，激活站点和 Web 范围的功能，在某些情况下，启动项目。 在某些情况下，您可能必须手动打开项目。 有关详细信息，请参阅 [SharePoint 解决方案疑难解答](../sharepoint/troubleshooting-sharepoint-solutions.md)和[调试 SharePoint 解决方案](../sharepoint/debugging-sharepoint-solutions.md)。

## <a name="debug-and-verify-sharepoint-solutions-by-using-azure-devops-services-features"></a>使用 Azure DevOps Services 功能调试和验证 SharePoint 解决方案
 Azure DevOps Services 功能（例如单元测试和 IntelliTrace）可以更准确地查明 SharePoint 解决方案中的问题。 通过分析，您可以查找并确定 SharePoint 解决方案中的性能问题区域。 有关详细信息，请参阅[验证和调试 SharePoint 代码](../sharepoint/verifying-and-debugging-sharepoint-code.md)和[分析 SharePoint 应用程序的性能](../sharepoint/profiling-the-performance-of-sharepoint-applications.md)。

## <a name="security-during-the-build-process"></a>生成过程中的安全性
 若要打包或部署 SharePoint 解决方案，[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 必须具有将文件复制到 SharePoint 服务器的权限。 必须将 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 作为提升的进程运行，且你的用户帐户必须是 SharePoint 服务器上的网站集管理员。 此外，必须指定你的项目是沙盒解决方案还是场解决方案。 有关详细信息，请参阅[沙盒解决方案与场解决方案之间的差异](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)。

## <a name="using-the-clean-command"></a>使用 Clean 命令
 在 SharePoint 服务器上安装 SharePoint 解决方案以便进行调试时，“Clean”命令不会卸载解决方案。 相反，必须通过 SharePoint 配置来停用“功能”。

## <a name="see-also"></a>另请参阅
- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)
- [使用服务器资源管理器浏览 SharePoint 连接](../sharepoint/browsing-sharepoint-connections-using-server-explorer.md)
- [打包和部署 SharePoint 解决方案](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
