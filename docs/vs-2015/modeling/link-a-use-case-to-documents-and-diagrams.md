---
title: 将用例链接到文档和关系图 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: c713759a8ea75eed3048469327f962668efa4f70
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657643"
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

4. 使用 **依赖关系**从项目连接到用例。

### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>若要链接到诸如 Word 文档或 PowerPoint 演示文稿等解决方案文件

1. 向解决方案中添加文档。

    1. 将该 Word 文档移入解决方案所在的 Windows 文件夹。

    2. 在解决方案资源管理器中，右键单击解决方案，指向 " **添加**"，然后单击 " **现有项**"。

    3. 导航到 Word 文档，然后单击 " **添加**"。

         该 Word 文档将显示在解决方案资源管理器的解决方案文件夹中。

2. 将 Word 文档从解决方案资源管理器拖动到用例图的空白部分。

     随即显示新项目。

3. 使用 **依赖关系**从项目连接到用例。

### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>若要链接到共享文档、OneNote 元素或网页

1. 获取的共享元素的 URL。 例如，这可以是网络文件路径开始 " \\ \\ "，或以 "http://" 开头的网页或 Sharepoint URL，也可以是指向 onenote 节、页面或段落开始 "onenote：" 的链接。

2. 在 "工具箱" 中，单击 " **项目** "，然后在用例图中单击。

3. 选择新的项目后，将 URL 键入或粘贴到 **Hyperlink** 属性中。

    > [!NOTE]
    > 如果要提供文件路径，最好在公共工作区中选择一个文件 (以 " \\ \\ " ) 开头，或在 Visual Studio 解决方案中选择一个文件。 这可以确保文件路径在其他团队成员的计算机上或该解决方案被移动后仍将有效。 若要向解决方案中添加文档（如 Word 文档），请右键单击 "解决方案资源管理器中的解决方案，指向" **添加** "，然后单击" **现有项**"。

## <a name="see-also"></a>另请参阅
 [Uml 用例图：引用](../modeling/uml-use-case-diagrams-reference.md) [uml 用例图：准则](../modeling/uml-use-case-diagrams-guidelines.md)[编辑 uml 模型和关系图](../modeling/edit-uml-models-and-diagrams.md)[为应用程序创建模型](../modeling/create-models-for-your-app.md)
