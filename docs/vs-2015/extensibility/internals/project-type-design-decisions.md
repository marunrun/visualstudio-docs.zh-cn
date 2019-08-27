---
title: 项目类型设计决策 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project types, project file persistence
- project types, commitment mechanics
- project types, items
- project types, design decisions
ms.assetid: f68671fe-fd7a-4e56-a0b5-330b0f1fedb1
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cd26e08ab153e96fc601e89788008cb0e9ca38c8
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704081"
---
# <a name="project-type-design-decisions"></a>项目类型设计决策
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

在创建新的项目类型之前，必须将多个设计决策制定您的项目类型。 您必须决定要将哪些类型的项将包含你的项目、 如何将保留项目文件，以及哪些承诺模型。  
  
## <a name="project-items"></a>项目项  
 将你的项目使用的文件或抽象对象？ 如果使用的文件，它们将是基于引用的或基于目录的文件？ 是否要为本地或远程的文件或接下来的抽象对象？  
  
 在项目中的项可以是文件，或它们可以在 Internet 上是更加抽象对象，例如数据库存储库或数据连接中的对象。 如果项是文件，项目可以是基于引用的或基于目录的项目。  
  
 在基于引用的项目中，项可以出现在多个项目。 但是，一个项代表的实际文件位于仅限一个目录中。 在基于目录的项目中，所有项目项的目录结构中都存在。 有关详细信息，请参阅[NIB： 项目管理在项目中](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)。  
  
 本地项存储在安装应用程序的同一计算机上。 远程项目可以存储在本地网络中，单独的服务器上或在 Internet 上的其他位置。  
  
## <a name="project-file-persistence"></a>项目文件持久性  
 将数据存储在常见的平面文件系统，或在结构化存储？ 将使用标准编辑器中或特定于项目的编辑器中打开文件？  
  
 若要保存其数据，大多数应用程序将其数据保存在文件中，，然后阅读它时用户必须查看或更改的信息。  
  
 多个组件对象模型 (COM) 对象需要将其保留的数据存储在单个文件时，通常使用结构化的存储，也称为复合文件。 使用结构化存储，多个不同的软件组件可以共享单个磁盘文件。  
  
 你有若干选项，需要注意的有关你的项目中的项的持久性。 您可以执行以下选项之一：  
  
- 单独保存每个文件，它已被更改时。  
  
- 捕获在单个的多个事务**保存**操作。  
  
- 保存文件进行本地，然后发布到服务器或使用项表示远程对象的数据连接时保存项目项的另一种方法。  
  
  有关持久性的详细信息，请参阅[项目持久性](../../extensibility/internals/project-persistence.md)并[打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)。  
  
## <a name="project-commitment-model"></a>项目的承诺模型  
 将打开持久化的数据对象在直接模式下或事务处理模式下？  
  
 当在直接模式下打开数据对象时，立即或在用户手动保存该文件时合并数据所做的更改。  
  
 当通过使用事务处理模式下打开数据对象时，更改保存到内存中的临时位置和不会提交直到用户手动选择要保存该文件。 此时，所有更改必须一起都出现，或将进行任何更改。  
  
## <a name="see-also"></a>请参阅  
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [NIB： 项目管理在项目中](https://msdn.microsoft.com/762e606b-7f44-4b66-97a1-e30a703654a0)   
 [打开和保存项目项](../../extensibility/internals/opening-and-saving-project-items.md)   
 [项目持久性](../../extensibility/internals/project-persistence.md)   
 [项目模型的元素](../../extensibility/internals/elements-of-a-project-model.md)   
 [项目模型核心组件](../../extensibility/internals/project-model-core-components.md)   
 [创建项目类型](../../extensibility/internals/creating-project-types.md)
