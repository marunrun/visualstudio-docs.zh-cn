---
title: 创建带有隐私提示的自定义引导程序
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
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
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a8fbb05fcfdb1a639855ca31e9574d3037559610
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90809271"
---
# <a name="walkthrough-create-a-custom-bootstrapper-with-a-privacy-prompt"></a>演练：创建带有隐私提示的自定义引导程序
可以将 ClickOnce 应用程序配置为在具有更新的文件版本和程序集版本的程序集可用时自动更新。 若要确保你的客户同意此行为，你可以向他们显示隐私提示。 然后，他们可以选择是否向应用程序授予自动更新的权限。 如果不允许应用程序自动更新，则不会安装该应用程序。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- Visual Studio 2010。

## <a name="create-an-update-consent-dialog-box"></a>"创建更新许可" 对话框
 若要显示隐私提示，请创建一个应用程序，要求读者同意应用程序的自动更新。

#### <a name="to-create-a-consent-dialog-box"></a>创建许可对话框

1. 在 **“文件”** 菜单上，指向 **“新建”** ，再单击 **“项目”** 。

2. 在 " **新建项目** " 对话框中，单击 " **Windows**"，然后单击 " **WindowsFormsApplication**"。

3. 对于 " **名称**"，请键入 **ConsentDialog**，然后单击 **"确定"**。

4. 在设计器中，单击窗体。

5. 在 " **属性** " 窗口中，将 " **文本** " 属性更改为 " **更新许可" 对话框**。

6. 在 " **工具箱**" 中，展开 " **所有 Windows 窗体**"，然后将 " **标签** " 控件拖动到窗体上。

7. 在设计器中，单击 "标签" 控件。

8. 在 "**属性**" 窗口中，将 "**外观**" 下的 "**文本**" 属性更改为以下内容：

    要安装的应用程序会在 Web 上检查最新更新。 单击 "我同意" 即可授权应用程序自动从 Internet 检查和安装更新。

9. 在 " **工具箱**" 中，将 " **Checkbox** " 控件拖到窗体的中间。

10. 在 "**属性**" 窗口中，将 "**布局**" 下的 "**文本**" 属性更改为 "**同意**"。

11. 在 " **工具箱**" 中，将 " **按钮** " 控件拖动到窗体的左下角。

12. 在 "**属性**" 窗口中，更改 "**布局**" 下的 "**文本**" 属性以**继续**。

13. 在 "**属性**" 窗口中，**将 "ProceedButton" 下的**" ** () 名称**" 属性更改为 " **ProceedButton**"。

14. 在 " **工具箱**" 中，将 " **按钮** " 控件拖动到窗体的右下方。

15. 在 "**属性**" 窗口中，将 "**布局**" 下的**Text**属性更改为 "**取消**"。

16. 在 "**属性**" 窗口中，**将 "CancelButton" 下的**" ** () 名称**" 属性更改为 " **CancelButton**"。

17. 在设计器中，双击 " **我同意** " 复选框以生成 CheckedChanged 事件处理程序。

18. 在 Form1 代码文件中，为 CheckedChanged 事件处理程序添加以下代码。

     [!code-csharp[ConsentDialog#1](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_1.cs)]
     [!code-vb[ConsentDialog#1](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_1.vb)]

19. 更新类构造函数，以在默认情况下禁用 " **继续** " 按钮。

     [!code-csharp[ConsentDialog#6](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_2.cs)]
     [!code-vb[ConsentDialog#6](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_2.vb)]

20. 在 Form1 代码文件中，为布尔变量添加以下代码，以跟踪最终用户是否同意联机更新。

     [!code-csharp[ConsentDialog#3](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_3.cs)]
     [!code-vb[ConsentDialog#3](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_3.vb)]

21. 在设计器中，双击 " **继续** " 按钮生成 click 事件处理程序。

22. 在 Form1 代码文件中，将以下代码添加到 " **继续** " 按钮的 Click 事件处理程序中。

     [!code-csharp[ConsentDialog#2](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_4.cs)]
     [!code-vb[ConsentDialog#2](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_4.vb)]

23. 在设计器中，双击 " **取消** " 按钮生成 click 事件处理程序。

24. 在 Form1 代码文件中，为 " **取消** " 按钮的 Click 事件处理程序添加以下代码。

     [!code-csharp[ConsentDialog#4](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_5.cs)]
     [!code-vb[ConsentDialog#4](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_5.vb)]

25. 如果最终用户未同意联机更新，则更新应用程序以返回错误。

     仅适用于 Visual Basic 开发人员：

    1. 在 **解决方案资源管理器**中，单击 **ConsentDialog**。

    2. 在 " **项目** " 菜单上，单击 " **添加模块**"，然后单击 " **添加**"。

    3. 在 *Module1* 代码文件中，添加以下代码。

        [!code-vb[ConsentDialog#7](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_6.vb)]

    4. 在 " **项目** " 菜单上，单击 " **ConsentDialog 属性**"，然后单击 " **应用程序** " 选项卡。

    5. 取消选中 " **启用应用程序框架**"。

    6. 在 " **启动对象** " 下拉菜单中，选择 " **Module1**"。

       > [!NOTE]
       > 禁用应用程序框架将禁用 Windows XP 视觉样式、应用程序事件、初始屏幕、单个实例应用程序等功能。 有关详细信息，请参阅 [Application Page, Project Designer (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)（应用程序页、项目设计器 (Visual Basic)。

       仅适用于 Visual c # 开发人员：

       打开 *Program.cs* 代码文件，并添加以下代码。

       [!code-csharp[ConsentDialog#5](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-bootstrapper-to-show-a-privacy-prompt_7.cs)]

26. 在 " **生成** " 菜单上，单击 " **依次**"。

## <a name="create-the-custom-bootstrapper-package"></a>创建自定义引导程序包
 若要向最终用户显示隐私提示，你可以为 "更新许可" 对话框应用程序创建自定义引导程序包，并在所有 ClickOnce 应用程序中将其包含为必备组件。

 此过程演示如何通过创建以下文档来创建自定义引导程序包：

- 一个 *product.xml* 清单文件，用于描述引导程序的内容。

- 一个 *package.xml* 清单文件，用于列出包的本地化特定方面，如字符串和软件许可条款。

- 软件许可条款的文档。

#### <a name="step-1-to-create-the-bootstrapper-directory"></a>步骤1：创建引导程序目录

1. 在 *%PROGRAMFILES%\Microsoft SDKs\Windows\v7.0A\Bootstrapper\Packages*中创建名为**UpdateConsentDialog**的目录。

    > [!NOTE]
    > 若要创建此文件夹，可能需要管理权限。

2. 在 *UpdateConsentDialog* 目录中，创建一个名为 *en*的子目录。

    > [!NOTE]
    > 为每个区域设置创建一个新目录。 例如，可以为 fr 和 de 区域设置添加子目录。 如有必要，这些目录将包含法语和德语字符串和语言包。

#### <a name="step-2-to-create-the-productxml-manifest-file"></a>步骤2：创建 product.xml 清单文件

1. 创建名为 *product.xml*的文本文件。

2. 在 *product.xml* 文件中，添加以下 XML 代码。 请确保不会覆盖现有的 XML 代码。

    ```xml
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

3. 将该文件保存到 UpdateConsentDialog 引导程序目录。

#### <a name="step-3-to-create-the-packagexml-manifest-file-and-the-software-license-terms"></a>步骤3：创建 package.xml 清单文件和软件许可条款

1. 创建名为 *package.xml*的文本文件。

2. 在 *package.xml* 文件中，添加以下 XML 代码以定义区域设置并包括软件许可条款。 请确保不会覆盖现有的 XML 代码。

    ```xml
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

3. 将该文件保存到 UpdateConsentDialog 引导程序目录中的 en 子目录。

4. 为软件许可条款创建一个名为 " *eula* " 的文档。

    > [!NOTE]
    > 软件许可条款应包括有关许可、担保、责任和本地法律的信息。 这些文件应是特定于区域设置的，因此请确保以支持 MBCS 或 UNICODE 字符的格式保存文件。 向法律部门咨询软件许可条款的内容。

5. 将文档保存到 *UpdateConsentDialog* 引导程序目录中的 en 子目录。

6. 如有必要，请为每个区域设置的软件许可条款创建新的 *package.xml* 清单文件和新的 *eula* 文档。 例如，如果为 fr 和 de 区域设置创建了子目录，请创建单独的 package.xml 清单文件和软件许可条款，并将其保存到 fr 和 de 子目录。

## <a name="set-the-update-consent-application-as-a-prerequisite"></a>将更新许可应用程序设置为先决条件
 在 Visual Studio 中，你可以将更新许可应用程序设置为必备组件。

#### <a name="to-set-the-update-consent-application-as-a-prerequisite"></a>将更新许可应用程序设置为必备组件

1. 在 **解决方案资源管理器**中，单击要部署的应用程序的名称。

2. 在“项目”菜单上，单击“ProjectName”属性****** ****。

3. 单击 " **发布** " 页，然后单击 " **必备组件**"。

4. 选择 " **更新许可" 对话框**。

    > [!NOTE]
    > 可能需要关闭并重新打开 Visual Studio，才能在 "系统必备" 对话框中看到 "更新许可" 对话框。

5. 单击“确定”。 

## <a name="create-and-test-the-setup-program"></a>创建和测试安装程序
 将更新许可应用程序设置为必备项后，你可以为应用程序生成安装程序和引导程序。

#### <a name="to-create-and-test-the-setup-program-by-not-clicking-i-agree"></a>若要创建和测试安装程序，请不要单击 "我同意"

1. 在 **解决方案资源管理器**中，单击要部署的应用程序的名称。

2. 在“项目”菜单上，单击“ProjectName”属性****** ****。

3. 单击 " **发布** " 页，然后单击 " **立即发布**"。

4. 如果 "发布" 输出未自动打开，请导航到 "发布输出"。

5. 运行 *Setup.exe* 程序。

     安装程序显示 "更新许可" 对话框软件许可协议。

6. 阅读软件许可协议，然后单击 " **接受**"。

     此时将显示 "更新许可" 对话框应用程序并显示以下文本：你要安装的应用程序在 Web 上检查最新更新。 单击 "我同意" 即表示授权应用程序在 Internet 上自动检查更新。

7. 关闭应用程序，或单击 "取消"。

     应用程序显示错误：安装适用于 *ApplicationName*的系统组件时出错。 在成功安装所有系统组件之前，安装程序无法继续。

8. 单击 "详细信息" 以显示以下错误消息：组件更新许可对话框安装失败，并显示以下错误消息： "不接受自动更新协议。 以下组件安装失败：-更新许可对话框

9. 单击“关闭”。

#### <a name="to-create-and-test-the-setup-program-by-clicking-i-agree"></a>通过单击 "我同意" 来创建和测试安装程序

1. 在 **解决方案资源管理器**中，单击要部署的应用程序的名称。

2. 在“项目”菜单上，单击“ProjectName”属性****** ****。

3. 单击 " **发布** " 页，然后单击 " **立即发布**"。

4. 如果 "发布" 输出未自动打开，请导航到 "发布输出"。

5. 运行 *Setup.exe* 程序。

     安装程序显示 "更新许可" 对话框软件许可协议。

6. 阅读软件许可协议，然后单击 " **接受**"。

     此时将显示 "更新许可" 对话框应用程序并显示以下文本：你要安装的应用程序在 Web 上检查最新更新。 单击 "我同意" 即表示授权应用程序在 Internet 上自动检查更新。

7. 单击 " **我同意**"，然后单击 " **继续**"。

     应用程序将开始安装。

8. 如果出现 "应用程序安装" 对话框，请单击 " **安装**"。

## <a name="see-also"></a>另请参阅
- [应用程序部署必备](../deployment/application-deployment-prerequisites.md)
- [创建引导程序包](../deployment/creating-bootstrapper-packages.md)
- [如何：创建产品清单](../deployment/how-to-create-a-product-manifest.md)
- [如何：创建程序包清单](../deployment/how-to-create-a-package-manifest.md)
- [产品和包架构引用](../deployment/product-and-package-schema-reference.md)