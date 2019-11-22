---
title: Define a custom modeling toolbox item | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, customizing the toolbox
ms.assetid: a2463606-1100-40ac-97f3-5ba22ca47b7c
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ac299f18e544ef4f3215707abbdc3d9e8d266de6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299289"
---
# <a name="define-a-custom-modeling-toolbox-item"></a>定义自定义建模工具箱项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

为了能够轻松地基于经常使用的模式创建一个元素或一组元素，你可以在 Visual Studio 中向建模图的工具箱添加新工具。 你可以将这些工具箱项分发给其他 Visual Studio 用户。

 若要查看支持此功能的 Visual Studio 的版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。

 自定义工具在关系图中创建一个或多个新元素。 例如，可以制作一个自定义工具来创建以下元素：

- 链接到 .NET 配置文件的包和具有 .NET 构造型的类。

- 由关联链接的用于表示观察者模式的一对类。

> [!NOTE]
> 你可以使用此方法来创建元素工具。 也就是说，你可以创建将从工具箱拖到关系图上的工具。 你不能创建连接器工具。

## <a name="DefineTool"></a> Defining a Custom Modeling Tool

#### <a name="to-define-a-custom-modeling-tool"></a>定义自定义建模工具

1. 创建包含一个元素或一组元素的 UML 关系图。

    - 这些元素之间可以具有关系，也可以具有端口、特性、操作或插针等附属元素。

2. 命名新工具并以此来保存关系图。 On the **File** menu, use **Save…As**.

3. 使用 Windows 资源管理器，将两个关系图文件复制到以下文件夹或任何子文件夹中：

     *YourDocuments* **\Visual Studio\Architecture Tools\Custom Toolbox Items**

    - 如果不存在此文件夹，请进行创建。 You might have to create both **Architecture Tools** and **Custom Toolbox Items**.

    - Copy both diagram files, one with a name that ends "…**diagram**" and the other with a name that ends "…**diagram.layout**"

    - 你可以随意创建任意多个自定义工具。 为每个工具使用一个关系图。

4. (Optional) Create a **.tbxinfo** file as described in [How to Define the Properties of Custom Tools](#tbxinfo), and add it to the same directory. 这样，便可以定义工具箱图标、工具提示等。

    - A single **.tbxinfo** file can be used to define several tools. 该文件可以引用子文件夹中的关系图文件。

5. 重新启动 Visual Studio。 其他工具会显示在相应类型关系图的工具箱中。

### <a name="what-the-custom-tool-will-replicate"></a>自定义工具将复制的内容
 自定义工具会复制源关系图的大部分功能：

- 名称。 当从工具箱中创建项时，必要时会在名称末尾添加数字以避免在同一命名空间出现重复名称。

- 颜色、大小和形状

- 构造型和包配置文件

- 属性值，如 Is Abstract

- 链接的工作项

- 关系的重数和其他属性

- 形状的相对位置。

  将不会在自定义工具中保留以下功能：

- 简单形状。 这些形状与模型元素无关，并可以在某些类型的关系图中绘制。

- 连接器路由。 如果手动传送连接器，则在使用你的工具时不会保留该路由。 一些嵌套形状（如端口）的位置不会相对于其所有者而保留。

## <a name="tbxinfo"></a> How to Define the Properties of Custom Tools
 A toolbox information ( **.tbxinfo**) file allows you to specify a toolbox name, icon, tooltip, tab, and help keyword for one or more custom tools. Give it any name, such as **MyTools.tbxinfo**.

 该文件的一般形式如下所示：

```
<?xml version="1.0" encoding="utf-8" ?>
<customToolboxItems xmlns="http://schemas.microsoft.com/visualstudio/[version]/ArchitectureTools/CustomToolboxItems">
  <customToolboxItem fileName="MyObserverTool.classdiagram">
    <displayName>
       <value>Observer Pattern</value>
    </displayName>
    <tabName>
       <value>UML Class Diagram</value>
    </tabName>
    <image><bmp fileName="ObserverPatternIcon.bmp"/></image>
    <f1Keyword>
      <value>ObserverPatternHelp</value>
    </f1Keyword>
    <tooltip>
       <value>Create a pair of classes</value>
    </tooltip>
  </customToolboxItem>
</customToolboxItems>
```

 每项的值可为：

- 如示例中所示，工具箱图标的值为 `<bmp fileName="…"/>`，而其他项的值为 `<value>string</value>`。

  \- 或 -

- `<resource fileName="Resources.dll"`

   `baseName="Observer.resources" id="Observer.tabname" />`

   在这种情况下，你提供一个已编译程序集，其中字符串值已编译为资源。

  为想要定义的每个工具箱添加一个 `<customToolboxItem>` 节点。

  The nodes in the **.tbxinfo** file are as follows. 每个节点都有一个默认值。

|节点名称|定义|
|---------------|-------------|
|displayName|工具箱项的名称。|
|tabName|应在其中显示该项的工具箱选项卡。 可以指定此类型关系图的常规选项卡名称，或者指定一个单独的名称。|
|图像|The location of the bitmap ( **.bmp**) file, which must have height and width of 16, and a color depth of 24 bits.|
|f1Keyword|用于定位帮助主题的关键字。|
|工具提示|此工具的工具提示。|

 可以在 Visual Studio 中编辑位图文件，并在“属性”窗口中将其高度和宽度设置为 16。

> [!NOTE]
> 如果在单独试用关系图文件后开始使用 .tbxinfo 文件，则可能会发现工具箱同时包含新旧版本的工具箱项。 如果在 .tbxinfo 文件中键入了错误的关系图文件名称，也会发生此问题。 If this occurs, on the shortcut menu of the toolbox choose **Reset Toolbox**. 将不会显示自定义工具箱项。 重新启动 Visual Studio，此时将显示正确的自定义项。

## <a name="Extension"></a> How to Distribute Toolbox Items in a Visual Studio Extension
 You can distribute toolbox items to other [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] users by packaging them into a Visual Studio Extension (VSIX). 可以将命令、配置文件和其他扩展打包到同一个 VSIX 文件。 For more information, see [Deploying Visual Studio Extensions](https://go.microsoft.com/fwlink/?LinkId=160780).

 通常使用 VSIX 项目模板来构建 Visual Studio 扩展。 若要执行此操作，必须已安装 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]。

#### <a name="to-add-a-toolbox-item-to-a-visual-studio-extension"></a>向 Visual Studio 扩展添加工具箱项

1. [Create and test one or more custom tools](#DefineTool).

2. [Create a .tbxinfo file](#tbxinfo) that references the tools.

3. 打开现有 Visual Studio 扩展项目。

     \- 或 -

     定义新的 Visual Studio 扩展项目。

    1. 在“文件” 菜单上，选择“新建”、“项目”。

    2. In the **New Project** dialog box, under **Installed Templates**, choose **Visual C#** , **Extensibility**, **VSIX project**.

4. 将工具箱定义添加到项目。 Include the **.tbxinfo** file, the diagram files, bitmap files, and any resource files, and make sure that they are included in the VSIX.

    - In Solution Explorer, on the shortcut menu of the VSIX project, choose **Add**, **Existing Item**. In the dialog box, set **Objects of Type: All Files**. Locate the files, select them all, and then choose **Add**.

        > [!NOTE]
        > 在此项目中，你不能在模型编辑器中打开关系图文件。

5. 设置刚添加的所有文件的以下属性。 通过在解决方案资源管理器中选择所有文件，可以同时设置这些属性。 请注意不要更改项目中其他文件的属性。

     **Copy to Output Directory** = **Copy Always**

     **Build Action** = **Content**

     **Include in VSIX** = **true**

6. 打开 **source.extension.vsixmanifest**。 它将在扩展清单编辑器中打开。

7. Under **Metadata**, add a description for the custom tools.

     Under **Assets**, choose **New** and then set the fields in the dialog as follows:

    - **Type** = **Custom Extension Type**

    - “类型”= `Microsoft.VisualStudio.ArchitectureTools.CustomToolboxItems`

        > [!NOTE]
        > 这并不是下拉列表中的选项。 你必须使用键盘进行输入。

    - **Source** = **File on filesystem**.

    - **Path** = your **.tbxinfo** file, for example **MyTools.tbxinfo**

8. 生成项目。

9. **To verify that the extension works**, press F5. 启动 Visual Studio 的实验实例。

     在实验实例中，创建或打开相关类型的 UML 关系图。 验证新工具是否显示在工具箱中以及能否正确创建元素。

10. **To obtain a VSIX file for deployment:** In Windows Explorer, open the folder **.\bin\Debug** or **.\bin\Release** to find the **.vsix** file. 此文件是 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展文件。 可将其安装在自己的计算机上，也可以发送给其他 Visual Studio 用户。

#### <a name="to-install-custom-tools-from-a-visual-studio-extension"></a>从 Visual Studio 扩展安装自定义工具

1. 在 Windows 资源管理器或 Visual Studio 中，打开 `.vsix` 文件。

2. Choose **Install** in the dialog box that appears.

3. To uninstall or temporarily disable the extension, open **Extensions and Updates** from the **Tools** menu.

## <a name="localization"></a>本地化
 构建一个扩展，使其在安装到另一台计算机中时，以目标计算机语言显示工具名称和工具提示。

#### <a name="to-provide-versions-of-the-tool-in-more-than-one-language"></a>提供多种语言的工具版本

1. 创建包含一个或多个自定义工具的 Visual Studio 扩展项目。

    In the **.tbxinfo** file, use the resource file method to define the tool's `displayName`, toolbox `tabName`, and the tooltip. 创建在其中定义了这些字符串的资源文件，将该文件编译到一个程序集中，并从 tbxinfo 文件中对其进行引用。

2. 创建包含具有其他语言字符串的资源文件的附加程序集。

3. 将每个附加程序集放在名称为对应语言区域性代码的文件夹中。 For example, place a French version of the assembly inside a folder that is named **fr**.

4. 应使用非特定区域性代码（通常为两个字母），而不应使用特定区域性代码（例如 `fr-CA`）。 For more information about culture codes, see [CultureInfo.GetCultures method](https://go.microsoft.com/fwlink/?LinkId=160782), which provides a complete list of culture codes.

5. 生成 Visual Studio 扩展并发布。

6. 在另一台计算机上安装该扩展后，将自动加载用户本地区域性的资源文件的版本。 如果尚未提供用户区域性的版本，则将使用默认资源。

   不能使用此方法来安装不同版本的原型关系图。 在每次安装中，元素和连接器的名称都是相同的。

## <a name="other-toolbox-operations"></a>其他工具箱操作
 通常，在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中，可以通过重命名工具、将工具移到不同的工具箱选项卡以及删除工具来个性化工具箱。 但这些更改不会如本主题中描述的创建步骤一样可以保存自定义建模工具。 重新启动 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 时，会重新显示自定义工具及其定义的名称和工具箱位置。

 Furthermore, your custom tools will disappear if you perform the **Reset Toolbox** command. 但是，当重新启动 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 时，它们将重新显示。

## <a name="see-also"></a>请参阅
 [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md) [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md) [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md) [Define validation constraints for UML models](../modeling/define-validation-constraints-for-uml-models.md)
