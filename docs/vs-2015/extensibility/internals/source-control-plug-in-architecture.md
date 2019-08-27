---
title: 源代码管理插件体系结构 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, architecture
ms.assetid: 35351d4c-9414-409b-98fc-f2023e2426b7
caps.latest.revision: 25
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 370f88ce4d8fc372ce31e1e85e88d5379f4e1ba5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68183383"
---
# <a name="source-control-plug-in-architecture"></a>源代码管理插件体系结构
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

您可以添加到源控件支持[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]实现并附加了源代码管理插件集成的开发环境 (IDE)。 IDE 连接到源代码管理插件通过定义完善的源控制插件 API。 IDE 公开源控制系统版本控制的功能通过提供工具栏和菜单命令组成的用户界面 (UI)。 源代码管理插件实现的源代码管理功能。  
  
## <a name="source-control-plug-in-resources"></a>源控制插件资源  
 源代码管理插件提供资源来帮助创建并连接到你的版本控制应用程序[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE。 源代码管理插件包含 API 规范，以便它可以集成到源代码管理插件必须实现[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]IDE。 它还包含一个代码示例 (编写C++)，它实现的主干源控制插件演示实现基本功能与源控制插件 API 兼容。  
  
 源控件插件 API 规范可支持你将所选的任何源代码管理系统，如果使用所需的源控制插件 API 根据实现的函数集创建源控件 DLL。  
  
## <a name="components"></a>组件  
 在关系图中的源控件适配器包是将转换为函数调用受源代码管理插件的源代码管理操作的用户的请求在 IDE 的组件。 这种情况发生，IDE 和源代码管理插件必须具有一个有效的对话框，它在 IDE 和插件之间来回传递信息。 有关此对话框中进行，它们都必须都使用相同语言。 在本文档中所述的源控制插件 API 是此交换的常见词汇。  
  
 ![源代码控制体系结构关系图](../../extensibility/internals/media/vs-sccsdk-plug-in-arch.gif "vs_sccsdk_plug_in_arch")  
显示 VS 和源代码之间的交互插件体系结构图示  
  
 体系结构关系图中所示[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]shell 中，为 VS shell 在图中，标记为托管用户的工作项目和相关的组件，例如编辑器和解决方案资源管理器。 源控件适配器包处理 IDE 和源代码管理插件之间的交互。 源控件适配器包提供了其自己的源控件 UI。 它是顶级用户启动和定义的源代码管理操作的作用域以便与交互的 UI。  
  
 源代码管理插件可以有自己的 UI，可能包含两个部分，如图所示。 标记为"供应商 UI"的框表示你，作为源控制插件创建者，提供的自定义用户界面元素。 当用户调用高级的源代码管理操作时直接通过源代码管理插件显示。 标有"帮助程序 UI"的框是一组源代码管理可以通过 IDE 间接调用的插件 UI 功能。 源代码管理插件将与 UI 相关的消息传递到通过特殊的回调函数与 IDE 提供的 IDE。 帮助器 UI 帮助与在 IDE 的更加无缝集成 (通常通过使用的**高级**按钮)，从而提供更统一的最终用户体验。  
  
 源代码管理插件不能进行更改到[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]shell，因此，源控件适配器包或源控件提供由 IDE 用户界面。 它必须使最充分地利用通过为最终用户提供的集成体验到的各种源控制插件 API 函数的实现所提供的灵活性。 源控件插件 API 文档的参考部分包含一些高级的源代码管理插件功能的信息。 若要利用这些功能，源代码管理插件必须声明其向 IDE 的高级的功能在初始化期间，，它必须实现特定的高级的函数，每个功能。  
  
## <a name="see-also"></a>请参阅  
 [源代码管理插件](../../extensibility/source-control-plug-ins.md)   
 [术语表](../../extensibility/source-control-plug-in-glossary.md)   
 [创建源代码管理插件](../../extensibility/internals/creating-a-source-control-plug-in.md)
