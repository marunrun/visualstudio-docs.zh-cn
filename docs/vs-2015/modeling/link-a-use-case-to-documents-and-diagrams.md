---
title: 用例链接到文档和关系图 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.usecasediagram.artifact.properties.artifactlink
- vs.teamarch.usecasediagram.artifact
helpviewer_keywords:
- use case diagrams
ms.assetid: 4c9ed205-9197-4ed5-b39d-ddfa24a0a421
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ee7657b12741cf65583317ba87bd465e15eb02bb
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440971"
---
# <a name="link-a-use-case-to-documents-and-diagrams"></a>将用例链接到文档和关系图
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以将用例图中的用例链接到另一个关系图或文档。 例如，可以将用例链接到以下关系图和文档：  
  
- 序列图，显示如何通过用户和系统设置或其中主要组件之间的交互实现用例的目标。  
  
- 活动图，显示执行用例的用户和系统或其主要组件的详细活动。  
  
- 详细描述此用例的 OneNote 页面或段落。  
  
- 详细描述用例的 Word 文档或 PowerPoint 演示文稿。 可以将此类文档保留在解决方案中或团队可访问的位置（如 SharePoint 网站）。  
  
  若要将某个用例链接到文档，请在用例图上创建一个项目，然后将该用例连接到该项目。 在项目的属性中，设置其他关系图或文档的文件路径。 双击该项目，即会打开其他关系图或文档。  
  
  你可以根据需要将多个项目连接到每个用例。 还可以将项目链接到用例图上其他类型的元素。  
  
### <a name="to-open-a-document-associated-with-an-artifact"></a>打开与项目关联的文档  
  
- 在用例图上，双击项目形状。  
  
     关联的文档随即打开。  
  
### <a name="to-link-a-use-case-to-a-diagram-or-file-in-the-same-solution"></a>若要将用例链接到同一解决方案中的关系图或文件  
  
1. 绘制关系图（如序列图或活动图）来演示用例的方案。  
  
2. 返回到用例图。  
  
3. 将关系图或文件从解决方案资源管理器拖动到用例图的空白部分。  
  
4. 从项目连接到使用大小写使用**依赖项**。  
  
### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>若要链接到诸如 Word 文档或 PowerPoint 演示文稿等解决方案文件  
  
1. 向解决方案中添加文档。  
  
    1. 将该 Word 文档移入解决方案所在的 Windows 文件夹。  
  
    2. 在解决方案资源管理器中右键单击解决方案，指向**外**，然后单击**现有项**。  
  
    3. 导航到 Word 文档，然后单击**添加**。  
  
         该 Word 文档将显示在解决方案资源管理器的解决方案文件夹中。  
  
2. 将 Word 文档从解决方案资源管理器拖动到用例图的空白部分。  
  
     随即显示新项目。  
  
3. 从项目连接到使用大小写使用**依赖项**。  
  
### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>若要链接到共享文档、OneNote 元素或网页  
  
1. 获取的共享元素的 URL。 这可能是，例如，从网络文件路径开始\\\\，或网页上或 Sharepoint URL 开头 http:// 或指向 OneNote 节、 页面上，或段落开头 onenote:。  
  
2. 在工具箱中，单击**项目**，然后单击用例关系图中。  
  
3. 选择新项目后，键入或粘贴到 URL**超链接**属性。  
  
    > [!NOTE]
    > 如果你想要提供的文件路径，则最好在常见的工作区中选择一个文件 (从开始\\\\)，或在 Visual Studio 解决方案中的文件。 这可以确保文件路径在其他团队成员的计算机上或该解决方案被移动后仍将有效。 若要将文档如 Word 文档添加到你的解决方案，右键单击解决方案资源管理器中的解决方案，指向**外**，然后单击**现有项**。  
  
## <a name="see-also"></a>请参阅  
 [UML 用例关系图：引用](../modeling/uml-use-case-diagrams-reference.md)   
 [UML 用例关系图：指导原则](../modeling/uml-use-case-diagrams-guidelines.md)   
 [编辑 UML 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)   
 [为应用程序创建模型](../modeling/create-models-for-your-app.md)
