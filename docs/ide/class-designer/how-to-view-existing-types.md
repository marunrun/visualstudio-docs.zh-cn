---
title: 如何：查看现有类型（类设计器）
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.CannotShowBaseType
helpviewer_keywords:
- types [Visual Studio], visualizing
- types [Visual Studio], class diagrams
- class diagrams, types
ms.assetid: de110a4e-5b51-4a40-9dee-615df4d8f999
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef2882fec8d213c38a2e125d4e3f0c3f22d1d581
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62975159"
---
# <a name="how-to-view-existing-types-in-class-designer"></a>如何：在类设计器中查看现有类型

若要查看现有类型及其成员，请将其形状添加到类图。

你可以查看本地类型和引用类型。 本地类型存在于当前打开的项目中，是可读/写的。 被引用的类型存在于其他项目中或被引用程序集中，是只读的。

若要在类图上设计新类型，请参阅[如何：使用类设计器创建类型](how-to-create-types.md)。

## <a name="to-see-types-in-a-project-on-a-class-diagram"></a>在类图上查看项目中的类型

1. 从解决方案资源管理器的项目中，打开现有类图 (.cd) 文件。 如果不存在任何类图，请向项目中添加新类图。 请参阅[如何：向项目添加类图](how-to-add-class-diagrams-to-projects.md)。

2. 从解决方案资源管理器的项目中，将源代码文件拖动到类图中。

    > [!NOTE]
    > 如果你的解决方案有共享跨多个应用的代码的项目，则可以仅从以下源将文件或代码拖动到类图：
    >
    > - 包含图的应用项目
    > - 应用项目导入的共享项目
    > - 引用的项目
    > - 程序集

    表示在源代码文件中定义的类型的形状即会显示在关系图上你将源代码文件拖动到的位置。

你还可通过将一个或多个类型从类视图中的项目节点拖动到类图中，来查看项目中的类型。

> [!TIP]
> 如果类视图尚未打开，则从“视图”菜单打开类视图。

若要在关系图上的默认位置显示类型，请在类视图中选择一个或多个类型，右击选择的类型，再选择“查看类图”。

> [!NOTE]
> 如果某个已关闭的类图包含项目中业已存在的类型，则类图会打开以显示该类型形状。 但是，如果没有任何类图包含项目中已存在的类型，则类设计器将在项目内创建一个新的类图，并打开该关系图以显示该类型。

第一次在关系图上显示一个类型时，在默认情况下，其形状以折叠方式显示。 你可以展开该形状以查看其内容。

### <a name="to-display-the-contents-of-a-project-in-a-class-diagram"></a>若要在类图中显示项目的内容

在“解决方案资源管理器”或“类视图”中，右键单击该项目并选择“视图”，然后选择“查看类图”。 即会创建一个自动填充的类图。

## <a name="see-also"></a>请参阅

- [如何：查看类型之间的继承](how-to-view-inheritance-between-types.md)
- [如何：自定义类图](how-to-customize-class-diagrams.md)
- [查看类型和关系](designing-and-viewing-classes-and-types.md)