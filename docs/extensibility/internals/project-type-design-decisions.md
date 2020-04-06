---
title: 项目类型设计决策 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5e33ac1c4168593b881f799dfdfb94005fb55fc1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80706362"
---
# <a name="project-type-design-decisions"></a>项目类型设计决策
在创建新项目类型之前，必须就项目类型做出多个设计决策。 您必须决定项目将包含哪些类型的项目、如何保留项目文件以及您将使用的承诺模型。

## <a name="project-items"></a>项目项
 您的项目是否使用文件或抽象对象？ 如果使用文件，这些文件是基于引用还是基于目录的文件？ 文件或抽象对象是本地还是远程？

 项目中的项目可以是文件，也可以是更抽象的对象，如数据库存储库中的对象或 Internet 上的数据连接。 如果项目是文件，则项目可以是基于引用的项目，也可以是基于目录的项目。

 在基于引用的项目中，项可以出现在多个项目中。 但是，项表示的实际文件仅位于一个目录中。 在基于目录的项目中，目录结构中存在所有项目项。

 本地项目存储在安装应用程序的同一台计算机上。 远程项目可以存储在本地网络中的单独服务器上，也可以存储在 Internet 的其他地方。

## <a name="project-file-persistence"></a>项目文件持久性
 数据是存储在通用平面文件系统中还是存储在结构化存储中？ 文件是使用标准编辑器还是特定于项目的编辑器打开？

 要保留其数据，大多数应用程序将其数据保存在文件中，然后在用户必须查看或更改信息时将其读取。

 当多个组件对象模型 （COM） 对象需要将其持久化数据存储在单个文件中时，通常使用结构化存储（也称为复合文件）。 使用结构化存储，多个不同的软件组件可以共享单个磁盘文件。

 对于项目中项目的持久性，需要考虑多个选项。 您可以执行以下任一选项：

- 更改后单独保存每个文件。

- 在单个 **"保存"** 操作中捕获多个事务。

- 在本地保存文件，然后发布到服务器，或者当项目表示与远程对象的数据连接时，使用另一种方法保存项目项。

  有关持久性的详细信息，请参阅[项目持久性](../../extensibility/internals/project-persistence.md)以及[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。

## <a name="project-commitment-model"></a>项目承诺模型
 持久化数据对象是否会在直接模式或交易模式下打开？

 当直接模式打开数据对象时，将立即合并对数据所做的更改，或者当用户手动保存文件时。

 使用事务模式打开数据对象时，更改将保存到内存中的临时位置，直到用户手动选择保存文件之前不会提交更改。 此时，所有更改必须同时发生，否则不会进行任何更改。

## <a name="see-also"></a>请参阅
- [清单：新建项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)
- [项目持久性](../../extensibility/internals/project-persistence.md)
- [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)
- [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)
- [创建项目类型](../../extensibility/internals/creating-project-types.md)
