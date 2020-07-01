---
title: 自定义模型资源管理器
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.dsldesigner.explorerbehavior
helpviewer_keywords:
- Domain-Specific Language Tools, Domain-Specific Language Explorer
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 625ba0d592d0dbdaa8cb910c366852fe32c5f220
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548364"
---
# <a name="customizing-the-model-explorer"></a>自定义模型资源管理器
可以按如下所示更改域特定语言设计器的资源管理器的外观和行为：

- 更改窗口标题。

- 更改选项卡图标。

- 更改节点的图标。

- 隐藏节点。

## <a name="changing-the-window-title"></a>更改窗口标题
 若要更改生成的资源管理器的窗口标题，请在**DSL 资源管理器**中选择 "**资源管理器行为**"，然后在 "**属性**" 窗口中，将 "**标题**" 属性设置为所需的标题。

## <a name="changing-the-tab-icon"></a>更改选项卡图标
 若要更改资源管理器的选项卡图标，请在 .bmp 文件中使用16x16 像素的图标。 将图标文件放在 \DslPackage\Resources\ 文件夹中，然后将文件名更改为**ModelExplorerToolWindowBitmaps.bmp**。 例如，你可以将 Visual Studio 安装 .ico 图标文件更改为 .bmp 格式，并将其重命名为**DSLLanguageName\DslPackage\Resources\ModelExplorerToolWindowBitmaps.bmp**。 当资源管理器与**解决方案资源管理器**一起停靠时，生成的设计器将在您的资源管理器的选项卡上显示此图标。

## <a name="setting-custom-icons-on-explorer-nodes"></a>在资源管理器节点上设置自定义图标
 可以通过使用资源管理器节点设置自定义资源管理器中的节点。 下面的过程演示如何将图标添加到节点。

#### <a name="to-add-an-icon-to-an-explorer-node"></a>向资源管理器节点添加图标

1. [!INCLUDE[dsl](../modeling/includes/dsl_md.md)]使用 "任务流" 解决方案模板创建解决方案。

2. 在解决方案的**Dsl\Resources**文件夹中放置一个包含16x16 像素图标的 .bmp 文件。

3. 在**DSL 资源管理器**中，右键单击 "**资源管理器行为**"，然后单击 "**添加新资源管理器节点设置**"。

    "**自定义节点设置**" 节点下将显示一个**ExplorerNodeSettings**节点。

4. 选择 " **ExplorerNodeSettings**"，然后在 "**属性**" 窗口中，将 "**类**" 设置为 "**参与者**"。

5. 将**图标设置为显示**在图标文件的路径中。

6. 转换所有模板，然后生成并运行解决方案。

7. 在生成的设计器中，打开示例关系图。

    资源管理器应显示**三个**具有您的图标的执行组件节点。

> [!NOTE]
> 如果已为显示在生成的资源管理器中的任何元素设置了节点图标，则所有 "资源管理器" 节点都将显示该图标。 如果未设置图标，节点将显示默认图标。

## <a name="changing-the-name-displayed-on-an-explorer-node"></a>更改 "资源管理器" 节点上显示的名称
 你可以更改模型元素的名称在你的资源管理器中的显示方式。 下面的过程演示如何在 "注释" 节点中显示**注释**引用的**任务**的名称。

#### <a name="to-display-a-property"></a>显示属性

1. 打开在前面的过程中创建的解决方案。

2. 请确保**注释**仅引用单个域类，方法是将具有属性名称 "**主体**" 的角色的重数设置为 0 ..1。 属性名称应为**Subject**，关系名称应变为**CommentReferencesSubject**。

3. 在**DSL 资源管理器**中，右键单击 "**资源管理器行为**"，然后单击 "**添加新资源管理器节点设置**"。

     "**自定义节点设置**" 节点下将显示一个**ExplorerNodeSettings**节点。

4. 选择 " **ExplorerNodeSettings**"，然后在 "**属性**" 窗口中，将 "**类**" 设置为 "**注释**"。

5. 右键单击 "**注释**" 节点，然后单击 "**添加新属性路径**"。

     此时会显示一个名为 "已命名**属性**" 的新节点。

6. 选择 "**显示的属性**"，然后在 "**属性**" 窗口中，单击 "**路径到" 属性**的值字段。 依次选择 "**注释**"、" **CommentReferencesSubject**" 和 " **FlowElement**"。 生成的路径应类似于**CommentReferencesSubject/！主题**。

7. 在**属性**的值字段中，选择 "**名称**"。

8. 转换所有模板，然后生成并运行解决方案。

9. 在生成的设计器中，打开示例关系图。

10. 绘制关系图上注释元素和**Task1**元素之间的**注释连接器**。

     "资源管理器" 节点应将注释显示为 " **Task1**"。

## <a name="hiding-nodes"></a>隐藏节点
 可以通过将节点的路径添加到**DSL 资源管理器**的 "**隐藏节点**" 节点来隐藏资源管理器中的节点。 下面的过程演示如何隐藏**注释**节点。

#### <a name="to-hide-an-explorer-node"></a>隐藏资源管理器节点

1. 打开在前面的过程中创建的解决方案。

2. 在**DSL 资源管理器**中，右键单击 "**资源管理器行为**"，然后单击 "**添加新域路径**"。

     "**隐藏节点**" 下将出现**域路径**节点。

3. 选择 "**域路径**"，然后在 "**属性**" 窗口中，单击 "**路径定义**" 的值字段。 依次选择 " **FlowGraph**" 和 " **FlowGraphHasComments**"。 生成的路径应类似于**FlowGraphHasComments**

4. 转换所有模板，然后生成并运行解决方案。

5. 在生成的设计器中，打开示例关系图。

     "资源管理器" 应仅显示 "**参与者**" 节点，不应显示 "**注释**" 节点。

## <a name="see-also"></a>另请参阅

- [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
