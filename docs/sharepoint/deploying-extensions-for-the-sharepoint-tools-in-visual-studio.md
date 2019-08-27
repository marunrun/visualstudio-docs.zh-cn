---
title: 部署 Visual Studio 中的 SharePoint 工具扩展 |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 53e36d993e72da759c87e7d2d2f908818b3d9024
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62580639"
---
# <a name="deploy-extensions-for-the-sharepoint-tools-in-visual-studio"></a>部署 Visual Studio 中的 SharePoint 工具扩展

若要部署 SharePoint 工具扩展，创建[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]扩展 (VSIX) 包，其中包含扩展插件程序集和你想要将与该扩展一起分发的任何其他文件。 VSIX 包是一个压缩的文件，遵循开放式打包约定 (OPC) 标准。 VSIX 包具有 *.vsix*扩展。

创建 VSIX 包后，其他用户可以运行要安装扩展的.vsix 文件。 当用户安装您的扩展插件时，到 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions 文件夹安装的所有文件。 若要将扩展部署，可以上传到 VSIX 包[Visual Studio Marketplace](https://marketplace.visualstudio.com/) Web 网站，或者可以将包分发到你的客户通过某种其他方式，包括托管的网络共享或某些其他 Web 上的包站点。

有关创建 VSIX 包和部署到这些详细信息[Visual Studio Marketplace](https://marketplace.visualstudio.com/)，请参阅[传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

 可以使用创建 VSIX 包**VSIX 项目**模板中 Visual Studio 中，也可以手动创建 VSIX 包。

## <a name="use-vsix-projects-to-create-vsix-packages"></a>使用 VSIX 项目创建 VSIX 包

可以使用**VSIX 项目**模板提供的 Visual Studio SDK，若要为 SharePoint 工具扩展创建 VSIX 包。 使用 VSIX 项目通过手动创建 VSIX 包提供以下几个好处：

- 生成项目时，visual Studio 会自动生成 VSIX 包。 为您完成任务，例如向包中添加部署文件和创建包 [Content_Types].xml 文件。

- 可以配置要包含在 VSIX 包中的扩展项目和其他文件，如项目模板和项模板的生成输出 VSIX 项目。

有关使用 VSIX 项目的详细信息，请参阅[VSIX 项目模板](../extensibility/vsix-project-template.md)。

### <a name="organize-your-projects"></a>组织项目

默认情况下，VSIX 项目仅生成 VSIX 包，不是程序集。 因此，您通常也不实现 SharePoint 工具扩展的 VSIX 项目中。 通常使用至少两个项目：

- 一个 VSIX 项目。

- 一个用于实现你的扩展的库项目。

您可能还会使用其他项目对于某些类型的扩展：

- 一个实现任何由你的扩展的 SharePoint 命令的类库项目。 有关演示此方案的演练，请参阅[演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 如果您的扩展插件定义新类型的 SharePoint 项目项创建项模板或项目模板，项模板或项目模板项目。 有关演示此方案的演练，请参阅[演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

- 如果您的扩展插件包括模板实现的项模板或项目模板的自定义向导的类库项目。 有关演示此方案的演练，请参阅[演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

如果在同一 Visual Studio 解决方案中包含的所有项目，您可以修改 source.extension.vsixmanifest 文件中要包括的类库项目生成输出的 VSIX 项目中。

### <a name="edit-the-vsix-manifest"></a>编辑 VSIX 清单

必须编辑 source.extension.vsixmanifest 文件中要包括想要包括在扩展中的所有项的条目的 VSIX 项目中。 当从其快捷菜单打开 source.extension.vsixmanifest 文件时，该文件将显示用于编辑 XML 文件中提供的用户界面的设计器中。 有关详细信息，请参阅[VSIX 清单设计器](../extensibility/vsix-manifest-designer.md)。

必须将条目添加到 source.extension.vsixmanifest 文件中的以下各项：

- 扩展插件程序集。

- 实现任何由你的扩展的 SharePoint 命令的程序集。

- 任何项目模板或与您的扩展插件相关联的项模板。

- 用于与您的扩展插件相关联的模板的自定义向导。

以下过程介绍如何将条目添加到的.vsixmanifest 文件中，为每个这些项。

#### <a name="to-include-the-extension-assembly"></a>若要包括的扩展程序集

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择**打开**。

     在设计器中打开该文件

2. 上**资产**选项卡的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即打开。

3. 在中**类型**列表中，选择**Microsoft.VisualStudio.MefComponent**。

4. 在中**源**列表中，执行以下步骤之一：

    - 如果扩展插件程序集生成 VSIX 项目的同一个解决方案中的项目中，选择**当前解决方案中的项目**。 在中**项目**列表中，选择项目的名称。

    - 如果扩展插件程序集包含为你的项目中的文件，请选择**在文件系统上的文件**。 在中**路径**列表中，输入指向扩展程序集文件，完整路径或使用**浏览**按钮以找到并选择程序集文件。

5. 选择“确定”  按钮。

#### <a name="to-include-a-sharepoint-command-assembly"></a>包含 SharePoint 命令程序集

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择**打开**按钮。

     在设计器中打开该文件。

2. 在中**资产**部分中的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即打开。

3. 在中**类型**框中，输入**SharePoint.Commands.v4**。

4. 在中**源**列表中，执行以下步骤之一：

    - 如果命令程序集生成 VSIX 项目的同一个解决方案中的项目中，选择**当前解决方案中的项目**。 在中**项目**列表中，选择项目的名称。

    - 如果为你的项目中的文件包括命令程序集，则选择**在文件系统上的文件**。 在中**路径**列表中，输入指向扩展程序集文件，完整路径或使用**浏览**按钮以找到并选择程序集文件。

5. 选择“确定”  按钮。

#### <a name="to-include-a-template-that-you-create"></a>若要包括你创建的模板

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择**打开**按钮。

     在设计器中打开该文件。

2. 在中**资产**部分中的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即打开。

3. 在中**类型**列表中，选择**Microsoft.VisualStudio.ProjectTemplate**或**Microsoft.VisualStudio.ItemTemplate**。

4. 在中**源**列表中，选择**当前解决方案中的项目**。

5. 在中**项目**列表中，选择项目的名称，然后选择**确定**按钮。

6. 在中**解决方案资源管理器**，打开你的项目模板或项模板项目的快捷菜单，然后选择**卸载项目**。

7. 再次，打开项目节点的快捷菜单，然后选择**编辑**_YourTemplateProjectName_**.csproj**或者**编辑**_YourTemplateProjectName_**.vbproj**。

8. 找到以下`VSTemplate`项目文件中的元素。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
    ```

9. 此元素替换为以下 XML。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素指定其他文件夹中生成项目时在其下创建项目模板的路径。 此处指定的文件夹确保，仅当客户打开的项模板将在可用**添加新项目**对话框框中，展开**SharePoint**节点，然后选择**2010年**节点。

10. 保存并关闭文件。

11. 在中**解决方案资源管理器**，打开为项目模板或项模板项目的快捷菜单，然后选择**重新加载项目**。

#### <a name="to-include-a-template-that-you-create-manually"></a>若要包括手动创建的模板

1. 在 VSIX 项目中，将新文件夹添加到项目，以包含该模板。

2. 此新文件夹下创建以下子文件夹，并添加到模板 (.zip) 文件*区域设置 ID*文件夹。

     *YourTemplateFolder*

     **SharePoint**

     **SharePoint14**

     *区域设置 ID*

     *YourTemplateName*.zip

     例如，如果你具有名为 ContosoCustomAction.zip 支持英语 （美国） 区域设置的项模板，完整路径可能是*ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*。

3. 在中**解决方案资源管理器**，选择的模板文件 (*YourTemplateName*.zip)。

4. 在中**属性**窗口中，将**生成操作**属性设置为**内容**。

5. 打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择**打开**。

     在设计器中打开该文件。

6. 在中**资产**部分中的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即打开。

7. 在中**类型**列表中，选择**Microsoft.VisualStudio.ItemTemplate**或**Microsoft.VisualStudio.ProjectTemplate**。

8. 在中**源**列表中，选择**在文件系统上的文件**。

9. 在中**路径**字段中，输入程序集的完整路径 (例如， *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*，或使用**浏览**按钮来定位并选择该程序集，然后选择**确定**按钮。

#### <a name="to-include-a-wizard-for-a-project-template-or-item-template"></a>若要包括的项目模板或项模板向导

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择**打开**。

     在设计器中打开该文件。

2. 在中**资产**部分中的编辑器中，选择**新建**按钮。

     **添加新资产**对话框随即打开。

3. 在中**类型**列表中，选择**Microsoft.VisualStudio.Assembly**。

4. 在中**源**列表中，执行以下步骤之一：

    - 如果向导程序集生成 VSIX 项目的同一个解决方案中的项目中，选择**当前解决方案中的项目**。 在中**项目**列表中，选择项目的名称。

    - 如果向导程序集包含为你的项目中的文件，请选择**在文件系统上的文件**。 在中**路径**字段中，输入指向程序集文件中，完整路径或使用**浏览**按钮以找到并选择程序集。

5. 选择“确定”  按钮。

### <a name="related-walkthroughs"></a>相关的演练

下表列出的演练，演示如何使用 VSIX 项目来部署不同类型的 SharePoint 工具扩展。

|扩展类型|相关的演练|
|--------------------|--------------------------|
|包括的扩展程序集扩展|[演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)<br /><br /> [演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)<br /><br /> [演练：调入 SharePoint 客户端对象模型中的服务器资源管理器扩展](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)|
|一个扩展，包括 SharePoint 命令|[演练：创建 SharePoint 项目的自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)<br /><br /> [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)<br /><br /> [演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|
|一个扩展，包括 Visual Studio 模板|[演练：使用项模板，第 1 部分创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)<br /><br /> [演练：使用项目模板，第 1 部分创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)|
|一个扩展，包括模板向导|[演练：使用项模板，第 2 部分中创建自定义操作项目项](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)<br /><br /> [演练：使用项目模板，第 2 部分中创建站点栏项目项](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|

## <a name="create-vsix-packages-manually"></a>手动创建 VSIX 包

如果你想要手动创建您的 SharePoint 工具扩展的 VSIX 包，请执行以下步骤：

1. 在新的文件夹中创建 extension.vsixmanifest 文件和 [Content_Types].xml 文件。 有关详细信息，请参阅[VSIX 包的剖析](../extensibility/anatomy-of-a-vsix-package.md)。

2. 在 Windows 资源管理器，右键单击包含两个 XML 文件的文件夹，单击发送到，然后单击压缩 (zipped) 文件夹。 生成的.zip 文件重命名为 Filename.vsix，其中 Filename 是用于安装包的可再发行文件的名称。

3. 将扩展插件程序集添加到 VSIX 包。 如果您的扩展插件包括 SharePoint 命令，还添加到 VSIX 包的 SharePoint 命令实现的程序集。

4. 修改 extension.vsixmanifest 文件：

    - 添加`Microsoft.VisualStudio.MefComponent`元素下的`Assets`元素，并设置 VSIX 包中实现您的扩展插件的程序集的相对路径的新元素的值。 有关详细信息，请参阅[MEFComponent 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

    - 如果您的扩展插件中包含到服务器对象模型调用 SharePoint 的 SharePoint 命令，添加`Microsoft.VisualStudio.Assembly`元素下的`Assets`元素。 将新元素的值设置为 VSIX 包中实现 SharePoint 命令的程序集的相对路径。 有关详细信息，请参阅[资产元素 （VSX 架构）](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737)。

    - 如果您的扩展插件包括项目模板或项模板，添加`ProjectTemplate`或`ItemTemplate`元素下的`Assets`元素。 将新元素的值设置为包含在 VSIX 包中的模板的文件夹的相对路径。 有关详细信息，请参阅[ProjectTemplate 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\))并[ItemTemplate 元素 （VSX 架构）](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))。

    - 如果您的扩展插件中包含的项目模板或项模板的自定义向导，添加`Assembly`元素下的`Assets`元素。 将新元素的值设置为在 VSIX 包中，程序集的相对路径，然后设置`AssemblyName`属性为完整的程序集名称 （包括版本、 区域性和公钥标记）。 有关详细信息，请参阅[依赖关系元素 （VSX 架构）](https://msdn.microsoft.com/1f63f60a-98ad-48ec-8e44-4eba383d3e37)。

### <a name="example"></a>示例

下面的示例显示了用于 SharePoint 工具扩展的 extension.vsixmanifest 文件的内容。 扩展是在名为 Contoso.ProjectExtension.dll 程序集中实现的。 扩展插件包括 Contoso.ExtensionCommands.dll 和项模板名为的文件夹下名为的 SharePoint 命令程序集**ItemTemplates** VSIX 包中。 此示例假定这两个程序集是在 VSIX 包中 extension.vsixmanifest 文件所在的同一文件夹中。

```xml
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <Identity Id="CustomActionProjectItem.Microsoft.b99efe4d-cef3-4afd-b9af-034ca0c52743" Version="1.0" Language="en-US" Publisher="Microsoft" />
    <DisplayName>CustomActionProjectItem</DisplayName>
    <Description>Empty VSIX Project.</Description>
  </Metadata>
  <Installation>
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="11.0" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" Version="4.5" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.ItemTemplate" Path="ItemTemplates" />
    <Asset Type="Microsoft.VisualStudio.MefComponent" Path="ProjectItemDefinition.dll" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>请参阅

- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展服务器资源管理器中的 SharePoint 连接节点](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [调试 Visual Studio 中的 SharePoint 工具扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
