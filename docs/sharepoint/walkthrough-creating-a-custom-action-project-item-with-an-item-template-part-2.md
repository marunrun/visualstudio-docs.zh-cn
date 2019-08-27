---
title: 使用项模板，第 2 部分中创建自定义操作项目项
ms.date: 02/02/2017
ms.topic: conceptual
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], creating template wizards
- SharePoint project items, creating template wizards
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6fa4915b9621789c68ed994440de3a1ef544c40c
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401165"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>演练：使用项模板，第 2 部分中创建自定义操作项目项
  定义自定义类型的 SharePoint 项目项并将其与 Visual Studio 中的项模板后，可能想要为模板提供一个向导。 该向导可用于从用户收集信息，当用户使用模板向项目添加项目项的新实例。 可以使用你收集的信息来初始化项目项。

 在本演练中，您将对自定义操作项目项中所示添加向导[演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。 当用户将自定义操作项目项添加到 SharePoint 项目时，则向导会收集有关自定义操作 （如其位置和最终用户选择它时要导航到的 URL） 的信息，并添加到此信息*Elements.xml*新的项目项中的文件。

 本演练演示了下列任务：

- 创建用于与项模板关联的自定义 SharePoint 项目项类型的向导。

- 定义自定义向导类似于内置在 Visual Studio 中的 SharePoint 项目项中的向导的 UI。

- 使用可替换参数初始化 SharePoint 项目文件使用此向导中收集的数据。

- 调试和测试该向导。

> [!NOTE]
> 您可以下载的示例[Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) ，演示如何创建自定义工作流活动。

## <a name="prerequisites"></a>系统必备
 若要执行本演练中，您必须首先创建 CustomActionProjectItem 解决方案完成[演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

 您还需要完成本演练在开发计算机上的以下组件：

- 支持的 Windows、 SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用**VSIX 项目**中此 SDK 来创建 VSIX 包来部署项目项模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 用于 Visual Studio 中的项目和项模板的向导。 有关详细信息，请参阅[如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)和<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口。

- 在 SharePoint 中的自定义操作。 有关详细信息，请参阅[自定义操作](http://go.microsoft.com/fwlink/?LinkId=177800)。

## <a name="create-the-wizard-project"></a>创建向导项目
 若要完成本演练中，必须将项目添加到你在中创建的 CustomActionProjectItem 解决方案[演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。 将实现<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口，并在此项目中定义的向导 UI。

#### <a name="to-create-the-wizard-project"></a>若要创建向导项目

1. 在 Visual Studio 中，打开 CustomActionProjectItem 解决方案

2. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

3. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**Windows**节点。

4. 在顶部**新的项目**对话框框中，请确保 **.NET Framework 4.5** .NET Framework 版本的列表中选择。

5. 选择**WPF 用户控件库**项目模板，请将项目命名**ItemTemplateWizard**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**ItemTemplateWizard**到解决方案。

6. 从项目中删除 UserControl1 项。

## <a name="configure-the-wizard-project"></a>配置向导项目
 在创建该向导之前，必须添加 Windows Presentation Foundation (WPF) 窗口、 代码文件中，并对项目的程序集引用。

#### <a name="to-configure-the-wizard-project"></a>若要配置向导项目

1. 在中**解决方案资源管理器**，打开快捷菜单，从**ItemTemplateWizard**项目节点，然后选择**属性**。

2. 在中**项目设计器**，请确保目标框架设置为.NET Framework 4.5。

     对于 Visual C# 项目，可以将此值设置上**应用程序**选项卡。对于 Visual Basic 项目，可以将此值设置上**编译**选项卡。有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。

3. 在中**ItemTemplateWizard**项目中，添加**Window (WPF)** 项到项目中，并将其命名为项**WizardWindow**。

4. 添加两个分别名为 CustomActionWizard 和字符串的代码文件。

5. 打开快捷菜单**ItemTemplateWizard**项目，，然后选择**添加引用**。

6. 在中**引用管理器-ItemTemplateWizard**对话框中的**程序集**节点，选择**扩展**节点。

7. 选择以下程序集旁的复选框，然后选择**确定**按钮：

    - EnvDTE

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

8. 在中**解决方案资源管理器**，在**引用**ItemTemplateWizard 项目文件夹选择**EnvDTE**引用。

9. 在中**属性**窗口中，更改的值**嵌入互操作类型**属性设置为**False**。

## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>定义的默认位置和自定义操作的 ID 字符串
 每个自定义操作具有位置和中指定的 ID`GroupID`并`Location`的属性`CustomAction`中的元素*Elements.xml*文件。 在此步骤中，可以定义一些 ItemTemplateWizard 项目中的这些属性的有效字符串。 完成本演练后，这些字符串写入*Elements.xml*中当用户在向导中指定的位置和 ID 的自定义操作项目项文件。

 为简单起见，此示例支持可用的默认位置和 Id 的一个子集。 有关完整列表，请参阅[默认自定义操作位置和 Id](http://go.microsoft.com/fwlink/?LinkId=181964)。

#### <a name="to-define-the-default-location-and-id-strings"></a>若要定义的默认位置和 ID 字符串

1. 打开。

2. 在中**ItemTemplateWizard**项目中，字符串的代码文件中的代码替换为以下代码。

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs#6)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb#6)]

## <a name="create-the-wizard-ui"></a>创建向导用户界面
 添加 XAML 来定义 UI 的向导中，并添加一些代码以在向导中的一些控件绑定到的 ID 字符串。 该向导创建类似于 Visual Studio 中的 SharePoint 项目的内置向导。

#### <a name="to-create-the-wizard-ui"></a>若要创建向导用户界面

1. 在中**ItemTemplateWizard**项目中，打开快捷菜单**WizardWindow.xaml**文件，，然后选择**打开**以在设计器中打开窗口。

2. 在 XAML 视图中，使用以下 XAML 替换当前的 XAML。 XAML 定义包含一个标题，用于指定自定义操作和在窗口底部的导航按钮的行为控件的 UI。

    > [!NOTE]
    > 添加此代码后，项目将具有某些编译错误。 在后续步骤中添加代码时，这些错误将消失。

     [!code-xml[SPExtensibility.ProjectItem.CustomAction#9](../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml#9)]

    > [!NOTE]
    > 在此 XAML 中创建的窗口派生自<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>基类。 当向 Visual Studio 添加自定义的 WPF 对话框中时，我们建议从为具有其他对话框在 Visual Studio 中使用一致样式并避免问题可能会出现与模式对话框的此类派生您的对话框。 有关详细信息，请参阅[创建和管理模式对话框](/visualstudio/extensibility/creating-and-managing-modal-dialog-boxes)。

3. 如果要开发 Visual Basic 项目，删除`ItemTemplateWizard`从命名空间`WizardWindow`中的类名`x:Class`属性的`Window`元素。 此元素是在 XAML 中的第一行中。 完成后，第一行应类似于以下代码：

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. 在代码隐藏文件 WizardWindow.xaml 文件中，将当前的代码替换下面的代码。

     [!code-vb[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs#7)]

## <a name="implement-the-wizard"></a>实现向导
 通过实现定义的向导功能<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口。

#### <a name="to-implement-the-wizard"></a>若要实现该向导

1. 在中**ItemTemplateWizard**项目中，打开**CustomActionWizard**代码文件，并且此文件中的当前代码将替换为以下代码：

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs#8)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb#8)]

## <a name="checkpoint"></a>检查点
 此时在演练中，该向导的所有代码都现项目中。 生成项目，以确保它在编译时没有错误。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="associate-the-wizard-with-the-item-template"></a>带有项模板关联向导
 现在，已实现了向导，您必须将其与**自定义操作**项模板通过完成三个主要步骤：

1. 向导程序集具有强名称签名。

2. 获取向导程序集的公钥令牌。

3. 在.vstemplate 文件中添加对向导程序集的引用**自定义操作**项模板。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>为向导程序集具有强名称签名

1. 在中**解决方案资源管理器**，打开快捷菜单，从**ItemTemplateWizard**项目节点，然后选择**属性**。

2. 上**签名**选项卡上，选择**程序集签名**复选框。

3. 在中**选择强名称密钥文件**列表中，选择 **\<新建...>** 。

4. 在中**创建强名称密钥**对话框框中，输入一个名称，清除**保护密钥文件使用密码**复选框，，然后选择**确定**按钮。

5. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>若要获取的公钥令牌向导程序集

1. 在 Visual Studio 命令提示符窗口中，运行以下命令，用*PathToWizardAssembly*生成 ItemTemplateWizard.dll ItemTemplateWizard 上的项目开发的程序集的完整路径计算机。

    ```xml
    sn.exe -T PathToWizardAssembly
    ```

     公钥标记*ItemTemplateWizard.dll*程序集写入到 Visual Studio 命令提示符窗口。

2. Visual Studio 命令提示符窗口保持打开。 你将需要完成下一个过程中的公钥标记。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>若要添加的.vstemplate 文件中的向导程序集的引用

1. 在中**解决方案资源管理器**，展开**ItemTemplate**项目节点，并打开*ItemTemplate.vstemplate*文件。

2. 在文件末尾附近添加以下`WizardExtension`之间的元素`</TemplateContent>`和`</VSTemplate>`标记。 替换*YourToken*的值`PublicKeyToken`与上一步骤中获取的公钥标记的属性。

    ```xml
    <WizardExtension>
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>
    </WizardExtension>
    ```

     有关详细信息`WizardExtension`元素，请参阅[WizardExtension 元素&#40;Visual Studio 模板&#41;](/visualstudio/extensibility/wizardextension-element-visual-studio-templates)。

3. 保存并关闭文件。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>添加到可替换参数*Elements.xml*项模板中的文件
 添加到多个可替换参数*Elements.xml* ItemTemplate 项目文件中的。 在初始化这些参数`PopulateReplacementDictionary`中的方法`CustomActionWizard`前面定义的类。 当用户将自定义操作项目项添加到项目时，Visual Studio 将自动替换中的这些参数*Elements.xml*中用它们在向导中指定的值的新项目项文件。

 可替换参数是一个标记，用于开始和结束的美元符号 （$） 字符。 除了定义自己的可替换参数，可以使用内置的 SharePoint 项目系统定义并初始化的参数。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>若要添加到可替换参数*Elements.xml*文件

1. 在项模板项目中，替换的内容*Elements.xml*使用以下 XML 文件。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="$IdValue$"
                    GroupId="$GroupIdValue$"
                    Location="$LocationValue$"
                    Sequence="1000"
                    Title="$TitleValue$"
                    Description="$DescriptionValue$" >
        <UrlAction Url="$UrlValue$"/>
      </CustomAction>
    </Elements>
    ```

     新的 XML 更改的值`Id`， `GroupId`， `Location`， `Description`，和`Url`属性到可替换参数。

2. 保存并关闭文件。

## <a name="add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包
 在 source.extension.vsixmanifest 文件在 VSIX 项目中，添加对向导项目的引用，以便它与包含项目项的 VSIX 包一起部署。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>若要将向导添加到 VSIX 包

1. 在**解决方案资源管理器**，打开快捷菜单，从**source.extension.vsixmanifest** CustomActionProjectItem 项目中的文件，然后选择**打开**打开清单编辑器中的文件。

2. 在清单编辑器中，选择**资产**选项卡，然后选择**新建**按钮。

     **添加新资产**对话框随即出现。

3. 在中**类型**列表中，选择**Microsoft.VisualStudio.Assembly**。

4. 在中**源**列表中，选择**当前解决方案中的项目**。

5. 在中**项目**列表中，选择**ItemTemplateWizard**，然后选择**确定**按钮。

6. 在菜单栏上依次选择**构建** > **生成解决方案**，然后确保该解决方案在编译时没有错误。

## <a name="test-the-wizard"></a>测试向导
 现在您可以对向导进行测试。 首先，请启动要调试 Visual Studio 的实验实例中 CustomActionProjectItem 解决方案。 然后在 Visual Studio 的实验实例中的 SharePoint 项目中测试自定义操作项目项的向导。 最后，生成并运行 SharePoint 项目以验证自定义操作按预期方式正常工作。

#### <a name="to-start-to-debug-the-solution"></a>若要开始调试解决方案

1. 使用管理凭据，重新启动 Visual Studio，然后打开 CustomActionProjectItem 解决方案。

2. 在 ItemTemplateWizard 项目中，打开 CustomActionWizard 代码文件，并将断点添加到代码中的第一行`RunStarted`方法。

3. 在菜单栏上依次选择**调试** > **异常**。

4. 在中**异常**对话框框中，请确保**引发**并**用户未处理**对应的复选框**公共语言运行时异常**已清除，然后选择**确定**按钮。

5. 开始调试通过选择**F5** ，或者，在菜单栏中选择**调试** > **开始调试**。

     Visual Studio 会将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom 操作项目 Item\1.0 并启动 Visual Studio 的实验实例。 在 Visual Studio 的此实例中，将测试项目项。

#### <a name="to-test-the-wizard-in-visual-studio"></a>若要在 Visual Studio 中测试向导

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**文件** > **新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**节点 （具体取决于您的项模板支持的语言），展开**SharePoint**节点，然后选择**2010年**节点。

3. 在项目模板列表中，选择**SharePoint 2010 项目**，将项目命名**CustomActionWizardTest**，然后选择**确定**按钮。

4. 在中**SharePoint 自定义向导**，输入你想要用于调试，站点的 URL，然后选择**完成**按钮。

5. 在中**解决方案资源管理器**，打开项目节点的快捷菜单，选择**添加**，然后选择**新项**。

6. 在中**添加新项-CustomItemWizardTest**对话框框中，展开**SharePoint**节点，然后展开**2010年**节点。

7. 在项目项的列表中，选择**自定义操作**项，，然后选择**添加**按钮。

8. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`RunStarted`方法。

9. 继续调试该项目通过选择**F5**关键的或在菜单栏中选择**调试** > **继续**。

     SharePoint 自定义向导将显示。

10. 下**位置**，选择**列表的编辑**选项按钮。

11. 在中**组 ID**列表中，选择**通信**。

12. 在中**标题**框中，输入**SharePoint 开发人员中心**。

13. 在中**描述**框中，输入**此时将打开 SharePoint 开发人员中心网站**。

14. 在中**URL**框中，输入 **https://docs.microsoft.com/sharepoint/dev/** ，然后选择**完成**按钮。

     Visual Studio 将添加名为的项**CustomAction1**项目并打开*Elements.xml*在编辑器中的文件。 确认*Elements.xml*包含向导中指定的值。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>若要在 SharePoint 中测试自定义操作

1. 在 Visual Studio 的实验实例中，选择**F5**键，或在菜单栏上选择**调试** > **开始调试**。

     打包和部署到 SharePoint 站点指定的自定义操作**站点 URL**属性的项目，并在 web 浏览器将打开到此站点的默认页。

    > [!NOTE]
    > 如果**脚本调试被禁用**出现对话框，请选择**是**按钮。

2. 在 SharePoint 站点列表区域中，选择**任务**链接。

     **任务的所有任务**页将出现。

3. 上**列表工具**选项卡的功能区中，选择**列表**选项卡上，然后在**设置**组中，选择**列表设置**。

     **列表设置**页将出现。

4. 下**通信**标题页的顶部附近，选择**SharePoint 开发人员中心**链接，请验证是否在浏览器打开该网站 https://docs.microsoft.com/sharepoint/dev/，然后关闭浏览器。

## <a name="cleaning-up-the-development-computer"></a>清理开发计算机
 在完成测试的项目项后，从 Visual Studio 的实验实例中删除项目项模板。

#### <a name="to-clean-up-the-development-computer"></a>若要清理开发计算机

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**工具** > **扩展和更新**。

     此时，“扩展和更新”  对话框打开。

2. 在扩展的列表，选择**自定义操作项目项**扩展，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**按钮以确认你要卸载扩展，然后选择**立即重新启动**按钮以完成卸载。

4. 关闭 Visual Studio （实验实例和在其中 CustomActionProjectItem 解决方案已打开的 Visual Studio 的实例） 的两个实例。

## <a name="see-also"></a>请参阅
- [演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [创建项模板和用于 SharePoint 项目项的项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio 模板架构参考](/visualstudio/extensibility/visual-studio-template-schema-reference)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
- [自定义操作的默认位置和 Id](http://go.microsoft.com/fwlink/?LinkId=181964)
