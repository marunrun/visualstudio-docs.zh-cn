---
title: 管理项目和解决方案属性 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: d727efc0-1096-4ede-84b6-31a65da22ac0
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ec48aac60a8f15527c92d19a38ca9f996dcfdd6f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651360"
---
# <a name="managing-project-and-solution-properties"></a>管理项目和解决方案属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

项目具有一些控制编译、调试、测试和部署的很多方面的属性。 有些属性在所有项目类型中是通用的，而有些则只用于特定语言或平台。 右键单击解决方案资源管理器中的项目节点并选择属性，或者将属性键入菜单栏中的“快速启动”**** 搜索框，可访问项目属性。

 ![项目上下文菜单](../ide/media/vs2015-proj-prop-menu.gif "vs2015_proj_prop_menu")

 在项目树本身，.NET 项目也具有一个属性节点。

 ![解决方案资源管理器树中的属性节点](../ide/media/vs2015-props-se.png "VS2015_Props_SE")

> [!TIP]
> 解决方案具有几个属性，因此是项目项;这些属性可在 " [属性" 窗口](../ide/reference/properties-window.md)中访问，而不是在 **项目设计器**中访问。

## <a name="project-properties"></a>项目属性
 项目属性分到各个组且每组具有自己的属性页，而这些页面可能因语言和项目类型不同而有所不同。

### <a name="c-and-visual-basic-projects"></a>C# 和 Visual Basic 项目
 在 C# 和 Visual Basic 项目中，属性在“项目设计器”**** 中公开。 下图显示了 C# 中的 WPF 项目的生成属性页：

 ![Visual Studio 项目设计器](../ide/media/vs2015-proppage-build.png "VS2015_PropPage_Build")

 有关 "项目设计器" 中每个属性页的信息，请参阅 [项目属性引用](../ide/reference/project-properties-reference.md)。

### <a name="c-and-javascript-projects"></a>C++ 和 JavaScript 项目
 C++ 和 JavaScript 项目对于管理项目属性有不同的用户界面。 此图显示了 C++ 项目属性页（JavaScript 页面与此类似）：

 ![Visual C&#43;&#43; 项目属性](../ide/media/vs2015-projprops-cpp.png "VS2015_ProjProps_cpp")

 有关 C++ 项目属性的信息，请参阅[使用项目属性](https://msdn.microsoft.com/library/9b0d6f8b-7d4e-4e61-aa75-7d14944816cd)。 有关 JavaScript 属性的详细信息，请参阅 [属性页，JavaScript](../ide/reference/property-pages-javascript.md)。

## <a name="solution-properties"></a>解决方案属性
 若要访问解决方案上的属性，请右键单击“解决方案资源管理器”**** 中的解决方案节点，然后选择“属性”****。 在对话框中，可以设置用于“调试”或“发布”版本的项目配置，选择按下 F5 时应为启动项目的项目，然后设置代码分析选项。

## <a name="see-also"></a>另请参阅
 [Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)
