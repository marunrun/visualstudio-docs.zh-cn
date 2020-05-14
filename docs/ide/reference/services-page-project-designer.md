---
title: “项目设计器”->“服务”页
ms.date: 01/18/2018
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesServices
helpviewer_keywords:
- Services page in Project Designer
- Project Designer, Services page
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d30d8e8ddcdc8c1fa4fe1935da1f1dedd1b18f4b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "75593559"
---
# <a name="services-page-project-designer"></a>“项目设计器”->“服务”页

使用客户端应用程序服务，可简便地从 Windows 窗体和 Windows Presentation Foundation (WPF) 应用程序访问 [!INCLUDE[ajax_current_short](../../ide/reference/includes/ajax_current_short_md.md)] 登录、角色和配置文件服务。 可以使用“项目设计器”  的“服务”  页为项目启用并配置客户端应用程序服务。

通过客户端应用程序服务，可以使用集中式服务器对用户进行验证，确定为每个用户分配的角色，并存储每个用户的应用程序设置，可以在网络上共享这些设置。 有关详细信息，请参阅[客户端应用程序服务](/dotnet/framework/common-client-technologies/client-application-services)。

若要访问“服务”  页，请在“解决方案资源管理器”  中选择项目节点，然后在“项目”  菜单上单击“属性”  。 显示“项目设计器”  时，单击“服务”  选项卡。

## <a name="task-list"></a>任务列表

[如何：配置客户端应用程序服务](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)

## <a name="uielement-list"></a>UIElement 列表

 **配置**

此控件在本页面上不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) 或[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

 **平台**

此控件在本页面上不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) 或[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

 **启用客户端应用程序服务**

选中该项可启用客户端应用程序服务。 必须在“服务”  页上指定服务位置，才能使用客户端应用程序服务。

 **使用 Windows 身份验证**

指示验证提供程序将使用基于 Windows 的身份验证，即 Windows 操作系统提供的标识。

 **使用 Forms 身份验证**

指示验证提供程序将使用 Forms 身份验证。 这意味着应用程序必须提供用户界面以供登录。 有关详细信息，请参阅[如何：使用客户端应用程序服务来实现用户登录](/dotnet/framework/common-client-technologies/how-to-implement-user-login-with-client-application-services)。

 **身份验证服务位置**

仅用于 Forms 身份验证。 指定身份验证服务的位置。

 **可选：凭据提供程序**

仅用于 Forms 身份验证。 当应用程序调用 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider>`static` 方法以及为参数传递空字符串或 <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 时，指示身份验证服务将用于显示登录对话框的 `null` 实现。 如果将此框留空，则必须向 <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法传递有效的用户名和密码。 必须将凭据提供程序指定为程序集限定类型名称。 有关详细信息，请参阅 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=fullName> 和[程序集名称](/dotnet/framework/app-domains/assembly-names)。 程序集限定类型名称最简单的形式类似于下面的示例：`MyNamespace.MyLoginClass, MyAssembly`

 **角色服务位置**

指定角色服务的位置。

 **Web 设置服务位置**

指定配置文件（Web 设置）服务的位置。

 **高级**

打开[“高级服务设置”对话框](../../ide/reference/advanced-settings-for-services-dialog-box.md)，可以使用该对话框重写默认行为。 例如，可以使用此对话框指定一个数据库进行脱机存储，而不是使用本地文件系统。 有关详细信息，请参阅[“高级服务设置”对话框](../../ide/reference/advanced-settings-for-services-dialog-box.md)。

## <a name="see-also"></a>另请参阅

- [客户端应用程序服务](/dotnet/framework/common-client-technologies/client-application-services)
- [“高级服务设置”对话框](../../ide/reference/advanced-settings-for-services-dialog-box.md)
- [如何：配置客户端应用程序服务](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)
- [“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md)
- [“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)
