---
title: 用例图上 UML 元素的属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.usecasediagram.artifact.properties
- vs.teamarch.usecasediagram.shapes.properties
helpviewer_keywords:
- use case diagrams, properties
ms.assetid: 2728fb26-a275-4fce-8a2c-5a78af6bee04
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b52afab80bc22c03dc5ff980b937cad53869f5db
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63444414"
---
# <a name="properties-of-elements-on-uml-use-case-diagrams"></a>UML 用例图上元素的属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 UML 用例图中，关系图上的每个元素都具有属性。 若要查看某个元素的属性，请右键单击元素关系图上或在**UML 模型资源管理器**，然后单击**属性**。 属性将显示在**属性**窗口。  
  
> [!NOTE]
> 本主题是关于在 UML 用例图中的元素的属性。 有关如何读取 UML 活动图的详细信息，请参阅[UML 用例图：参考](../modeling/uml-use-case-diagrams-reference.md)。 有关如何绘制 UML 活动图的详细信息，请参阅[UML 用例图：指导原则](../modeling/uml-use-case-diagrams-guidelines.md)。  
  
## <a name="properties-of-elements"></a>元素的属性  
  
|属性|默认|元素|描述|  
|--------------|-------------|-------------|-----------------|  
|**名称**|默认名称|全部|标识元素。|  
|**限定的名称**|包::名称|全部|唯一标识元素。 以包含它的包的限定名为前缀。|  
|**工作项**|0 associated|全部|与此元素关联的工作项的数目。 若要将工作项相关联，请参阅[链接模型元素和工作项](../modeling/link-model-elements-and-work-items.md)。|  
|**说明**|(无)|全部|可在此处记下有关元素的常规说明。|  
|**Color**|（默认）|全部|形状的颜色。 与其他属性不同，这不是形状显示的元素属性。|  
|**映像路径**|(无)|Actor|应使用的图像文件路径，而不使用默认的参与者图标。 该图标应为 Visual Studio 项目中的资源文件。|  
|**Subjects**|(无)|用例|拥有用例的子系统或其他类型。<br /><br /> 通过将用例置于关系图的子系统上来对其进行设置。|  
|**可见性**|Public|用例、参与者、子系统|**公共**-全局可见。<br /><br /> **包**-在包内可见。|  
|**IsAbstract**|False|用例、参与者、子系统|如果为 True，则该类型不能被实例化，其目的是作为其他定义的专用化基础。|  
|**为间接实例化**|True|子系统|子系统仅作为设计项目存在。 在运行时只有其部件存在。|  
|**超链接**|(无)|项目|关系图或文档的 URL 或文件路径，项目将提供一个指向此 URL 或文件路径的链接。|  
  
 有关关联的属性的列表，请参阅[属性关联在 UML 类图](../modeling/properties-of-associations-on-uml-class-diagrams.md)。  
  
## <a name="see-also"></a>请参阅  
 [UML 用例关系图：引用](../modeling/uml-use-case-diagrams-reference.md)   
 [UML 用例关系图：指南](../modeling/uml-use-case-diagrams-guidelines.md)
