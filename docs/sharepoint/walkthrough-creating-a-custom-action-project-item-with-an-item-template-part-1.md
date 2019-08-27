---
title: 使用项模板，第 1 部分创建自定义操作项目项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 3e00d87079fe4986dc378540c1456508c2afa0b7
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66401119"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-1"></a>演练：使用项模板，第 1 部分创建自定义操作项目项
  可以通过创建你自己的项目项类型来扩展 Visual Studio 中的 SharePoint 项目系统。 在本演练中，将创建可以添加到 SharePoint 项目，以便在 SharePoint 站点上创建自定义操作项目项。 自定义操作添加的菜单项**站点操作**菜单中的 SharePoint 站点。

 本演练演示了下列任务：

- 创建 Visual Studio 扩展中定义自定义操作的 SharePoint 项目项的新类型。 新的项目项类型实现多个自定义功能：

  - 快捷菜单，具有与项目项，例如，在 Visual Studio 中显示用于自定义操作的设计器相关的其他任务的起始点。

  - 开发人员更改某些属性的项目项和包含它的项目时运行的代码。

  - 在项目项的旁边显示一个自定义图标**解决方案资源管理器**。

- 创建项目项的 Visual Studio 项模板。

- 生成 Visual Studio 扩展 (VSIX) 包部署的项目项模板和扩展插件程序集。

- 调试和测试的项目项。

  这是一个独立的演练。 完成本演练后，您可以通过将一个向导添加到项模板增强的项目项。 有关详细信息，请参见[演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

> [!NOTE]
> 您可以下载的示例[Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) ，演示如何创建自定义工作流活动。

## <a name="prerequisites"></a>系统必备
 需要要完成本演练的开发计算机上安装以下组件：

- 支持的 Microsoft Windows、 SharePoint 和 Visual Studio 版本。

- [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] 本演练使用**VSIX 项目**中此 SDK 来创建 VSIX 包来部署项目项模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 在 SharePoint 中的自定义操作。 有关详细信息，请参阅[自定义操作](http://go.microsoft.com/fwlink/?LinkId=177800)。

- 在 Visual Studio 中的项模板。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练中，您需要创建三个项目：

- 一个 VSIX 项目。 此项目创建 VSIX 包以部署 SharePoint 项目项。

- 项模板项目。 此项目将创建可用于将 SharePoint 项目项添加到 SharePoint 项目项模板。

- 一个类库项目。 此项目实现 Visual Studio 扩展中定义的 SharePoint 项目项的行为。

  首先演练创建项目。

#### <a name="to-create-the-vsix-project"></a>若要创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件”   > “新建”   > “项目”  。

3. 在顶部的列表**新的项目**对话框框中，请确保 **.NET Framework 4.5**处于选中状态。

4. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**扩展性**节点。

    > [!NOTE]
    > **扩展性**节点是安装 Visual Studio SDK 的情况下才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

5. 选择**VSIX 项目**模板。

6. 在中**名称**框中，输入**CustomActionProjectItem**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**CustomActionProjectItem**投影到**解决方案资源管理器**。

#### <a name="to-create-the-item-template-project"></a>若要创建项模板项目

1. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在顶部的列表**新的项目**对话框框中，请确保 **.NET Framework 4.5**处于选中状态。

3. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，然后选择**扩展性**节点。

4. 在项目模板列表中，选择**C# 项模板**或**Visual Basic 项模板**模板。

5. 在中**名称**框中，输入**ItemTemplate**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**ItemTemplate**到解决方案。

#### <a name="to-create-the-extension-project"></a>若要创建扩展项目

1. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在顶部的列表**新的项目**对话框框中，请确保 **.NET Framework 4.5**处于选中状态。

3. 在中**新的项目**对话框框中，展开**Visual C#** 或**Visual Basic**节点，选择**Windows**节点，然后选择**类库**项目模板。

4. 在中**名称**框中，输入**ProjectItemDefinition**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**ProjectItemDefinition**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 在编写代码以定义 SharePoint 项目项类型之前，必须添加代码文件和程序集引用的扩展项目。

#### <a name="to-configure-the-project"></a>若要配置项目

1. 在中**解决方案资源管理器**，打开快捷菜单**ProjectItemDefinition**项目中，选择**添加**，然后选择**新项**。

2. 在项目项的列表中，选择**代码文件**。

3. 在中**名称**框中，输入名称**CustomAction**具有相应文件扩展名，，然后选择**添加**按钮。

4. 在中**解决方案资源管理器**，打开快捷菜单**ProjectItemDefinition**项目，，然后选择**添加引用**。

5. 在中**引用管理器-ProjectItemDefinition**对话框框中，选择**程序集**节点，然后选择**Framework**节点。

6. 选择以下程序集的每个旁边的复选框：

    - System.ComponentModel.Composition

    - System.Windows.Forms

7. 选择**扩展**节点，选择 Microsoft.VisualStudio.Sharepoint 程序集，旁边的复选框，然后选择**确定**按钮。

## <a name="define-the-new-sharepoint-project-item-type"></a>定义新的 SharePoint 项目项类型
 创建一个实现类<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>接口可定义新的项目项类型的行为。 实现此接口，只要您想要定义新的项目项类型。

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>若要定义新的 SharePoint 项目项类型

1. 在 ProjectItemDefinition 项目中，打开 CustomAction 代码文件。

2. 此文件中的代码替换为以下代码。

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#1](../sharepoint/codesnippet/CSharp/customactionprojectitem/projectitemtypedefinition/customaction.cs#1)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#1](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/projectitemdefinition/customaction.vb#1)]

## <a name="create-an-icon-for-the-project-item-in-solution-explorer"></a>在解决方案资源管理器中创建的项目项的图标
 创建自定义 SharePoint 项目项时，您可以与项目项关联图像 （图标或位图）。 此图像中项目项的旁边会出现**解决方案资源管理器**。

 在下面的过程中，创建项目项的图标和图标嵌入扩展插件程序集。 引用此图标<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute>的`CustomActionProjectItemTypeProvider`前面创建的类。

#### <a name="to-create-a-custom-icon-for-the-project-item"></a>若要创建的项目项的自定义图标

1. 在中**解决方案资源管理器**，打开快捷菜单**ProjectItemDefinition**项目中，选择**添加**，然后选择**新项...** .

2. 在项目项的列表中，选择**图标文件**项。

    > [!NOTE]
    > 在 Visual Basic 项目中，您必须选择**常规**节点以显示**图标文件**项。

3. 在中**名称**框中，输入**CustomAction_SolutionExplorer.ico**，然后选择**添加**按钮。

     在中打开新建图标**的图像编辑器**。

4. 编辑图标文件的 16 x 16 版本，使它具有可以识别，并保存该图标文件的设计。

5. 在中**解决方案资源管理器**，选择**CustomAction_SolutionExplorer.ico**。

6. 在中**属性**窗口中，选择箭头旁边**生成操作**属性。

7. 在显示的列表，选择**嵌入的资源**。

## <a name="checkpoint"></a>检查点
 此时在演练中，项目项的所有代码都现项目中。 生成项目以验证它在编译时没有错误。

#### <a name="to-build-your-project"></a>若要生成你的项目

1. 打开快捷菜单**ProjectItemDefinition**项目，然后选择**生成**。

## <a name="create-a-visual-studio-item-template"></a>创建 Visual Studio 项模板
 若要启用其他开发人员能够使用您的项目项，必须创建项目模板或项模板。 开发人员在 Visual Studio 中使用这些模板创建项目项的实例，通过创建一个新项目，或通过将项添加到现有项目。 对于本演练中，使用 ItemTemplate 项目配置您的项目项。

#### <a name="to-create-the-item-template"></a>若要创建项模板

1. 从 ItemTemplate 项目删除 Class1 代码文件。

2. 在项模板项目中，打开*ItemTemplate.vstemplate*文件。

3. 该文件的内容替换为以下 XML，然后保存并关闭文件。

    > [!NOTE]
    > 以下 XML 是为 Visual C# 项模板。 如果要创建 Visual Basic 项模板的值替换`ProjectType`具有元素`VisualBasic`。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
      <TemplateData>
        <DefaultName>CustomAction</DefaultName>
        <Name>Custom Action</Name>
        <Description>SharePoint Custom Action by Contoso</Description>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>1000</SortOrder>
        <Icon>ItemTemplate.ico</Icon>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
      <TemplateContent>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\Elements.xml">Elements.xml</ProjectItem>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\SharePointProjectItem.spdata">CustomAction.spdata</ProjectItem>
      </TemplateContent>
    </VSTemplate>
    ```

     此文件定义的内容和项模板的行为。 此文件的内容的详细信息，请参阅[Visual Studio 模板架构引用](/visualstudio/extensibility/visual-studio-template-schema-reference)。

4. 在中**解决方案资源管理器**，打开快捷菜单**ItemTemplate**项目中，选择**添加**，然后选择**新项**。

5. 在中**添加新项**对话框框中，选择**文本文件**模板。

6. 在中**名称**框中，输入**CustomAction.spdata**，然后选择**添加**按钮。

7. 添加到下面的 XML *CustomAction.spdata*文件，然后保存并关闭该文件。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ProjectItem Type="Contoso.CustomAction" DefaultFile="Elements.xml"
     xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
      <Files>
        <ProjectItemFile Source="Elements.xml" Target="$fileinputname$\" Type="ElementManifest" />
      </Files>
    </ProjectItem>
    ```

     此文件包含有关所包含的项目项文件的信息。 `Type`的属性`ProjectItem`元素必须设置为相同的字符串传递给<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>项目项定义上 (`CustomActionProjectItemTypeProvider`之前在本演练中创建的类)。 详细了解的内容 *.spdata*文件，请参阅[SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。

8. 在中**解决方案资源管理器**，打开快捷菜单**ItemTemplate**项目中，选择**添加**，然后选择**新项**。

9. 在中**添加新项**对话框框中，选择**XML 文件**模板。

10. 在中**名称**框中，输入**Elements.xml**，然后选择**添加**按钮。

11. 内容替换为*Elements.xml*文件用下列 XML，然后保存并关闭该文件。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="Replace this with a GUID or some other unique string"
                    GroupId="SiteActions"
                    Location="Microsoft.SharePoint.StandardMenu"
                    Sequence="1000"
                    Title="Replace this with your title"
                    Description="Replace this with your description" >
        <UrlAction Url="~site/Lists/Tasks/AllItems.aspx"/>
      </CustomAction>
    </Elements>
    ```

     此文件定义创建的菜单项的默认自定义操作**站点操作**菜单中的 SharePoint 站点。 当用户选择菜单项时，URL 中指定`UrlAction`元素将在 web 浏览器中打开。 有关可用于定义自定义操作的 XML 元素的详细信息，请参阅[自定义操作定义](http://go.microsoft.com/fwlink/?LinkId=177801)。

12. （可选） 打开*ItemTemplate.ico*文件，并对其进行修改，以便它具有可以识别的设计。 此图标将显示在项目项旁边**添加新项**对话框。

13. 在中**解决方案资源管理器**，打开快捷菜单**ItemTemplate**项目，，然后选择**卸载项目**。

14. 打开快捷菜单**ItemTemplate**同样，项目，然后选择**编辑 ItemTemplate.csproj**或**编辑 ItemTemplate.vbproj**。

15. 找到以下`VSTemplate`项目文件中的元素。

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
    ```

16. 将此替换`VSTemplate`元素使用以下 XML 中，然后保存并关闭文件。

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素指定其他文件夹中生成项目时在其下创建项模板的路径。 此处指定的文件夹确保，仅当客户打开的项模板将在可用**添加新项**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

17. 在中**解决方案资源管理器**，打开快捷菜单**ItemTemplate**项目，，然后选择**重新加载项目**。

## <a name="create-a-vsix-package-to-deploy-the-project-item"></a>创建 VSIX 包来部署项目项
 若要将扩展部署，使用 VSIX 项目在解决方案中创建 VSIX 包。 首先，通过修改包含在 VSIX 项目的 source.extension.vsixmanifest 文件中配置 VSIX 包。 然后，通过生成解决方案中创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>若要配置和创建 VSIX 包

1. 在中**解决方案资源管理器**，打开快捷菜单**source.extension.vsixmanifest** CustomActionProjectItem 项目中的文件，然后选择**打开**。

     Visual Studio 清单编辑器中打开该文件。 在 source.extension.vsixmanifest 文件是所有 VSIX 包都需要 extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅[VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在中**产品名称**框中，输入**自定义操作项目项**。

3. 在中**作者**框中，输入**Contoso**。

4. 在中**描述**框中，输入**表示自定义操作的 SharePoint 项目项**。

5. 上**资产**选项卡上，选择**新建**按钮。

     **添加新资产**对话框随即出现。

6. 在中**类型**列表中，选择**Microsoft.VisualStudio.ItemTemplate**。

    > [!NOTE]
    > 此值对应于`ItemTemplate`extension.vsixmanifest 文件中的元素。 此元素标识的子文件夹中包含的项目项模板的 VSIX 包。 有关详细信息，请参阅[ItemTemplate 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))。

7. 在中**源**列表中，选择**当前解决方案中的项目**。

8. 在中**项目**列表中，选择**ItemTemplate**，然后选择**确定**按钮。

9. 在中**资产**选项卡上，选择**新建**按钮再次。

     **添加新资产**对话框随即出现。

10. 在中**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。

    > [!NOTE]
    > 此值对应于`MefComponent`extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中的扩展插件程序集名称。 有关详细信息，请参阅[MEFComponent 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

11. 在中**源**列表中，选择**当前解决方案中的项目**。

12. 在中**项目**列表中，选择**ProjectItemDefinition**。

13. 选择“确定”  按钮。

14. 在菜单栏上依次选择**构建** > **生成解决方案**，然后确保该项目在编译时没有错误。

15. 请确保 CustomActionProjectItem 项目的生成输出文件夹包含 CustomActionProjectItem.vsix 文件。

     默认情况下，生成输出文件夹是...包含 CustomActionProjectItem 项目文件夹下的 \bin\Debug 文件夹。

## <a name="test-the-project-item"></a>测试项目项
 现在你可以进行测试的项目项。 首先，开始调试 Visual Studio 的实验实例中的 CustomActionProjectItem 解决方案。 然后，测试**自定义操作**Visual Studio 的实验实例中的 SharePoint 项目中的项目项。 最后，生成并运行 SharePoint 项目以验证自定义操作按预期方式正常工作。

#### <a name="to-start-debugging-the-solution"></a>若要开始调试解决方案

1. 使用管理凭据，重新启动 Visual Studio，然后打开 CustomActionProjectItem 解决方案。

2. 打开 CustomAction 代码文件，并将断点添加到代码中的第一行`InitializeType`方法。

3. 选择**F5**键启动调试。

     Visual Studio 会将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Custom 操作项目 Item\1.0 并启动 Visual Studio 的实验实例。 在 Visual Studio 的此实例中，将测试项目项。

#### <a name="to-test-the-project-item-in-visual-studio"></a>若要在 Visual Studio 中测试的项目项

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**文件** > **新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic** （具体取决于您的项模板支持的语言），展开**SharePoint**，然后选择**2010年**节点。

3. 在项目模板列表中，选择**SharePoint 2010 项目**。

4. 在中**名称**框中，输入**CustomActionTest**，然后选择**确定**按钮。

5. 在中**SharePoint 自定义向导**，输入你想要用于调试，站点的 URL，然后选择**完成**按钮。

6. 在中**解决方案资源管理器**，打开项目节点的快捷菜单，选择**添加**，然后选择**新项**。

7. 在中**添加新项**对话框框中，选择**2010年**节点下的**SharePoint**节点。

     确认**自定义操作**项出现在项目项的列表。

8. 选择**自定义操作**项，，然后选择**添加**按钮。

     Visual Studio 将添加名为的项**CustomAction1**项目并打开*Elements.xml*在编辑器中的文件。

9. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`InitializeType`方法。

10. 选择**F5**键继续调试项目。

11. 在 Visual Studio 的实验实例中**解决方案资源管理器**，打开快捷菜单**CustomAction1**节点，然后选择**视图自定义操作设计器**.

12. 确认消息框出现，然后选择**确定**按钮。

     此快捷菜单可用于为开发人员，例如，显示用于自定义操作的设计器提供其他选项或命令。

13. 在菜单栏上依次选择**视图** > **输出**。

     **输出**窗口随即打开。

14. 在中**解决方案资源管理器**，打开快捷菜单**CustomAction1**项，然后其名称更改为**MyCustomAction**。

     在中**输出**窗口中，将显示一条确认消息。 此消息写入由<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemNameChanged>中定义的事件处理程序`CustomActionProjectItemTypeProvider`类。 您可以处理此事件和其他项目项事件，以实现自定义行为时，开发人员修改的项目项。

#### <a name="to-test-the-custom-action-in-sharepoint"></a>若要在 SharePoint 中测试自定义操作

1. 在 Visual Studio 的实验实例中，打开*Elements.xml*的子文件**MyCustomAction**项目项。

2. 在中*Elements.xml*文件，进行以下更改，然后保存该文件：

    - 在中`CustomAction`元素中，设置`Id`属性为 GUID 或其他唯一的字符串，如以下示例所示：

        ```xml
        Id="cd85f6a7-af2e-44ab-885a-0c795b52121a"
        ```

    - 在中`CustomAction`元素中，设置`Title`属性，如以下示例所示：

        ```xml
        Title="SharePoint Developer Center"
        ```

    - 在中`CustomAction`元素中，设置`Description`属性，如以下示例所示：

        ```xml
        Description="Opens the SharePoint Developer Center Web site."
        ```

    - 在中`UrlAction`元素中，设置`Url`属性，如以下示例所示：

        ```xml
        Url="https://docs.microsoft.com/sharepoint/dev/"
        ```

3. 选择 F5  。

     打包和部署到 SharePoint 站点中指定的自定义操作**站点 URL**项目的属性。 Web 浏览器打开到此站点的默认页。

    > [!NOTE]
    > 如果**脚本调试被禁用**出现对话框，请选择**是**按钮以继续调试项目。

4. 上**站点操作**菜单中，选择**SharePoint 开发人员中心**，验证是否在浏览器打开该网站 https://docs.microsoft.com/sharepoint/dev/，然后关闭 web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 在完成测试的项目项后，从 Visual Studio 的实验实例中删除项目项模板。

#### <a name="to-clean-up-the-development-computer"></a>若要清理开发计算机

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**工具** > **扩展和更新**。

     此时，“扩展和更新”  对话框打开。

2. 在扩展的列表，选择**自定义操作项目项**，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**按钮以确认你想要卸载扩展。

4. 选择**立即重新启动**按钮以完成卸载。

5. 关闭 Visual Studio 的实验实例和在其中 CustomActionProjectItem 解决方案已打开的实例。

## <a name="next-steps"></a>后续步骤
 完成本演练后，可以将向导添加到项模板。 当用户将自定义操作项目项添加到 SharePoint 项目时，则向导会收集有关的操作 （如其位置和操作选择时要导航到的 URL） 的信息，并添加到此信息*Elements.xml*中新的项目项文件。 有关详细信息，请参见[演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

## <a name="see-also"></a>请参阅

- [演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [创建项模板和用于 SharePoint 项目项的项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [使用 SharePoint 项目服务](../sharepoint/using-the-sharepoint-project-service.md)
- [Visual Studio 模板架构参考](/visualstudio/extensibility/visual-studio-template-schema-reference)
- [图标的图像编辑器](/cpp/windows/image-editor-for-icons)
- [创建图标或其他图像&#40;图标的图像编辑器&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)