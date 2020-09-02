---
title: 在 Visual Studio 中部署 SharePoint 工具扩展 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62580639"
---
# <a name="deploy-extensions-for-the-sharepoint-tools-in-visual-studio"></a>在 Visual Studio 中部署 SharePoint 工具扩展

若要部署 SharePoint 工具扩展，请创建一个 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 扩展 (VSIX) 包，其中包含扩展程序集以及要使用该扩展分发的任何其他文件。 VSIX 包是遵循开放打包约定 (OPC) standard 的压缩文件。 VSIX 包的扩展名为 *.vsix* 。

创建 VSIX 包后，其他用户可以运行 .vsix 文件来安装扩展。 当用户安装你的扩展时，所有文件都将安装到%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions 文件夹中。 若要部署该扩展，您可以将该 VSIX 包上传到 [Visual Studio Marketplace](https://marketplace.visualstudio.com/) 网站，也可以通过其他一些方式将包分发给客户，例如在网络共享或某个其他网站上托管包。

有关创建 VSIX 包并将其部署到 [Visual Studio Marketplace](https://marketplace.visualstudio.com/)的详细信息，请参阅 [发布 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)。

 您可以通过使用 Visual Studio 中的 **Vsix 项目** 模板来创建 vsix 包，也可以手动创建 vsix 包。

## <a name="use-vsix-projects-to-create-vsix-packages"></a>使用 VSIX 项目创建 VSIX 包

你可以使用 Visual Studio SDK 提供的 **Vsix 项目** 模板来创建 SharePoint 工具扩展的 vsix 包。 与手动创建 VSIX 包相比，使用 VSIX 项目具有若干优点：

- 生成项目时，Visual Studio 会自动生成 VSIX 包。 将部署文件添加到包，并为包创建 [Content_Types] .xml 文件等任务。

- 你可以配置 VSIX 项目，使其包含扩展项目的生成输出和 VSIX 包中的其他文件，如项目模板和项模板。

有关使用 VSIX 项目的详细信息，请参阅 [Vsix 项目模板](../extensibility/vsix-project-template.md)。

### <a name="organize-your-projects"></a>组织项目

默认情况下，VSIX 项目仅生成 VSIX 包，而不生成程序集。 因此，您通常不会在 VSIX 项目中实现 SharePoint 工具扩展。 通常使用至少两个项目：

- 一个 VSIX 项目。

- 实现扩展的类库项目。

对于某些类型的扩展，你还可以使用其他项目：

- 一个类库项目，用于实现扩展所使用的任何 SharePoint 命令。 有关演示此方案的演练，请参阅 [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)。

- 一个项模板或项目模板项目，如果你的扩展定义了新类型的 SharePoint 项目项，则创建项模板或项目模板。 有关演示此方案的演练，请参阅 [演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)。

- 一个类库项目，它实现项模板或项目模板的自定义向导（如果你的扩展插件包含模板）。 有关演示此方案的演练，请参阅 [演练：使用项模板创建自定义操作项目项（第2部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)。

如果在同一 Visual Studio 解决方案中包含所有项目，则可以修改 VSIX 项目中的 source.extension.vsixmanifest 文件以包括类库项目的生成输出。

### <a name="edit-the-vsix-manifest"></a>编辑 VSIX 清单

必须在 VSIX 项目中编辑 source.extension.vsixmanifest 文件，以包含要包含在扩展中的所有项的项。 当你从快捷菜单中打开 source.extension.vsixmanifest 文件时，该文件将显示在一个设计器中，该设计器提供用于在文件中编辑 XML 的 UI。 有关详细信息，请参阅 [VSIX 清单设计器](../extensibility/vsix-manifest-designer.md)。

必须将条目添加到以下项的 source.extension.vsixmanifest 文件中：

- 扩展程序集。

- 实现扩展所使用的任何 SharePoint 命令的程序集。

- 与扩展关联的任何项目模板或项模板。

- 与扩展关联的模板的自定义向导。

下面的过程介绍如何为每个项将条目添加到 source.extension.vsixmanifest 文件。

#### <a name="to-include-the-extension-assembly"></a>包括扩展程序集

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 " **打开**"。

     文件将在设计器中打开

2. 在编辑器的 " **资产** " 选项卡上，选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

3. 在 " **类型** " 列表中，选择 " **VisualStudio. microsoft.visualstudio.mefcomponent**"。

4. 在 " **源** " 列表中，执行以下步骤之一：

    - 如果扩展程序集是从与 VSIX 项目相同的解决方案中的项目生成的，请选择 " **当前解决方案中的项目**"。 在 " **项目** " 列表中，选择项目的名称。

    - 如果扩展程序集以文件的形式包含在项目中，请选择 **"文件系统"**。 在 " **路径** " 列表中，输入扩展程序集文件的完整路径，或使用 " **浏览** " 按钮查找并选择程序集文件。

5. 选择“确定”  按钮。

#### <a name="to-include-a-sharepoint-command-assembly"></a>包括 SharePoint 命令程序集

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 " **打开** " 按钮。

     文件将在设计器中打开。

2. 在编辑器的 " **资产** " 部分中，选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

3. 在 "**类型**" 框中 **，输入 "node.js"。**

4. 在 " **源** " 列表中，执行以下步骤之一：

    - 如果命令程序集是使用与 VSIX 项目相同的解决方案中的项目生成的，请选择 " **当前解决方案中的项目**"。 在 " **项目** " 列表中，选择项目的名称。

    - 如果命令程序集以文件的形式包含在项目中，请选择 **"文件系统"**。 在 " **路径** " 列表中，输入扩展程序集文件的完整路径，或使用 " **浏览** " 按钮查找并选择程序集文件。

5. 选择“确定”  按钮。

#### <a name="to-include-a-template-that-you-create"></a>包含您创建的模板

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 " **打开** " 按钮。

     文件将在设计器中打开。

2. 在编辑器的 " **资产** " 部分中，选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

3. 在 " **类型** " 列表中，选择 " **VisualStudio** " 或 " **VisualStudio**"。

4. 在 " **源** " 列表中，选择 " **当前解决方案中的项目**"。

5. 在 " **项目** " 列表中，选择项目的名称，然后选择 **"确定"** 按钮。

6. 在 **解决方案资源管理器**中，打开项目模板或项模板项目的快捷菜单，然后选择 " **卸载项目**"。

7. 再次打开项目节点的快捷菜单，然后选择 " **编辑**_YourTemplateProjectName_**" 或 "** **编辑**_YourTemplateProjectName_**.vbproj**"。

8. `VSTemplate`在项目文件中查找以下元素。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
    ```

9. 将此元素替换为以下 XML。

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     `OutputSubPath`元素指定在生成项目时创建项目模板的路径中的其他文件夹。 此处指定的文件夹确保项模板仅在客户打开 " **添加新项目** " 对话框时可用，展开 " **SharePoint** " 节点，然后选择 " **2010** " 节点。

10. 保存并关闭该文件。

11. 在 **解决方案资源管理器**中，打开项目模板或项模板项目的快捷菜单，然后选择 " **重新加载项目**"。

#### <a name="to-include-a-template-that-you-create-manually"></a>添加手动创建的模板

1. 在 VSIX 项目中，将一个新文件夹添加到项目中以包含模板。

2. 在此新文件夹下，创建以下子文件夹，然后将模板 ( .zip) 文件添加到 *区域设置 ID* 文件夹中。

     *YourTemplateFolder*

     **SharePoint**

     **SharePoint14**

     *区域设置 ID*

     *YourTemplateName*.zip

     例如，如果你有一个名为 ContosoCustomAction.zip 的项模板，该模板支持英语 (美国) 区域设置，则可能 *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*完整路径。

3. 在 **解决方案资源管理器**中，选择 (*YourTemplateName*) 的模板文件。

4. 在 " **属性** " 窗口中，将 " **生成操作** " 属性设置为 " **内容**"。

5. 打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 " **打开**"。

     文件将在设计器中打开。

6. 在编辑器的 " **资产** " 部分中，选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

7. 在 " **类型** " 列表中，选择 " **VisualStudio** " 或 " **ProjectTemplate**"。

8. 在 " **源** " 列表中，选择 **文件系统上的文件**。

9. 在 " **路径** " 字段中，输入程序集的完整路径 (例如， *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*，或使用 " **浏览** " 按钮查找并选择程序集，然后选择 " **确定"** 按钮。

#### <a name="to-include-a-wizard-for-a-project-template-or-item-template"></a>为项目模板或项模板包含向导

1. 在 VSIX 项目中，打开 source.extension.vsixmanifest 文件的快捷菜单，然后选择 " **打开**"。

     文件将在设计器中打开。

2. 在编辑器的 " **资产** " 部分中，选择 " **新建** " 按钮。

     此时将打开 " **添加新资产** " 对话框。

3. 在 " **类型** " 列表中，选择 " **VisualStudio**"。

4. 在 " **源** " 列表中，执行以下步骤之一：

    - 如果向导程序集是从与 VSIX 项目相同的解决方案中的项目生成的，则选择 " **当前解决方案中的项目**"。 在 " **项目** " 列表中，选择项目的名称。

    - 如果向导程序集以文件的形式包含在项目中，请选择 **"文件系统"**。 在 " **路径** " 字段中，输入程序集文件的完整路径，或使用 " **浏览** " 按钮查找并选择程序集。

5. 选择“确定”  按钮。

### <a name="related-walkthroughs"></a>相关演练

下表列出了演示如何使用 VSIX 项目部署不同类型的 SharePoint 工具扩展的演练。

|扩展类型|相关演练|
|--------------------|--------------------------|
|仅包含扩展程序集的扩展|[演练：扩展 SharePoint 项目项类型](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)<br /><br /> [演练：创建 SharePoint 项目扩展](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)<br /><br /> [演练：在服务器资源管理器扩展中调入 SharePoint 客户端对象模型](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)|
|包含 SharePoint 命令的扩展插件|[演练：为 SharePoint 项目创建自定义部署步骤](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)<br /><br /> [演练：扩展服务器资源管理器以显示 web 部件](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)<br /><br /> [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|
|包含 Visual Studio 模板的扩展|[演练：使用项模板创建自定义操作项目项（第1部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)<br /><br /> [演练：使用项目模板创建网站栏项目项（第1部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)|
|包含模板向导的扩展|[演练：使用项模板创建自定义操作项目项（第2部分）](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)<br /><br /> [演练：使用项目模板创建网站栏项目项（第2部分）](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|

## <a name="create-vsix-packages-manually"></a>手动创建 VSIX 包

若要为 SharePoint 工具扩展手动创建 VSIX 包，请执行以下步骤：

1. 在新文件夹中创建 source.extension.vsixmanifest 文件和 [Content_Types] .xml 文件。 有关详细信息，请参阅 [VSIX 包的解析](../extensibility/anatomy-of-a-vsix-package.md)。

2. 在 Windows 资源管理器中，右键单击包含两个 XML 文件的文件夹，单击 "发送到"，然后单击 "压缩 (zipped) 文件夹。 将生成的 .zip 文件重命名为 Filename.vsix，其中 Filename 是用于安装包的可再发行文件的名称。

3. 将扩展程序集添加到 VSIX 包。 如果您的扩展插件包含一个 SharePoint 命令，还应将实现 SharePoint 命令的程序集添加到 VSIX 包。

4. 修改 source.extension.vsixmanifest 文件：

    - `Microsoft.VisualStudio.MefComponent`在元素下添加一个元素 `Assets` ，然后将新元素的值设置为在 VSIX 包中实现扩展的程序集的相对路径。 有关详细信息，请参阅 [Microsoft.visualstudio.mefcomponent 元素 (VSX Schema) ](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\))。

    - 如果你的扩展插件包含调用到 SharePoint 服务器对象模型的 SharePoint 命令，请在 `Microsoft.VisualStudio.Assembly` 元素下添加一个元素 `Assets` 。 将新元素的值设置为实现 VSIX 包中的 SharePoint 命令的程序集的相对路径。 有关详细信息，请参阅 [资产元素 (VSX 架构) ](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737)。

    - 如果扩展插件包括项目模板或项模板，请 `ProjectTemplate` `ItemTemplate` 在元素下添加或元素 `Assets` 。 将新元素的值设置为包含 VSIX 包中的模板的文件夹的相对路径。 有关详细信息，请参阅 [ProjectTemplate 元素 (VSX schema) ](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\)) 和 [ITEMTEMPLATE 元素 (VSX 架构) ](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\))。

    - 如果扩展插件包含用于项目模板或项模板的自定义向导，请 `Assembly` 在元素下添加 `Assets` 元素。 将新元素的值设置为 VSIX 包中的程序集的相对路径，然后将 `AssemblyName` 属性设置为完整的程序集名称 (包括版本、区域性和公钥标记) 。 有关详细信息，请参阅 [依赖关系元素 (VSX 架构) ](https://msdn.microsoft.com/1f63f60a-98ad-48ec-8e44-4eba383d3e37)。

### <a name="example"></a>示例

下面的示例演示了 SharePoint 工具扩展的 source.extension.vsixmanifest 文件的内容。 在名为 Contoso.ProjectExtension.dll 的程序集中实现该扩展。 该扩展插件包括一个名为 Contoso.ExtensionCommands.dll 的 SharePoint 命令程序集，以及一个名为 " **ItemTemplates** " 的文件夹中的项模板。 此示例假定两个程序集位于 VSIX 包中与 source.extension.vsixmanifest 文件相同的文件夹中。

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

## <a name="see-also"></a>另请参阅

- [扩展 SharePoint 项目系统](../sharepoint/extending-the-sharepoint-project-system.md)
- [扩展中的 "SharePoint 连接" 节点服务器资源管理器](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [调入 SharePoint 对象模型](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Visual Studio 中的 SharePoint 工具的调试扩展](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
