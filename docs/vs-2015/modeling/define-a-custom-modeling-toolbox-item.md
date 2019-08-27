---
title: 定义一个自定义建模工具箱项 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, customizing the toolbox
ms.assetid: a2463606-1100-40ac-97f3-5ba22ca47b7c
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: fc8bcd7a373ab6ee63e32b5873fd149001137511
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433189"
---
# <a name="define-a-custom-modeling-toolbox-item"></a>定义自定义建模工具箱项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

为了能够轻松地基于经常使用的模式创建一个元素或一组元素，你可以在 Visual Studio 中向建模图的工具箱添加新工具。 你可以将这些工具箱项分发给其他 Visual Studio 用户。  
  
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
 自定义工具在关系图中创建一个或多个新元素。 例如，可以制作一个自定义工具来创建以下元素：  
  
- 链接到 .NET 配置文件的包和具有 .NET 构造型的类。  
  
- 由关联链接的用于表示观察者模式的一对类。  
  
> [!NOTE]
> 你可以使用此方法来创建元素工具。 也就是说，你可以创建将从工具箱拖到关系图上的工具。 你不能创建连接器工具。  
  
## <a name="DefineTool"></a> 定义自定义建模工具  
  
#### <a name="to-define-a-custom-modeling-tool"></a>定义自定义建模工具  
  
1. 创建包含一个元素或一组元素的 UML 关系图。  
  
    - 这些元素之间可以具有关系，也可以具有端口、特性、操作或插针等附属元素。  
  
2. 命名新工具并以此来保存关系图。 上**文件**菜单中，使用**保存...作为**。  
  
3. 使用 Windows 资源管理器，将两个关系图文件复制到以下文件夹或任何子文件夹中：  
  
     *YourDocuments* **\Visual Studio\Architecture Tools\Custom 工具箱项**  
  
    - 如果不存在此文件夹，请进行创建。 可能需要创建这两项**体系结构工具**并**自定义工具箱项**。  
  
    - 复制这两个关系图文件，另一个使用的名称以"...**关系图**"和另一个结束的名称以"...**diagram.layout**"  
  
    - 你可以随意创建任意多个自定义工具。 为每个工具使用一个关系图。  
  
4. （可选）创建 **.tbxinfo**文件中所述[如何定义自定义工具属性](#tbxinfo)，并将其添加到同一个目录。 这样，便可以定义工具箱图标、工具提示等。  
  
    - 将单个 **.tbxinfo**文件可用于定义多个工具。 该文件可以引用子文件夹中的关系图文件。  
  
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
  
## <a name="tbxinfo"></a> 如何定义的自定义工具属性  
 工具箱信息 (**.tbxinfo**) 文件，可以指定工具箱名称、 图标、 工具提示、 选项卡上，并帮助对一个或多个自定义工具的关键字。 为其指定任何名称，例如**MyTools.tbxinfo**。  
  
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
  
  中的节点 **.tbxinfo**文件如下所示。 每个节点都有一个默认值。  
  
|节点名称|定义|  
|---------------|-------------|  
|displayName|工具箱项的名称。|  
|tabName|应在其中显示该项的工具箱选项卡。 可以指定此类型关系图的常规选项卡名称，或者指定一个单独的名称。|  
|图像|位图的位置 (**.bmp**) 文件，其必须具有高度和宽度为 16，颜色深度为 24 位。|  
|f1Keyword|用于定位帮助主题的关键字。|  
|工具提示|此工具的工具提示。|  
  
 可以在 Visual Studio 中编辑位图文件，并在“属性”窗口中将其高度和宽度设置为 16。  
  
> [!NOTE]
> 如果在单独试用关系图文件后开始使用 .tbxinfo 文件，则可能会发现工具箱同时包含新旧版本的工具箱项。 如果在 .tbxinfo 文件中键入了错误的关系图文件名称，也会发生此问题。 如果发生这种情况，工具箱的快捷菜单上选择**重置工具箱**。 将不会显示自定义工具箱项。 重新启动 Visual Studio，此时将显示正确的自定义项。  
  
## <a name="Extension"></a> 如何将分发在 Visual Studio 扩展中的工具箱项  
 您可以将分发到其他的工具箱项[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]用户通过将它们打包到 Visual Studio 扩展 (VSIX)。 可以将命令、配置文件和其他扩展打包到同一个 VSIX 文件。 有关详细信息，请参阅[部署 Visual Studio 扩展](http://go.microsoft.com/fwlink/?LinkId=160780)。  
  
 通常使用 VSIX 项目模板来构建 Visual Studio 扩展。 若要执行此操作，必须已安装 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]。  
  
#### <a name="to-add-a-toolbox-item-to-a-visual-studio-extension"></a>向 Visual Studio 扩展添加工具箱项  
  
1. [创建和测试一个或多个自定义工具](#DefineTool)。  
  
2. [创建.tbxinfo 文件](#tbxinfo)引用这些工具。  
  
3. 打开现有 Visual Studio 扩展项目。  
  
     \- 或 -  
  
     定义新的 Visual Studio 扩展项目。  
  
    1. 在“文件”  菜单上，选择“新建” 、“项目” 。  
  
    2. 在中**新的项目**对话框中的**已安装的模板**，选择**Visual C#**，**扩展性**， **VSIX项目**。  
  
4. 将工具箱定义添加到项目。 包括 **.tbxinfo**文件中，关系图文件、 位图文件和所有资源文件，并确保它们都包括在 VSIX 中。  
  
    - 在解决方案资源管理器，在该 VSIX 项目的快捷菜单上选择**外**，**现有项**。 在对话框中，将**对象的类型：所有文件**。 找到的文件，它们全部选中，并选择**添加**。  
  
        > [!NOTE]
        > 在此项目中，你不能在模型编辑器中打开关系图文件。  
  
5. 设置刚添加的所有文件的以下属性。 通过在解决方案资源管理器中选择所有文件，可以同时设置这些属性。 请注意不要更改项目中其他文件的属性。  
  
     **复制到输出目录** = **始终复制**  
  
     **生成操作** = **内容**  
  
     **包括在 VSIX** = **，则返回 true**  
  
6. 打开 **source.extension.vsixmanifest**。 它将在扩展清单编辑器中打开。  
  
7. 下**元数据**，添加自定义工具的说明。  
  
     下**资产**，选择**新建**然后将字段设置在对话框中，如下所示：  
  
    - **类型** = **自定义扩展插件类型**  
  
    - “类型”= `Microsoft.VisualStudio.ArchitectureTools.CustomToolboxItems`  
  
        > [!NOTE]
        > 这并不是下拉列表中的选项。 你必须使用键盘进行输入。  
  
    - **源** = **在文件系统上的文件**。  
  
    - **路径**= 你 **.tbxinfo**文件，如**MyTools.tbxinfo**  
  
8. 生成项目。  
  
9. **若要验证该扩展适用**，按 F5。 启动 Visual Studio 的实验实例。  
  
     在实验实例中，创建或打开相关类型的 UML 关系图。 验证新工具是否显示在工具箱中以及能否正确创建元素。  
  
10. **若要获取部署的 VSIX 文件：** 在 Windows 资源管理器中，打开文件夹 **.\bin\Debug**或 **.\bin\Release**若要查找 **.vsix**文件。 此文件是 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 扩展文件。 可将其安装在自己的计算机上，也可以发送给其他 Visual Studio 用户。  
  
#### <a name="to-install-custom-tools-from-a-visual-studio-extension"></a>从 Visual Studio 扩展安装自定义工具  
  
1. 在 Windows 资源管理器或 Visual Studio 中，打开 `.vsix` 文件。  
  
2. 选择**安装**中出现的对话框。  
  
3. 若要卸载或临时禁用该扩展，打开**扩展和更新**从**工具**菜单。  
  
## <a name="localization"></a>本地化  
 构建一个扩展，使其在安装到另一台计算机中时，以目标计算机语言显示工具名称和工具提示。  
  
#### <a name="to-provide-versions-of-the-tool-in-more-than-one-language"></a>提供多种语言的工具版本  
  
1. 创建包含一个或多个自定义工具的 Visual Studio 扩展项目。  
  
    在中 **.tbxinfo**文件，请使用资源文件方法来定义该工具`displayName`，工具箱`tabName`，和工具提示。 创建在其中定义了这些字符串的资源文件，将该文件编译到一个程序集中，并从 tbxinfo 文件中对其进行引用。  
  
2. 创建包含具有其他语言字符串的资源文件的附加程序集。  
  
3. 将每个附加程序集放在名称为对应语言区域性代码的文件夹中。 例如，名为的文件夹中将法语版本的程序集**fr**。  
  
4. 应使用非特定区域性代码（通常为两个字母），而不应使用特定区域性代码（例如 `fr-CA`）。 有关区域性代码的详细信息，请参阅[CultureInfo.GetCultures 方法](http://go.microsoft.com/fwlink/?LinkId=160782)，提供区域性代码的完整列表。  
  
5. 生成 Visual Studio 扩展并发布。  
  
6. 在另一台计算机上安装该扩展后，将自动加载用户本地区域性的资源文件的版本。 如果尚未提供用户区域性的版本，则将使用默认资源。  
  
   不能使用此方法来安装不同版本的原型关系图。 在每次安装中，元素和连接器的名称都是相同的。  
  
## <a name="other-toolbox-operations"></a>其他工具箱操作  
 通常，在 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 中，可以通过重命名工具、将工具移到不同的工具箱选项卡以及删除工具来个性化工具箱。 但这些更改不会如本主题中描述的创建步骤一样可以保存自定义建模工具。 重新启动 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 时，会重新显示自定义工具及其定义的名称和工具箱位置。  
  
 如果您执行此外，您自定义工具将消失**重置工具箱**命令。 但是，当重新启动 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 时，它们将重新显示。  
  
## <a name="see-also"></a>请参阅  
 [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)   
 [定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)   
 [在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [为 UML 模型定义验证约束](../modeling/define-validation-constraints-for-uml-models.md)
