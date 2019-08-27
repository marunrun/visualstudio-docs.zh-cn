---
title: 运行工作进程的用户帐户下 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- user accounts, aspnet_wp.exe
- ASP.NET, debugging Web applications
- tools, aspnet_wp.exe
- ASP.NET, tools
- aspnet_wp.exe
ms.assetid: b58e97b1-e62a-4318-aea4-52276ea20735
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aebe1faf31d53fb44cf5efddbee154018e42a365
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62847760"
---
# <a name="how-to-run-the-worker-process-under-a-user-account"></a>如何：在用户帐户下运行工作进程
若要设置计算机以便在某个用户帐户下运行 [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] 辅助进程（aspnet_wp.exe 或 w3wp.exe），请执行下列步骤。

 > [!IMPORTANT]
 > 从 Windows Server 2008 R2 开始，我们建议使用[ApplicationPoolIdentity](/iis/manage/configuring-security/application-pool-identities)作为为每个应用程序池标识。

## <a name="procedure"></a>过程

#### <a name="to-run-aspnetwpexe-under-a-user-account"></a>以用户帐户运行 aspnet_wp.exe

1. 打开 machine.config 文件，此文件位于计算机上运行时安装路径下的 CONFIG 文件夹中。

2. 找到 &lt;processModel&gt; 节，将用户和密码属性更改为希望用于运行 aspnet_wp.exe 的用户帐户的名称和密码。

3. 保存 machine.config 文件。

4. 在 [!INCLUDE[winxpsvr](../debugger/includes/winxpsvr_md.md)]上，默认情况下已安装 IIS 6.0。 相应的辅助进程是 w3wp.exe。若要在 IIS 6.0 模式下运行并将 aspnet_wp.exe 用作辅助进程，必须执行下列步骤：

   1. 单击 **“开始”**，单击 **“管理工具”** ，然后选择 **“Internet 信息服务”**。

   2. 在 **“Internet 信息服务”** 对话框中，右击 **“网站”** 文件夹并选择 **“属性”**。

   3. 在 **“网站属性”** 对话框中选择 **“服务”**。

   4. 选择 **“以 IIS6.0 隔离模式运行 WWW 服务”**。

   5. 关闭 **“属性”** 对话框和 **“Internet 服务管理器”**。

5. 打开 Windows 命令提示窗口，通过运行下面的命令重置服务器：

   ```cmd
   iisreset
   ```

   — 或 —

   ```cmd
   net stop iisadmin /y
   net start w3svc
   ```

6. 找到 Temporary [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Files 文件夹，它应位于 CONFIG 文件夹所在的路径中。 右键单击 Temporary [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Files 文件夹，然后选择快捷菜单上的“属性”  。

7. 在 **“临时 ASP.NET 文件属性”** 对话框中单击 **“安全性”** 选项卡。

8. 单击 **“高级”**。

9. 在 **“临时 ASP.Net 文件的高级安全设置”** 对话框中单击 **“添加”**。

    将出现 **“选择用户、计算机或组”** 对话框。

10. 在 **“输入要选择的对象名称”** 框中键入用户名，然后单击 **“确定”**。 用户名称必须遵循以下格式：域名 \ 用户名。

11. 在 **“临时 ASP.Net 文件的权限项”** 对话框中，授予用户 **“完全控制”**，然后单击 **“确定”** 以关闭 **“临时 ASP.Net 文件项”** 对话框。

12. 将出现 **“安全性”** 对话框，询问是否确实要更改系统文件夹的权限。 单击 **“是”**。

13. 单击 **“确定”** 以关闭 **“临时 ASP.NET 文件属性”** 对话框。

## <a name="see-also"></a>请参阅
- [调试 ASP.NET 应用程序](../debugger/how-to-enable-debugging-for-aspnet-applications.md)
- [ASP.NET 调试：系统要求](../debugger/aspnet-debugging-system-requirements.md)
