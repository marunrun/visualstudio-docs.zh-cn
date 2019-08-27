---
title: 使用项目模板，第 2 部分中创建站点栏项目项
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
ms.openlocfilehash: 821638c09b64d9cf7045f8985a54cb5e4223d019
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401103"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>演练：使用项目模板，第 2 部分中创建站点栏项目项
  定义自定义类型的 SharePoint 项目项并将其与 Visual Studio 中的项目模板关联后，可能想要为模板提供一个向导。 该向导可用于从用户收集信息，当用户使用模板创建新的项目包含项目项。 可以使用你收集的信息来初始化项目项。

 在本演练中，您将添加一个向导，网站栏项目模板中所示[演练：使用项目模板创建站点栏项目项，第 1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。 当用户创建网站栏项目时，该向导收集有关站点列 （如其基类型和组） 的信息，并添加到此信息*Elements.xml*新项目文件中的。

 本演练演示了下列任务：

- 创建与项目模板关联的自定义 SharePoint 项目项类型的向导。

- 定义自定义向导类似于 Visual Studio 中的 SharePoint 项目中的内置向导的 UI。

- 创建两个*SharePoint 命令*，用于运行向导时调用到本地 SharePoint 站点。 SharePoint 命令是 Visual Studio 扩展可用于在 SharePoint 服务器对象模型中调用 Api 的方法。 有关详细信息，请参阅[调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)。

- 使用可替换参数初始化 SharePoint 项目文件使用此向导中收集的数据。

- 在每个新的网站栏项目实例中创建新的.snk 文件。 此文件用于输出，以便可以将 SharePoint 解决方案程序集部署到全局程序集缓存该项目进行签名。

- 调试和测试该向导。

> [!NOTE]
> 一系列的示例工作流，请参阅[SharePoint 工作流示例](https://docs.microsoft.com/sharepoint/dev/general-development/sharepoint-workflow-samples)。

## <a name="prerequisites"></a>系统必备
 若要执行本演练中，您必须首先创建 SiteColumnProjectItem 解决方案完成[演练：使用项目模板创建站点栏项目项，第 1 部分](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)。

 您还需要完成本演练在开发计算机上的以下组件：

- 支持的 Windows、 SharePoint 和 Visual Studio 版本。

- Visual Studio SDK。 本演练使用**VSIX 项目**中此 SDK 来创建 VSIX 包来部署项目项模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 用于 Visual Studio 中的项目和项模板的向导。 有关详细信息，请参阅[如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)和<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口。

- 在 SharePoint 中的站点列。 有关详细信息，请参阅[列](http://go.microsoft.com/fwlink/?LinkId=183547)。

## <a name="understand-the-wizard-components"></a>了解向导组件
 本演练中演示此向导包含多个组件。 下表描述了这些组件。

|组件|描述|
|---------------|-----------------|
|向导实现|这是一个类，名为`SiteColumnProjectWizard`，它可以实现<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口。 此接口定义 Visual Studio 会在向导启动和完成后，、 在特定时间，同时在向导运行时调用的方法。|
|向导用户界面|这是一个基于 WPF 的窗口，名为`WizardWindow`。 此窗口包含两个用户控件，分别命名为`Page1`和`Page2`。 这些用户控件表示的两个向导页面。<br /><br /> 在此演练中，<xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A>向导实现的方法会显示向导用户界面。|
|向导数据模型|这是一个名为的中间类`SiteColumnWizardModel`，其中提供了向导用户界面和向导实现之间的层。 此示例使用此类来帮助将向导实现和从每个其他; 向导用户界面此类不是所有向导的必需的组件。<br /><br /> 在本演练中，该向导实现将传递`SiteColumnWizardModel`向导窗口时它将显示向导用户界面的对象。 向导 UI 使用此对象的方法将控件的值保存在 UI 中，以及执行任务，如验证输入的站点 URL 有效。 用户完成该向导后，使用该向导实现`SiteColumnWizardModel`对象，以确定用户界面的最终状态。|
|项目签名管理器|这是一个帮助器类，名为`ProjectSigningManager`，用于由向导实现每个新项目实例中创建一个新的 key.snk 文件。|
|SharePoint 命令|这些是向导数据模型用于到本地 SharePoint 站点中运行该向导时调用的方法。 因为 SharePoint 命令必须以.NET Framework 3.5 为目标，这些命令与向导代码的其余部分的不同程序集中实现。|

## <a name="create-the-projects"></a>创建项目
 若要完成本演练，需要将多个项目添加到你在中创建 SiteColumnProjectItem 解决方案[演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md):

- WPF 项目。 将实现<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口，并在此项目中定义的向导 UI。

- 一个定义的 SharePoint 命令的类库项目。 此项目必须面向.net Framework 3.5。

  首先演练创建项目。

#### <a name="to-create-the-wpf-project"></a>创建 WPF 项目

1. 在[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]，打开 SiteColumnProjectItem 解决方案。

2. 在中**解决方案资源管理器**，打开快捷菜单**SiteColumnProjectItem**解决方案节点，选择**添加**，然后选择**新项目**.

3. 在顶部**添加新项目**对话框框中，请确保 **.NET Framework 4.5** .NET Framework 版本的列表中选择。

4. 展开**Visual C#** 节点或**Visual Basic**节点，然后选择**Windows**节点。

5. 在项目模板列表中，选择**WPF 用户控件库**，将项目命名**ProjectTemplateWizard**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**ProjectTemplateWizard**到解决方案，并打开默认 UserControl1.xaml 文件。

6. 从项目中删除 UserControl1.xaml 文件。

#### <a name="to-create-the-sharepoint-commands-project"></a>若要创建 SharePoint 命令项目

1. 在中**解决方案资源管理器**，打开 SiteColumnProjectItem 解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在顶部**添加新项目**对话框框中，选择 **.NET Framework 3.5** .NET Framework 版本的列表中。

3. 展开**Visual C#** 节点或**Visual Basic**节点，然后选择**Windows**节点。

4. 选择**类库**项目模板，请将项目命名**SharePointCommands**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**SharePointCommands**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

## <a name="configure-the-projects"></a>配置项目
 在创建该向导之前，必须添加一些代码文件和项目的程序集引用。

#### <a name="to-configure-the-wizard-project"></a>若要配置向导项目

1. 在中**解决方案资源管理器**，打开快捷菜单**ProjectTemplateWizard**项目节点，然后选择**属性**。

2. 在中**项目设计器**，选择**应用程序**对于 Visual C# 项目的选项卡或**编译**Visual Basic 项目的选项卡。

3. 请确保目标框架设置为.NET Framework 4.5，而非.NET Framework 4.5 客户端配置文件。

     有关详细信息，请参阅[如何：面向 .NET Framework 的某个版本](../ide/how-to-target-a-version-of-the-dotnet-framework.md)。

4. 打开快捷菜单**ProjectTemplateWizard**项目中，选择**添加**，然后选择**新项**。

5. 选择**Window (WPF)** 项，该项**WizardWindow**，然后选择**添加**按钮。

6. 添加两个**用户控件 (WPF)** 项目到项目中，并将它们命名**Page1**并**Page2**。

7. 将四个代码文件添加到项目中，并为其提供以下名称：

    - SiteColumnProjectWizard

    - SiteColumnWizardModel

    - ProjectSigningManager

    - CommandIds

8. 打开快捷菜单**ProjectTemplateWizard**项目节点，然后选择**添加引用**。

9. 展开**程序集**节点，选择**扩展**节点，并选择以下程序集旁的复选框：

    - EnvDTE

    - Microsoft.VisualStudio.OLE.Interop

    - Microsoft.VisualStudio.SharePoint

    - Microsoft.VisualStudio.Shell.11.0

    - Microsoft.VisualStudio.Shell.Interop.10.0

    - Microsoft.VisualStudio.Shell.Interop.11.0

    - Microsoft.VisualStudio.TemplateWizardInterface

10. 选择**确定**按钮将程序集添加到项目。

11. 在中**解决方案资源管理器**下**引用**文件夹**ProjectTemplateWizard**项目中，选择**EnvDTE**。

12. 在中**属性**窗口中，更改的值**嵌入互操作类型**属性设置为**False**。

13. 如果要开发 Visual Basic 项目，ProjectTemplateWizard 命名空间导入你的项目通过使用**项目设计器**。

     有关详细信息，请参阅[如何：添加或删除导入命名空间&#40;Visual Basic&#41;](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md)。

#### <a name="to-configure-the-sharepointcommands-project"></a>若要配置 SharePointcommands 项目

1. 在中**解决方案资源管理器**，选择**SharePointCommands**项目节点。

2. 在菜单栏上依次选择**项目**，**添加现有项**。

3. 在中**添加现有项**对话框中，浏览到包含 ProjectTemplateWizard 项目的代码文件的文件夹，然后选择**CommandIds**代码文件。

4. 选择箭头旁边**外**按钮，，然后选择**添加为链接**上显示的菜单选项。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加到代码文件**SharePointCommands**作为链接的项目。 代码文件位于**ProjectTemplateWizard**还编译项目，但文件中的代码**SharePointCommands**项目。

5. 在中**SharePointCommands**项目中，添加名为命令的另一个代码文件。

6. 选择 SharePointCommands 项目，然后在菜单栏上选择**项目** > **添加引用**。

7. 展开**程序集**节点，选择**扩展**节点，并选择以下程序集旁的复选框：

    - Microsoft.SharePoint

    - Microsoft.VisualStudio.SharePoint.Commands

8. 选择**确定**按钮将程序集添加到项目。

## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>创建向导模型、 签名管理器和 SharePoint 命令 Id
 将代码添加到 ProjectTemplateWizard 项目，以实现示例中的以下组件：

- SharePoint 命令 Id。 这些字符串标识该向导将使用的 SharePoint 命令。 稍后在本演练中，你会将代码添加到 SharePointCommands 项目以实现命令。

- 向导数据模型。

- 项目签名管理器。

  有关这些组件的详细信息，请参阅[了解向导组件](#understand-the-wizard-components)。

#### <a name="to-define-the-sharepoint-command-ids"></a>若要定义的 SharePoint 命令 Id

1. 在 ProjectTemplateWizard 项目中，打开 CommandIds 代码文件，以及然后将此文件的全部内容替换为以下代码。

     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs#5)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb#5)]

#### <a name="to-create-the-wizard-model"></a>若要创建向导模型

1. 打开 SiteColumnWizardModel 代码文件，并且此文件的全部内容替换为以下代码。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb#6)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs#6)]

#### <a name="to-create-the-project-signing-manager"></a>若要创建项目签名管理器

1. 打开 ProjectSigningManager 代码文件，然后将此文件的全部内容替换为以下代码。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb#8)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs#8)]

## <a name="create-the-wizard-ui"></a>创建向导用户界面
 添加 XAML 定义的用户界面的向导窗口和用户界面提供向导页中，两个用户控件并添加代码以定义的窗口和用户控件的行为。 该向导创建类似于 Visual Studio 中的 SharePoint 项目的内置向导。

> [!NOTE]
> 在以下步骤中，项目将具有某些编译错误后将 XAML 或代码添加到你的项目。 在后续步骤中添加代码时，这些错误将消失。

#### <a name="to-create-the-wizard-window-ui"></a>若要创建向导窗口 UI

1. 在 ProjectTemplateWizard 项目中，打开 WizardWindow.xaml 文件的快捷菜单，然后选择**打开**以在设计器中打开窗口。

2. 在设计器的 XAML 视图中，使用以下 XAML 替换当前的 XAML。 XAML 定义包含一个标题的 UI<xref:System.Windows.Controls.Grid>包含向导页，并在窗口底部的导航按钮。

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#10](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml#10)]

    > [!NOTE]
    > 在此 XAML 中创建的窗口派生自<xref:Microsoft.VisualStudio.PlatformUI.DialogWindow>基类。 时向 Visual Studio 添加自定义的 WPF 对话框中，我们建议从为具有与其他 Visual Studio 对话框一致样式并避免可能出现的模式对话框问题此类派生您的对话框。 有关详细信息，请参阅[创建和管理模式对话框](/visualstudio/extensibility/creating-and-managing-modal-dialog-boxes)。

3. 如果要开发 Visual Basic 项目，删除`ProjectTemplateWizard`从命名空间`WizardWindow`中的类名`x:Class`属性的`Window`元素。 此元素是在 XAML 中的第一行中。 完成后，第一行应类似下面的示例。

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. 打开 WizardWindow.xaml 文件的代码隐藏文件。

5. 此文件的内容替换为除`using`声明在该文件，使用以下代码的顶部。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb#4)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs#4)]

#### <a name="to-create-the-first-wizard-page-ui"></a>若要创建第一个向导页 UI

1. 在 ProjectTemplateWizard 项目中，打开 Page1.xaml 文件的快捷菜单，然后选择**打开**以在设计器中打开用户控件。

2. 在设计器的 XAML 视图中，使用以下 XAML 替换当前的 XAML。 XAML 定义包含一个文本框，用户可以在其中输入他们想要用于调试的本地站点的 URL 的 UI。 UI 还包含一些用户可以通过它指定该项目进行沙箱处理的选项按钮。

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#11](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml#11)]

3. 如果你正在开发的 Visual Basic 项目，删除`ProjectTemplateWizard`从命名空间`Page1`中的类名`x:Class`属性的`UserControl`元素。 这是在 XAML 中的第一行中。 完成后，第一行应如以下所示。

    ```xml
    <UserControl x:Class="Page1"
    ```

4. Page1.xaml 文件的内容替换为除`using`声明在该文件，使用以下代码的顶部。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs#2)]

#### <a name="to-create-the-second-wizard-page-ui"></a>若要创建第二个向导页 UI

1. 在 ProjectTemplateWizard 项目中，打开 Page2.xaml 文件的快捷菜单，然后选择**打开**。

     用户控件将在设计器中打开。

2. 在 XAML 视图中，使用以下 XAML 替换当前的 XAML。 XAML 定义包含下拉列表选择网站栏、 用于指定在其下的网站栏显示在库中，内置或自定义组的组合框和文本框中指定的站点列的名称的基类型的 UI。

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#12](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml#12)]

3. 如果你正在开发的 Visual Basic 项目，删除`ProjectTemplateWizard`从命名空间`Page2`中的类名`x:Class`属性的`UserControl`元素。 这是在 XAML 中的第一行中。 完成后，第一行应如以下所示。

    ```xml
    <UserControl x:Class="Page2"
    ```

4. Page2.xaml 文件中，代码隐藏文件的内容替换为除`using`声明在该文件，使用以下代码的顶部。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb#3)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs#3)]

## <a name="implement-the-wizard"></a>实现向导
 通过实现定义向导的主要功能<xref:Microsoft.VisualStudio.TemplateWizard.IWizard>接口。 此接口定义 Visual Studio 会在向导启动和完成后，、 在特定时间，同时在向导运行时调用的方法。

#### <a name="to-implement-the-wizard"></a>若要实现该向导

1. 在 ProjectTemplateWizard 项目中，打开 SiteColumnProjectWizard 代码文件。

2. 此文件的全部内容替换为以下代码。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs#7)]

## <a name="create-the-sharepoint-commands"></a>创建 SharePoint 命令
 创建调入 SharePoint 服务器对象模型的两个自定义命令。 一个命令将确定用户键入在向导中的站点 URL 是否有效。 一个命令获取的所有字段类型从指定的 SharePoint 站点，以便用户可以选择要用作其新站点列的基础。

#### <a name="to-define-the-sharepoint-commands"></a>若要定义的 SharePoint 命令

1. 在中**SharePointCommands**项目中，打开命令的代码文件。

2. 此文件的全部内容替换为以下代码。

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb#9)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs#9)]

## <a name="checkpoint"></a>检查点
 此时在演练中，该向导的所有代码都现项目中。 生成项目，以确保它在编译时没有错误。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 在菜单栏上，依次选择“生成” > “生成解决方案”   。

## <a name="removing-the-keysnk-file-from-the-project-template"></a>从项目模板中删除的 key.snk 文件
 在[演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)，您创建的项目模板包含用于登录网站栏项目的每个实例的 key.snk 文件。 此 key.snk 文件不再必要，因为该向导现在会生成新的 key.snk 文件为每个项目。 从项目模板中删除的 key.snk 文件并删除对此文件的引用。

#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>若要从项目模板中删除的 key.snk 文件

1. 在中**解决方案资源管理器**下**SiteColumnProjectTemplate**节点，打开快捷菜单**key.snk**文件中，，然后选择**删除**.

2. 在出现确认对话框中，选择**确定**按钮。

3. 下**SiteColumnProjectTemplate**节点，打开 SiteColumnProjectTemplate.vstemplate 文件，并从其删除以下元素。

    ```xml
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
    ```

4. 保存并关闭文件。

5. 下**SiteColumnProjectTemplate**节点，打开 ProjectTemplate.csproj 或 ProjectTemplate.vbproj 文件，然后删除以下`PropertyGroup`从它的元素。

    ```xml
    <PropertyGroup>
      <SignAssembly>true</SignAssembly>
      <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
    </PropertyGroup>
    ```

6. 删除以下`None`元素。

    ```xml
    <None Include="key.snk" />
    ```

7. 保存并关闭文件。

## <a name="associating-the-wizard-with-the-project-template"></a>将与项目模板关联向导
 现在，已实现了向导，您必须将关联了向导，并且**站点列**项目模板。 有三个过程必须完成若要执行此操作：

1. 向导程序集具有强名称签名。

2. 获取向导程序集的公钥令牌。

3. 在.vstemplate 文件中添加对向导程序集的引用**站点列**项目模板。

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>为向导程序集具有强名称签名

1. 在中**解决方案资源管理器**，打开快捷菜单**ProjectTemplateWizard**项目，，然后选择**属性**。

2. 上**签名**选项卡上，选择**程序集签名**复选框。

3. 在中**选择强名称密钥文件**列表中，选择 **\<新建...>** 。

4. 在中**创建强名称密钥**对话框框中，输入新的密钥文件的名称，清除**保护密钥文件使用密码**复选框，，然后选择**确定**按钮。

5. 打开快捷菜单**ProjectTemplateWizard**项目，，然后选择**生成**创建 ProjectTemplateWizard.dll 文件。

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>若要获取的公钥令牌向导程序集

1. 上**开始菜单**，选择**所有程序**，选择**Microsoft Visual Studio**，选择**Visual Studio Tools**，然后选择**开发人员命令提示**。

     Visual Studio 命令提示符窗口将打开。

2. 运行以下命令，替换*PathToWizardAssembly*生成 ProjectTemplateWizard.dll ProjectTemplateWizard 项目在开发计算机上的程序集的完整路径：

    ```cmd
    sn.exe -T PathToWizardAssembly
    ```

     ProjectTemplateWizard.dll 程序集的公钥标记写入到 Visual Studio 命令提示符窗口。

3. Visual Studio 命令提示符窗口保持打开。 在下一个过程中，将需要公钥标记。

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>若要添加的.vstemplate 文件中的向导程序集的引用

1. 在中**解决方案资源管理器**，展开**SiteColumnProjectTemplate**项目节点，然后打开 SiteColumnProjectTemplate.vstemplate 文件。

2. 在文件末尾附近添加以下`WizardExtension`之间的元素`</TemplateContent>`和`</VSTemplate>`标记。 替换*你的令牌*的值`PublicKeyToken`与上一步骤中获取的公钥标记的属性。

    ```xml
    <WizardExtension>
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>
    </WizardExtension>
    ```

     有关详细信息`WizardExtension`元素，请参阅[WizardExtension 元素&#40;Visual Studio 模板&#41;](/visualstudio/extensibility/wizardextension-element-visual-studio-templates)。

3. 保存并关闭文件。

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>将可替换参数添加到项目模板中的 Elements.xml 文件
 添加到多个可替换参数*Elements.xml* SiteColumnProjectTemplate 项目文件中的。 在初始化这些参数`RunStarted`中的方法`SiteColumnProjectWizard`前面定义的类。 当用户创建网站栏项目时，Visual Studio 将自动替换中的这些参数*Elements.xml*文件在新项目中使用它们在向导中指定的值。

 可替换参数是开始和结束的美元符号 （$） 字符的标记。 除了定义自己的可替换参数，可以使用内置参数定义和初始化 SharePoint 项目系统。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>要添加到 Elements.xml 文件的可替换参数

1. 在 SiteColumnProjectTemplate 项目中，替换的内容*Elements.xml*使用以下 XML 文件。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
             Name="$fieldname$"
             DisplayName="$fieldname$"
             Type="$selectedfieldtype$"
             Group="$selectedgrouptype$">
      </Field>
    </Elements>
    ```

     新的 XML 更改的值`Name`， `DisplayName`， `Type`，和`Group`向自定义可替换参数属性。

2. 保存并关闭文件。

## <a name="add-the-wizard-to-the-vsix-package"></a>将向导添加到 VSIX 包
 若要部署使用包含网站栏项目模板的 VSIX 包向导，将对向导项目和 SharePoint 命令项目的引用添加到 VSIX 项目中的 source.extension.vsixmanifest 文件中。

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>若要将向导添加到 VSIX 包

1. 在中**解决方案资源管理器**，在**SiteColumnProjectItem**项目中，打开快捷菜单**source.extension.vsixmanifest**文件，，然后选择**打开**。

     Visual Studio 清单编辑器中打开该文件。

2. 上**资产**选项卡的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即打开。

3. 在中**类型**列表中，选择**Microsoft.VisualStudio.Assembly**。

4. 在中**源**列表中，选择**当前解决方案中的项目**。

5. 在中**项目**列表中，选择**ProjectTemplateWizard**，然后选择**确定**按钮。

6. 上**资产**选项卡的编辑器中，选择**新建**按钮再次。

     **添加新资产**对话框随即打开。

7. 在中**类型**列表中，输入**SharePoint.Commands.v4**。

8. 在中**源**列表中，选择**当前解决方案中的项目**。

9. 在中**项目**列表中，选择**SharePointCommands**项目，，然后选择**确定**按钮。

10. 在菜单栏上依次选择**构建** > **生成解决方案**，并确保正确生成解决方案。

## <a name="test-the-wizard"></a>测试向导
 现在您可以对向导进行测试。 首先，开始调试 Visual Studio 的实验实例中的 SiteColumnProjectItem 解决方案。 然后，Visual Studio 的实验实例中测试的网站栏项目的向导。 最后，生成并运行项目以验证站点列按预期方式正常工作。

#### <a name="to-start-debugging-the-solution"></a>若要开始调试解决方案

1. 使用管理凭据，重新启动 Visual Studio，然后打开 SiteColumnProjectItem 解决方案。

2. 在 ProjectTemplateWizard 项目中，打开 SiteColumnProjectWizard 代码文件，并将断点添加到代码中的第一行`RunStarted`方法。

3. 在菜单栏上依次选择**调试** > **异常**。

4. 在中**异常**对话框框中，请确保**引发**并**用户未处理**对应的复选框**公共语言运行时异常**已清除，然后选择**确定**按钮。

5. 开始调试通过选择**F5**关键的或在菜单栏中选择**调试** > **开始调试**。

     Visual Studio 会将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0 并启动 Visual Studio 的实验实例。 在 Visual Studio 的此实例中，将测试项目项。

#### <a name="to-test-the-wizard-in-visual-studio"></a>若要在 Visual Studio 中测试向导

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**文件** > **新建** > **项目**。

2. 展开**Visual C#** 节点或**Visual Basic**节点 （具体取决于你的项目模板支持的语言），展开**SharePoint**节点，然后选择**2010年**节点。

3. 在项目模板列表中，选择**网站栏**，将项目命名**SiteColumnWizardTest**，然后选择**确定**按钮。

4. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`RunStarted`方法。

5. 继续调试该项目通过选择**F5**关键的或在菜单栏中选择**调试** > **继续**。

6. 在中**SharePoint 自定义向导**，输入你想要用于调试，站点的 URL，然后选择**下一步**按钮。

7. 中的第二页**SharePoint 自定义向导**，进行以下选择：

   - 在中**类型**列表中，选择**布尔**。

   - 在中**组**列表中，选择**自定义否列**。

   - 在中**名称**框中，输入**我否列**，然后选择**完成**按钮。

     中**解决方案资源管理器**，新的项目出现，其中包含名为一个项目项**Field1**，并打开项目的 Visual Studio *Elements.xml*在编辑器中的文件。

8. 确认*Elements.xml*包含向导中指定的值。

#### <a name="to-test-the-site-column-in-sharepoint"></a>若要在 SharePoint 中测试的网站栏

1. 在 Visual Studio 的实验实例中，选择**F5**密钥。

     为打包的站点列并将其部署到 SharePoint 站点**站点 URL**项目的属性指定。 Web 浏览器打开到此站点的默认页。

    > [!NOTE]
    > 如果**脚本调试被禁用**出现对话框，请选择**是**按钮以继续调试项目。

2. 上**站点操作**菜单中，选择**站点设置**。

3. 在站点设置页下**库**，选择**站点列**链接。

4. 在站点列的列表中，验证是否**自定义否列**组中包含的列，名为**我否列**，然后关闭 web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 在完成测试的项目项后，从 Visual Studio 的实验实例中删除的项目模板。

#### <a name="to-clean-up-the-development-computer"></a>若要清理开发计算机

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**工具** > **扩展和更新**。

     此时，“扩展和更新”  对话框打开。

2. 在扩展的列表，选择**网站栏**，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**按钮以确认你要卸载扩展，然后选择**立即重新启动**按钮以完成卸载。

4. 关闭 Visual Studio 的实验实例和在其中 CustomActionProjectItem 解决方案已打开的实例。

     有关如何部署信息[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展，请参阅[传送 Visual Studio 扩展](/visualstudio/extensibility/shipping-visual-studio-extensions)。

## <a name="see-also"></a>请参阅
- [演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [为 SharePoint 项目项创建项模板和项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Visual Studio 模板架构参考](/visualstudio/extensibility/visual-studio-template-schema-reference)
- [如何：使用向导来处理项目模板](../extensibility/how-to-use-wizards-with-project-templates.md)
