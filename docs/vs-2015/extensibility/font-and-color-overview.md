---
title: 字体和颜色概述 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], font and color
- font and color control [Visual Studio SDK], editors
ms.assetid: 2203e4e7-8b7f-44ec-8884-6ff718d4f278
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0a20cfa2372b1e55652ffcebe6d173cff86140a6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204343"
---
# <a name="font-and-color-overview"></a>字体和颜色概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题讨论中的文本字体和颜色设置[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成的开发环境 (IDE)。 它还引入了类别和显示项的概念并介绍 Vspackage 和核心编辑器如何使用文本特性。  
  
## <a name="the-fonts-and-colors-property-page"></a>字体和颜色属性页  
 你可以管理属性中显示的文本[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成的开发环境 (IDE) 通过**字体和颜色**属性页。 若要查找**字体和颜色**属性页上，在**工具**菜单中，单击**选项**。 展开**环境**，然后单击**字体和颜色**。  
  
## <a name="categories-and-display-items"></a>类别和显示项  
 字体和颜色分为**类别**并**显示项**。  
  
- 一个**类别**是大量的逻辑或功能容器**显示项**。  
  
   一系列**类别**处于**显示其设置**的下拉列表框**字体和颜色**属性页。  
  
- 一个**显示项**是如注释、 字符串或将时显示着色的控制结构的定义完善的文本实体。  
  
  每个**显示项**唯一定义内**类别**包含它。 因此，多个**类别**可以**显示项**具有相同的名称。  
  
## <a name="vspackage-control-of-fonts-and-colors"></a>VSPackage 控制的字体和颜色  
 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]允许 Vspackage 到：  
  
- 定义字体和颜色**类别**。  
  
- 指定的字体和颜色用于呈现**显示项**。  
  
- 与之交互**字体和颜色**属性页。  
  
- 聚合多个**类别**成组。  
  
- 保留默认设置中的更改。  
  
  有两种方法中的字体和颜色选择与交互[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]。  
  
- 一种方法称为*语法着色*。 使用自定义现有的 vspackage[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]编辑器实现的语言服务和创建编辑器的源。  
  
   只有一个**类别**即支持此机制，则**文本编辑器**。  
  
- 更多常规的替代方法支持所有其他**类别**和显示文本时在源编辑器之外的用户界面组件。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> 。  
  
## <a name="core-editor-text-settings"></a>核心编辑器文本设置  
 核心编辑器的语言服务对象的字体和颜色设置受**文本 EditorCategory**中找到**显示其设置**的下拉列表框**字体和颜色**属性页。  
  
 使用编辑器时, 应使用专用的字体和颜色控制机制的语言服务都会提供控制和扩展**文本编辑器**设置。 该机制称为*语法着色，大*，并提供：  
  
- 一种用于管理的字体和颜色显示项的简化的方法。  
  
   有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>。  
  
- 一种明确定义和优化着色机制。  
  
   有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>。  
  
- 可以使用内置的显示项从**文本 EditorCategory**和对其进行扩展。  
  
   有关详细信息，请参阅[如何：使用内置的可着色项](../extensibility/internals/how-to-use-built-in-colorable-items.md)并[自定义可着色项](../extensibility/internals/custom-colorable-items.md)。  
  
- 自动持久化的当前状态的两个内置和自定义显示的项**文本编辑器**类别。  
  
  有关详细信息的语法着色，请参阅[旧版语言服务中的语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。  
  
## <a name="see-also"></a>请参阅  
 [在编辑器中的旧接口](../extensibility/legacy-interfaces-in-the-editor.md)   
 [在旧版语言服务中进行语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
