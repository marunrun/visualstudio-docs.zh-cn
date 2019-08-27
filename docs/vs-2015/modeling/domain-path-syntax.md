---
title: 域路径语法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, domain path
ms.assetid: 945994f9-72b9-42e0-81b2-e5fb3d0e282d
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2c115e8fff6cddbc1b08c697b72c7bda3a970ed4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68203464"
---
# <a name="domain-path-syntax"></a>域路径语法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

DSL 定义使用类似 XPath 的语法在模型中查找特定元素。  
  
 通常，你不必直接使用此语法。 在“DSL 详细信息”或“属性”窗口中，你可以在它所显示的位置中单击向下箭头并使用路径编辑器。 但是，在使用编辑器后，该路径将以此形式显示在字段中。  
  
 域路径采用以下形式：  
  
 *RelationshipName.PropertyName/!Role*  
  
 ![CommentReferencesSubjects 引用关系](../modeling/media/dsl-reference.png "dsl_reference")  
  
 该语法将遍历模型树。 例如，域关系**CommentReferencesSubjects**上图中具有**主题**角色。 路径段 **/ ！Subjectt 将**指定路径结束于元素通过访问**使用者**角色。  
  
 每段都以域关系的名称开头。 如果遍历从元素到关系，则路径段将显示为*Relationship.PropertyName*。 如果跃点是从链接到一个元素，则路径段将显示为*关系 / ！RoleName*。  
  
 使用斜杠分隔路径的语法。 每个路径段是都从元素到链接（关系的实例）或从链接到元素的跳跃。 路径段经常成对显示。 一个路径段表示从元素到链接的跳跃，而下一个段则表示从链接到另一端的元素的跳跃。 （任何链接还可以是关系本身的源或目标）。  
  
 用于元素到链接跳跃的名称是角色的 `Property Name` 的值。 用于链接到元素跳跃的名称是目标角色名称。  
  
## <a name="see-also"></a>请参阅  
 [了解模型、类和关系](../modeling/understanding-models-classes-and-relationships.md)
