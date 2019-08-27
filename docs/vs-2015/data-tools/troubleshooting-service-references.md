---
title: 服务引用疑难解答 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: reference
f1_keywords:
- msvse_wcf.Err.ReferenceGroup_NamespaceConflictsOther
- msvse_wcf.Err.AddSvcRefDlg_NothingSelectedOnGo
- msvse_wcf.Err.ErrorOnOK
- msvse_wcf.cfg.ConfigurationErrorsException
helpviewer_keywords:
- service references [Visual Studio], troubleshooting
- WCF services, troubleshooting
ms.assetid: 3b531120-1325-4734-90c6-6e6113bd12ac
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f1c5886d4ac3efcb906a27f73af6a79fad95a5af
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65700234"
---
# <a name="troubleshooting-service-references"></a>服务引用疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
本主题列出了你正在使用时，可能发生的常见问题[!INCLUDE[vsindigo](../includes/vsindigo-md.md)]或[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]中的引用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。

## <a name="error-returning-data-from-a-service"></a>从服务返回数据时出错
 当您返回`DataSet`或`DataTable`从一种服务，可能会收到"传入消息的最大大小配额已超出"异常。 默认情况下，`MaxReceivedMessageSize`某些绑定属性设置为相对较小的值，以降低遭受拒绝服务攻击。 可以增大此值以避免此异常。

 修复此错误的方法：

1. 在中**解决方案资源管理器**，双击 app.config 文件以将其打开。

2. 找到`MaxReceivedMessageSize`属性并将其更改为更大的值。

## <a name="cannot-find-a-service-in-my-solution"></a>我的解决方案中找不到服务
 当您单击**Discover**按钮**添加服务引用**对话框中，解决方案中的一个或多个 WCF 服务库项目并不出现在服务列表。 如果服务库已添加到解决方案，但尚未编译，这可能发生。

 修复此错误的方法：

- 在中**解决方案资源管理器**，右键单击 WCF 服务库项目，然后单击**生成**。

## <a name="error-accessing-a-service-over-a-remote-desktop"></a>通过远程桌面访问服务时出错
 当用户访问通过远程桌面连接和用户的 Web 承载的 WCF 服务不具有管理权限，使用 NTLM 身份验证。 如果用户没有管理权限，用户可能会收到以下错误消息："HTTP 请求是未经授权的客户端身份验证方案 Anonymous。 从服务器收到的身份验证标头是 NTLM"。

 修复此错误的方法：

1. 在网站项目中，打开**属性**页。

2. 上**启动选项**选项卡上，清除**NTLM 身份验证**复选框。

    > [!NOTE]
    > 您应关闭 NTLM 身份验证仅对以独占方式包含 WCF 服务的网站。 通过 web.config 文件中的配置管理的 WCF 服务的安全性。 这使得 NTLM 身份验证不必要。

## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>生成的类的访问级别设置不起作用
 设置**访问生成的类的级别**选项**配置服务引用**对话框，以便**内部**或者**友元**可能并非始终有效。 尽管起来在对话框中设置此选项，将以一种访问级别的生成产生的支持类`Public`。

 这是某些类型，例如那些使用序列化的已知的限制<xref:System.Xml.Serialization.XmlSerializer>。

## <a name="error-debugging-service-code"></a>错误调试服务代码
 当您单步执行 WCF 服务的代码从客户端代码时，可能会收到与缺少符号相关的错误。 这可能是你的解决方案的一部分的服务已移动或从解决方案中移除时。

 首次添加到当前解决方案的一部分的 WCF 服务的引用，该服务项目和服务客户端项目之间添加显式生成依赖项。 这可以保证，客户端将始终访问最新的服务二进制文件，这一点尤为重要的调试方案，例如从客户端代码单步服务代码。

 如果从解决方案中删除服务项目，此显式生成依赖项会失效。 Visual Studio 无法再保证，重新生成服务项目在必要时。

 若要修复此错误，您必须手动重新生成服务项目：

1. 在 **“工具”** 菜单上，单击 **“选项”**。

2. 在中**选项**对话框框中，展开**项目和解决方案**，然后选择**常规**。

3. 请确保**显示高级生成配置**复选框已选中，然后依次**确定**。

4. 加载该 WCF 服务项目。 有关详细信息，请参阅[NIB 如何：创建多项目解决方案](https://msdn.microsoft.com/02ecd6dd-0114-46fe-b335-ba9c5e3020d6)。

5. 在中**Configuration Manager**对话框中，将**活动解决方案配置**到**调试**。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。

6. 在中**解决方案资源管理器**，选择的 WCF 服务项目。

7. 上**构建**菜单上，单击**重新生成**重新生成 WCF 服务项目。

## <a name="wcf-data-services-do-not-display-in-the-browser"></a>WCF 数据服务不会显示在浏览器中
 在尝试查看的 XML 表示形式中的数据[!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)]，Internet Explorer 可能曲解为 RSS 源的数据。 必须确保禁用显示 RSS 源的选项。

 若要解决此错误，请禁用 RSS 源：

1. 在 Internet Explorer 中，单击“工具”菜单中的“Internet 选项”。

2. 上**内容**选项卡上，在**馈送**部分中，单击**设置**。

3. 在中**源设置**对话框中，清除**打开源阅读视图**复选框，然后依次**确定**。

4. 单击**确定**以关闭**Internet 选项**对话框。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)