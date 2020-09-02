---
title: 手动部署 ClickOnce 应用，保留品牌
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- branding
- preserved branding information
- ClickOnce deployment, manually
- multiple ClickOnce deployment and branding
- ClickOnce deployment, SDK tools
- customer deployments
- manual ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, deployed by others
ms.assetid: c21822fb-d4ee-42e4-b72d-41ee9786efe5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 47db202d07fd88bfb5e922964caf2cdd5008c6fd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "66263428"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information"></a>演练：手动部署不需要重新签名并且保留署名信息的 ClickOnce 应用程序
当你创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序并将其提供给客户进行发布和部署时，客户通常必须更新部署清单并对其进行重新签名。 虽然这在大多数情况下仍是首选方法，但 .NET Framework 3.5 使你可以创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 可由客户部署的部署，而无需重新生成新的部署清单。 有关详细信息，请参阅 [部署 ClickOnce 应用程序用于测试和生产服务器而无需让步](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)。

 当你创建 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 应用程序，然后将其分配给客户进行发布和部署时，应用程序可以使用客户的品牌或保留你的品牌。 例如，如果应用程序是单个专用应用程序，你可能想要保留你的品牌。 如果对每个客户的应用程序进行了高度自定义，则可能要使用客户的品牌。 通过 .NET Framework 3.5，你可以在将应用程序提供给组织进行部署时保留你的品牌、出版商信息和安全签名。 有关详细信息，请参阅 [创建 ClickOnce 应用程序供其他人部署](../deployment/creating-clickonce-applications-for-others-to-deploy.md)。

> [!NOTE]
> 在本演练中，你将使用命令行工具 *Mage.exe* 或 *MageUI.exe*的图形工具手动创建部署。 有关手动部署的详细信息，请参阅 [演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="prerequisites"></a>先决条件
 若要执行本演练中的步骤，需要以下各项：

- 准备好部署的 Windows 窗体应用程序。 此应用程序将被称为 *WindowsFormsApp1*。

- Visual Studio 或 Windows SDK。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageexe"></a>使用 Mage.exe 部署具有多个部署和品牌支持的 ClickOnce 应用程序

1. 打开 Visual Studio 命令提示符或 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 命令提示符，并更改为要在其中存储文件的目录 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

2. 在部署的当前版本后创建一个名为的目录。 如果这是你首次部署应用程序，则可能会选择 " **1.0.0.0**"。

   > [!NOTE]
   > 部署版本可能与应用程序文件的版本不同。

3. 创建一个名为 **bin** 的子目录，并将所有应用程序文件（包括可执行文件、程序集、资源和数据文件）复制到此处。

4. 通过调用 Mage.exe 来生成应用程序清单。

   ```cmd
   mage -New Application -ToFile 1.0.0.0\WindowsFormsApp1.exe.manifest -Name "Windows Forms App 1" -Version 1.0.0.0 -FromDirectory 1.0.0.0\bin -UseManifestForTrust true -Publisher "A. Datum Corporation"
   ```

5. 用数字证书对应用程序清单进行签名。

   ```cmd
   mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx
   ```

6. 通过调用 *Mage.exe*生成部署清单。 默认情况下， *Mage.exe* 会将 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署标记为已安装的应用程序，以便它可以联机和脱机运行。 若要使应用程序仅在用户处于联机状态时可用，请使用 `-i` 值为的参数 `f` 。 由于此应用程序将利用多个部署功能，因此请排除 `-providerUrl` *Mage.exe*的参数。 在版本3.5 之前的 .NET Framework (版本中，不包括 `-providerUrl` 脱机应用程序将导致错误。 ) 

   ```cmd
   mage -New Deployment -ToFile WindowsFormsApp1.application -Name "Windows Forms App 1" -Version 1.0.0.0 -AppManifest 1.0.0.0\WindowsFormsApp1.manifest
   ```

7. 不要对部署清单进行签名。

8. 向客户提供所有要在其网络上部署应用程序的文件。

9. 此时，客户必须用自己的自行生成的证书对部署清单进行签名。 例如，如果客户针对名为 "艾德公司" 的公司工作，则他可以使用 *MakeCert.exe* 工具生成自签名证书。 接下来，使用 *Pvk2pfx.exe* 工具将 *MakeCert.exe* 创建的文件合并到可传递到 *Mage.exe*的 PFX 文件中。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

10. 接下来，客户使用此证书对部署清单进行签名。

    ```cmd
    mage -Sign WindowsFormsApp1.application -CertFile MyCert.pfx
    ```

11. 客户向其用户部署应用程序。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageuiexe"></a>使用 MageUI.exe 部署具有多个部署和品牌支持的 ClickOnce 应用程序

1. 打开 Visual Studio 命令提示符或 [!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)] 命令提示符，然后导航到要存储文件的目录 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

2. 创建一个名为 **bin** 的子目录，并将所有应用程序文件（包括可执行文件、程序集、资源和数据文件）复制到此处。

3. 在部署的当前版本后创建一个名为的子目录。 如果这是你首次部署应用程序，则可能会选择 " **1.0.0.0**"。

   > [!NOTE]
   > 部署版本可能与应用程序文件的版本不同。

4. 将 \\ **bin**目录移动到步骤2中创建的目录中。

5. *MageUI.exe*启动图形工具。

   ```cmd
   MageUI.exe
   ```

6. 通过从菜单中选择 " **文件**"、" **新建**"、" **应用程序清单** " 来创建新的应用程序清单。

7. 在 "默认 **名称** " 选项卡上，输入此部署的名称和版本号。 此外，为 **Publisher**提供一个值，它将在部署时用作 "开始" 菜单中的应用程序快捷方式链接的文件夹名称。

8. 选择 " **应用程序选项** " 选项卡，然后单击 " **为信任信息使用应用程序清单**"。 这将为此应用程序启用第三方品牌标记 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。

9. 选择 "**文件**" 选项卡，然后单击 "**应用程序目录**" 文本框旁边的 "**浏览**" 按钮。

10. 选择包含在步骤2中创建的应用程序文件的目录，然后在 "文件夹选择" 对话框中单击 **"确定"** 。

11. 单击 " **填充** " 按钮，将所有应用程序文件添加到文件列表。 如果你的应用程序包含多个可执行文件，则通过从 "**文件类型**" 下拉列表中选择 "**入口点**"，将此部署的主要可执行文件标记为启动应用程序。  (如果你的应用程序只包含一个可执行文件， *MageUI.exe* 会将其标记为你。 ) 

12. 选择 " **所需权限** " 选项卡，并选择需要应用程序断言的信任级别。 默认值为 " **完全信任**"，这将适用于大多数应用程序。

13. 从菜单中选择 " **文件**"、" **保存** "，并保存应用程序清单。 保存应用程序清单时，系统将提示您对应用程序清单进行签名。

14. 如果你的证书作为文件存储在文件系统中，请使用 " **签名为证书文件** " 选项，然后使用省略号 (**...**) "按钮从文件系统中选择该证书。

     - 或 -

     如果证书保存在可从计算机访问的证书存储中，请选择 " **使用存储的证书签名" 选项**，然后从提供的列表中选择证书。

15. 从菜单中选择 " **文件**"、" **新建**"、" **部署清单** " 以创建部署清单，然后在 " **名称** " 选项卡上，在此示例) 中提供 (**1.0.0.0** 的名称和版本号。

16. 切换到 " **更新** " 选项卡，指定要更新此应用程序的频率。 如果应用程序使用 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 部署 API 来检查更新本身，请清除标签为 " **此应用程序应检查更新**" 的复选框。

17. 切换到 " **应用程序引用** " 选项卡。您可以通过单击 " **选择清单** " 按钮，然后选择在前面的步骤中创建的应用程序清单，预先填充此选项卡上的所有值。

18. 选择 " **保存** "，并将部署清单保存到磁盘。 保存应用程序清单时，系统将提示您对应用程序清单进行签名。 单击 " **取消** " 可保存清单，而无需对其进行签名。

19. 向客户提供所有应用程序文件。

20. 此时，客户必须用自己的自行生成的证书对部署清单进行签名。 例如，如果客户针对名为 "艾德公司" 的公司工作，则他可以使用 *MakeCert.exe* 工具生成自签名证书。 接下来，使用 *Pvk2pfx.exe* 工具将 *MakeCert.exe* 创建的文件合并到可传递到 *MageUI.exe*的 PFX 文件中。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

21. 生成证书后，客户现在会通过在 *MageUI.exe*中打开部署清单并保存来签署部署清单。 当 "签名" 对话框出现时，客户选择 " **签名为证书文件** " 选项，然后选择已保存在磁盘上的 PFX 文件。

22. 客户向其用户部署应用程序。

## <a name="see-also"></a>另请参阅
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [MakeCert](/windows/desktop/SecCrypto/makecert)
