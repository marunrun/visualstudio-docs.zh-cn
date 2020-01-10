---
title: 错误：调试失败，因为没有启用集成 Windows 身份验证 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.webdbg_ntlm_authn_not_enabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- debugger, Web application errors
ms.assetid: 6027cd94-74cf-470f-b7ce-6f6b68bc56ba
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 89afba591899b626863b0157f6d9d955d46e46cf
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851915"
---
# <a name="error-debugging-failed-because-integrated-windows-authentication-is-not-enabled"></a>错误：调试失败，因为没有启用集成 Windows 身份验证
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

由于身份验证错误，无法对请求调试的用户进行身份验证。 当你尝试单步执行 Web 应用程序或 XML Web services 时，就可能出现此问题。 导致此错误的一种原因是没有启用集成 Windows 身份验证。 若要启用该身份验证，请按照“启用集成 Windows 身份验证”中的步骤操作。  
  
 如果已启用集成 Windows 身份验证，但仍然出现此错误，则导致此错误的原因可能是启用了“Windows 域服务器的摘要式身份验证”。 在这种情况下，应与您的网络管理员联系。  
  
### <a name="to-enable-integrated-windows-authentication"></a>启用集成 Windows 身份验证  
  
1. 使用管理员帐户登录 Web 服务器。  
  
2. 单击“开始”，然后单击“控制面板”。  
  
3. 在“控制面板”中双击“管理工具”。  
  
4. 双击“Internet Information Services”。  
  
5. 单击 Web 服务器节点。  
  
     服务器名称下方将打开一个“网站”文件夹。  
  
6. 你可以为所有网站或个别网站配置身份验证。 若要为所有网站配置身份验证，请右键单击“网站”文件夹，然后单击“属性”。 若要为单个网站配置身份验证，请打开“网站”文件夹，右键单击单个网站，然后单击“属性”。  
  
     屏幕上会显示“属性”对话框。  
  
7. 单击“目录安全性”选项卡。  
  
8. 在“匿名访问和身份验证控制”节中，单击“编辑”。  
  
     随即会显示“身份验证方法”对话框。  
  
9. 在“用户访问需经过身份验证”下，选择“集成 Windows 身份验证”。  
  
10. 单击“确定”以关闭“身份验证方法”对话框。  
  
11. 单击“确定”以关闭“属性”对话框。  
  
12. 关闭“Internet Information Services”窗口。  
  
### <a name="to-enable-integrated-windows-authentication-in-windows-vistaiis-7"></a>在 Windows Vista/IIS 7 中启用集成 Windows 身份验证  
  
1. 使用管理员帐户登录 Web 服务器。  
  
2. 按照下列步骤启用 Windows 身份验证和 II6 管理兼容性（如果尚未启用）：  
  
    1. 单击 "**开始**"，再单击 **"控制面板**"，然后单击 "**程序**"。  
  
    2. 在“程序和功能”下，单击“打开或关闭 Windows 功能”。  
  
         将出现“用户帐户控制”对话框，并提示您是否允许继续。  
  
    3. 单击“继续”。  
  
         将出现“Windows 功能”对话框。  
  
    4. 在功能列表中，展开“Internet Information Services”节点。  
  
    5. 在“Internet Information Services”下，展开“万维网服务”节点。  
  
    6. 在“万维网服务”下，单击“安全”。  
  
    7. 单击“Windows 身份验证”。  
  
    8. 在“Internet Information Services”下，展开“Web 管理工具”节点。  
  
    9. 在“Web 管理工具”下，展开“IIS 6 管理兼容性”节点，然后选中“IIS 6 元数据库和 IIS 6 配置兼容性”复选框。  
  
    10. 在“Web 管理工具”下，选择“IIS 管理控制台”，然后单击“确定”。  
  
    11. 重新启动计算机，以使这些更改生效。  
  
3. 单击“开始”，然后单击“控制面板”。  
  
4. 单击“经典视图”，然后双击“管理工具”。  
  
5. 在“名称”列中，双击“Internet Information Services (IIS) 管理器”。  
  
6. 在“连接”列中，展开服务器的节点。  
  
     服务器名称下方将打开一个“网站”文件夹。  
  
7. 展开“网站”节点，然后单击要为其启用集成 Windows 身份验证的网站。  
  
8. 中心窗格标题将更改为所选网站的名称。 在此窗格的“IIS”标题下，双击“身份验证”。  
  
     该窗格的标题将更改为“身份验证”。  
  
9. 在“身份验证”窗格的“名称”列中，右键单击“Windows 身份验证”，然后单击“启用”。  
  
10. 关闭“Internet Information Services (IIS) 管理器”窗口。  
  
## <a name="see-also"></a>请参阅  
 [调试 Web 应用程序：错误和疑难解答](../debugger/debugging-web-applications-errors-and-troubleshooting.md)   
 [Microsoft 摘要式身份验证](https://msdn2.microsoft.com/library/Aa378744.aspx)   
 [在 Windows Vista 上运行带有 IIS 7.0 和 Visual Studio 的 Web 应用程序](https://msdn.microsoft.com/library/262a82ac-dd0e-4096-86c6-fb463e88be66)
