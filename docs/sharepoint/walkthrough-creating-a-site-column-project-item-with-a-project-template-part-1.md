---
title: 使用项目模板，第 1 部分创建站点栏项目项
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint projects, creating custom templates
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 60e4f4e035b381b8bfda8e14ee705471b0fad2b8
ms.sourcegitcommit: 13ab9a5ab039b070b9cd9251d0b83dd216477203
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177565"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-1"></a>演练：使用项目模板，第 1 部分创建站点栏项目项
  SharePoint 项目是针对一个或多个 SharePoint 项目项的容器。 可以通过创建自己的 SharePoint 项目项类型，然后将其关联到的项目模板来扩展 Visual Studio 中的 SharePoint 项目系统。 在此演练中，将为创建网站栏中，定义项目项类型，然后将创建可用于创建包含网站栏项目项的新项目的项目模板。

 本演练演示了下列任务：

- 创建 Visual Studio 扩展中定义一种新的站点列的 SharePoint 项目项。 项目项类型包括一个简单的自定义属性中显示**属性**窗口。

- 创建[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]项目项的项目模板。

- 构建[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]要部署的项目模板和扩展插件程序集的扩展 (VSIX) 包。

- 调试和测试的项目项。

  这是一个独立的演练。 完成本演练后，您可以将向导添加到项目模板来增强项目项。 有关详细信息，请参见[演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

> [!NOTE]
> 一系列的示例工作流，请参阅[SharePoint 工作流示例](https://docs.microsoft.com/sharepoint/dev/general-development/sharepoint-workflow-samples)。

## <a name="prerequisites"></a>系统必备
 需要要完成本演练的开发计算机上安装以下组件：

- 支持的 Microsoft Windows，SharePoint 版本和[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

- [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)] 本演练使用**VSIX 项目**中此 SDK 来创建 VSIX 包来部署项目项模板。 有关详细信息，请参阅[扩展 Visual Studio 中的 SharePoint 工具](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)。

  了解以下概念很有帮助，但不是必需，若要完成本演练：

- 在 SharePoint 中的站点列。 有关详细信息，请参阅[列](http://go.microsoft.com/fwlink/?LinkId=183547)。

- 在 Visual Studio 中的项目模板。 有关详细信息，请参阅[创建项目和项模板](../ide/creating-project-and-item-templates.md)。

## <a name="create-the-projects"></a>创建项目
 若要完成本演练中，您需要创建三个项目：

- 一个 VSIX 项目。 此项目创建 VSIX 包来部署站点栏项目项和项目模板。

- 项目模板项目。 此项目创建可用于创建新的 SharePoint 项目包含网站栏项目项的项目模板。

- 一个类库项目。 此实现定义的网站栏项目项的行为的 Visual Studio 扩展的项目。

  首先演练创建项目。

#### <a name="to-create-the-vsix-project"></a>若要创建 VSIX 项目

1. 启动 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

2. 在菜单栏上，依次选择“文件” > “新建” > “项目”。

3. 在顶部**新的项目**对话框框中，请确保 **.NET Framework 4.5** .NET Framework 版本的列表中选择。

4. 展开**Visual Basic**或**Visual C#** 节点，然后选择**扩展性**节点。

    > [!NOTE]
    > **扩展性**节点是安装 Visual Studio SDK 的情况下才可用。 有关详细信息，请参阅本主题前面的先决条件部分。

5. 在项目模板列表中，选择**VSIX 项目**。

6. 在中**名称**框中，输入**SiteColumnProjectItem**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**SiteColumnProjectItem**投影到**解决方案资源管理器**。

#### <a name="to-create-the-project-template-project"></a>若要创建项目模板项目

1. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在顶部**新的项目**对话框框中，请确保 **.NET Framework 4.5** .NET Framework 版本的列表中选择。

3. 展开**Visual C#** 或**Visual Basic**节点，然后选择**扩展性**节点。

4. 在项目模板列表中，选择**C# 项目模板**或**Visual Basic 项目模板**模板。

5. 在中**名称**框中，输入**SiteColumnProjectTemplate**，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**SiteColumnProjectTemplate**到解决方案。

6. 从项目中删除的 Class1 代码文件。

7. 如果创建了 Visual Basic 项目，还从项目中删除以下文件：

    - *MyApplication.Designer.vb*

    - MyApplication.myapp

    - *Resources.Designer.vb*

    - *Resources.resx*

    - *Settings.Designer.vb*

    - Settings.settings

#### <a name="to-create-the-extension-project"></a>若要创建扩展项目

1. 在中**解决方案资源管理器**，打开解决方案节点的快捷菜单，选择**添加**，然后选择**新项目**。

2. 在顶部**新的项目**对话框框中，请确保 **.NET Framework 4.5** .NET Framework 版本的列表中选择。

3. 展开**Visual C#** 或**Visual Basic**节点，选择**Windows**节点，然后选择**类库**模板。

4. 在中**名称**框中，输入**ProjectItemTypeDefinition** ，然后选择**确定**按钮。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 将添加**ProjectItemTypeDefinition**到解决方案并打开默认 Class1 代码文件。

5. 从项目中删除的 Class1 代码文件。

## <a name="configure-the-extension-project"></a>配置扩展项目
 添加代码文件和程序集引用，若要配置扩展项目。

#### <a name="to-configure-the-project"></a>若要配置项目

1. 在 ProjectItemTypeDefinition 项目中，添加一个文件，其中名为**SiteColumnProjectItemTypeProvider**。

2. 在菜单栏上，选择“项目” > “添加引用”。

3. 在中**引用管理器-ProjectItemTypeDefinition**对话框框中，展开**程序集**节点，选择**Framework**节点，并选择System.ComponentModel.Composition 复选框。

4. 选择**扩展**节点，选择 Microsoft.VisualStudio.SharePoint 程序集，旁边的复选框，然后选择**确定**按钮。

## <a name="define-the-new-sharepoint-project-item-type"></a>定义新的 SharePoint 项目项类型
 创建一个实现类<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>接口可定义新的项目项类型的行为。 实现此接口，只要您想要定义新的项目项类型。

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>若要定义新的 SharePoint 项目项类型

1. 在中**SiteColumnProjectItemTypeProvider**代码文件，默认代码替换为以下代码，并保存该文件。

     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#1](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.cs#1)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#1](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projectitemtypedefinition/sitecolumnprojectitemtypeprovider.vb#1)]

## <a name="create-a-visual-studio-project-template"></a>创建 Visual Studio 项目模板
 通过创建项目模板，可以启用其他开发人员可以创建包含站点栏项目项的 SharePoint 项目。 SharePoint 项目模板包括所需的所有项目在 Visual Studio 中，如文件 *.csproj*或 *.vbproj*并 *.vstemplate*文件，并保护的文件是特定于 SharePoint 项目。 有关详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

 在此过程中，创建空 SharePoint 项目来生成特定于 SharePoint 项目的文件。 您将添加这些文件到 SiteColumnProjectTemplate 项目，以便它们包含在此项目中生成的模板。 您还配置 SiteColumnProjectTemplate 项目文件来指定项目模板中的显示位置**新的项目**对话框。

#### <a name="to-create-the-files-for-the-project-template"></a>若要创建项目模板文件

1. 启动的第二个实例[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]具有管理凭据。

2. 创建名为 SharePoint 2010 项目**BaseSharePointProject**。

   > [!IMPORTANT]
   > 在中**SharePoint 自定义向导**，不选择**部署为场解决方案**选项按钮。

3. 将空元素项添加到项目中，并将其命名为项**Field1**。

4. 保存项目，然后关闭第二个实例[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]。

5. 实例中[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]SiteColumnProjectItem 解决方案打开，在具有**解决方案资源管理器**，打开快捷菜单**SiteColumnProjectTemplate**项目节点，选择**添加**，然后选择**现有项**。

6. 在中**添加现有项**对话框中，打开的文件扩展名的列表，然后选择**的所有文件 (\*。\*)** .

7. 在目录中包含 BaseSharePointProject 项目，选择 key.snk 文件，然后选择**添加**按钮。

   > [!NOTE]
   > 在本演练中，您创建的项目模板使用相同的 key.snk 文件进行签名使用模板创建的每个项目。 若要了解如何扩展此示例，以便创建不同的 key.snk 文件，为每个项目实例，请参阅[演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

8. 重复步骤 5-8，从 BaseSharePointProject 目录中指定的子文件夹中添加以下文件：

   - *\Field1\Elements.xml*

   - *\Field1\SharePointProjectItem.spdata*

   - *\Features\Feature1\Feature1.feature*

   - *\Features\Feature1\Feature1.Template.xml*

   - *\Package\Package.package*

   - *\Package\Package.Template.xml*

     这些文件将直接添加到 SiteColumnProjectTemplate 项目中;不重新创建该项目中的 Field1、 功能或包子文件夹。 有关这些文件的详细信息，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

#### <a name="to-configure-how-developers-discover-the-project-template-in-the-new-project-dialog-box"></a>若要配置开发人员如何发现的新项目对话框中的项目模板

1. 在中**解决方案资源管理器**，打开快捷菜单**SiteColumnProjectTemplate**项目节点，然后选择**卸载项目**。 如果系统提示您将更改保存到的任何文件时，选择**是**按钮。

2. 打开快捷菜单**SiteColumnProjectTemplate**节点，然后选择**编辑 SiteColumnProjectTemplate.csproj**或**编辑 SiteColumnProjectTemplate.vbproj**.

3. 在项目文件中，找到以下`VSTemplate`元素。

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
    ```

4. 此元素替换为以下 XML。

    ```xml
    <VSTemplate Include="SiteColumnProjectTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素指定其他文件夹中生成项目时在其下创建项目模板的路径。 此处指定的文件夹确保，仅当客户打开的项目模板将在可用**新的项目**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

5. 保存并关闭文件。

6. 在中**解决方案资源管理器**，打开快捷菜单**SiteColumnProjectTemplate**项目，，然后选择**重新加载项目**。

## <a name="edit-the-project-template-files"></a>编辑项目模板文件
 在 SiteColumnProjectTemplate 项目中，编辑以下文件来定义项目模板的行为：

- *AssemblyInfo.cs*或*AssemblyInfo.vb*

- *Elements.xml*

- *SharePointProjectItem.spdata*

- *Feature1.feature*

- *Package.package*

- *SiteColumnProjectTemplate.vstemplate*

- *ProjectTemplate.csproj*或*ProjectTemplate.vbproj*

  在以下过程中，会将可替换参数添加到其中的某些文件。 可替换参数是一个标记，用于开始和结束的美元符号 （$） 字符。 当用户使用此项目模板创建项目时，Visual Studio 将自动替换这些参数在新项目中具有特定值。 有关详细信息，请参阅[可替换参数](../sharepoint/replaceable-parameters.md)。

#### <a name="to-edit-the-assemblyinfocs-or-assemblyinfovb-file"></a>若要编辑的 AssemblyInfo.cs 或 AssemblyInfo.vb 文件

1. 在 SiteColumnProjectTemplate 项目中，打开*AssemblyInfo.cs*或*AssemblyInfo.vb*文件中，并将以下语句添加到它的顶部：

    ```vb
    Imports System.Security
    ```

    ```csharp
    using System.Security;
    ```

     当**沙盒解决方案**SharePoint 项目的属性设置为**True**，Visual Studio 将添加<xref:System.Security.AllowPartiallyTrustedCallersAttribute>AssemblyInfo 代码文件。 但是，不能导入的项目模板中的 AssemblyInfo 代码文件<xref:System.Security>默认情况下的命名空间。 必须添加这**使用**或**导入**语句阻止编译错误。

2. 保存并关闭文件。

#### <a name="to-edit-the-elementsxml-file"></a>若要编辑的 Elements.xml 文件

1. 在 SiteColumnProjectTemplate 项目中，替换的内容*Elements.xml*使用以下 XML 文件。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">
      <Field ID="{$guid5$}"
          Name="$safeprojectname$"
          DisplayName="$projectname$"
          Type="Text"
          Group="Custom Columns">
      </Field>
    </Elements>
    ```

     添加了新的 XML`Field`定义站点列，其基类型和要在其中列出库中的站点列组的名称的元素。 此文件的内容的详细信息，请参阅[字段定义架构](http://go.microsoft.com/fwlink/?LinkId=184290)。

2. 保存并关闭文件。

#### <a name="to-edit-the-sharepointprojectitemspdata-file"></a>若要编辑 SharePointProjectItem.spdata 文件

1. 在 SiteColumnProjectTemplate 项目中，替换的内容*SharePointProjectItem.spdata*使用以下 XML 文件。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <ProjectItem Type="Contoso.SiteColumn" DefaultFile="Elements.xml"
                xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
     <Files>
       <ProjectItemFile Source="Elements.xml" Target="$safeprojectname$\" Type="ElementManifest" />
     </Files>
   </ProjectItem>
   ```

    新的 XML 会对文件进行以下更改：

   - 更改`Type`的属性`ProjectItem`元素为相同字符串传递给<xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>项目项定义上 (`SiteColumnProjectItemTypeProvider`之前在本演练中创建的类)。

   - 移除`SupportedTrustLevels`并`SupportedDeploymentScopes`属性从`ProjectItem`元素。 这些属性值是不必要的因为中指定的信任级别和部署范围`SiteColumnProjectItemTypeProvider`ProjectItemTypeDefinition 项目中的类。

     详细了解的内容 *.spdata*文件，请参阅[SharePoint 项目项架构参考](../sharepoint/sharepoint-project-item-schema-reference.md)。

2. 保存并关闭文件。

#### <a name="to-edit-the-feature1feature-file"></a>若要编辑 Feature1.feature 文件

1. 在 SiteColumnProjectTemplate 项目中，替换的内容*Feature1.feature*使用以下 XML 文件。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <feature xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0" Id="$guid4$" featureId="$guid4$"
            imageUrl="" solutionId="00000000-0000-0000-0000-000000000000" title="Site Column Feature1" version=""
            deploymentPath="$SharePoint.Project.FileNameWithoutExtension$_$SharePoint.Feature.FileNameWithoutExtension$"
            xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/FeatureModel">
     <projectItems>
       <projectItemReference itemId="$guid2$" />
     </projectItems>
   </feature>
   ```

    新的 XML 会对文件进行以下更改：

   - 更改的值`Id`并`featureId`的属性`feature`元素`$guid4$`。

   - 更改的值`itemId`的属性`projectItemReference`元素`$guid2$`。

     有关详细信息 *.feature*文件，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

2. 保存并关闭文件。

#### <a name="to-edit-the-packagepackage-file"></a>若要编辑 Package.package 文件

1. 在 SiteColumnProjectTemplate 项目中，替换的内容*Package.package*使用以下 XML 文件。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <package xmlns:dm0="http://schemas.microsoft.com/VisualStudio/2008/DslTools/Core" dslVersion="1.0.0.0"
            Id="$guid3$" solutionId="$guid3$" resetWebServer="false" name="$safeprojectname$"
            xmlns="http://schemas.microsoft.com/VisualStudio/2008/SharePointTools/PackageModel">
     <features>
       <featureReference itemId="$guid4$" />
     </features>
   </package>
   ```

    新的 XML 会对文件进行以下更改：

   - 更改的值`Id`并`solutionId`的属性`package`元素`$guid3$`。

   - 更改的值`itemId`的属性`featureReference`元素`$guid4$`。

     有关详细信息 *.package*文件，请参阅[创建项模板和项目模板的 SharePoint 项目项](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)。

2. 保存并关闭文件。

#### <a name="to-edit-the-sitecolumnprojecttemplatevstemplate-file"></a>若要编辑 sitecolumnprojecttemplate.vstemplate 文件

1. 在 SiteColumnProjectTemplate 项目中，将替换 XML 的以下部分之一为 SiteColumnProjectTemplate.vstemplate 文件的内容。

   - 如果要创建 Visual C# 项目模板，使用下面的 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">
     <TemplateData>
       <Name>Site Column</Name>
       <Description>Creates a new site column in SharePoint</Description>
       <FrameworkVersion>3.5</FrameworkVersion>
       <ProjectType>CSharp</ProjectType>
       <CreateNewFolder>true</CreateNewFolder>
       <CreateInPlace>true</CreateInPlace>
       <ProvideDefaultName>true</ProvideDefaultName>
       <DefaultName>SiteColumn</DefaultName>
       <LocationField>Enabled</LocationField>
       <EnableLocationBrowseButton>true</EnableLocationBrowseButton>
       <PromptForSaveOnCreation>true</PromptForSaveOnCreation>
       <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
       <Icon>SiteColumnProjectTemplate.ico</Icon>
       <SortOrder>1000</SortOrder>
     </TemplateData>
     <TemplateContent>
       <Project TargetFileName="SharePointProject1.csproj" File="ProjectTemplate.csproj" ReplaceParameters="true">
         <ProjectItem ReplaceParameters="true" TargetFileName="Properties\AssemblyInfo.cs">AssemblyInfo.cs</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>
         <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
       </Project>
     </TemplateContent>
   </VSTemplate>
   ```

   - 如果要创建 Visual Basic 项目模板，使用下面的 XML。

   ```xml
   <?xml version="1.0" encoding="utf-8"?>
   <VSTemplate Version="3.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Project">
     <TemplateData>
       <Name>Site Column</Name>
       <Description>Creates a new site column in SharePoint</Description>
       <FrameworkVersion>3.5</FrameworkVersion>
       <ProjectType>VisualBasic</ProjectType>
       <CreateNewFolder>true</CreateNewFolder>
       <CreateInPlace>true</CreateInPlace>
       <ProvideDefaultName>true</ProvideDefaultName>
       <DefaultName>SiteColumn</DefaultName>
       <LocationField>Enabled</LocationField>
       <EnableLocationBrowseButton>true</EnableLocationBrowseButton>
       <PromptForSaveOnCreation>true</PromptForSaveOnCreation>
       <NumberOfParentCategoriesToRollUp>1</NumberOfParentCategoriesToRollUp>
       <Icon>SiteColumnProjectTemplate.ico</Icon>
       <SortOrder>1000</SortOrder>
     </TemplateData>
     <TemplateContent>
       <Project TargetFileName="SharePointProject1.vbproj" File="ProjectTemplate.vbproj" ReplaceParameters="true">
         <ProjectItem ReplaceParameters="true" TargetFileName="My Project\AssemblyInfo.vb">AssemblyInfo.vb</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.feature">Feature1.feature</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Features\Feature1\Feature1.Template.xml">Feature1.template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.package">Package.package</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Package\Package.Template.xml">Package.Template.xml</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\SharePointProjectItem.spdata">SharePointProjectItem.spdata</ProjectItem>
         <ProjectItem ReplaceParameters="true" TargetFileName="Field1\Elements.xml" OpenInEditor="true">Elements.xml</ProjectItem>
         <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
       </Project>
     </TemplateContent>
   </VSTemplate>
   ```

    新的 XML 会对文件进行以下更改：

   - 集`Name`的值的元素**站点列**。 (此名称将显示在**新的项目**对话框)。

   - 添加`ProjectItem`每个项目实例中包含的元素的每个 filethat。

   - 使用的命名空间"<http://schemas.microsoft.com/developer/vstemplate/2005>"。 在此解决方案，使用其他项目文件"<http://schemas.microsoft.com/developer/msbuild/2003>"命名空间。 因此，将生成 XML 架构的警告消息，但你可以在本演练中忽略它们。

     详细了解的内容 *.vstemplate*文件，请参阅[Visual Studio 模板架构引用](/visualstudio/extensibility/visual-studio-template-schema-reference)。

2. 保存并关闭文件。

#### <a name="to-edit-the-projecttemplatecsproj-or-projecttemplatevbproj-file"></a>若要编辑的 projecttemplate.csproj 或 projecttemplate.vbproj 文件

1. 在 SiteColumnProjectTemplate 项目中，替换的内容*ProjectTemplate.csproj*文件或*ProjectTemplate.vbproj*具有之一的以下各节的 XML 文件。

    - 如果要创建 Visual C# 项目模板，使用下面的 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid>{$guid1$}</ProjectGuid>
        <OutputType>Library</OutputType>
        <AppDesignerFolder>Properties</AppDesignerFolder>
        <RootNamespace>$safeprojectname$</RootNamespace>
        <AssemblyName>$safeprojectname$</AssemblyName>
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
        <FileAlignment>512</FileAlignment>
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{14822709-B5A1-4724-98CA-57A101D1B079};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineConstants>DEBUG;TRACE</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <DebugType>pdbonly</DebugType>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <DefineConstants>TRACE</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
      <PropertyGroup>
        <SignAssembly>true</SignAssembly>
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="System" />
        <Reference Include="System.Core" />
        <Reference Include="System.Data" />
        <Reference Include="System.Data.DataSetExtensions" />
        <Reference Include="System.Web" />
        <Reference Include="System.Xml" />
        <Reference Include="System.Xml.Linq" />
        <Reference Include="Microsoft.SharePoint" />
        <Reference Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="Properties\AssemblyInfo.cs" />
      </ItemGroup>
      <ItemGroup>
        <None Include="Field1\SharePointProjectItem.spdata">
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>
        </None>
        <None Include="Field1\Elements.xml" />
      </ItemGroup>
      <ItemGroup>
        <None Include="key.snk" />
        <None Include="Package\Package.package">
          <PackageId>{$guid3$}</PackageId>
        </None>
        <None Include="Package\Package.Template.xml">
          <DependentUpon>Package.package</DependentUpon>
        </None>
        <None Include="Features\Feature1\Feature1.feature">
          <FeatureId>{$guid4$}</FeatureId>
        </None>
        <None Include="Features\Feature1\Feature1.Template.xml">
          <DependentUpon>Feature1.feature</DependentUpon>
        </None>
      </ItemGroup>
      <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />
    </Project>
    ```

    1. 如果要创建 Visual Basic 项目模板，使用下面的 XML。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
        <ProductVersion>
        </ProductVersion>
        <SchemaVersion>
        </SchemaVersion>
        <ProjectGuid>{$guid1$}</ProjectGuid>
        <OutputType>Library</OutputType>
        <RootNamespace>$safeprojectname$</RootNamespace>
        <AssemblyName>$safeprojectname$</AssemblyName>
        <TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
        <FileAlignment>512</FileAlignment>
        <ProjectTypeGuids>{BB1F664B-9266-4fd6-B973-E1E44974B511};{D59BE175-2ED0-4C54-BE3D-CDAA9F3214C8};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>
        <OptionExplicit>On</OptionExplicit>
        <OptionCompare>Binary</OptionCompare>
        <OptionStrict>Off</OptionStrict>
        <OptionInfer>On</OptionInfer>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <DefineDebug>true</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <OutputPath>bin\Debug\</OutputPath>
        <WarningLevel>4</WarningLevel>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <DebugType>pdbonly</DebugType>
        <DefineDebug>false</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <UseVSHostingProcess>false</UseVSHostingProcess>
      </PropertyGroup>
      <PropertyGroup>
        <SignAssembly>true</SignAssembly>
        <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="System" />
        <Reference Include="System.Core" />
        <Reference Include="System.Data" />
        <Reference Include="System.Data.DataSetExtensions" />
        <Reference Include="System.Xml" />
        <Reference Include="System.Xml.Linq" />
        <Reference Include="Microsoft.SharePoint" />
        <Reference Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Import Include="Microsoft.VisualBasic" />
        <Import Include="System" />
        <Import Include="System.Collections" />
        <Import Include="System.Collections.Generic" />
        <Import Include="System.Data" />
        <Import Include="System.Diagnostics" />
        <Import Include="System.Linq" />
        <Import Include="System.Xml.Linq" />
        <Import Include="Microsoft.SharePoint" />
        <Import Include="Microsoft.SharePoint.Security" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="My Project\AssemblyInfo.vb" />
      </ItemGroup>
      <ItemGroup>
        <AppDesigner Include="My Project\" />
      </ItemGroup>
      <ItemGroup>
        <None Include="Features\Feature1\Feature1.feature">
          <FeatureId>{$guid4$}</FeatureId>
        </None>
        <None Include="Field1\SharePointProjectItem.spdata">
          <SharePointProjectItemId>{$guid2$}</SharePointProjectItemId>
        </None>
        <None Include="key.snk" />
        <None Include="Package\Package.package">
          <PackageId>{$guid3$}</PackageId>
        </None>
        <None Include="Package\Package.Template.xml">
          <DependentUpon>Package.package</DependentUpon>
        </None>
      </ItemGroup>
      <ItemGroup>
        <None Include="Features\Feature1\Feature1.Template.xml">
          <DependentUpon>Feature1.feature</DependentUpon>
        </None>
        <None Include="Field1\Elements.xml" />
      </ItemGroup>
      <Import Project="$(MSBuildToolsPath)\Microsoft.VisualBasic.targets" />
      <Import Project="$(MSBuildExtensionsPath32)\Microsoft\VisualStudio\v10.0\SharePointTools\Microsoft.VisualStudio.SharePoint.targets" />
    </Project>
    ```

     新的 XML 会对文件进行以下更改：

    - 使用`TargetFrameworkVersion`元素指定.NET Framework 3.5，而不是 4.5。

    - 将添加`SignAssembly`和`AssemblyOriginatorKeyFile`要签名项目输出的元素。

    - 添加`Reference`程序集的元素引用该 SharePoint 项目使用。

    - 将为每个默认文件的元素添加在项目中，如*Elements.xml*并*SharePointProjectItem.spdata*。

2. 保存并关闭文件。

## <a name="create-a-vsix-package-to-deploy-the-project-template"></a>创建 VSIX 包来部署项目模板
 若要将扩展部署，请使用中的 VSIX 项目**SiteColumnProjectItem**解决方案，以创建 VSIX 包。 首先，通过修改包含在 VSIX 项目的 source.extension.vsixmanifest 文件中配置 VSIX 包。 然后，通过生成解决方案中创建 VSIX 包。

#### <a name="to-configure-and-create-the-vsix-package"></a>若要配置和创建 VSIX 包

1. 在中**解决方案资源管理器**，在**SiteColumnProjectItem**项目中，在清单编辑器中打开 source.extension.vsixmanifest 文件中。

     在 source.extension.vsixmanifest 文件是所有 VSIX 包都需要 extension.vsixmanifest 文件的基础。 有关此文件的详细信息，请参阅[VSIX 扩展架构 1.0 参考](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b)。

2. 在中**产品名称**框中，输入**站点列**。

3. 在中**作者**框中，输入**Contoso**。

4. 在中**描述**框中，输入**用于创建网站栏的 SharePoint 项目**。

5. 选择**资产**选项卡，然后选择**新建**按钮。

     **添加新资产**对话框随即打开。

6. 在中**类型**列表中，选择**Microsoft.VisualStudio.ProjectTemplate**。

    > [!NOTE]
    > 此值对应于`ProjectTemplate`extension.vsixmanifest 文件中的元素。 此元素标识的子文件夹中包含的项目模板的 VSIX 包。 有关详细信息，请参阅[ProjectTemplate 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\))。

7. 在中**源**列表中，选择**当前解决方案中的项目**。

8. 在中**项目**列表，并选择**SiteColumnProjectTemplate**，然后选择**确定**按钮。

9. 选择**新建**按钮再次。

     **添加新资产**对话框随即打开。

10. 在中**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。

    > [!NOTE]
    > 此值对应于`MefComponent`extension.vsixmanifest 文件中的元素。 此元素指定 VSIX 包中的扩展插件程序集名称。 有关详细信息，请参阅[MEFComponent 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

11. 在中**源**列表中，选择**当前解决方案中的项目**。

12. 在中**项目**列表中，选择**ProjectItemTypeDefinition**，然后选择**确定**按钮。

13. 在菜单栏上依次选择**构建** > **生成解决方案**，然后确保该项目在编译时没有错误。

## <a name="test-the-project-template"></a>测试项目模板
 现在您就可以测试项目模板。 首先，开始调试 Visual Studio 的实验实例中的 SiteColumnProjectItem 解决方案。 然后，测试**站点列**Visual Studio 的实验实例中的项目。 最后，生成并运行 SharePoint 项目以验证站点列按预期方式正常工作。

#### <a name="to-start-debugging-the-solution"></a>若要开始调试解决方案

1. 使用管理凭据，重新启动 Visual Studio，然后打开 SiteColumnProjectItem 解决方案。

2. 在 SiteColumnProjectItemTypeProvider 代码文件中，将断点添加到代码中的第一行`InitializeType`方法，然后选择**F5**键启动调试。

     Visual Studio 会将扩展安装到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Site Column\1.0 并启动 Visual Studio 的实验实例。 在 Visual Studio 的此实例中，将测试项目项。

#### <a name="to-test-the-project-in-visual-studio"></a>若要在 Visual Studio 中测试项目

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**文件** > **新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**节点 （具体取决于你的项目模板支持的语言），展开**SharePoint**节点，然后选择**2010年**节点。

3. 在项目模板列表中，选择**站点列**模板。

4. 在中**名称**框中，输入**SiteColumnTest** ，然后选择**确定**按钮。

     在中**解决方案资源管理器**，使用名为一个项目项将显示新项目**Field1**。

5. 验证中设置的断点处停止 Visual Studio 的其他实例中的代码`InitializeType`方法，然后选择**F5**键继续调试项目。

6. 在中**解决方案资源管理器**，选择**Field1**节点，然后选择**F4**密钥。

     **属性**窗口随即打开。

7. 在属性列表中，验证属性**的示例属性**出现。

#### <a name="to-test-the-site-column-in-sharepoint"></a>若要在 SharePoint 中测试的网站栏

1. 在中**解决方案资源管理器**，选择**SiteColumnTest**节点。

2. 在中**属性**窗口中的下, 一步是在文本框中**站点 URL**属性中，输入**http://localhost**。

     此步骤中指定你想要用于调试的开发计算机上的本地 SharePoint 站点。

    > [!NOTE]
    > **站点 URL**属性为空默认情况下，因为网站栏项目模板不会提供一个向导，用于创建项目时收集此值。 若要了解如何将添加一个向导，要求开发人员输入此值，然后在新项目中配置此属性，请参阅[演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

3. 选择 F5。

     打包和部署到 SharePoint 站点中指定的网站栏**站点 URL**项目的属性。 Web 浏览器打开到此站点的默认页。

    > [!NOTE]
    > 如果**脚本调试被禁用**出现对话框，请选择**是**按钮以继续调试项目。

4. 上**站点操作**菜单中，选择**站点设置**。

5. 上**站点设置**页面上，在**库**列表中，选择**站点列**链接。

6. 在站点列的列表中，确认**自定义列**组中包含的列，名为**SiteColumnTest**。

7. 关闭 Web 浏览器。

## <a name="clean-up-the-development-computer"></a>清理开发计算机
 在完成测试项目后，从 Visual Studio 的实验实例中删除项目模板。

#### <a name="to-clean-up-the-development-computer"></a>若要清理开发计算机

1. 在实验实例中的 Visual Studio 中，在菜单栏上，选择**工具** > **扩展和更新**。

     此时，“扩展和更新”对话框打开。

2. 在扩展的列表，选择**网站栏**扩展，然后选择**卸载**按钮。

3. 在出现的对话框中，选择**是**按钮以确认你想要卸载扩展。

4. 选择**关闭**按钮以完成卸载。

5. 关闭 Visual Studio （实验实例和在其中 SiteColumnProjectItem 解决方案已打开的 Visual Studio 的实例） 的两个实例。

## <a name="next-steps"></a>后续步骤
 完成本演练后，可以将向导添加到项目模板。 当用户创建网站栏项目时，该向导会要求提供网站 URL 以用于调试和新的解决方案是否为沙盒解决方案，用户和该向导将新项目配置使用此信息。 该向导还收集有关列 （如基类型和要在其中列出网站栏库中的列组） 的信息，并添加到此信息*Elements.xml*新项目文件中的。 有关详细信息，请参见[演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)。

## <a name="see-also"></a>请参阅

- [演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)
- [定义自定义 SharePoint 项目项类型](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [创建项模板和用于 SharePoint 项目项的项目模板](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [将数据保存在 SharePoint 项目系统的扩展](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [将自定义数据与 SharePoint 工具扩展相关联](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)