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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 60f06aa64cf6a6b96f0c4d610fba1d20b794c55f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667201"
---
# <a name="troubleshooting-service-references"></a>服务引用疑难解答
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
本主题列出了在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中处理 [!INCLUDE[vsindigo](../includes/vsindigo-md.md)] 或 [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] 引用时可能出现的常见问题。

## <a name="error-returning-data-from-a-service"></a>从服务返回数据时出错
 从服务返回 `DataSet` 或 `DataTable` 时，可能会收到 "超出传入消息的最大大小配额" 异常。 默认情况下，某些绑定的 `MaxReceivedMessageSize` 属性设置为相对较小的值，以限制遭受拒绝服务攻击。 可以增加此值以防止发生此异常。

 修复此错误的方法：

1. 在**解决方案资源管理器**中，双击 app.config 文件以将其打开。

2. 找到 `MaxReceivedMessageSize` 属性，并将其更改为更大的值。

## <a name="cannot-find-a-service-in-my-solution"></a>在我的解决方案中找不到服务
 单击 "**添加服务引用**" 对话框中的 "**发现**" 按钮时，解决方案中的一个或多个 WCF 服务库项目不会显示在 "服务" 列表中。 如果服务库已添加到解决方案中但尚未编译，则会发生这种情况。

 修复此错误的方法：

- 在**解决方案资源管理器**中，右键单击 WCF 服务库项目，然后单击 "**生成**"。

## <a name="error-accessing-a-service-over-a-remote-desktop"></a>通过远程桌面访问服务时出错
 当用户通过远程桌面连接访问 Web 承载的 WCF 服务，并且该用户不具有管理权限时，将使用 NTLM 身份验证。 如果用户不具有管理权限，则用户可能会收到以下错误消息： "HTTP 请求未通过客户端身份验证方案" 匿名 "授权。 从服务器收到的身份验证标头为 "NTLM"。

 修复此错误的方法：

1. 在网站项目中，打开 "**属性**" 页。

2. 在 "**启动选项**" 选项卡上，清除 " **NTLM 身份验证**" 复选框。

    > [!NOTE]
    > 只应为仅包含 WCF 服务的网站关闭 NTLM 身份验证。 WCF 服务的安全性通过 web.config 文件中的配置进行管理。 这使得 NTLM 身份验证不必要。

## <a name="access-level-for-generated-classes-setting-has-no-effect"></a>"生成的类的访问级别" 设置不起作用
 如果将 "**配置服务引用**" 对话框中的 "**生成的类的访问级别**" 选项设置为 "**内部**" 或 "**朋友**"，则可能并非始终有效。 即使此选项似乎在对话框中设置，生成的支持类也将使用 `Public` 的访问级别生成。

 这是特定类型的已知限制，如使用 <xref:System.Xml.Serialization.XmlSerializer> 序列化的类型。

## <a name="error-debugging-service-code"></a>调试服务代码时出错
 当你从客户端代码单步执行 WCF 服务的代码时，可能会收到与缺少符号相关的错误。 如果已在解决方案中移动或删除了作为解决方案一部分的服务，则可能会发生这种情况。

 当你首次添加对作为当前解决方案一部分的 WCF 服务的引用时，将在服务项目和服务客户端项目之间添加显式生成依赖项。 这可以确保客户端始终访问最新的服务二进制文件，这对于调试方案（如从客户端代码到服务代码的单步执行）尤其重要。

 如果从解决方案中删除服务项目，则此显式生成依赖项将失效。 Visual Studio 不能再保证在必要时重新生成服务项目。

 若要修复此错误，你必须手动重新生成服务项目：

1. 在 **“工具”** 菜单上，单击 **“选项”** 。

2. 在 "**选项**" 对话框中，展开 "**项目和解决方案**"，然后选择 "**常规**"。

3. 确保选中 "**显示高级生成配置**" 复选框，然后单击 **"确定"** 。

4. 加载 "WCF 服务" 项目。 有关详细信息，请参阅[笔尖如何：创建多项目解决方案](https://msdn.microsoft.com/02ecd6dd-0114-46fe-b335-ba9c5e3020d6)。

5. 在 " **Configuration Manager** " 对话框中，将 "**活动解决方案配置**" 设置为 "**调试**"。 有关详细信息，请参阅[如何：创建和编辑配置](../ide/how-to-create-and-edit-configurations.md)。

6. 在**解决方案资源管理器**中，选择 "WCF 服务" 项目。

7. 在 "**生成**" 菜单上，单击 "**重新生成**" 以重新生成 WCF 服务项目。

## <a name="wcf-data-services-do-not-display-in-the-browser"></a>WCF 数据服务不会在浏览器中显示
 如果尝试在 [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] 中查看数据的 XML 表示形式，Internet Explorer 可能会将数据作为 RSS 源误认为。 必须确保禁用显示 RSS 源的选项。

 若要修复此错误，请禁用 RSS 源：

1. 在 Internet Explorer 中，单击“工具”菜单中的“Internet 选项”。

2. 在 "**内容**" 选项卡上的 "**源**" 部分中，单击 "**设置**"。

3. 在 "**源设置**" 对话框中，清除 "**打开源阅读视图**" 复选框，然后单击 **"确定"** 。

4. 单击 **"确定"** 以关闭 " **Internet 选项**" 对话框。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)