---
title: 手动部署 ClickOnce 应用程序保留的品牌
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
ms.sourcegitcommit: 117ece52507e86c957a5fd4f28d48a0057e1f581
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2019
ms.locfileid: "66263428"
---
# <a name="walkthrough-manually-deploy-a-clickonce-application-that-does-not-require-re-signing-and-that-preserves-branding-information"></a>演练：手动部署 ClickOnce 应用程序不需要重新签名并且保留署名信息
当你创建[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序并将它提供给客户进行发布和部署信息，通常客户必须更新部署清单并对其进行重新签名。 .NET Framework 3.5 时，仍是在大多数情况下的首选的方法，使您能够创建[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]可以由其客户部署而无需重新生成新的部署清单的部署。 有关详细信息，请参阅[无需重新签名的测试和生产服务器部署 ClickOnce 应用程序](../deployment/deploying-clickonce-applications-for-testing-and-production-without-resigning.md)。

 当你创建[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序，然后为其提供给客户进行发布和部署，请在应用程序可以使用客户的署名，也可以保留你的品牌。 例如，如果应用程序是一个单一的专有应用程序，你可能想要保留你的品牌。 如果应用程序高度自定义每个客户，可能想要使用客户的品牌。 .NET Framework 3.5，您可以保留你的品牌、 发布服务器信息和安全签名时，显示组织的应用程序部署。 有关详细信息，请参阅[创建 ClickOnce 应用程序以供他人部署](../deployment/creating-clickonce-applications-for-others-to-deploy.md)。

> [!NOTE]
> 在本演练中你创建部署手动使用命令行工具*Mage.exe*或图形工具*MageUI.exe*。 有关手动部署的详细信息，请参阅[演练：手动部署 ClickOnce 应用程序](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)。

## <a name="prerequisites"></a>系统必备
 若要执行本演练中的步骤需要具备以下：

- 已准备好部署一个 Windows 窗体应用程序。 此应用程序将引用作为*WindowsFormsApp1*。

- Visual Studio 或 Windows SDK。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageexe"></a>若要部署 ClickOnce 应用程序具有多个部署和使用 Mage.exe 的品牌支持

1. 打开 Visual Studio 命令提示符或[!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)]命令提示符，并将更改为在其中将存储的目录在[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]文件。

2. 创建一个名为你的部署的当前版本。 如果这是首次部署应用程序，可能会选择**1.0.0.0**。

   > [!NOTE]
   > 你的部署的版本可能不同于你的应用程序文件的版本。

3. 创建一个名为子目录**bin**并将所有应用程序文件，包括可执行文件、 程序集、 资源和数据文件复制。

4. 生成应用程序清单，Mage.exe 调用。

   ```cmd
   mage -New Application -ToFile 1.0.0.0\WindowsFormsApp1.exe.manifest -Name "Windows Forms App 1" -Version 1.0.0.0 -FromDirectory 1.0.0.0\bin -UseManifestForTrust true -Publisher "A. Datum Corporation"
   ```

5. 使用数字证书对应用程序清单进行签名。

   ```cmd
   mage -Sign WindowsFormsApp1.exe.manifest -CertFile mycert.pfx
   ```

6. 生成部署清单通过调用*Mage.exe*。 默认情况下*Mage.exe*会将标记应用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]作为已安装应用程序，因此它可以同时在线运行和脱机部署。 若要使应用程序可用，仅当用户处于联机状态时，使用`-i`自变量的值与`f`。 由于此应用程序将充分利用多个部署功能，排除`-providerUrl`自变量*Mage.exe*。 (不包括.NET Framework 版本 3.5 中之前, 的版本中`-providerUrl`的脱机应用程序将导致错误。)

   ```cmd
   mage -New Deployment -ToFile WindowsFormsApp1.application -Name "Windows Forms App 1" -Version 1.0.0.0 -AppManifest 1.0.0.0\WindowsFormsApp1.manifest
   ```

7. 不要对部署清单进行签名。

8. 提供的所有文件的客户，将部署他的网络上的应用程序。

9. 此时，客户必须使用他自己自行生成的证书的部署清单签名。 例如，如果客户适用于名为 Adventure Works 的公司，他可以生成自签名的证书使用*MakeCert.exe*工具。 接下来，使用*Pvk2pfx.exe*工具来组合创建的文件*MakeCert.exe*到 PFX 文件，可传递给*Mage.exe*。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

10. 接下来，客户使用此证书部署清单进行签名。

    ```cmd
    mage -Sign WindowsFormsApp1.application -CertFile MyCert.pfx
    ```

11. 客户就可以部署到其用户的应用程序。

### <a name="to-deploy-a-clickonce-application-with-multiple-deployment-and-branding-support-using-mageuiexe"></a>若要部署 ClickOnce 应用程序具有多个部署和使用 MageUI.exe 的品牌支持

1. 打开 Visual Studio 命令提示符或[!INCLUDE[winsdkshort](../debugger/debug-interface-access/includes/winsdkshort_md.md)]命令提示符处，并导航到在其中将存储的目录在[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]文件。

2. 创建一个名为子目录**bin**并将所有应用程序文件，包括可执行文件、 程序集、 资源和数据文件复制。

3. 创建你的部署的当前版本命名的子目录。 如果这是首次部署应用程序，可能会选择**1.0.0.0**。

   > [!NOTE]
   > 你的部署的版本可能不同于你的应用程序文件的版本。

4. 移动\\ **bin**目录到在步骤 2 中创建的目录。

5. 启动的图形化工具*MageUI.exe*。

   ```cmd
   MageUI.exe
   ```

6. 通过选择创建新的应用程序清单**文件**，**新建**，**应用程序清单**菜单中。

7. 在默认**名称**选项卡上，输入此部署的名称和版本号。 此外，请提供的值**发布服务器**，它将作为使用开始菜单中的应用程序的快捷方式链接的文件夹名称在部署时。

8. 选择**应用程序选项**选项卡，单击**将应用程序清单信任信息**。 这将使第三方品牌此[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]应用程序。

9. 选择**文件**选项卡，单击**浏览**按钮旁边**应用程序目录**文本框。

10. 选择包含您在步骤 2 中创建的应用程序文件的目录，然后单击**确定**文件夹选择对话框上。

11. 单击**Populate**按钮将所有应用程序文件添加到的文件列表。 如果你的应用程序包含多个可执行文件，将启动应用程序为此部署的主要可执行文件标记通过选择**入口点**从**文件类型**下拉列表。 (如果你的应用程序仅包含一个可执行文件*MageUI.exe*会将它标记为您。)

12. 选择**所需权限**选项卡，然后选择需要你的应用程序要断言的信任级别。 默认值是**完全信任**，这将适用于大多数应用程序。

13. 选择**文件**，**保存**从菜单中，并保存应用程序清单。 系统将提示您为应用程序清单签名时将其保存。

14. 如果必须将证书作为文件系统上的文件存储，使用**作为证书文件签名**选项，然后选择该证书从文件系统使用的省略号 ( **...** ) 按钮。

     或

     如果你的证书保存在可以从您的计算机访问的证书存储中，选择**使用存储的证书选项签名**，然后从提供的列表中选择的证书。

15. 选择**文件**，**新建**，**部署清单**从菜单以创建部署清单，然后在**名称**选项卡上，提供名称和版本号 (**1.0.0.0**在此示例中)。

16. 切换到**更新**选项卡，然后指定希望此应用程序的更新的频率。 如果应用程序使用[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]部署 API 以检查是否有更新自身，清除标记的复选框**此应用程序应检查更新**。

17. 切换到**应用程序引用**选项卡。可以通过单击预填充此选项卡上的值的所有**选择清单**上一步骤中创建按钮，选择应用程序清单。

18. 选择**保存**并将部署清单保存到磁盘。 系统将提示您为应用程序清单签名时将其保存。 单击**取消**保存而无需对它的签名的清单。

19. 为客户提供的所有应用程序文件。

20. 此时，客户必须使用他自己自行生成的证书的部署清单签名。 例如，如果客户适用于名为 Adventure Works 的公司，他可以生成自签名的证书使用*MakeCert.exe*工具。 接下来，使用*Pvk2pfx.exe*工具来组合创建的文件*MakeCert.exe*到 PFX 文件，可传递给*MageUI.exe*。

    ```cmd
    makecert -r -pe -n "CN=Adventure Works" -sv MyCert.pvk MyCert.cer
    pvk2pfx.exe -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx
    ```

21. 生成的证书，客户现在签名部署清单通过打开部署清单中的*MageUI.exe*，并进行保存。 签名对话框中出现时，客户选择**作为证书文件签名**选项，并选择他已经保存在磁盘的 PFX 文件。

22. 客户就可以部署到其用户的应用程序。

## <a name="see-also"></a>请参阅
- [Mage.exe（清单生成和编辑工具）](/dotnet/framework/tools/mage-exe-manifest-generation-and-editing-tool)
- [MageUI.exe（图形化客户端中的清单生成和编辑工具）](/dotnet/framework/tools/mageui-exe-manifest-generation-and-editing-tool-graphical-client)
- [MakeCert](/windows/desktop/SecCrypto/makecert)
