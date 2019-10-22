---
title: 代码图
ms.date: 05/16/2018
ms.topic: conceptual
f1_keywords:
- vs.progression.codemap
- vs.progression.standardgraphsdialog
helpviewer_keywords:
- DGML
- graph documents
- code visualization [Visual Studio]
- dependencies, visualizing
- dependency graphs
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 45fb9b1a08dc54257f24f469d3a717b82faccf45
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661541"
---
# <a name="map-dependencies-with-code-maps"></a>映射与代码图的依赖项

您可以通过创建代码图来可视化代码中的依赖项。 代码图可帮助你查看代码如何相互配合，而无需读取文件和代码行。

![在 Visual Studio 中查看与代码图的依赖项](../modeling/media/codemapsmainintro.png)

若要创建和编辑代码图，需要 Visual Studio Enterprise 版本。 在 Visual Studio 社区版和专业版中，你可以打开在 Enterprise edition 中生成的关系图，但不能对其进行编辑。

> [!NOTE]
> 在与使用 Visual Studio Professional 的其他人共享 Visual Studio Enterprise 创建的地图之前，请确保地图上的所有项（例如隐藏项、展开的组和跨组链接）均可见。

可以映射以下语言中的代码的依赖项：

- 解决方案C#或程序集（ *.dll*或 *.exe*）中的视觉对象或 Visual Basic

- 本机或托管的 C C++或 Visual C++项目、头文件（ *.h*或 `#include`）或二进制文件中的代码

- 通过 Microsoft Dynamics AX 的 .NET 模块生成的 X++ 项目和程序集

> [!NOTE]
> 对于C#或 Visual Basic 以外的项目，用于启动代码图或将项添加到现有代码图的选项较少。 例如，不能用鼠标右键单击 C++ 项目的文本编辑器中的对象并将其添加到代码图。 不过，您可以将各个代码元素或文件拖放到**解决方案资源管理器**、**类视图**和**对象浏览器**。

## <a name="install-code-map-and-live-dependency-validation"></a>安装代码图和实时依赖项验证

若要在 Visual Studio 中创建代码图，请首先安装**代码图**和**实时依赖项验证**组件：

1. 打开**Visual Studio 安装程序**。 你可以从 Windows 的 "开始" 菜单或在 Visual Studio 中通过选择 "**工具**"  > **获取工具和功能**"来打开它。

1. 选择“各个组件”选项卡。

1. 向下滚动到 "**代码工具**" 部分，并选择 "**代码图**" 和 "**实时依赖项验证**"。

   ![Visual Studio 安装程序中的代码图和实时依赖项验证组件](media/modeling-components.png)

1. 选择“修改”。

   **代码图**和**实时依赖项验证**组件会开始安装。 系统可能会要求你关闭 Visual Studio。

## <a name="add-a-code-map"></a>添加代码图

您可以创建空代码图，并将项拖动到其上，包括程序集引用、文件和文件夹，也可以为解决方案的全部或部分生成代码图。

添加空代码图：

1. 在“解决方案资源管理器”中，打开顶级解决方案节点的快捷菜单。 选择 "**添加** > **新项**"。

2. 在 "**添加新项**" 对话框中的 "**已安装**" 下，选择 "**常规**" 类别。

3. 选择 "**定向关系图文档（.dgml）** " 模板，然后选择 "**添加**"。

   > [!TIP]
   > 此模板可能不会按字母顺序显示，因此，如果看不到，请向下滚动到模板列表的底部。

   解决方案的 "**解决方案项**" 文件夹中将显示一个空白地图。

同样，你可以创建新的代码映射文件，而无需将其添加到解决方案中，只需选择 "**体系结构**"  > **新的代码图**或**文件** > **新**的  > **文件**中。

## <a name="generate-a-code-map-for-your-solution"></a>为解决方案生成代码图

查看解决方案中的所有依赖项：

1. 在菜单栏上，选择 "**体系结构**"  >  "**生成解决方案的代码图**"。 如果代码自上次生成后未发生更改，则可以选择 "**体系结构**"  > **生成解决方案的代码图**，而不是生成。

   ![生成代码映射命令](../modeling/media/codemapsarchitecturemenu.png)

   将生成一个映射，其中显示顶级程序集和它们之间的聚合链接。 聚合链路越广，它所代表的依赖关系就越多。

2. 使用代码图工具栏上的“图例” 按钮以显示或隐藏项目类型图标（如测试项目、Web 项目和 Phone 项目）、代码项（如类、方法和属性）以及关系类型（如继承自、实现和调用）的列表。

   ![程序集的顶级依赖项关系图](../modeling/media/dependencygraph_toplevelassemblies.png)

   此示例解决方案包含解决方案文件夹（“测试” 和“组件”），测试项目、Web 项目和程序集。 默认情况下，所有包含关系均以 *“组”* 的形式显示，你可以对其进行展开和折叠。 “外部”组包含你的解决方案之外的任何内容，包括平台依赖项。 外部程序集仅显示已使用的项。 默认情况下，系统基类型隐藏在代码图中以减少混乱。

3. 若要深入了解代码图中，请展开表示项目和程序集的组。 可以通过按“CTRL+A” 展开全部内容以选择所有节点，然后选择“组”，再选择快捷菜单中的“展开” 。

   ![展开代码映射中的所有组](../modeling/media/codemapsexpandallgroups.png)

4. 但是，这对大型解决方案可能并无作用。 事实上，对于复杂的解决方案，内存限制可能会阻止你展开所有组。 相反，若要在单个节点内进行查看，则将其展开。 将鼠标指针移动到节点的顶部，然后单击出现的 V 形。

   ![展开代码映射中的节点](../modeling/media/dependencygraph_containment.png)

   或使用键盘选择项，然后按加号键（“+” **+** ）。 若要查看更深层次的代码，请对命名空间、类型和成员执行相同操作。

   > [!TIP]
   > 有关使用鼠标、键盘和触控处理代码图的详细信息，请参阅[浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)。

5. 若要简化代码图并将重点关注各个部分，选择代码图工具栏上的“筛选器” ，然后仅选择你感兴趣的节点和链接类型。 例如，可以隐藏所有的解决方案文件夹和程序集容器。

   ![通过筛选容器来简化映射](../modeling/media/codemapsfilterfoldersassemblies.png)

   还可以通过从代码图中隐藏或删除单个组和项来简化代码图，而不影响基础解决方案代码。

6. 若要查看各项间的关系，请在代码图中选择各项。 链接的颜色指示关系的类型，如“图例” 窗格中所示。

   ![查看解决方案中的依赖关系](../modeling/media/codemapsmainintro.png)

   在此示例中，紫色链接为调用，点式链接为引用，浅蓝色链接为字段访问。 绿色链接可以是继承，也可能是指示一个以上关系（或 *“类别”* ）类型的 *“聚合链接”* 。

   > [!TIP]
   > 如果你看到的是绿色链接，它是指可能不仅仅存在继承关系。 可能也存在方法调用，但是这些都被继承关系所隐藏。 若要查看特定类型的链接，请使用 "**筛选器**" 窗格中的复选框来隐藏不感兴趣的类型。

7. 若要获取有关项或链接的详细信息，请将指针移至其顶部，直至出现工具提示。 这将显示代码元素或链接所表示的类别的详细信息。

   ![显示关系的类别](../modeling/media/codemapsshowlinkcatgories.png)

8. 若要检查聚合链接表示的项和依赖项，请首先选择该链接，然后打开它的快捷菜单。 选择“显示参与链接” （或“在新代码图上显示参与链接”）。 这将展开位于链接两端的组，且仅显示参与链接的项和依赖项。

9. 若要重点关注地图的特定部分，可继续删除不感兴趣的项。 例如，若要深入了解类和成员视图，只需筛选“筛选器” 窗格中的所有命名空间节点。

   ![向下钻取到类和成员级别](../modeling/media/dependencygraph_expandedselectedgroups_2012.png)

10. 集中精力处理复杂的解决方案代码图的另一种方式是从现有代码图生成包含选定项的新代码图。 按住**Ctrl**的同时选择要关注的项，打开快捷菜单，然后从 "选择"**中选择 "新建关系图**"。

    ![显示新代码映射上的选定项](../modeling/media/codemapsshowonnewmap.png)

11. 将包含上下文转入新代码图。 使用 "**筛选器**" 窗格隐藏解决方案文件夹以及不想看到的任何其他容器。

    ![筛选容器以简化视图](../modeling/media/codemapsexpandnewgroups.png)

12. 展开组，选择代码图中的项，以便查看关系。

    ![选择项以查看关系](../modeling/media/codemapsviewnewrelationships.png)

另请参见：

- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
- [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
- 通过[运行分析器](../modeling/find-potential-problems-using-code-map-analyzers.md)发现代码中的潜在问题

## <a name="view-specific-dependencies-in-a-code-map"></a>查看代码图中的特定依赖关系

假设你有一个代码评审，可在某些具有挂起更改的文件中执行。 若要查看这些更改中的依赖关系，请从这些文件中创建一个代码图。

   ![显示代码图上的特定依赖关系](../modeling/media/codemapsspecificdependenciesintro.png)

1. 在**解决方案资源管理器**中，选择要映射的项目、程序集引用、文件夹、文件、类型或成员。

   ![选择要映射的项](../modeling/media/codemapsselectinsolutionexplorer.png)

1. 在**解决方案资源管理器**工具栏上，选择 "**在代码图上显示**" ![Create ](../modeling/media/createnewgraphfromselectedbutton.gif) "选定节点中的新图形" 按钮。 或者，打开一个或一组项目的快捷菜单，然后选择 "**在代码图上显示**"。

   还可以将项从**解决方案资源管理器**、**类视图**或**对象浏览器**拖动到[新](#add-a-code-map)的或现有的代码图中。 若要包含项的父层次结构，请在拖动项时按住**Ctrl**键，或者使用代码图工具栏上的 "**包括父级**" 按钮来指定默认操作。 你还可以从 Visual Studio 外（例如，从**Windows 资源管理器**）中拖动程序集文件。

   > [!NOTE]
   > 当你从在多个应用之间共享的项目（如 Windows Phone 或 Microsoft Store）添加项时，这些项将与当前活动的应用程序项目一起显示在映射上。 如果你将上下文更改为另一个应用程序项目并从共享的项目添加更多项，则这些项现在将与最近活动的应用程序项目一起显示。 你对代码图上的项执行的操作仅适用于共享相同上下文的项。

3. 代码图将显示在选定项的包含程序集内的选定项。

   ![在映射上显示为组的选定项](../modeling/media/codemapsshowitemsfromsolnexplorer.png)

4. 如要查看项，请把项展开。 将鼠标指针移动到项的顶部，然后单击出现的 V 形（向下键）。

   ![展开代码图中的节点](../modeling/media/dependencygraph_containment.png)

   若要展开所有项，请使用**Ctrl** + **，** 然后打开映射的快捷菜单并选择 "**组** > **展开**"。 然而，如果展开所有组会生成不可用的代码图或产生内存问题，则该选项不可用。

5. 如果需要，请继续展开感兴趣的项，直到类和成员级别。

   ![将组展开到类和成员级别](../modeling/media/codemapsexpandtoclassandmember.png)

   若要查看代码中的成员，但不显示在地图上，请单击组左上角的 "**重新提取子级**" 图标 ![Refetch 子图标 ](../modeling/media/dependencygraph_deletednodesicon.png)。

6. 若要查看更多与代码图上的项相关的项，请选择其中一个，再选择代码图工具栏上的“显示相关内容” ，然后选择要添加到图中的相关项的类型。 或者，选择一个或多个项，打开快捷菜单，然后为要添加到映射的相关项的类型选择 "**显示**" 选项。 例如:

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

    ![显示此成员调用的方法](../modeling/media/codemapsshowrelatedmethods.png)

7. 代码图显示关系。 在此示例中，映射显示 `Find` 方法调用的方法及其在解决方案中或在外部的位置。

   ![显示代码图上的特定依赖关系](../modeling/media/codemapsspecificdependenciesintro.png)

8. 若要简化代码图并将重点关注各个部分，选择代码图工具栏上的“筛选器” ，然后仅选择你感兴趣的节点和链接类型。 例如，关闭解决方案文件夹、程序集和命名空间的显示。

   ![使用“筛选器”窗格以简化显示](../modeling/media/almcodemapfilterpane.png)

## <a name="see-also"></a>请参阅

- [视频：利用 Visual Studio 2015 代码图从代码中了解设计](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)
- [使用代码图调试应用程序](../modeling/use-code-maps-to-debug-your-applications.md)
- [调试时映射调用堆栈上的方法](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [使用代码图分析查找潜在问题](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [浏览和重新排列代码图](../modeling/browse-and-rearrange-code-maps.md)
- [Customize code maps by editing the DGML files](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
