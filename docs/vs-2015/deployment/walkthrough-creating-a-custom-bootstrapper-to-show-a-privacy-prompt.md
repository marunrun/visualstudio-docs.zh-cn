---
title: 演练：创建自定义引导程序以显示隐私提示 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, prerequisites
- dependencies [.NET Framework], custom bootstrapper package
- deploying applications [Visual Studio], custom prerequisites
- Windows Installer deployment, prerequisites
- prerequisites [.NET Framework], custom bootstrapper package
ms.assetid: 2f3edd6a-84d1-4864-a1ae-6a13c5732aae
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6d93d9f771da9387661603f3eb71301e9d9aead7
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427133"
---
# <a name="walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt"></a>演练：创建自定义引导程序以显示隐私提示
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以配置 ClickOnce 应用程序具有更高版本的文件版本和程序集版本的程序集变得可用时自动更新。 若要确保你的客户同意此行为，可以向他们显示隐私提示。 然后，他们可以选择是否要自动更新的应用程序的权限授予。 如果应用程序不允许自动更新，它不会安装。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>系统必备  
 你需要以下组件来完成本演练：  
  
- Visual Studio 2010。  
  
## <a name="creating-an-update-consent-dialog-box"></a>创建更新同意对话框中  
 若要显示隐私提示，请创建的应用程序询问读取器同意自动更新应用程序。  
  
#### <a name="to-create-a-consent-dialog-box"></a>若要创建同意对话框  
  
1. 在 **“文件”** 菜单上，指向 **“新建”**，然后单击 **“项目”**。  
  
2. 在中**新的项目**对话框中，单击**Windows**，然后单击**WindowsFormsApplication**。  
  
3. 有关**名称**，类型**ConsentDialog**，然后单击**确定**。  
  
4. 在设计器中，单击窗体。  
  
5. 在中**属性**窗口中，更改**文本**属性设置为**更新同意对话框**。  
  
6. 在中**工具箱**，展开**所有 Windows 窗体**，并将其拖**标签**到窗体控件。  
  
7. 在设计器中，单击标签控件。  
  
8. 在中**属性**窗口中，更改**文本**下的属性**外观**所示：  
  
    在 Web 上找到最新的更新检查要安装的应用程序。 单击"我同意"，则表示您授权应用程序检查并自动从 Internet 安装更新。  
  
9. 在中**工具箱**，拖动**复选框**中间部分的窗体控件。  
  
10. 在中**属性**窗口中，更改**文本**下的属性**布局**到**我同意**。  
  
11. 在中**工具箱**，拖动**按钮**到左下方的窗体控件。  
  
12. 在中**属性**窗口中，更改**文本**下的属性**布局**到**继续**。  
  
13. 在中**属性**窗口中，更改 **（名称）** 下的属性**设计**到**ProceedButton**。  
  
14. 在中**工具箱**，拖动**按钮**到窗体的右下角的控件。  
  
15. 在中**属性**窗口中，更改**文本**下的属性**布局**到**取消**。  
  
16. 在中**属性**窗口中，更改 **（名称）** 下的属性**设计**到**CancelButton**。  
  
17. 在设计器中，双击**我同意**复选框可生成的 CheckedChanged 事件处理程序。  
  
18. 在 Form1 代码文件中，添加以下代码的 CheckedChanged 事件处理程序。  
  
     [!code-csharp[ConsentDialog#1](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#1)]
     [!code-vb[ConsentDialog#1](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#1)]  
  
19. 更新类构造函数来禁用**继续**默认情况下的按钮。  
  
     [!code-csharp[ConsentDialog#6](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#6)]
     [!code-vb[ConsentDialog#6](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#6)]  
  
20. 在 Form1 代码文件中，添加以下代码来跟踪如果最终用户已经同意联机更新的布尔变量。  
  
     [!code-csharp[ConsentDialog#3](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#3)]
     [!code-vb[ConsentDialog#3](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#3)]  
  
21. 在设计器中，双击**继续**按钮以生成 Click 事件处理程序。  
  
22. 在 Form1 代码文件中，将以下代码添加到的单击事件处理程序**继续**按钮。  
  
     [!code-csharp[ConsentDialog#2](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#2)]
     [!code-vb[ConsentDialog#2](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#2)]  
  
23. 在设计器中，双击**取消**按钮以生成 Click 事件处理程序。  
  
24. 在 Form1 代码文件中，添加的单击事件处理程序的以下代码**取消**按钮。  
  
     [!code-csharp[ConsentDialog#4](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/form1.cs#4)]
     [!code-vb[ConsentDialog#4](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/form1.vb#4)]  
  
25. 更新应用程序，如果最终用户不同意联机更新时返回错误。  
  
     对于 Visual Basic 开发：  
  
    1. 在中**解决方案资源管理器**，单击**ConsentDialog**。  
  
    2. 上**项目**菜单上，单击**添加模块**，然后单击**添加**。  
  
    3. 在 Module1.vb 代码文件中，添加以下代码。  
  
        [!code-vb[ConsentDialog#7](../snippets/visualbasic/VS_Snippets_ProTools/consentdialog/vb/module1.vb#7)]  
  
    4. 上**项目**菜单上，单击**ConsentDialog 属性**，然后单击**应用程序**选项卡。  
  
    5. 取消选中**启用应用程序框架**。  
  
    6. 在中**启动对象**下拉列表菜单中，选择**Module1**。  
  
       > [!NOTE]
       > 禁用应用程序框架将禁用功能，例如 Windows XP 视觉样式、 应用程序事件、 初始屏幕、 单实例应用程序和的详细信息。 有关详细信息，请参阅 [Application Page, Project Designer (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)（应用程序页、项目设计器 (Visual Basic)。  
  
       Visual C# 仅适用于开发人员：  
  
       打开 Program.cs 代码文件，并添加以下代码。  
  
       [!code-csharp[ConsentDialog#5](../snippets/csharp/VS_Snippets_ProTools/consentdialog/cs/program.cs#5)]  
  
26. 上**构建**菜单上，单击**生成解决方案**。  
  
## <a name="creating-the-custom-bootstrapper-package"></a>创建自定义引导程序包  
 若要向最终用户显示隐私提示，可以创建自定义引导程序包的更新的同意对话框应用程序并将其作为必备组件包含在所有 ClickOnce 应用程序。  
  
 此过程说明了如何创建自定义引导程序包，通过创建以下文档：  
  
- Product.xml 清单文件来描述引导程序的内容。  
  
- 若要列出的包，如字符串和软件许可条款的特定于本地化的方面 package.xml 清单文件。  
  
- 面向软件许可条款的文档。  
  
#### <a name="step-1-to-create-the-bootstrapper-directory"></a>步骤 1：若要创建引导程序目录  
  
1. 创建一个名为**UpdateConsentDialog** %PROGRAMFILES%\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages 中。  
  
    > [!NOTE]
    > 您可能需要管理权限才能创建此文件夹。  
  
2. 在 UpdateConsentDialog 目录中，创建一个名为 en 子目录。  
  
    > [!NOTE]
    > 创建每个区域设置的新目录。 例如，可以添加 fr 和 de 区域设置的子目录。 如有必要，这些目录将包含法语和德语字符串和语言包。  
  
#### <a name="step-2-to-create-the-productxml-manifest-file"></a>步骤 2：若要创建 product.xml 清单文件  
  
1. 创建名为文本文件`product.xml`。  
  
2. 在 product.xml 文件中，添加以下 XML 代码。 请确保不覆盖现有的 XML 代码。  
  
    ```  
    <Product  
      xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
      ProductCode="Microsoft.Sample.EULA">  
      <!-- Defines the list of files to be copied on build. -->  
      <PackageFiles CopyAllPackageFiles="false">  
        <PackageFile Name="ConsentDialog.exe"/>  
      </PackageFiles>  
  
      <!-- Defines how to run the Setup package.-->  
      <Commands >  
        <Command PackageFile = "ConsentDialog.exe" Arguments=''>  
          <ExitCodes>  
            <ExitCode Value="0" Result="Success" />  
            <ExitCode Value="-1" Result="Fail" String="AU_Unaccepted" />  
            <DefaultExitCode Result="Fail"   
              FormatMessageFromSystem="true" String="GeneralFailure" />  
          </ExitCodes>  
        </Command>  
      </Commands>  
  
    </Product>  
    ```  
  
3. 将文件保存到 UpdateConsentDialog 引导程序目录。  
  
#### <a name="step-3-to-create-the-packagexml-manifest-file-and-the-software-license-terms"></a>步骤 3：若要创建 package.xml 清单文件和软件许可条款  
  
1. 创建名为文本文件`package.xml`。  
  
2. 在 package.xml 文件中，添加下面的 XML 代码，以定义区域设置和包括的软件许可条款。 请确保不覆盖现有的 XML 代码。  
  
    ```  
    <Package   
      xmlns="http://schemas.microsoft.com/developer/2004/01/bootstrapper"  
      Name="DisplayName"  
      Culture="Culture"  
      LicenseAgreement="eula.rtf">  
      <PackageFiles>  
        <PackageFile Name="eula.rtf"/>  
      </PackageFiles>  
  
      <!-- Defines a localizable string table for error messages. -->  
      <Strings>  
        <String Name="DisplayName">Update Consent Dialog</String>  
        <String Name="Culture">en</String>  
        <String Name="AU_Unaccepted">The automatic update agreement is not accepted.</String>  
        <String Name="GeneralFailure">A failure occurred attempting to launch the setup.</String>  
      </Strings>  
    </Package>  
    ```  
  
3. 将文件保存到 UpdateConsentDialog 引导程序目录中的 en 子目录。  
  
4. 创建一个名为软件许可条款 eula.rtf 的文档。  
  
    > [!NOTE]
    > 软件许可条款应包括有关许可、 保证、 责任和当地法律信息。 这些文件应是特定于区域设置的因此请确保该文件的保存支持 MBCS 或 UNICODE 字符格式。 请咨询您的软件许可条款内容有关的法律部门。  
  
5. 将文档保存到 UpdateConsentDialog 引导程序目录中的 en 子目录。  
  
6. 如有必要，为每个区域设置的软件许可条款创建新的 package.xml 清单文件和新 eula.rtf 文档。 例如，如果创建的 fr 和 de 区域设置的子目录，创建单独 package.xml 清单文件和软件许可条款，并将其保存到的 fr 和 de 子目录。  
  
## <a name="setting-the-update-consent-application-as-a-prerequisite"></a>设置更新同意应用程序的必备组件  
 在 Visual Studio 中，您可以设置更新许可应用程序的必备组件。  
  
#### <a name="to-set-the-update-consent-application-as-a-prerequisite"></a>若要更新许可应用程序设置的必备组件  
  
1. 在中**解决方案资源管理器**，单击你想要部署应用程序的名称。  
  
2. 在“项目”菜单上，单击“ProjectName”属性。  
  
3. 单击**发布**页上，然后依次**先决条件**。  
  
4. 选择**更新同意对话框**。  
  
    > [!NOTE]
    > 您可能需要关闭并重新打开 Visual Studio 以查看更新的同意对话框中系统必备组件对话框。  
  
5. 单击 **“确定”**。  
  
## <a name="creating-and-testing-the-setup-program"></a>创建和测试安装程序  
 在设置更新许可应用程序的必备组件后，可以为应用程序中生成的安装程序和引导程序。  
  
#### <a name="to-create-and-test-the-setup-program-by-not-clicking-i-agree"></a>若要创建和测试安装程序不单击我同意  
  
1. 在中**解决方案资源管理器**，单击你想要部署应用程序的名称。  
  
2. 在“项目”菜单上，单击“ProjectName”属性。  
  
3. 单击**发布**页上，然后依次**立即发布**。  
  
4. 如果发布输出不会自动打开，导航到发布输出。  
  
5. 运行 Setup.exe 程序。  
  
     安装程序显示同意对话框中更新软件许可协议。  
  
6. 阅读软件许可协议，然后依次**接受**。  
  
     同意对话框中更新应用程序将出现并显示以下文本：在 Web 上找到最新的更新检查要安装的应用程序。 通过单击我同意，您授权检查在 Internet 上的自动更新应用程序。  
  
7. 关闭应用程序，或单击取消。  
  
     应用程序将显示错误：安装的系统组件时出错*ApplicationName*。 已成功安装所有系统组件之前，安装程序无法继续。  
  
8. 单击以显示以下错误消息的详细信息：组件更新同意对话框无法安装具有以下错误消息："自动更新协议是不被接受。" 无法安装以下组件:-更新同意对话框  
  
9. 单击 **“关闭”**。  
  
#### <a name="to-create-and-test-the-setup-program-by-clicking-i-agree"></a>若要创建和测试安装程序通过单击我同意  
  
1. 在中**解决方案资源管理器**，单击你想要部署应用程序的名称。  
  
2. 在“项目”菜单上，单击“ProjectName”属性。  
  
3. 单击**发布**页上，然后依次**立即发布**。  
  
4. 如果发布输出不会自动打开，导航到发布输出。  
  
5. 运行 Setup.exe 程序。  
  
     安装程序显示同意对话框中更新软件许可协议。  
  
6. 阅读软件许可协议，然后依次**接受**。  
  
     同意对话框中更新应用程序将出现并显示以下文本：在 Web 上找到最新的更新检查要安装的应用程序。 通过单击我同意，您授权检查在 Internet 上的自动更新应用程序。  
  
7. 单击**我同意**，然后单击**继续**。  
  
     应用程序将开始安装。  
  
8. 如果出现安装应用程序对话框中，单击**安装**。  
  
## <a name="see-also"></a>请参阅  
 [应用程序部署必备](../deployment/application-deployment-prerequisites.md)   
 [创建引导程序包](../deployment/creating-bootstrapper-packages.md)   
 [如何：创建产品清单](../deployment/how-to-create-a-product-manifest.md)   
 [如何：创建程序包清单](../deployment/how-to-create-a-package-manifest.md)   
 [产品和包架构引用](../deployment/product-and-package-schema-reference.md)
