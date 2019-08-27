---
title: SharePoint 解决方案的安全性 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- security [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, security
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 31bcd41dc1a6fd7f314c7d701f52c3728dd2ee8c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009776"
---
# <a name="security-for-sharepoint-solutions"></a>SharePoint 解决方案的安全性
  [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 包含以下功能，可帮助增强 SharePoint 应用程序的安全性。

## <a name="safe-control-entries"></a>安全控件项
 每个 SharePoint 项目项中创建[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]已**安全控件项**属性表示一个安全控件集合。 其**安全**子属性，可指定您考虑安全的控件。 有关详细信息，请参阅[提供在项目项中的包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)并[指定安全的 Web 部件](http://go.microsoft.com/fwlink/?LinkId=177521)。

## <a name="allowpartiallytrustedcallers-attribute"></a>AllowPartiallyTrustedCallers 属性
 默认情况下，只有完全信任的运行时代码访问安全性 (CAS) 系统的应用程序可以访问共享的托管的代码程序集。 标记具有 AllowPartiallyTrustedCallers 属性的完全受信任程序集允许部分受信任的程序集，若要对其进行访问。

 AllowPartiallyTrustedCallers 属性添加到任何 SharePoint 解决方案，不部署到系统全局程序集缓存 ( [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)])。 这包括沙盒解决方案或解决方案部署到 SharePoint 应用程序 Bin 目录。 有关详细信息，请参阅[用于 Microsoft.NET Framework 版本 1 的安全性更改](http://go.microsoft.com/fwlink/?LinkId=177515)并[SharePoint Foundation 中部署 Web 部件](http://go.microsoft.com/fwlink/?LinkId=177509)。

## <a name="safe-against-script-property"></a>安全应对脚本属性
 *脚本注入*是潜在的恶意代码插入到控件或网页。 为了帮助保护对脚本注入的 SharePoint 2010 站点，参与者无法查看或编辑默认的 Web 部件或其属性。 通过调用 SafeAgainstScript SafeControl 属性控制此行为。 在中[!include[vsprvs](../sharepoint/includes/vsprvs-md.md)]，将此属性设置中的项目项**安全控件项**子属性**安全应对脚本**。 有关详细信息，请参阅[提供在项目项中的包和部署信息](../sharepoint/providing-packaging-and-deployment-information-in-project-items.md)和[如何：将控件标记为安全控件](../sharepoint/how-to-mark-controls-as-safe-controls.md)。

## <a name="vista-and-windows-7-user-account-control"></a>Vista 和 Windows 7 用户帐户控制
 [!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)] 和[!INCLUDE[win7](../sharepoint/includes/win7-md.md)]包含一个名为用户帐户控制 (UAC) 的安全功能。 开发 SharePoint 解决方案中的[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]上[!INCLUDE[windowsver](../sharepoint/includes/windowsver-md.md)]并[!INCLUDE[win7](../sharepoint/includes/win7-md.md)]系统中，UAC 要求运行[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]作为系统管理员。 从**启动**菜单中，打开快捷菜单[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，然后选择**以管理员身份运行**。

 若要配置[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]快捷方式，以便始终以管理员身份运行，打开其快捷菜单，选择**属性**，选择**高级**按钮**属性**对话框中，并选择**以管理员身份运行**复选框。

 有关详细信息，请参阅[理解和 Windows Vista 中配置用户帐户控制](http://go.microsoft.com/fwlink/?LinkID=156476)。 并[Windows 7 用户帐户控制](http://go.microsoft.com/fwlink/?LinkId=177523)。

## <a name="sharepoint-permissions-considerations"></a>SharePoint 权限注意事项
 若要开发 SharePoint 解决方案，必须具有足够的权限来运行和调试 SharePoint 解决方案。 你可以测试 SharePoint 解决方案之前，请执行以下步骤以确保拥有所需的权限：

1. 将你的用户帐户添加为系统上的管理员。

2. 将你的用户帐户添加为 SharePoint 服务器场管理员。

    1. 在 SharePoint 2010 管理中心，选择**管理服务器场管理员组**链接。

    2. 上**服务器场管理员**页上，选择**新建**菜单选项

3. 添加到你的用户帐户向 WSS_ADMIN_WPG 组。

## <a name="additional-security-resources"></a>其他安全资源
 有关安全问题的详细信息，请参阅。

### <a name="visual-studio-security"></a>Visual Studio 安全

- [安全性和用户权限](http://go.microsoft.com/fwlink/?LinkId=177503)

- [本机代码和.NET Framework 代码中的安全性](http://go.microsoft.com/fwlink/?LinkId=177504)

- [.NET Framework 中的安全性](http://go.microsoft.com/fwlink/?LinkId=177502)

### <a name="sharepoint-security"></a>SharePoint 安全性

- [SharePoint Foundation 管理和安全性](http://go.microsoft.com/fwlink/?LinkId=177501)

- [SharePoint 安全资源中心](http://go.microsoft.com/fwlink/?LinkId=177498)

- [保护 SharePoint Foundation 中的 Web 部件](http://go.microsoft.com/fwlink/?LinkId=177511)

- [提高 Web 应用程序安全性：威胁和对策](http://go.microsoft.com/fwlink/?LinkID=140080)

### <a name="general-security"></a>常规安全

- [MSDN 安全开发生命周期](http://go.microsoft.com/fwlink/?LinkID=147149)

- [构建安全的 ASP.NET 应用程序：身份验证、 授权和安全通信](http://go.microsoft.com/fwlink/?LinkId=177494)

## <a name="see-also"></a>请参阅

- [开发 SharePoint 解决方案](../sharepoint/developing-sharepoint-solutions.md)