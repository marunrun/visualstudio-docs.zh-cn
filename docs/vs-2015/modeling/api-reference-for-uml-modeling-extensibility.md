---
title: UML 建模扩展性的 API 参考 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- UML - extending
- UML API
- UML model, API
ms.assetid: 2b2ffe93-c358-4d28-a5e5-3d0474629b58
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 12eadb9844df5da78b11367708fed715f1c13672
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68159676"
---
# <a name="api-reference-for-uml-modeling-extensibility"></a>UML 建模扩展性的 API 参考
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以编写程序代码来读取和修改你使用 Visual Studio 创建的模型。 API 参考提供了特定类的相关信息来帮助你进行工作。 有关面向任务的详细信息，请参阅下的主题[扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)。 若要查看支持 UML 模式的 Visual Studio 版本，请参阅 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
## <a name="assemblies"></a>程序集  
  
|Assembly|允许执行的操作|  
|--------------|--------------------------------|  
|Microsoft.VisualStudio.Uml.Interfaces.dll|-将读取和更改模型元素，例如 IUseCase、 IAssociation 等。<br />导航元素之间的关系。<br /><br /> 命名空间和类型与那些在 UML 规范中定义的内容相对应。|  
|Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll|-创建模型元素的新实例<br />-访问和修改形状和关系图。|  
  
## <a name="see-also"></a>请参阅  
 [扩展 UML 模型和关系图](../modeling/extend-uml-models-and-diagrams.md)   
 [Visual Studio 的建模 SDK 的 API 参考](../modeling/api-reference-for-modeling-sdk-for-visual-studio.md)
