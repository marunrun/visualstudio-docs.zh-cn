---
title: 演练：手动部署 ClickOnce 应用程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Mage.exe, manual ClickOnce deployments
- MageUI.exe, manual ClickOnce deployments
- deploying applications [ClickOnce], manual ClickOnce deployments
- ClickOnce deployment, manually
- ClickOnce deployment, SDK tools
- manual ClickOnce deployments
- manifests [ClickOnce]
ms.assetid: ccee6551-a1b9-4ca2-8845-9c1cf4ac2560
caps.latest.revision: 51
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: cba55c9f4a8f7436b97099b6b548b916ea6e5ecb
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75844944"
---
# <a name="walkthrough-manually-deploying-a-clickonce-application"></a>演练：手动部署 ClickOnce 应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果无法使用 Visual Studio 来部署 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 的应用程序，或者需要使用高级部署功能（如受信任的应用程序部署），则应使用 Mage.exe 命令行工具创建 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 清单。 本演练介绍如何使用清单生成和编辑工具的命令行版本（Mage.exe）或图形版本（Mageui.exe）来创建 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署。  
  
## <a name="prerequisites"></a>先决条件  
 在生成部署之前，此演练具有一些需要选择的先决条件和选项。  
  
- 安装 Mage.exe 和 Mageui.exe。  
  
     Mage.exe 和 Mageui.exe 是 [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]的一部分。 您必须安装 [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] 或 Visual Studio 随附 [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] 的版本。 有关详细信息，请参阅 MSDN 上的[Windows SDK](https://msdn.microsoft.com/windowsserver/bb980924.aspx) 。  
  
- 提供要部署的应用程序。  
  
     本演练假定您已准备好部署 Windows 应用程序。 此应用程序将被称为 AppToDeploy。  
  
- 确定将如何分发部署。  
  
     分发选项包括： Web、文件共享或 CD。 有关详细信息，请参阅 [ClickOnce Security and Deployment](../deployment/clickonce-security-and-deployment.md)。  
  
- 确定应用程序是否需要提升的信任级别。  
  
     如果你的应用程序需要完全信任（例如，对用户系统的完全访问权限），则可以使用 Mage.exe 的 `-TrustLevel` 选项来设置此项。 如果要为应用程序定义自定义权限集，可以从另一个清单复制 Internet 或 intranet 权限部分，对其进行修改以满足你的需求，并使用文本编辑器或 Mageui.exe 将其添加到应用程序清单。 有关更多信息，请参见 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。  
  
- 获取 Authenticode 证书。  
  
     应使用 Authenticode 证书对部署进行签名。 可以通过使用 Visual Studio、Mageui.exe 或 MakeCert 和 Pvk2Pfx 工具生成测试证书，也可以从证书颁发机构（CA）获取证书。 如果选择使用受信任的应用程序部署，还必须在所有客户端计算机上执行一次证书安装。 有关更多信息，请参见 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。  
  
    > [!NOTE]
    > 你还可以使用可从证书颁发机构获取的 CNG 证书对你的部署进行签名。  
  
- 请确保应用程序没有带有 UAC 信息的清单。  
  
     你需要确定你的应用程序是否包含具有用户帐户控制（UAC）信息的清单，如 `<dependentAssembly>` 元素。 若要检查应用程序清单，可以使用 Windows Sysinternals [Sigcheck](https://technet.microsoft.com/sysinternals/bb897441.aspx)实用程序。  
  
     如果你的应用程序包含具有 UAC 详细信息的清单，则必须在不使用 UAC 信息的情况下重新生成它。 对于 Visual C# Studio 中的项目，打开 "项目属性"，然后选择 "应用程序" 选项卡。在 "**清单**" 下拉列表中，选择 "**创建不带清单的应用程序**"。 对于 Visual Studio 中的 Visual Basic 项目，请打开项目属性，选择 "应用程序" 选项卡，然后单击 "**查看 UAC 设置**"。 在打开的清单文件中，删除单个 `<asmv1:assembly>` 元素中的所有元素。  
  
- 确定应用程序是否需要客户端计算机上的必备组件。  
  
     从 Visual Studio 部署的 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 应用程序可以在部署中包含先决条件安装引导程序（setup.exe）。 本演练将创建 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署所需的两个清单。 可以使用[GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)创建必备组件引导程序。  
  
### <a name="to-deploy-an-application-with-the-mageexe-command-line-tool"></a>使用 Mage.exe 命令行工具部署应用程序  
  
1. 创建一个将在其中存储 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署文件的目录。  
  
2. 在刚创建的部署目录中，创建版本子目录。 如果这是你首次部署应用程序，请将版本命名为 "子目录**1.0.0.0**"。  
  
    > [!NOTE]
    > 部署版本可能与应用程序的版本不同。  
  
3. 将所有应用程序文件复制到版本子目录，其中包括可执行文件、程序集、资源和数据文件。 如有必要，你可以创建包含其他文件的其他子目录。  
  
4. 打开 [!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)] 或 Visual Studio 命令提示符，然后更改为版本子目录。  
  
5. 使用 Mage.exe 调用创建应用程序清单。 以下语句将为编译为在 Intel x86 处理器上运行的代码创建应用程序清单。  
  
    ```  
    mage -New Application -Processor x86 -ToFile AppToDeploy.exe.manifest -name "My App" -Version 1.0.0.0 -FromDirectory .   
    ```  
  
    > [!NOTE]
    > 请确保在 `-FromDirectory` 选项后包含点（.），该选项指示当前目录。 如果不包含句点，则必须指定应用程序文件的路径。  
  
6. 用 Authenticode 证书对应用程序清单进行签名。 将*mycert.cer*替换为证书文件的路径。 将*密码替换为证书文件的密码*。  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile mycert.pfx -Password passwd  
    ```  
  
     若要使用 CNG 证书对应用程序清单进行签名，请使用以下。 将*cngCert*替换为证书文件的路径。  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile cngCert.pfx  
    ```  
  
7. 更改为部署目录的根目录。  
  
8. 通过调用 Mage.exe 生成部署清单。 默认情况下，Mage.exe 会将 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署标记为已安装的应用程序，以便它可以联机和脱机运行。 若要使应用程序仅在用户处于联机状态时可用，请使用值为 `false`的 `-Install` 选项。 如果使用默认值，并且用户将从网站或文件共享安装应用程序，请确保 `-ProviderUrl` 选项的值指向 Web 服务器或共享上的应用程序清单的位置。  
  
    ```  
    mage -New Deployment -Processor x86 -Install true -Publisher "My Co." -ProviderUrl "\\myServer\myShare\AppToDeploy.application" -AppManifest 1.0.0.0\AppToDeploy.exe.manifest -ToFile AppToDeploy.application  
    ```  
  
9. 用 Authenticode 或 CNG 证书对部署清单进行签名。  
  
    ```  
    mage -Sign AppToDeploy.application -CertFile mycert.pfx -Password passwd  
    ```  
  
     或  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile cngCert.pfx  
    ```  
  
10. 将部署目录中的所有文件复制到部署目标或媒体。 这可能是网站或 FTP 站点、文件共享或 cd-rom 上的文件夹。  
  
11. 为用户提供安装应用程序所需的 URL、UNC 或物理介质。 如果提供 URL 或 UNC，则必须为用户提供部署清单的完整路径。 例如，如果 AppToDeploy 部署到 http://webserver01/ AppToDeploy 目录中，在完整的 URL 路径应 http://webserver01/AppToDeploy/AppToDeploy.application 。  
  
### <a name="to-deploy-an-application-with-the-mageuiexe-graphical-tool"></a>使用 Mageui.exe 图形工具部署应用程序  
  
1. 创建一个将在其中存储 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 部署文件的目录。  
  
2. 在刚创建的部署目录中，创建版本子目录。 如果这是你首次部署应用程序，请将版本命名为 "子目录**1.0.0.0**"。  
  
    > [!NOTE]
    > 部署的版本可能与应用程序的版本不同。  
  
3. 将所有应用程序文件复制到版本子目录，其中包括可执行文件、程序集、资源和数据文件。 如有必要，你可以创建包含其他文件的其他子目录。  
  
4. 启动 Mageui.exe 图形工具。  
  
    ```  
    MageUI.exe  
    ```  
  
5. 通过从菜单中选择 "**文件**"、"**新建**"、"**应用程序清单**" 来创建新的应用程序清单。  
  
6. 在 "默认**名称**" 选项卡上，键入此部署的名称和版本号。 还要指定为其生成应用程序的**处理器**，如 x86。  
  
7. 选择 "**文件**" 选项卡，然后单击 "**应用程序目录**" 文本框旁边的省略号（ **...** ）按钮。 此时将显示 "浏览文件夹" 对话框。  
  
8. 选择包含应用程序文件的版本子目录，然后单击 **"确定"** 。  
  
9. 如果要从 Internet Information Services （IIS）进行部署，请选中 "**填充时将 .deploy 扩展添加到任何不具有它的文件**" 复选框。  
  
10. 单击 "**填充**" 按钮，将所有应用程序文件添加到文件列表。 如果你的应用程序包含多个可执行文件，则通过从 "**文件类型**" 下拉列表中选择 "**入口点**"，将此部署的主要可执行文件标记为启动应用程序。 （如果你的应用程序只包含一个可执行文件，则 Mageui.exe 会将其标记为你。）  
  
11. 选择 "**所需权限**" 选项卡，然后选择你需要应用程序断言的信任级别。 默认值为**FullTrust**，适用于大多数应用程序。  
  
12. 从菜单中选择 "**文件**"、"**另存为**"。 此时会显示 "签名选项" 对话框，提示您对应用程序清单进行签名。  
  
13. 如果在文件系统上将证书存储为文件，请使用 "**使用证书签名**" 选项，并使用省略号（ **...** ）按钮从文件系统中选择证书。 然后键入证书密码。  
  
     或  
  
     如果证书保存在可从计算机访问的证书存储中，请选择 "**使用存储的证书签名**" 选项，然后从提供的列表中选择证书。  
  
14. 单击 **"确定"** 以对你的应用程序清单进行签名。 此时会显示“另存为”对话框。  
  
15. 在 "另存为" 对话框中，指定版本目录，然后单击 "**保存**"。  
  
16. 从菜单中选择 "**文件**"、"**新建**"、"**部署清单**" 以创建部署清单。  
  
17. 在 "**名称**" 选项卡上，为此部署指定名称和版本号（在本示例中为**1.0.0.0** ）。 还要指定为其生成应用程序的**处理器**，如 x86。  
  
18. 选择 "**描述**" 选项卡，然后指定 "**发布者**" 和 "**产品**" 的值。 （**Product**是在客户端计算机上安装应用程序以供脱机使用时在 Windows "开始" 菜单上为应用程序指定的名称。）  
  
19. 选择 "**部署选项**" 选项卡，并在 "**启动位置**" 文本框中指定应用程序清单在 Web 服务器或共享上的位置。 例如，\\\myServer\myShare\AppToDeploy.application。  
  
20. 如果在上一步中添加了 .deploy 扩展，请在此处选择 "**使用文件扩展名**"。  
  
21. 选择 "**更新选项**" 选项卡，并指定要更新此应用程序的频率。 如果你的应用程序使用 <xref:System.Deployment.Application.UpdateCheckInfo> 来检查是否有更新，请清除 "**此应用程序应检查更新**" 复选框。  
  
22. 选择 "**应用程序引用**" 选项卡，然后单击 "**选择清单**" 按钮。 此时将显示 "打开" 对话框。  
  
23. 选择前面创建的应用程序清单，并单击 "**打开**"。  
  
24. 从菜单中选择 "**文件**"、"**另存为**"。 此时会显示 "签名选项" 对话框，提示您对部署清单进行签名。  
  
25. 如果在文件系统上将证书存储为文件，请使用 "**使用证书签名**" 选项，并使用省略号（ **...** ）按钮从文件系统中选择证书。 然后键入证书密码。  
  
     或  
  
     如果证书保存在可从计算机访问的证书存储中，请选择 "**使用存储的证书签名**" 选项，然后从提供的列表中选择证书。  
  
26. 单击 **"确定"** 以对你的部署清单进行签名。 此时会显示“另存为”对话框。  
  
27. 在 "**另存为**" 对话框中，将一个目录移到部署的根，然后单击 "**保存**"。  
  
28. 将部署目录中的所有文件复制到部署目标或媒体。 这可能是网站或 FTP 站点、文件共享或 cd-rom 上的文件夹。  
  
29. 为用户提供安装应用程序所需的 URL、UNC 或物理介质。 如果提供 URL 或 UNC，则必须为用户提供部署清单的完整路径。 例如，如果 AppToDeploy 部署到 http://webserver01/ AppToDeploy 目录中，在完整的 URL 路径应 http://webserver01/AppToDeploy/AppToDeploy.application 。  
  
## <a name="next-steps"></a>后续步骤  
 当需要部署应用程序的新版本时，请创建一个名为的新目录（例如1.0.0.1），并将新的应用程序文件复制到新目录中。 接下来，需要按照前面的步骤创建新的应用程序清单并对其进行签名，并对部署清单进行更新和签名。 请注意，在 Mage.exe `-New` 和 `–Update` 调用中指定相同的更高版本，因为 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 仅更新较高版本，最左端的整数最重要。 如果使用了 Mageui.exe，则可以通过打开部署清单、选择 "**应用程序引用**" 选项卡、单击 "**选择清单**" 按钮，然后选择更新的应用程序清单来更新部署清单。  
  
## <a name="see-also"></a>请参阅  
 [Mage.exe（清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe（图形化客户端中的清单生成和编辑工具）](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)   
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [ClickOnce 应用程序清单](../deployment/clickonce-application-manifest.md)
