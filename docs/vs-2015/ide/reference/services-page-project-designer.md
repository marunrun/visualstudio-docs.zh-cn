---
title: “项目设计器”->“服务”页 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesServices
helpviewer_keywords:
- Services page in Project Designer
- Project Designer, Services page
ms.assetid: 6dd9e0fa-acba-4d7d-b081-705b0fc86ff5
caps.latest.revision: 30
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 11e1cd997c76974e7b4b8771c0579c175469eca6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665479"
---
# <a name="services-page-project-designer"></a>“项目设计器”->“服务”页
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

使用客户端应用程序服务，可简便地从 Windows 窗体和 Windows Presentation Foundation (WPF) 应用程序访问 [!INCLUDE[ajax_current_short](../../includes/ajax-current-short-md.md)] 登录、角色和配置文件服务。 可以使用“项目设计器”的“服务”页为项目启用并配置客户端应用程序服务。

 通过客户端应用程序服务，可以使用集中式服务器对用户进行验证，确定为每个用户分配的角色，并存储每个用户的应用程序设置，可以在网络上共享这些设置。 有关详细信息，请参阅[客户端应用程序服务](https://msdn.microsoft.com/library/1487d8df-089e-4f21-abfb-a791a652b58e)。

 若要访问“服务”页，请在“解决方案资源管理器”中选择项目节点，然后在“项目”菜单上单击“属性”。 显示“项目设计器”时，单击“服务”选项卡。

> [!NOTE]
> 客户端应用程序服务要求完整版的 .NET Framework，在 .NET Framework Client Profile 中不受支持。 如果“启用客户端应用程序服务”复选框处于禁用状态，请验证“目标框架”是否设置为 .NET Framework 3.5 或更高版本。 若要查看 C# 中的“目标框架”设置，请打开项目设计器，然后单击“应用程序”页面。 若要查看 Visual Basic 中的“目标框架”设置，请打开项目设计器，单击“编译”页面，然后单击“高级编译选项”。

## <a name="task-list"></a>任务列表
 [如何：配置客户端应用程序服务](https://msdn.microsoft.com/library/34a8688a-a32c-40d3-94be-c8e610c6a4e8)

## <a name="uielement-list"></a>UIElement 列表
 **配置**此控件在此页上不可编辑。 有关此控件的说明，请参阅[“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) 或[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

 **平台**在本页中不可编辑此控件。 有关此控件的说明，请参阅[“项目设计器”->“编译”页 (Visual Basic)](../../ide/reference/compile-page-project-designer-visual-basic.md) 或[“项目设计器”->“生成”页 (C#)](../../ide/reference/build-page-project-designer-csharp.md)。

 **启用客户端应用程序服务**选择 "启用客户端应用程序服务"。 必须在“服务”页上指定服务位置，才能使用客户端应用程序服务。

 **使用 Windows 身份验证**指示身份验证提供程序将使用基于 Windows 的身份验证，即 Windows 操作系统提供的标识。

 **使用窗体身份验证**指示身份验证提供程序将使用 forms 身份验证。 这意味着应用程序必须提供用户界面以供登录。 有关详细信息，请参阅[如何：使用客户端应用程序服务来实现用户登录](https://msdn.microsoft.com/library/5431a671-eb02-4e18-a651-24764fccec9a)。

 **身份验证服务位置**仅与 forms 身份验证一起使用。 指定身份验证服务的位置。

 **可选：凭据提供程序**仅与 forms 身份验证一起使用。 当应用程序调用 `static`<xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法以及为参数传递空字符串或 `null` 时，指示身份验证服务将用于显示登录对话框的 <xref:System.Web.ClientServices.Providers.IClientFormsAuthenticationCredentialsProvider> 实现。 如果将此框留空，则必须向 <xref:System.Web.Security.Membership.ValidateUser%2A?displayProperty=fullName> 方法传递有效的用户名和密码。 必须将凭据提供程序指定为程序集限定类型名称。 有关详细信息，请参阅 <xref:System.Type.AssemblyQualifiedName%2A?displayProperty=fullName> 和[程序集名称](https://msdn.microsoft.com/library/8f8c2c90-f15d-400e-87e7-a757e4f04d0e)。 程序集限定类型名称最简单的形式类似于下面的示例：`MyNamespace.MyLoginClass, MyAssembly`

 **角色服务位置**指定角色服务的位置。

 **Web 设置服务位置**指定配置文件（Web 设置）服务的位置。

 **高级**打开 "[服务的高级设置" 对话框](../../ide/reference/advanced-settings-for-services-dialog-box.md)，您可以使用该对话框覆盖默认行为。 例如，可以使用此对话框指定一个数据库进行脱机存储，而不是使用本地文件系统。 有关详细信息，请参阅[“高级服务设置”对话框](../../ide/reference/advanced-settings-for-services-dialog-box.md)。

## <a name="see-also"></a>请参阅
 [客户端应用程序服务](https://msdn.microsoft.com/library/1487d8df-089e-4f21-abfb-a791a652b58e) ["服务的高级设置" 对话框](../../ide/reference/advanced-settings-for-services-dialog-box.md)[如何：配置客户端应用程序服务](https://msdn.microsoft.com/library/34a8688a-a32c-40d3-94be-c8e610c6a4e8) ["编译" 页、项目设计器（Visual Basic）](../../ide/reference/compile-page-project-designer-visual-basic.md) ["C#生成" 页、项目设计器（）](../../ide/reference/build-page-project-designer-csharp.md)[项目设计器简介](https://msdn.microsoft.com/898dd854-c98d-430c-ba1b-a913ce3c73d7)
