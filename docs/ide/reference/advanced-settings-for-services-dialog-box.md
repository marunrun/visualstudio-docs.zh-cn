---
title: “高级服务设置”对话框
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedServices
helpviewer_keywords:
- Advanced Settings for Services dialog box
ms.assetid: 6dde4a2d-85e1-4275-aa55-24b84111be91
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f7f599b4448fe39bf8c0d82d030f5f1173f28699
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919333"
---
# <a name="advanced-settings-for-services-dialog-box"></a>“高级服务设置”对话框
使用客户端应用程序服务，可简便地从 Windows 窗体和 Windows Presentation Foundation (WPF) 应用程序访问 [!INCLUDE[ajax_current_short](../../ide/reference/includes/ajax_current_short_md.md)] 登录、角色和配置文件服务。 可以使用“项目设计器”  的“服务”  页，配置客户端应用程序服务。 有关“服务”  页的详细信息，请参阅[“项目设计器”->“服务”页](../../ide/reference/services-page-project-designer.md)。

在“项目设计器”  中，使用“服务”  页的“服务的高级设置”  对话框，配置客户端应用程序服务的高级设置。 通过使用这些设置，可以重写一些默认应用程序服务行为，从而启用不太常见的方案。 有关详细信息，请参阅[客户端应用程序服务](/dotnet/framework/common-client-technologies/client-application-services)。

若要访问“服务的高级设置”  对话框，请在“解决方案资源管理器”  中选择项目节点，然后在“项目”  菜单上单击“属性”  。 显示“项目设计器”  后，单击“服务”  选项卡，然后单击“高级”  按钮。 启用客户端应用程序服务前，此按钮将处于禁用状态。

## <a name="task-list"></a>任务列表

- [如何：配置客户端应用程序服务](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)

## <a name="uielement-list"></a>UIElement 列表

 **本地保存密码哈希以启用脱机登录**指定是否本地缓存用户密码的加密形式，以便在应用程序处于脱机模式时允许用户登录。 默认情况下选择此选项。

 **每当服务器 Cookie 过期时要求用户重新登录**指定应用程序访问角色或配置文件服务并且服务器身份验证 cookie 已过期时，先前已通过身份验证的用户是否会自动重新验证。 选中此选项可以在 cookie 过期后，拒绝对应用程序服务的访问，并要求进行显式重新验证。 这对于公共位置中部署的应用程序来说非常有用，可确保让应用程序在使用后保持运行状态的用户不会无限期地保持通过身份验证的状态。 默认情况下清除此选项。

 **角色服务缓存超时**指定客户端角色提供程序使用缓存的角色值（而不是访问角色服务）的时间量。 频繁更新角色时，将此时间间隔设置为较小的值，而在不常更新角色时，将此时间间隔设置为较大的值。 默认值为一天。

调用 <xref:System.Web.Security.RolePrincipal.IsInRole%2A> 方法时，角色提供程序将访问缓存的角色值或角色服务。 若要以编程方式清除缓存并强制此方法访问远程服务，请调用 <xref:System.Web.ClientServices.Providers.ClientRoleProvider.ResetCache%2A> 方法。

 **使用自定义连接字符串**指定客户端服务提供程序是否将使用自定义数据存储进行本地缓存。 默认情况下，服务提供商将使用本地文件系统进行缓存。 选中此选项将自动使用默认连接字符串填充文本框。 可以保留默认连接字符串以自动生成和使用 SQL Server Compact Edition 数据库，或者可以为现有 SQL Server 数据库指定连接字符串。 有关详细信息，请参阅[如何：配置客户端应用程序服务](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)。 默认情况下清除此选项。

## <a name="see-also"></a>请参阅

- [客户端应用程序服务](/dotnet/framework/common-client-technologies/client-application-services)
- [“项目设计器”->“服务”页](../../ide/reference/services-page-project-designer.md)
- [如何：配置客户端应用程序服务](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)