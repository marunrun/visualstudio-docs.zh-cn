---
title: 自定义模型资源管理器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.dsltools.dsldesigner.explorerbehavior
helpviewer_keywords:
- Domain-Specific Language Tools, Domain-Specific Language Explorer
ms.assetid: d2926444-9408-41d8-a27e-3fd0c416f9ac
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 9206c4474b8ca3dc284aa474c645fddc3aecab18
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686725"
---
# <a name="customizing-the-model-explorer"></a>自定义模型资源管理器
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以更改的外观和行为在资源管理器域特定语言设计器，如下所示：  
  
- 更改窗口标题。  
  
- 更改选项卡图标。  
  
- 更改节点的图标。  
  
- 隐藏节点。  
  
## <a name="changing-the-window-title"></a>更改窗口标题  
 若要更改的生成资源管理器窗口标题，请选择**资源管理器行为**中**DSL 资源管理器**，然后在**属性**窗口中，设置**标题**属性设置为所需的标题。  
  
## <a name="changing-the-tab-icon"></a>更改选项卡图标  
 若要更改在资源管理器选项卡图标，.bmp 文件中使用 16 x 16 像素的图标。 将图标文件放置在 \DslPackage\Resources\ 文件夹中，然后将文件名称更改为**ModelExplorerToolWindowBitmaps.bmp**。 例如，可以更改[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]setup.ico 图标为.bmp 格式文件，并为其重命名**DSLLanguageName\DslPackage\Resources\ModelExplorerToolWindowBitmaps.bmp**。 生成的设计器将显示此图标在资源管理器的选项卡上停靠一起使用时**解决方案资源管理器**。  
  
## <a name="setting-custom-icons-on-explorer-nodes"></a>在资源管理器节点上设置自定义图标  
 你可以使用自定义节点在资源管理器中资源管理器节点设置。 以下过程演示如何将图标添加到节点。  
  
#### <a name="to-add-an-icon-to-an-explorer-node"></a>若要将图标添加到资源管理器节点  
  
1. 创建[!INCLUDE[dsl](../includes/dsl-md.md)]解决方案通过使用任务流解决方案模板。  
  
2. 将包含在一个 16 x 16 像素图标.bmp 文件放**Dsl\Resources**解决方案中的文件夹。  
  
3. 在中**DSL 资源管理器**，右键单击**资源管理器行为**，然后单击**添加新的资源管理器节点设置**。  
  
     **ExplorerNodeSettings**节点下显示**自定义节点设置**节点。  
  
4. 选择**ExplorerNodeSettings**，然后在**属性**窗口中，设置**类**到**Actor**。  
  
5. 设置**图标为显示**到图标文件的路径。  
  
6. 转换所有模板，然后生成并运行解决方案。  
  
7. 在生成的设计器中打开示例关系图。  
  
     在资源管理器应显示三个**Actor**具有您的图标的节点。  
  
> [!NOTE]
> 如果设置了生成资源管理器中显示的任何元素节点图标，资源管理器中的所有节点将都显示图标。 如果尚未设置任何图标，节点将显示默认图标。  
  
## <a name="changing-the-name-displayed-on-an-explorer-node"></a>更改显示在资源管理器节点的名称  
 您可以更改模型元素的名称在资源管理器中的显示方式。 下面的过程演示如何显示的名称**任务**引用**注释**注释节点中。  
  
#### <a name="to-display-a-property"></a>若要显示属性  
  
1. 打开在前面的过程中创建的解决方案。  
  
2. 请确保**注释**引用只有一个单一域类通过设置具有属性名称的 role 的多重性**主题**到 0..1。 属性名称会变得**使用者**，并应成为关系名称**CommentReferencesSubject**。  
  
3. 在中**DSL 资源管理器**，右键单击**资源管理器行为**，然后单击**添加新的资源管理器节点设置**。  
  
     **ExplorerNodeSettings**节点下显示**自定义节点设置**节点。  
  
4. 选择**ExplorerNodeSettings**，然后在**属性**窗口中，设置**类**到**注释**。  
  
5. 右键单击**注释**节点，并单击**添加新属性路径**。  
  
     新节点将出现名为**属性显示**。  
  
6. 选择**属性显示**，然后在**属性**窗口中，单击值字段**路径到属性**。 选择**注释**，然后**CommentReferencesSubject**，然后**FlowElement**。 生成的路径应类似于**CommentReferencesSubject.Subject/ ！使用者**。  
  
7. 中的值字段**属性**，选择**名称**。  
  
8. 转换所有模板，然后生成并运行你的解决方案。  
  
9. 在生成的设计器中打开示例关系图。  
  
10. 绘制**注释连接器**之间的注释元素和**Task1**关系图上的元素。  
  
     资源管理器节点应显示为注释**Task1**。  
  
## <a name="hiding-nodes"></a>隐藏节点  
 可以在资源管理器中隐藏节点，通过添加到其路径**隐藏节点**的节点**DSL 资源管理器**。 以下过程介绍如何隐藏**注释**节点。  
  
#### <a name="to-hide-an-explorer-node"></a>若要隐藏的资源管理器节点  
  
1. 打开在前面的过程中创建的解决方案。  
  
2. 在中**DSL 资源管理器**，右键单击**资源管理器行为**，然后单击**添加新域路径**。  
  
     一个**域路径**节点下显示**隐藏节点**。  
  
3. 选择**域路径**，然后在**属性**窗口中，单击值字段**路径定义**。 选择**FlowGraph**，然后**FlowGraphHasComments**。 生成的路径应类似于**FlowGraphHasComments.Comments**  
  
4. 转换所有模板，然后生成并运行你的解决方案。  
  
5. 在生成的设计器中打开示例关系图。  
  
     在资源管理器应仅显示**Actors**节点，然后，将不显示**注释**节点。  
  
## <a name="see-also"></a>请参阅  
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
