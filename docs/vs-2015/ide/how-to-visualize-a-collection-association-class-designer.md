---
title: 如何：可视化集合关联 （类设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.collectionassociationline
- vs.classdesigner.ShowAssociationException
helpviewer_keywords:
- collection associations
- collections, collection associations
- Class Designer [Visual Studio], collection associations
ms.assetid: 54e39838-2fc9-4dc2-85b6-7e88a743108e
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 490ee064903a0e2d119da891681da719e237acec
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68178782"
---
# <a name="how-to-visualize-a-collection-association-class-designer"></a>如何：直观显示集合关联（类设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

属于其他类型的集合的属性和字段可在类图上作为集合关联显示。 普通关联可将字段或属性显示为行，此行将拥有的类链接到字段的类型，与此不同，集合关联作为行显示，此行将拥有的类链接到已收集的类型。  
  
### <a name="to-create-a-collection-association"></a>创建集合联合  
  
1. 在代码中，创建一个属性或字段，其本身属于强类型集合。  
  
2. 在类图中扩展类，以便显示属性和字段。  
  
3. 在类中，右键单击该字段或属性，然后选择“显示为集合关联”  。  
  
     此属性或字段将显示为链接到已收集类型的关联行。  
  
## <a name="see-also"></a>请参阅  
 [如何：创建类型 （类设计器） 之间的关联](../ide/how-to-create-associations-between-types-class-designer.md)   
 [设计类和类型（类设计器）](../ide/designing-classes-and-types-class-designer.md)   
 [查看类型和关系（类设计器）](../ide/viewing-types-and-relationships-class-designer.md)
