---
title: 项目类型设计决策 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7d6d1df2a3b2188360b0ee60480b4d6580ed8faf
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72725381"
---
# <a name="project-type-design-decisions"></a>项目类型设计决策
在创建新的项目类型之前，必须对项目类型做出多种设计决策。 您必须确定您的项目将包含哪些类型的项、如何保存项目文件以及将使用哪种提交模型。

## <a name="project-items"></a>项目项
 你的项目将使用文件还是抽象对象？ 如果使用文件，它们是基于引用还是基于目录的文件？ 文件或抽象对象将是本地还是远程？

 项目中的项可以为文件，也可以是更多的抽象对象，例如数据库存储库中的对象或 Internet 上的数据连接。 如果项为文件，则项目可以是基于引用的项目，也可以是基于目录的项目。

 在基于引用的项目中，项可以出现在多个项目中。 不过，项所代表的实际文件仅位于一个目录中。 在基于目录的项目中，所有项目项都存在于目录结构中。

 本地项存储在安装了应用程序的同一计算机上。 远程项目可存储在本地网络中的单独服务器上，或存储在 Internet 上的其他位置。

## <a name="project-file-persistence"></a>项目文件持久性
 数据是存储在公用文件系统中还是存储在结构化存储中？ 文件是通过使用标准编辑器还是特定于项目的编辑器打开？

 若要保存数据，大多数应用程序会将其数据保存在文件中，然后在用户必须查看或更改信息时将其读回。

 结构化存储（也称为复合文件）通常在多个组件对象模型（COM）对象需要将其保存的数据存储在一个文件中时使用。 使用结构化存储，多个不同的软件组件可以共享单个磁盘文件。

 对于项目中的项，可以考虑使用几个选项。 可以执行以下任一选项：

- 更改每个文件后，单独保存该文件。

- 在单个**保存**操作中捕获多个事务。

- 当项表示到远程对象的数据连接时，在本地保存文件，然后发布到服务器，或使用另一种方法保存项目项。

  有关持久性的详细信息，请参阅[项目持久性](../../extensibility/internals/project-persistence.md)和[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="project-commitment-model"></a>项目承诺模型
 持久的数据对象是在直接模式下还是在事务模式下打开？

 在直接模式下打开数据对象时，对数据所做的更改将立即合并，或在用户手动保存文件时进行。

 使用事务处理模式打开数据对象时，会将更改保存到内存中的临时位置，并且在用户手动选择保存文件之前，不会提交这些更改。 此时，所有更改都必须一起出现，否则不会进行任何更改。

## <a name="see-also"></a>请参阅
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [项目持久性](../../extensibility/internals/project-persistence.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
- [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)