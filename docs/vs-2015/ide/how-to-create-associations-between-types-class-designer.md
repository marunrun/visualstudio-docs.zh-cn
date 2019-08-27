---
title: 如何：创建类型 （类设计器） 之间的关联 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.classdesigner.associationline
helpviewer_keywords:
- types [Visual Studio], associations
- association lines, defining (Class Designer)
- defining association lines (Class Designer)
- associations, types
- association lines
ms.assetid: adccb9c8-2f8a-4086-9fa9-f70f99fb6e00
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 2d152ce38c445955988ec76a2e328691eac152ca
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63416941"
---
# <a name="how-to-create-associations-between-types-class-designer"></a>如何：创建类型之间的关联（类设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

类设计器中的关联连线显示了关系图中各类之间的相互关系。 关联连线表示项目中是另一个类的属性或字段类型的类。 关联连线一般用于阐释项目中各类之间最重要的关系。  
  
 尽管可以将所有字段和属性显示为关联，但根据想要在关系图中强调的内容来将若干重要成员显示为关联更有意义。 （可将不太重要的成员显示为常规成员，或将其全部隐藏起来。）  
  
> [!NOTE]
> 类设计器仅支持单向关联。  
  
### <a name="to-define-an-association-line-in-the-class-diagram"></a>在类关系图中定义关联连线  
  
1. 在“工具箱”的“类设计器”下，选择“关联”。  
  
2. 在希望以关联关系链接的两个形状之间绘制一条连线。  
  
     这就在第一个类中创建了一个新属性。 此属性显示为一条具有默认名称的关联连线（而不是作为形状中隔离舱内的属性）。 其类型是关联连线所指向的形状。  
  
### <a name="to-change-the-name-of-an-association"></a>更改关联的名称  
  
- 在关系图面上单击并编辑关联连线的标签。  
  
  \- 或 -  
  
1. 单击包含显示为关联的属性的形状。  
  
     该形状获得焦点，且其成员显示在“类详细信息”窗口和“属性”窗口中。  
  
2. 在“类详细信息”窗口或“属性”窗口中，编辑该属性的名称字段，并按 Enter。  
  
     此名称在“类详细信息”窗口中、关联行上、“属性”窗口中和代码中同时得到更新。  
  
## <a name="see-also"></a>请参阅  
 [如何：在成员表示法与关联表示法之间转换（类设计器）](../ide/how-to-change-between-member-notation-and-association-notation-class-designer.md)
