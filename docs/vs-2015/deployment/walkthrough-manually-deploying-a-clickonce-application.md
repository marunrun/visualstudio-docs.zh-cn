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
ms.openlocfilehash: 239fdcea9b8b9613bcdaa2419aba211c2a2a98f4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686328"
---
# <a name="walkthrough-manually-deploying-a-clickonce-application"></a>演练：手动部署 ClickOnce 应用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果您不能使用 Visual Studio 部署应用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]应用程序，或者需要使用高级的部署功能，如受信任的应用程序部署，您应使用 Mage.exe 命令行工具来创建你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]清单。 本演练介绍如何创建[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]通过使用命令行版本 (Mage.exe) 或清单生成和编辑工具的图形版本 (MageUI.exe) 部署。  
  
## <a name="prerequisites"></a>系统必备  
 本演练中存在一些必备组件，则需要生成部署之前选择的选项。  
  
- 安装 Mage.exe 和 MageUI.exe。  
  
     Mage.exe 和 MageUI.exe 都属于[!INCLUDE[winsdklong](../includes/winsdklong-md.md)]。 您必须或者具有[!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)]安装的版本或[!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)]随附 Visual Studio。 有关详细信息，请参阅[Windows SDK](http://go.microsoft.com/fwlink/?LinkId=158044) MSDN 上。  
  
- 提供一个应用程序部署。  
  
     本演练假定您已准备好部署的 Windows 应用程序。 此应用程序称为 AppToDeploy。  
  
- 确定如何将分布式部署。  
  
     分布选项包括：Web、 文件共享或 CD。 有关详细信息，请参阅 [ClickOnce Security and Deployment](../deployment/clickonce-security-and-deployment.md)。  
  
- 确定应用程序是否需要提升的信任级别。  
  
     如果你的应用程序需要完全信任-等的完全访问权限用户的系统，可以使用`-TrustLevel`Mage.exe 的选项将此项设置。 如果你想要定义将应用程序设置的自定义权限，可以将 Internet 或 intranet 的权限部分复制从另一个清单、 其进行修改以满足你的需求，并将其添加使用文本编辑器或 MageUI.exe 应用程序清单。 有关详细信息，请参阅 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。  
  
- 获取一个验证码证书。  
  
     你应登录你的部署使用验证码证书。 可以使用 Visual Studio、 MageUI.exe 中，或 MakeCert.exe 和 Pvk2Pfx.exe 工具来生成测试证书，或可以从证书颁发机构 (CA) 获取证书。 如果您选择使用受信任的应用程序部署，您还必须执行的一次性安装到所有客户端计算机上的证书。 有关详细信息，请参阅 [Trusted Application Deployment Overview](../deployment/trusted-application-deployment-overview.md)。  
  
    > [!NOTE]
    > 也可以登录你的部署使用 CNG 证书，你可以从证书颁发机构获取。  
  
- 请确保该应用程序不具有与 UAC 信息嵌入到清单。  
  
     您需要确定你的应用程序是否包含具有用户帐户控制 (UAC) 信息的清单，如`<dependentAssembly>`元素。 若要检查的应用程序清单，可以使用 Windows Sysinternals [Sigcheck](http://go.microsoft.com/fwlink/?LinkId=158035)实用程序。  
  
     如果你的应用程序包含具有 UAC 的详细信息的清单，您必须重新生成不带 UAC 的信息。 对于 C# 项目在 Visual Studio 中，打开项目属性并选择应用程序选项卡。在中**清单**下拉列表中，选择**创建不带清单的应用程序**。 对于 Visual Basic 项目在 Visual Studio 中，打开项目属性，选择应用程序选项卡，然后单击**查看 UAC 设置**。 在打开清单文件中，删除的所有元素内单个`<asmv1:assembly>`元素。  
  
- 确定应用程序是否需要客户端计算机上的系统必备组件。  
  
     [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 从 Visual Studio 部署的应用程序可以包括与部署的必备组件安装引导程序 (setup.exe)。 本演练将创建所需的两个清单[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署。 可以使用创建系统必备组件的引导[GenerateBootstrapper 任务](../msbuild/generatebootstrapper-task.md)。  
  
### <a name="to-deploy-an-application-with-the-mageexe-command-line-tool"></a>若要使用 Mage.exe 命令行工具部署应用程序  
  
1. 创建一个目录将在其中存储你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署文件。  
  
2. 在部署目录中刚刚创建，创建一个版本子目录。 如果这是首次部署应用程序，命名为版本子目录**1.0.0.0**。  
  
    > [!NOTE]
    > 你的部署的版本可以不同于你的应用程序的版本。  
  
3. 所有应用程序文件复制到版本子目录，其中包括可执行文件、 程序集、 资源和数据文件。 如有必要，可以创建其他子目录包含其他文件。  
  
4. 打开[!INCLUDE[winsdkshort](../includes/winsdkshort-md.md)]或 Visual Studio 命令提示并将更改为版本子目录。  
  
5. 创建应用程序清单，Mage.exe 的调用。 以下语句创建代码编译为 Intel x86 处理器上运行的应用程序清单。  
  
    ```  
    mage -New Application -Processor x86 -ToFile AppToDeploy.exe.manifest -name "My App" -Version 1.0.0.0 -FromDirectory .   
    ```  
  
    > [!NOTE]
    > 请务必包括句点 （.） 后`-FromDirectory`选项，它指示当前目录。 如果不包含点，必须对应用程序文件指定的路径。  
  
6. 使用验证码证书对应用程序清单进行签名。 替换*mycert.pfx*替换为您的证书文件的路径。 替换*passwd*替换为您的证书文件的密码。  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile mycert.pfx -Password passwd  
    ```  
  
     若要使用 CNG 证书对应用程序清单进行签名，使用以下命令。 替换*cngCert.pfx*替换为您的证书文件的路径。  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile cngCert.pfx  
    ```  
  
7. 将更改为部署目录的根目录。  
  
8. 生成部署清单，Mage.exe 调用。 默认情况下，Mage.exe 会将标记应用[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]作为已安装应用程序，因此它可以同时在线运行和脱机部署。 若要使应用程序可用，仅当用户处于联机状态时，使用`-Install`选项中包含的值`false`。 如果使用默认设置，并且用户将从 Web 站点或文件共享安装应用程序，请确保值`-ProviderUrl`选项指向的位置的应用程序清单上的 Web 服务器或共享。  
  
    ```  
    mage -New Deployment -Processor x86 -Install true -Publisher "My Co." -ProviderUrl "\\myServer\myShare\AppToDeploy.application" -AppManifest 1.0.0.0\AppToDeploy.exe.manifest -ToFile AppToDeploy.application  
    ```  
  
9. 使用验证码或 CNG 证书的部署清单进行签名。  
  
    ```  
    mage -Sign AppToDeploy.application -CertFile mycert.pfx -Password passwd  
    ```  
  
     或  
  
    ```  
    mage -Sign AppToDeploy.exe.manifest -CertFile cngCert.pfx  
    ```  
  
10. 将在部署目录中的所有文件复制到部署目标或媒体中。 这可能是网站或 FTP 站点、 文件共享或 CD-ROM 上的文件夹。  
  
11. 向用户提供 URL、 UNC 或安装应用程序所需的物理介质。 如果提供的 URL 或 UNC，则必须向你的用户的完整路径的部署清单。 例如，如果 AppToDeploy 部署到 http://webserver01/ AppToDeploy 目录中，在完整的 URL 路径应 http://webserver01/AppToDeploy/AppToDeploy.application 。   
  
### <a name="to-deploy-an-application-with-the-mageuiexe-graphical-tool"></a>若要使用 MageUI.exe 图形工具部署应用程序  
  
1. 创建一个目录将在其中存储你[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]部署文件。  
  
2. 在部署目录中刚刚创建，创建一个版本子目录。 如果这是首次部署应用程序，命名为版本子目录**1.0.0.0**。  
  
    > [!NOTE]
    > 你的版本是部署的你的应用程序的版本可能不同。  
  
3. 所有应用程序文件复制到版本子目录，其中包括可执行文件、 程序集、 资源和数据文件。 如有必要，可以创建其他子目录包含其他文件。  
  
4. 启动 MageUI.exe 图形工具。  
  
    ```  
    MageUI.exe  
    ```  
  
5. 通过选择创建新的应用程序清单**文件**，**新建**，**应用程序清单**菜单中。  
  
6. 在默认**名称**选项卡上，键入此部署的名称和版本号。 此外指定**处理器**你的应用程序生成的例如，x86。  
  
7. 选择**文件**选项卡上，单击省略号 (**...**) 按钮旁边**应用程序目录**文本框。 浏览文件夹对话框。  
  
8. 选择包含您的应用程序文件，该版本子目录，然后单击**确定**。  
  
9. 如果将部署从 Internet 信息服务 (IIS) 中，选择**时填充将.deploy 扩展名添加到不具有任何文件**复选框。  
  
10. 单击**Populate**按钮将所有应用程序文件添加到的文件列表。 如果你的应用程序包含多个可执行文件，将启动应用程序为此部署的主要可执行文件标记通过选择**入口点**从**文件类型**下拉列表。 （如果你的应用程序仅包含一个可执行文件，MageUI.exe 会将其标记为您。）  
  
11. 选择**所需权限**选项卡，然后选择需要你的应用程序要断言的信任级别。 默认值是**FullTrust**，这将适用于大多数应用程序。  
  
12. 选择**文件**，**另存为**菜单中。 此时将出现签名选项对话框，提示您对应用程序清单进行签名。  
  
13. 如果必须将证书作为文件系统上的文件存储，使用**使用证书文件签名**选项，然后从文件系统选择的证书，使用旁边的省略号 (**...**) 按钮。 然后键入证书的密码。  
  
     或  
  
     如果你的证书保存在证书存储区可从您的计算机访问，请选择**使用存储的证书签名**选项，然后从提供的列表中选择证书。  
  
14. 单击**确定**应用程序清单进行签名。 将出现另存为对话框。  
  
15. 在另存为对话框中，指定版本目录，然后单击**保存**。  
  
16. 选择**文件**，**新建**，**部署清单**菜单以创建部署清单中。  
  
17. 上**名称**选项卡上，指定此部署的名称和版本号码 (**1.0.0.0**在此示例中)。 此外指定**处理器**你的应用程序生成的例如，x86。  
  
18. 选择**描述**选项卡，并为指定值**发布者**并**产品**。 (**产品**是供脱机使用客户端计算机上安装应用程序时提供给 Windows 开始菜单上的应用程序的名称。)  
  
19. 选择**部署选项**选项卡上，然后在**开始位置**文字框中，指定 Web 服务器或共享上的应用程序清单的位置。 例如， \\\myServer\myShare\AppToDeploy.application。  
  
20. 如果在上一步中添加.deploy 扩展名，还选择**使用.deploy 文件扩展名**此处。  
  
21. 选择**更新选项**选项卡，并指定此应用程序的更新频率。 如果应用程序使用<xref:System.Deployment.Application.UpdateCheckInfo>若要检查更新自身，清除**此应用程序应检查更新**复选框。  
  
22. 选择**应用程序引用**选项卡，然后单击**选择清单**按钮。 显示打开的对话框。  
  
23. 选择前面创建的应用程序清单，然后单击**打开**。  
  
24. 选择**文件**，**另存为**菜单中。 此时将出现签名选项对话框，提示你部署清单进行签名。  
  
25. 如果必须将证书作为文件系统上的文件存储，使用**使用证书文件签名**选项，然后从文件系统选择的证书，使用旁边的省略号 (**...**) 按钮。 然后键入证书的密码。  
  
     或  
  
     如果你的证书保存在证书存储区可从您的计算机访问，请选择**使用存储的证书签名**选项，然后从提供的列表中选择证书。  
  
26. 单击**确定**部署清单进行签名。 将出现另存为对话框。  
  
27. 在中**另存为**对话框中，一个目录移动到的部署，然后单击根目录**保存**。  
  
28. 将在部署目录中的所有文件复制到部署目标或媒体中。 这可能是网站或 FTP 站点、 文件共享或 CD-ROM 上的文件夹。  
  
29. 向用户提供 URL、 UNC 或安装应用程序所需的物理介质。 如果提供的 URL 或 UNC，您必须为用户提供的部署清单的完整路径。 例如，如果 AppToDeploy 部署到 http://webserver01/ AppToDeploy 目录中，在完整的 URL 路径应 http://webserver01/AppToDeploy/AppToDeploy.application 。   
  
## <a name="next-steps"></a>后续步骤  
 当你需要进行部署的应用程序的新版本时，创建新版本命名的新目录 — 1.0.0.1—and 例如，将新的应用程序文件复制到新目录。 接下来，您需要按照前面的步骤来创建和注册一个新的应用程序清单，并更新和部署清单进行签名。 请注意，在这两个在 Mage.exe 中指定相同的更高版本`-New`并`–Update`调用，作为[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]仅更新更高版本中，最重要的最左侧的整数。 如果你使用 MageUI.exe，则可以更新部署清单通过打开它，选择**应用程序引用**选项卡上，单击**选择清单**按钮，并选择已更新应用程序清单。  
  
## <a name="see-also"></a>请参阅  
 [Mage.exe（清单生成和编辑工具）](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)   
 [MageUI.exe（图形化客户端中的清单生成和编辑工具）](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)   
 [发布 ClickOnce 应用程序](../deployment/publishing-clickonce-applications.md)   
 [ClickOnce 部署清单](../deployment/clickonce-deployment-manifest.md)   
 [ndptecclick](../deployment/clickonce-application-manifest.md)
