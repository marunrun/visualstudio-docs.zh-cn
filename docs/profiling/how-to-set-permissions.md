---
title: 如何：设置权限 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling, setting permissions
- security [Visual Studio ALM], setting permissions
- permissions [Visual Studio ALM], profiling
- profiling tools, setting profiling permissions
- performance tools, setting profiling permissions
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: c1ab7705c7ab46b07b08b707ce447f37c581036a
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "74774584"
---
# <a name="how-to-set-permissions"></a>如何：设置权限

本文介绍计算机管理员如何向在该计算机上没有管理员权限的用户或组授予进行分析所需的安全权限。

一项基本的安全原则指出，应用程序运行时不应拥有超过其所需的权限。 此原则也适用于用户。 如果当用户作为用户组的成员（而不是管理员组的成员）登录时就具有足够的效力，则不应授予他们管理员权限。 第一个过程“创建拥有‘用户’权限的用户帐户”描述如何为用户组的成员创建用户帐户。

用户组的成员将需要访问磁盘上与团队的其他成员共享的文件夹和文件。 第二个过程“授予对共享项目文件的访问权限”描述如何授予该访问权限。

如果管理员为用户组的成员授予对分析工具的软件驱动程序的访问权限，则他们就可以运行分析工具。 最后一个过程“授予对分析驱动程序的访问权限”描述如何授予对该驱动程序的访问权限。

> [!NOTE]
> 需要管理员权限才能执行这些过程中的步骤。

## <a name="to-create-a-user-account-that-has-user-permissions"></a>创建拥有用户权限的用户帐户

1. 右键单击“我的电脑”，然后单击“管理”   。

     随即打开“计算机管理”窗口  。

2. 展开“本地用户和组”  。

3. 右键单击“用户”文件夹，然后单击“新建用户”   。

     随即出现“新建用户”对话框。 

4. 将所创建的用户帐户的信息填写在此对话框的字段中。 指定一个密码。 还可以选中要求用户下次登录时更改密码的复选框。

5. 单击“创建”，然后单击“关闭”   。

     新用户将出现在用户组（一组没有管理员权限的用户）中。

## <a name="to-grant-access-to-shared-project-files"></a>授予对共享项目文件的访问权限

1. 在 Windows 资源管理器（或文件资源管理器）中，找到此用户使用并由项目团队共享的项目文件的文件夹树根目录。

     此文件夹的路径可能如下所示：

    ```cmd
    D:\ourProject
    ```

2. 右键单击该文件夹，  然后单击“属性”。

     随即显示“**文件夹名称> 属性”\<** 对话框。

3. 单击 **“安全”** 选项卡。

4. 单击“组或用户名”  框中的用户帐户的名称。

5. 在“**用户名> 的权限”\<** 框中，选中“完全控制”复选框  。

6. 单击 **“确定”** 。

     这将授予用户对从第 5 步所选文件夹开始的共享文件夹树的权限。

## <a name="to-grant-access-to-the-profiling-driver"></a>授予对分析驱动程序的访问权限

1. 作为管理员打开命令提示。

2. 将目录切换到：

    ```cmd
    <drive>:\Program Files\Microsoft Visual Studio 14\Team Tools\Performance Tools
    ```

3. 运行以下命令：

    ```cmd
    vsperfcmd /admin:driver,start /admin:service,start
    ```

     此命令将安装并启动分析工具的驱动程序。

     此命令启动分析驱动程序和服务，以便非管理用户可以使用其用户进程空间中可用的分析功能。 只有管理员才能运行此命令，非管理用户无法运行。

     请注意，除非还执行本过程中的最后一步，否则此步骤的效果在计算机重新启动后撤消。

4. 运行此命令以允许对计算机没有管理员访问权限的用户或组访问分析驱动程序功能：

    ```cmd
    vsperfcmd /admin:security,allow,<right[,right],<user name|group name>
    ```

     此命令为 \<用户名> 或 \<组名称> 帐户授予对分析工具的访问权限。 \<权限> 选项用于确定用户可访问的分析功能。 \<权限> 选项可以是下面的一个或多个值：

    - FullAccess — 允许访问所有分析方法，包括从服务、采样和跨会话分析收集性能数据。

    - SampleProfiling — 允许访问采样分析方法

    - CrossSession — 允许访问分析服务所需的跨会话分析。

5. （可选）若要在计算机重新启动以后保留以上所有步骤的效果，请运行以下命令：

    ```cmd
    vsperfcmd /admin:driver,autostart,on
    ```

   现在，指定的用户登录后，能在没有管理员权限的情况下使用分析工具。

## <a name="see-also"></a>另请参阅

[配置性能会话](../profiling/configuring-performance-sessions.md)
[VSPerfCmd](../profiling/vsperfcmd.md)
[分析和 Windows Vista 安全性](../profiling/profiling-and-windows-vista-security.md)
