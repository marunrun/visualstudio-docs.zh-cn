---
title: “项目设计器”->“签名”页
ms.date: 11/04/2016
ms.technology: vs-ide-deployment
ms.topic: reference
f1_keywords:
- vs.AddNewStrongNameKey
- ResolveKeySource.KeyFileForSignAssemblyNotImported
- vb.ProjectPropertiesSigning.ChangePasswordDialog
- ResolveKeySource.KeyFileForManifestNotImported
- vb.ProjectPropertiesSigning
- vb.ProjectPropertiesSigning.PasswordNeededDialog
- vb.ProjectPropertiesSigning.PfxPasswordDialog
helpviewer_keywords:
- Project Designer, Signing page
- Signing page in Project Designer
ms.assetid: dab3ba13-2f92-4827-92bd-1be3c35bc48b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0d4fa326d65606fd06d41fc5c697b80a526c1059
ms.sourcegitcommit: 85d66dc9fea3fa49018263064876b15aeb6f9584
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68461290"
---
# <a name="signing-page-project-designer"></a>“项目设计器”->“签名”页

使用“项目设计器”  的“签名”  页对应用程序和部署清单及程序集进行签名（强名称签名）。

请注意，尽管这两项任务都在“签名”  页上执行，但应用程序和部署清单的签名过程与程序集的签名过程不同。

此外，清单签名和程序集签名的密钥文件信息存储方式不同。 对于清单签名，密钥信息存储在计算机的加密存储数据库和当前用户的 Windows 证书存储中。 对于程序集签名，密钥信息仅存储在计算机的加密存储数据库中。

若要访问“签名”  页面，请在“解决方案资源管理器”  中选择项目节点，然后在“项目”  菜单上单击“属性”  。 当“项目设计器”  出现时，单击“签名”  选项卡。

## <a name="application-and-deployment-manifest-signing"></a>应用程序和部署清单签名

“为 ClickOnce 清单签名”  复选框

选中此复选框以使用公钥/私钥对对应用程序和部署清单进行签名。 有关如何执行此操作的详细信息，请参阅[如何：对应用程序和部署清单签名](../../ide/how-to-sign-application-and-deployment-manifests.md)。

“从存储区选择”  按钮

可以从当前用户的个人证书存储区中选择现有证书。 可以选择其中一个证书来对应用程序和部署清单进行签名。

单击“从存储区选择”  将打开“选择证书”  对话框，其中列出了个人证书存储区中当前有效（未到期）且具有私钥的证书。 所选证书的用途应包括代码签名。

如果单击“查看证书属性”  ，将显示“证书详细信息”  对话框。 此对话框中包括有关证书的详细信息以及其他选项。 可以单击“了解证书详情”  以查看其他帮助信息。

“从文件中选择”  按钮

可以从现有的密钥文件中选择证书。

单击“从文件中选择”  将打开“选择文件”  对话框，使你能够选择证书密钥 (.pfx) 文件。 该文件必须受密码保护，并且不能位于个人证书存储区中。

在“输入密码以打开文件”  对话框中，输入密码以打开证书密钥 (.pfx) 文件。 密码信息存储在你的个人密钥容器列表和个人证书存储区中。

“创建测试证书”  按钮

允许你创建用于测试的证书。 测试证书用于对 ClickOnce 应用程序和部署清单进行签名。

单击“创建测试证书”  将打开“创建测试证书”  对话框，你可以在其中键入测试证书的强名称密钥文件的密码。 该文件名为 projectname  _TemporaryKey.pfx。 如果单击“确定”  而不输入密码，则 .pfx 文件不进行密码加密。

“时间戳服务器 URL”  框

指定为签名添加时间戳的服务器的地址。 当提供证书时，此外部站点将验证应用程序的签名时间。

## <a name="assembly-signing"></a>程序集签名

“为程序集签名”  复选框

选择此复选框可为程序集签名并创建强名称密钥文件。 有关使用“项目设计器”为程序集签名的详细信息，请参阅[如何  ：为程序集签名 (Visual Studio)](../managing-assembly-and-manifest-signing.md#how-to-sign-an-assembly-in-visual-studio)。

此选项使用 Windows 软件开发工具包 (SDK) 提供的 Al.exe 工具对程序集进行签名。 有关 Al.exe 的详细信息，请参阅[如何：使用强名称为程序集签名](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)。

“选择强名称密钥文件”  列表

使你可以指定一个新的或现有强名称密钥文件，用来对程序集签名。 选择“\<浏览...>”  以选择现有的密钥文件。

选择“\<新建...>”  以创建用来对程序集签名的新密钥文件。 将出现“创建强名称密钥”  对话框，你可以使用该对话框指定密钥文件名，并使用密码保护密钥文件。 密码长度必须至少为 6 个字符。 如果指定密码，则会创建个人信息交换 (.pfx) 文件；如果不指定密码，则创建强名称密钥 (.snk) 文件。

“更改密码”  按钮

更改用于对程序集签名的个人信息交换 (.pfx) 密钥文件的密码。

单击“更改密码”  将打开“更改密钥密码”  对话框。 在此对话框中，“旧密码”  为密钥文件的当前密码。 “新密码”  长度必须至少为 6 个字符。 密码信息存储在当前用户的 Windows 证书存储区中。

“仅延迟签名”  复选框

选中此复选框以启用延迟签名。

请注意，延迟签名的项目将不会运行，也不能调试。 但是，可以使用 [Sn.exe（强名称工具）](/dotnet/framework/tools/sn-exe-strong-name-tool)及 `-Vr` 选项，在开发过程中跳过验证。

> [!NOTE]
> 对程序集签名时，可能并不总是有权访问私钥。 例如，一个组织可能具有开发人员不是每天都能访问的严密保护密钥对。 公钥可能可用，但私钥的访问权限仅限于少数几个人。 在这种情况下，你可以使用延迟  或部分签名  来提供公钥，将私钥的添加延迟到转交该程序集后。

## <a name="see-also"></a>请参阅

- [项目属性引用](../../ide/reference/project-properties-reference.md)
- [管理程序集签名和清单签名](../../ide/managing-assembly-and-manifest-signing.md)
- [如何：对应用程序和部署清单签名](../../ide/how-to-sign-application-and-deployment-manifests.md)
- [如何：为程序集签名 (Visual Studio)](../managing-assembly-and-manifest-signing.md#how-to-sign-an-assembly-in-visual-studio)
- [如何：使用强名称为程序集签名](/dotnet/framework/app-domains/how-to-sign-an-assembly-with-a-strong-name)
- [具有强名称的程序集](/dotnet/framework/app-domains/strong-named-assemblies)