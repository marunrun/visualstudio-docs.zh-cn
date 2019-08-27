---
title: 域类的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
ms.assetid: a3993995-19e7-4761-a972-b1de89131a1b
caps.latest.revision: 23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: c668317fba69100701fac95bfa333ed7b3446488
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65701968"
---
# <a name="properties-of-domain-classes"></a>域类的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

域类具有下表中的属性。 域类的相关信息，请参阅[了解模型、 类和关系](../modeling/understanding-models-classes-and-relationships.md)。 有关如何使用这些属性的详细信息，请参阅[自定义和扩展域特定语言](../modeling/customizing-and-extending-a-domain-specific-language.md)。  
  
|属性|描述|默认|  
|--------------|-----------------|-------------|  
|访问修饰符|域类的访问级别（`public` 或 `internal`）。|`public`|  
|自定义特性|用于将属性添加到此域类从生成的源代码类。|\<none>|  
|生成双派生|如果`True`，将生成的基类和一个分部类 （以支持通过重写自定义）。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|  
|具有自定义构造函数|如果`True`，将在源代码中提供自定义构造函数。 有关详细信息，请参阅[重写和扩展生成的类](../modeling/overriding-and-extending-the-generated-classes.md)。|`False`|  
|继承修饰符|介绍的从域类生成的源代码类的继承的类型 (`none`，`abstract`或`sealed`)。|`none`|  
|基类|如果此域类派生，类的基类的名称。|\<none>|  
|名称|此域类的名称。|当前名称|  
|命名空间|此域类的命名空间。|当前命名空间|  
|说明|此域类相关联的非正式说明。|\<none>|  
|描述|用于记录生成的设计器的 UI 说明。|\<none>|  
|显示名称|将此域类生成的设计器中显示的名称。|\<none>|  
|帮助关键字|用于索引此域类的 F1 帮助中的可选关键字。|\<none>|  
  
## <a name="see-also"></a>请参阅  
 [域特定语言工具术语表](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
