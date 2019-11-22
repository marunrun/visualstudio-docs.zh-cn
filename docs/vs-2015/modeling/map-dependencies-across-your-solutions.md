---
title: Map dependencies across your solutions | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.progression.codemap
- vs.progression.standardgraphsdialog
helpviewer_keywords:
- Visual Studio Ultimate, dependency graphs
- code exploration, dependency graphs
- dependency graphs, exporting
- code exploration, relationships
- DGML
- graph documents
- code visualization [Visual Studio ALM]
- graph documents, saving
- dependencies, visualizing
- dependency graphs, saving
- Visual Studio Ultimate, code visualization
- code, visualizing
- dependency graphs, creating
- dependency graphs
- graph documents, exporting
- code exploration, visualizing
ms.assetid: e04850a2-17c5-459b-93ec-6c74143b3292
caps.latest.revision: 245
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b25d23b7c65742ffddadbe178d7550dc1794414a
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296331"
---
# <a name="map-dependencies-across-your-solutions"></a>映射解决方案中的依赖项
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要了解代码之间的依赖关系，可通过创建代码图使其可视化。 这样有助于你查看代码如何相互配合，而无需读取文件和各行代码。

 ![View dependencies across your solutions](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")

 **以下是一些相关视频**：

- [通过可视化了解代码依赖项](https://go.microsoft.com/fwlink/?LinkID=252065)

- [将更改的影响可视化](https://go.microsoft.com/fwlink/?LinkID=252068)

- [通过代码图理解复杂代码](https://go.microsoft.com/fwlink/?LinkID=259869)

## <a name="GetStarted"></a> 开始使用代码图
 **要使用代码图，将需要以下两者之一**：

- Visual Studio Enterprise：从代码编辑器、解决方案资源管理器、类视图或对象浏览器创建代码图。

- Visual Studio Professional：打开代码图、执行有限的编辑和浏览代码。

> [!WARNING]
> 在你与使用 Visual Studio Professional 的其他人共享 Visual Studio Enterprise 中创建的代码图之前，请确保代码图上的所有项（例如隐藏项、展开的组和跨组链接）均可见。

 **可以映射以下语言中的代码的依赖关系**：

- 解决方案或程序集（.dll 或 .exe）中的 Visual C# .NET 或 Visual Basic .NET

- Visual C++ 项目、头文件（.h 或 `#include`）或二进制文件中的本机或托管的 C 或 C++ 代码

- 通过 Microsoft Dynamics AX 的 .NET 模块生成的 X++ 项目和程序集

  **注意：** 除 C# 或 Visual Basic .NET 之外的项目，启动代码图或将项目添加到现有代码图的选项变得非常有限。 例如，不能用鼠标右键单击 C++ 项目的文本编辑器中的对象并将其添加到代码图。 但是，你可以从解决方案资源管理器、类视图和对象浏览器拖放各个代码元素或文件。

#### <a name="to-see-the-overall-dependencies-across-your-solution"></a>若要查看解决方案中的整体依赖关系

1. 打开“体系结构” 菜单。

2. 如果只是打开了解决方案而尚未生成解决方案，或者如果自上次生成代码以来代码已更改，则选择“生成解决方案的代码图”。

3. 如果代码自上次生成后未发生更改，选择“无需构造生成解决方案的代码图” 可在创建代码图时提高性能。

4. [查看整体依赖关系](#SeeOverviewSource) 以了解如何使用代码图来查看解决方案中的整体依赖关系。

#### <a name="to-see-specific-dependencies-within-your-solution"></a>要查看解决方案中的特定依赖关系

1. 在加载了解决方案的情况下，打开“解决方案资源管理器”。

2. 选择需映射的所有项目、程序集引用、文件夹、文件、类型或成员。

3. On the **Solution Explorer** toolbar, choose **Show on Code Map**![Create New Graph From Selected Nodes Button](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton"). 或者打开快捷菜单并选择“在代码图上显示”。 还可以将项从类视图或对象浏览器拖到新代码图或现有代码图中。

4. [查看特定依赖关系](#SeeSpecificSource) 以了解可如何使用代码图来查看解决方案中的特定依赖关系。

### <a name="CreateEmptyMap"></a> 向解决方案中添加新的空代码图

1. 在“解决方案资源管理器”中，打开顶级解决方案节点的快捷菜单。 选择“添加” ，然后选择“新项”。

2. 在“已安装”下，选择“常规”。

3. 在右窗格中，选择“定向关系图文档” ，然后选择“添加”。

     你现在具有一个空白的代码图，它显示在解决方案的“解决方案项” 文件夹中。

#### <a name="to-create-a-new-empty-code-map-without-adding-it-to-your-solution"></a>创建新的空代码图，而无需将其添加到解决方案中

1. 打开“体系结构” 菜单，然后选择“新建代码图”。

     \- 或 -

2. 打开“文件” 菜单，然后依次选择“新建” 和“文件”。

3. 在“已安装”下，选择“常规”。

4. 在右窗格中，选择“定向关系图文档” ，然后选择“打开”。

     你现在具有一个空白的代码图，它未显示在解决方案的文件夹中。

## <a name="SeeOverviewSource"></a> 查看整体依赖关系

### <a name="OverviewSource"></a> 查看解决方案中的依赖关系

1. 在“体系结构” 菜单上，选择“生成解决方案的代码图”。

    ![Generate a code map command](../modeling/media/codemapsarchitecturemenu.png "CodeMapsArchitectureMenu")

    你将获得显示顶级程序集和这些程序集之间的聚合链接的代码图。 聚合链路越广，它所代表的依赖关系就越多。

2. 使用代码图工具栏上的“图例” 按钮以显示或隐藏项目类型图标（如测试项目、Web 项目和 Phone 项目）、代码项（如类、方法和属性）以及关系类型（如继承自、实现和调用）的列表。

    ![Top&#45;level dependency graph of assemblies](../modeling/media/dependencygraph-toplevelassemblies.png "DependencyGraph_TopLevelAssemblies")

    此示例解决方案包含解决方案文件夹（“测试” 和“组件”），测试项目、Web 项目和程序集。 默认情况下，所有包含关系均以 *“组”* 的形式显示，你可以对其进行展开和折叠。 “外部”组包含你的解决方案之外的任何内容，包括平台依赖项。 外部程序集仅显示已使用的项。 默认情况下，系统基类型隐藏在代码图中以减少混乱。

3. 若要深入了解代码图中，请展开表示项目和程序集的组。 可以通过按“CTRL+A” 展开全部内容以选择所有节点，然后选择“组”，再选择快捷菜单中的“展开” 。

    ![Expanding all groups in a code map](../modeling/media/codemapsexpandallgroups.png "CodeMapsExpandAllGroups")

4. 但是，这对大型解决方案可能并无作用。 事实上，对于复杂的解决方案，内存限制可能会阻止你展开所有组。 相反，若要在单个节点内进行查看，则将其展开。 将鼠标指针移动到节点的顶部，然后单击出现的 V 形。

    ![Expanding a node in a code map](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")

    或使用键盘选择项，然后按加号键（“+” **+** ）。 若要查看更深层次的代码，请对命名空间、类型和成员执行相同操作。

   > [!TIP]
   > For more details of working with code maps using the mouse, keyboard, and touch, see [Browse and rearrange code maps](../modeling/browse-and-rearrange-code-maps.md).

5. 若要简化代码图并将重点关注各个部分，选择代码图工具栏上的“筛选器” ，然后仅选择你感兴趣的节点和链接类型。 例如，可以隐藏所有的解决方案文件夹和程序集容器。

    ![Simplify the map by filtering containers](../modeling/media/codemapsfilterfoldersassemblies.png "CodeMapsFilterFoldersAssemblies")

    还可以通过从代码图中隐藏或删除单个组和项来简化代码图，而不影响基础解决方案代码。

6. 若要查看各项间的关系，请在代码图中选择各项。 链接的颜色指示关系的类型，如“图例” 窗格中所示。

    ![View dependencies across your solutions](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")

    在此示例中，紫色链接为调用，点式链接为引用，浅蓝色链接为字段访问。 绿色链接可以是继承，也可能是指示一个以上关系（或 *“类别”* ）类型的 *“聚合链接”* 。

   > [!TIP]
   > 如果你看到的是绿色链接，它是指可能不仅仅存在继承关系。 可能也存在方法调用，但是这些都被继承关系所隐藏。 若要查看特定类型的链接，请使用“筛选器” 窗格中的复选框，以便隐藏不感兴趣的类型。

7. 若要获取有关项或链接的详细信息，请将指针移至其顶部，直至出现工具提示。 这将显示代码元素或链接所表示的类别的详细信息。

    ![Show the categories of a relationship](../modeling/media/codemapsshowlinkcatgories.png "CodeMapsShowLinkCatgories")

8. 若要检查聚合链接表示的项和依赖项，请首先选择该链接，然后打开它的快捷菜单。 选择“显示参与链接” （或“在新代码图上显示参与链接”）。 这将展开位于链接两端的组，且仅显示参与链接的项和依赖项。

9. 若要关注代码图的特定部分，可继续删除不感兴趣的项。 例如，若要深入了解类和成员视图，只需筛选“筛选器” 窗格中的所有命名空间节点。

     ![Drilling down to class and member level](../modeling/media/dependencygraph-expandedselectedgroups-2012.png "DependencyGraph_ExpandedSelectedGroups_2012")

10. 集中精力处理复杂的解决方案代码图的另一种方式是从现有代码图生成包含选定项的新代码图。 按住“CTRL” 同时选择需关注的项，打开快捷菜单并选择“从选定内容新建图”。

     ![Show selected items on a new code map](../ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")

11. 将包含上下文转入新代码图。 使用“筛选器” 窗格隐藏解决方案文件夹以及不想看到的任何其他容器。

     ![Filter the containers to simplify the view](../modeling/media/codemapsexpandnewgroups.png "CodeMapsExpandNewGroups")

12. 展开组，选择代码图中的项，以便查看关系。

     ![Select items to view the relationships](../modeling/media/codemapsviewnewrelationships.png "CodeMapsViewNewRelationships")

    另请参阅：

- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)

- [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)

- 通过 [运行分析器](../modeling/find-potential-problems-using-code-map-analyzers.md)发现代码中的潜在问题。

### <a name="OverviewCompiled"></a> 查看程序集间或二进制文件间的依赖关系

1. [创建空代码图](#GetStarted)，或打开现有代码图（.dgml 文件）。

2. 将需映射的程序集或二进制文件从 Visual Studio 外部拖至代码图。 例如，从 Windows 资源管理器或文件资源管理器拖动程序集或二进制文件。

> [!NOTE]
> 仅当在相同的用户访问控制 (UAC) 权限级别运行 Windows 资源管理器或文件资源管理器以及 Visual Studio 时，才能从 Windows 资源管理器或文件资源管理器拖动程序集或二进制文件。 例如，如果启用了 UAC，并且你正以管理员身份运行 Visual Studio，则 Windows 资源管理器或文件资源管理器将阻止拖动操作。 若要解决此问题，请确保这两者以相同的权限级别运行，或者关闭 UAC。

## <a name="SeeSpecificSource"></a> 查看特定依赖关系
 例如，假设你在一些具有挂起更改的文件中执行代码审阅。 若要查看这些更改中的依赖关系，请从这些文件中创建一个代码图。

 ![Show specific dependencies on a code map](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")

### <a name="see-specific-dependencies-in-your-solution"></a>查看解决方案中特定的依赖关系

1. 打开“解决方案资源管理器”。 选择你感兴趣的项目、程序集引用、文件夹、文件、类型和成员。 若要找出与类型或成员有依赖关系的项，请从“解决方案资源管理器”中打开类型或成员的快捷菜单。 选择依赖关系类型，然后选择结果。

2. 映射你的项及其成员。 On the **Solution Explorer** toolbar click **Show on Code Map**![Create New Graph From Selected Nodes Button](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton").

     ![Select the items you want to map](../modeling/media/codemapsselectinsolutionexplorer.png "CodeMapsSelectInSolutionExplorer")

3. 代码图将显示在选定项的包含程序集内的选定项。

     ![Selected items shown as groups on the map](../modeling/media/codemapsshowitemsfromsolnexplorer.png "CodeMapsShowItemsFromSolnExplorer")

     还可以将项从解决方案资源管理器、类视图或对象浏览器拖到空白代码图或现有代码图中。 若要创建空代码图，请参阅 [创建空代码图](#GetStarted)。 若要包含项的父层次结构，在按住“CTRL” 键的同时拖动项，或者使用代码图工具栏上的“包括父级” 按钮来指定默认操作。

    > [!NOTE]
    > 当你从在多个应用程序（如 Windows Phone 或 Windows 应用商店）之间共享的项目添加项时，这些项将与当前活动的应用程序项目一起显示在代码图上。 如果你将上下文更改为另一个应用程序项目并从共享的项目添加更多项，则这些项现在将与最近活动的应用程序项目一起显示。 你对代码图上的项执行的操作仅适用于共享相同上下文的项。

4. 如要查看项，请把项展开。 将鼠标指针移动到项的顶部，然后单击出现的 V 形（向下键）。

     ![Expanding a node in a code map](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")

     若要展开所有项，使用“CTRL+A”选择它们，然后打开代码图的快捷菜单并依次选择“组”、“展开”。 然而，如果展开所有组会生成不可用的代码图或产生内存问题，则该选项不可用。

5. 根据需要，继续展开感兴趣的项，直到类和成员级别。

     ![Expand groups to class and member level](../modeling/media/codemapsexpandtoclassandmember.png "CodeMapsExpandToClassAndMember")

     To see members that are in the code but don't appear on the map, click the **Refetch Children** icon ![Refetch Children Icon](../modeling/media/dependencygraph-deletednodesicon.png "DependencyGraph_DeletedNodesIcon") in the top left corner of a group.

6. 若要查看更多与代码图上的项相关的项，请选择其中一个，再选择代码图工具栏上的“显示相关内容” ，然后选择要添加到图中的相关项的类型。 或者，选择一个或多个项，打开快捷菜单，然后为要添加到图中的相关项类型选择“显示…” 选项。 例如:

     对于 **程序集**，请选择：

    |||
    |-|-|
    |**显示此项引用的程序集**|添加此程序集引用的程序集。 外部程序集将显示在“外部” 组中。|
    |**显示引用此项的程序集**|在解决方案中添加引用此程序集的程序集。|

     对于 **命名空间**，请选择“显示包含程序集”（如果它不可见）。

     对于 **类** 或 **接口**，请选择：

    |||
    |-|-|
    |**显示基类型**|对于类，添加基类和实现的接口。<br /><br /> 对于接口，请添加基接口。|
    |**显示派生类型**|对于类，添加派生类。<br /><br /> 对于接口，请添加派生接口和实现类或结构。|
    |**显示此项引用的类型**|添加此类使用的所有类及其成员。|
    |**显示引用此项的类型**|添加使用此类的所有类及其成员。|
    |**显示包含命名空间**|添加父命名空间。|
    |**显示包含命名空间和包含程序集**|添加父容器的层次结构。|
    |**显示所有基类型**|以递归方式添加基类或接口层次结构。|
    |**显示所有派生类型**|对于类，以递归方式添加所有派生类。<br /><br /> 对于接口，请以递归方式添加所有派生接口和实现类或结构。|

     对于 **方法**，请选择：

    |||
    |-|-|
    |**显示此项调用的方法**|添加此方法调用的方法。|
    |**显示此项引用的字段**|添加此方法引用的字段。|
    |**显示包含类型**|添加父类型。|
    |**显示包含类型、包含命名空间和包含程序集**|添加父容器的层次结构。|
    |**显示重写的方法**|对于重写其他方法或者实现接口方法的方法，在已重写的基类和已实现的接口方法（如果有）中添加所有抽象方法或虚方法。|

     对于 **字段** 或 **属性**，请选择：

    |||
    |-|-|
    |**显示包含类型**|添加父类型。|
    |**显示包含类型、包含命名空间和包含程序集**|添加父容器的层次结构。|

     ![Show methods called by this member](../modeling/media/codemapsshowrelatedmethods.png "CodeMapsShowRelatedMethods")

7. 代码图显示关系。 在此示例中，则为由 `Find` 调用的方法及其在解决方案中或在外部的位置。

     ![Show specific dependencies on a code map](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")

8. 若要简化代码图并将重点关注各个部分，选择代码图工具栏上的“筛选器” ，然后仅选择你感兴趣的节点和链接类型。 例如，关闭解决方案文件夹、程序集和命名空间的显示。

     ![Use the Filter pane to simplify the display](../modeling/media/almcodemapfilterpane.png "ALMCodeMapFilterPane")

## <a name="SeeSourceHeader"></a> 了解 C 和 C++ 源文件和头文件之间的依赖关系
 如果要创建更多 C++ 项目的完整代码图，请在这些项目上设置浏览信息编译器选项 ( **/FR**)。 请参阅 [/FR, /Fr (Create .Sbr File)](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896)。 否则，将出现一条消息并提示你设置此选项。 如果选择“确定”，就只会为当前代码图设置选项。 可以选择隐藏所有之后的代码图的信息。 如果你隐藏了该信息，则可以让它再显示。 将以下注册表项设置为 `0` 或删除该项：

 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\NativeProvider : AutoEnableSbr**

 打开包含 Visual C++ 项目的解决方案时，可能需要花一些时间来更新 IntelliSense 数据库。 在此期间，你可能无法为标头（.h 或 `#include`）文件创建代码图，直到 IntelliSense 数据库完成更新。 你可在 Visual Studio 状态栏中监视更新进度。 若要解决因某些 IntelliSense 设置被禁用而导致的问题或消息，请查看 [针对 C 和 C++ 代码的故障排除图](#Troubleshooting)。

- 若要查看解决方案中所有源文件和头文件间的依赖关系，请在“体系结构” 菜单上，选择“生成包含文件的关系图”。

     ![Dependency graph for native code](../modeling/media/dependencygraphgeneral-nativecode.png "DependencyGraphGeneral_NativeCode")

- 若要查看当前打开文件和相关的源文件以及头文件之间的依赖关系，请打开相关的源文件或头文件。 在文件内的任何地方打开文件快捷菜单。 选择“生成包含文件的关系图”。

     ![First&#45;level dependency graph for .h file](../modeling/media/dependencygraph-native-firstlevel.png "DependencyGraph_Native_FirstLevel")

### <a name="Troubleshooting"></a> 针对 C 和 C++ 代码的故障排除图
 C 和 C++ 代码不支持这些项：

- 基类型不会显示在包含父层次结构的图中。

- 大多数“显示” 菜单项不适用于 C 和 C++ 代码。

  在为 C 和 C++ 代码创建代码图时可能会出现这些问题：

|**问题**|**可能的原因**|**解决方法**|
|---------------|------------------------|--------------------|
|未能生成代码图。|解决方案中没有项目成功生成过。|修复出现的生成错误，然后重新生成代码图。|
|尝试从“体系结构”[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  **菜单生成代码图时，** 无响应。|程序数据库 (.pdb) 文件可能已损坏。<br /><br /> pdb 文件将存储调试信息，例如，类型、方法和源文件信息。|重新生成解决方案，然后重试。|
|禁用 IntelliSense 浏览器数据库的某些设置。|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] “选项”对话框中可能已禁用某些 IntelliSense 设置。|打开设置以启用它们。<br /><br /> See [Options, Text Editor, C/C++, Advanced](../ide/reference/options-text-editor-c-cpp-advanced.md).|
|消息“未知方法” 将出现在方法节点上。<br /><br /> 由于无法解析方法的名称，导致出现此问题。|二进制文件可能没有基重定位表。|在链接器中打开 **/FIXED:NO** 选项。<br /><br /> 请参阅 [/FIXED (Fixed Base Address)](https://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5)。|
||无法生成程序数据库 (.pdb) 文件。<br /><br /> pdb 文件将存储调试信息，例如，类型、方法和源文件信息。|在链接器中打开 **/DEBUG** 选项。<br /><br /> 请参阅 [/DEBUG (Generate Debug Info)](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103)。|
||无法在预期位置打开或找到 .pdb 文件。|确保 .pdb 文件位于预期位置。|
||已从 .pdb 文件中去除调试信息。|如果链接器中已使用 **/PDBSTRIPPED** 选项，则改为包含完整的 .pdb 文件。<br /><br /> 请参阅 [/PDBSTRIPPED (Strip Private Symbols)](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55)。|
||调用方不是函数，它是二进制文件中的形式转换 (thunk) 或数据节中的指针。|当调用方是形式转换 (thunk) 时，尝试使用 `_declspec(dllimport)` 以避免形式转换 (thunk)。<br /><br /> 请参阅：<br /><br /> -   [General Rules and Limitations](https://msdn.microsoft.com/library/6c48902d-4259-4761-95d4-e421d69aa050)<br />-   [Importing Function Calls Using __declspec(dllimport)](https://msdn.microsoft.com/library/6b53c616-0c6d-419a-8e2a-d2fff20510b3)<br />-   [dllexport, dllimport](https://msdn.microsoft.com/library/ff95b645-ef55-4e72-b848-df44657b3208)|

## <a name="RenderMoreQuickly"></a> 使代码图更快呈现
 在首次生成代码图时，Visual Studio 会将其找到的所有依赖关系都编入索引中。 这个过程可能需要一些时间，尤其是针对大型解决方案，但会提高之后的性能。 如果更改了代码，Visual Studio 只会将已更新的代码重新编入索引。 为了尽量减少代码图完成呈现所需的时间，请考虑以下内容：

- [仅映射你感兴趣的依赖关系。](#SeeSpecificSource)

- 在生成整个解决方案的代码图之前，缩小解决方案范围。

- 使用代码图工具栏上的“跳过生成” 按钮关闭自动生成解决方案。

- 使用代码图工具栏上的“包括父级” 按钮关闭自动添加父项。

- 直接编辑代码图文件，以删除不需要的节点和链接。 更改代码图不会影响基础代码。 请参阅 [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)。

  ![Skip Build and Include Parents buttons](../modeling/media/codemapsfilterskipbuildicons.png "CodeMapsFilterSkipBuildIcons")

  尽管 Visual Studio 可在 1 GB 内存下运行，但我们建议你的计算机至少具有 2 GB 内存，以避免在 Visual Studio 创建代码索引并生成代码图时产生长时间的延迟。

  当项目项的“复制到输出目录” 属性设置为“始终复制”时，通过解决方案资源管理器创建代码图或将项添加到代码图可能需要更多时间。 这可能导致增量生成问题，并且 Visual Studio 每次都重新生成项目。 若要提高性能，请将此属性更改为“如果较新则复制” 或 `PreserveNewest`。 请参阅 [Incremental Builds](../msbuild/incremental-builds.md)。

  完成的图只会为成功创建的代码显示依赖关系。 如果某些组件出现生成错误，这些错误会出现在代码图上。 在基于代码图做出体系结构决策时，请确保组件实际生成并且具有依赖项。

## <a name="SavingExporting"></a> 共享代码图

### <a name="share-the-map-with-other-visual-studio-users"></a>与其他 Visual Studio 用户共享代码图
 使用“文件” 菜单保存代码图。

 或

 To save the map as part of specific project, on the map toolbar, choose **Share**, **Move** \<*CodeMapName*> **.dgml into**, and then choose the project where you want to save the map.

 ![Move a map into another project](../modeling/media/codemapsmovemapmenu.png "CodeMapsMoveMapMenu")

 Visual Studio 将代码图另存为 .dgml 文件，以便你可与 Visual Studio Enterprise 和 Visual Studio Professional 的其他用户共享。

> [!NOTE]
> 在与使用 Visual Studio Professional 的用户共享代码图之前，请确保展开所有组、显示隐藏节点和跨组链接，并检索希望其他人在你的代码图上查看的所有已删除的节点。 否则，其他用户将无法查看这些项目。
>
> 保存建模项目中的代码图或从建模项目复制到其他位置的代码图时，可能会出现以下错误：
>
> “无法在项目目录外保存 *fileName* 。 不支持链接的项。”
>
> Visual Studio 将显示错误，但还是会创建保存的版本。 若要避免错误，请在建模项目外创建代码图。 然后，可将图形保存到所需的位置。 若只是将文件复制到解决方案中的其他位置，那么尝试保存图形将不起作用。

### <a name="export-the-map-as-an-image-so-you-can-copy-it-into-other-applications-such-as-microsoft-word-or-powerpoint"></a>将代码图导出为图像以便将它复制到其他应用程序，如 Microsoft Word 或 PowerPoint

1. 在代码图工具栏上，选择“共享”、“以图像形式发送电子邮件” 或“复制图像”。

2. 将该图像粘贴到另一个应用程序中。

### <a name="export-the-map-as-an-xps-file-so-you-can-see-it-in-xml-or-xaml-viewers-like-internet-explorer"></a>将代码图导出为 XPS 文件，以便你可以在 XML 或 XAML 查看器（如 Internet Explorer）中查看它

1. 在代码图工具栏上选择“共享”、“作为可移植 XPS 发送电子邮件” 或“另存为可移植 XPS”。

2. 浏览到你要保存文件的位置。

3. 对代码图命名。 Make sure that the **Save as type** box is set to **XPS files (\*.xps)** . 选择“保存”。

## <a name="what-else-can-i-do"></a>我还能执行什么操作？

- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)

- [调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)

- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)

- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)

- [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
