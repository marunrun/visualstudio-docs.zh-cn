---
title: 管理项目和解决方案属性
ms.date: 11/04/2016
ms.topic: conceptual
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99786cc2b646c011a0398e973e0fd3d4dd97583f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603440"
---
# <a name="manage-project-and-solution-properties"></a>管理项目和解决方案属性

项目具有一些控制编译、调试、测试和部署的很多方面的属性。 有些属性在所有项目类型中是通用的，而有些则只用于特定语言或平台。 右键单击“解决方案资源管理器”  中的项目节点并选择“属性”  ，或者在菜单栏上的搜索框中键入“属性”  并从结果中选择“属性窗口”  ，即可访问项目属性。

![项目上下文菜单](../ide/media/vs2015_proj_prop_menu.gif)

在项目树本身，.NET 项目也可能具有一个属性节点。

![解决方案资源管理器树中的属性节点](../ide/media/vs2015_props_se.png)

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 对于 Visual Studio for Mac，请参阅[管理解决方案和项目属性 (Visual Studio for Mac)](/visualstudio/mac/managing-solutions-and-project-properties)。

## <a name="project-properties"></a>项目属性

项目属性分到各个组且每组具有自己的属性页。 这些页面可能因语言和项目类型不同而有所不同。

### <a name="c-visual-basic-and-f-projects"></a>C#、Visual Basic 和 F# 项目

在 C#、Visual Basic 和 F# 项目中，属性在“项目设计器”  中公开。 下图显示了 C# 中的 WPF 项目的生成属性页  ：

![Visual Studio 项目设计器](../ide/media/vs2015_proppage_build.png)

有关“项目设计器”中每个属性页的信息，请参阅[项目属性引用](../ide/reference/project-properties-reference.md)  。

> [!TIP]
> 解决方案和项目项都具有一些属性；这些属性可在[属性窗口](../ide/reference/properties-window.md)中访问，而不是在**项目设计器**中访问。

### <a name="c-and-javascript-projects"></a>C++ 和 JavaScript 项目

C++ 和 JavaScript 项目对于管理项目属性有不同的用户界面。 此图显示了 C++ 项目属性页（JavaScript 页面与此类似）：

![Visual C++ 项目属性](../ide/media/vs2015_projprops_cpp.png)

有关 C++ 项目属性的信息，请参阅[使用项目属性 (C++)](/cpp/build/working-with-project-properties)。 有关 JavaScript 属性的详细信息，请参阅[属性页，JavaScript](../ide/reference/property-pages-javascript.md)。

## <a name="solution-properties"></a>解决方案属性

若要访问解决方案上的属性，请右键单击“解决方案资源管理器”  中的解决方案节点，然后选择“属性”  。 在对话框中，可以设置用于“调试”或“发布”版本的项目配置，选择按下 F5 时应启动的项目，然后设置代码分析选项    。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的解决方案和项目](../ide/solutions-and-projects-in-visual-studio.md)
- [管理解决方案和项目属性 (Visual Studio for Mac)](/visualstudio/mac/managing-solutions-and-project-properties)
