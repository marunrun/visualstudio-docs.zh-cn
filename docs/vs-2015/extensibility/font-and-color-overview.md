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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204343"
---
# <a name="font-and-color-overview"></a>字体和颜色概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题讨论 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 集成开发环境中 (IDE) 的文本字体和颜色设置。 它还介绍了类别和显示项的概念，并介绍了 Vspackage 和核心编辑器使用文本属性的方式。  
  
## <a name="the-fonts-and-colors-property-page"></a>"字体和颜色" 属性页  
 您可以 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 通过 " **字体和颜色** " 属性页 (IDE) 来管理集成开发环境中显示的文本的属性。 若要查找 " **字体和颜色** " 属性页，请在 " **工具** " 菜单上单击 " **选项**"。 展开“环境”****，再单击“字体和颜色”****。  
  
## <a name="categories-and-display-items"></a>类别和显示项  
 字体和颜色组织为 **类别** 和 **显示项**。  
  
- **类别**是多个**显示项**的逻辑或功能容器。  
  
   **类别**列表位于 "**字体和颜色**" 属性页的 "**显示其设置**" 下拉框中。  
  
- **显示项**是定义良好的文本实体，如注释、字符串或显示时要着色的控制结构。  
  
  每个 **显示项** 在包含它的 **类别** 中唯一定义。 因此，多个 **类别** 可以有一个具有相同名称的 **显示项** 。  
  
## <a name="vspackage-control-of-fonts-and-colors"></a>字体和颜色的 VSPackage 控件  
 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)]允许 vspackage：  
  
- 定义字体和颜色 **类别**。  
  
- 指定用于呈现 **显示项**的字体和颜色。  
  
- 与 " **字体和颜色** " 属性页交互。  
  
- 将多个 **类别** 聚合到组中。  
  
- 保留默认设置中的更改。  
  
  可以通过两种方式与中的字体和颜色选择交互 [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] 。  
  
- 一种方法称为 *语法着色*。 它由 VSPackage 用于自定义现有 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 编辑器以实现语言服务并创建源编辑器。  
  
   只有一个 **类别** 支持此机制，即 **文本编辑器**。  
  
- 更常规的替代方法在显示文本时支持除源编辑器之外的所有其他 **类别** 和用户界面组件。 有关详细信息，请参阅 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>。  
  
## <a name="core-editor-text-settings"></a>核心编辑器文本设置  
 语言服务对象的核心编辑器的字体和颜色设置由 "**字体和颜色**" 属性页的 "**显示其设置**" 下拉框中的**文本 EditorCategory**控制。  
  
 使用编辑器时，应使用语言服务提供的专用字体和颜色控制机制来控制和扩展 **文本编辑器** 设置。 此机制称为 *语法着色* ，并提供：  
  
- 用于管理显示项的字体和颜色的简化方法。  
  
   有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsProvideColorableItems> 和 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorableItem>。  
  
- 定义完善并经过优化的着色机制。  
  
   有关详细信息，请参阅 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer>。  
  
- 既可使用 **文本 EditorCategory** 中的内置显示项，也可对其进行扩展。  
  
   有关详细信息，请参阅 [如何：使用内置可着色项](../extensibility/internals/how-to-use-built-in-colorable-items.md) 和 [自定义可着色项](../extensibility/internals/custom-colorable-items.md)。  
  
- 内置和自定义显示项的当前状态与 **文本编辑器** 类别的自动持久性。  
  
  有关语法着色的详细信息，请参阅 [旧版语言服务中的语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。  
  
## <a name="see-also"></a>另请参阅  
 [编辑器中的旧接口](../extensibility/legacy-interfaces-in-the-editor.md)   
 [在旧版语言服务中进行语法着色](../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)
