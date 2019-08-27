---
title: 自定义模型使用配置文件和构造型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML model, profiles
- UML model, stereotypes
- UML model, customizing
ms.assetid: fd607157-0d3a-4583-a84e-427a4b2a5acb
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: f7e9aee38208a96ab75318a86810359392b5b8e1
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433348"
---
# <a name="customize-your-model-with-profiles-and-stereotypes"></a>使用配置文件和构造型自定义模型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以改写标准 UML 模型元素（如类和组件），以便为特定目的而对它们进行自定义。 您可以将应用*构造型*到模型元素，可以更改的属性的元素的列表。 名为集合中定义构造型*配置文件*。  
  
 若要查看支持此功能的 Visual Studio 的版本，请参阅 [体系结构和建模工具的版本支持](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)。  
  
 若要使用构造型，将包链接到配置文件。 这使你可将在配置文件中定义的构造型应用到包中的元素。 某些配置文件是与 Visual Studio 一起安装的。 此外，还可以定义自己的配置文件。  
  
 可在元素的属性列表中设置构造型。 对于关系图上主要类型的形状，应用的构造型也出现在该形状中，如该示例中所示。  
  
 ![具有 stereotype 的 UML 类。](../modeling/media/uml-class-stereotype.png "UML_class_stereotype")  
  
> [!NOTE]
> 如果使用配置文件创建模型，然后与他人共享该模型，他们将无法看到构造型，除非他们在计算机上安装了相同的配置文件。  
  
## <a name="related-topics"></a>相关主题  
  
|Title|描述|  
|-----------|-----------------|  
|[向 UML 模型元素添加构造型](../modeling/add-stereotypes-to-uml-model-elements.md)|将模型元素放在包中，将包链接到配置文件，并对该元素应用构造型。|  
|[UML 模型的标准构造型](../modeling/standard-stereotypes-for-uml-models.md)|UML 标准配置文件 L2 和 L3 随 Visual Studio 一起安装，并且默认情况下，每个模型都链接到它们。 它们提供了可用于为你的模型添加批注的构造型。<br /><br /> 例如，可以将 «规范» 构造型应用于类，以指示它旨在仅定义其实例的外部可见的行为。|  
|[定义用于扩展 UML 的配置文件](../modeling/define-a-profile-to-extend-uml.md)|你可以定义自己的构造型和工具，它们适用于你自己的应用程序区域。<br /><br /> 例如，如果开发银行软件，则可以定义能应用于类的 «帐户» 构造型。 然后可以使用类图来描述不同类型的帐户及其关系。|  
|[安装 UML 配置文件](../modeling/install-a-uml-profile.md)|如果有人给了你一个 UML 配置文件，可将它安装在你的计算机上。|  
|[定义自定义建模工具箱项](../modeling/define-a-custom-modeling-toolbox-item.md)|自定义工具箱项使你能避免在新元素上重复设置构造型。|  
|[UML 类的构造型的颜色](http://code.msdn.microsoft.com/UML-Color-Classes-by-07de2b70)|此示例代码扩展了 UML 关系图。 它根据元素的构造型自动设置 UML 形状的颜色。|
