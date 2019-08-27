---
title: 嵌套项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project nesting
- nested projects
- projects [Visual Studio SDK], child projects
- projects [Visual Studio SDK], nesting
ms.assetid: 12cce037-9840-4761-845e-5abd5fb317b0
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0e3a0fae42dc7bf1497e3d0d4a9d23f9cab50675
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68180409"
---
# <a name="nesting-projects"></a>嵌套项目
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

企业应用程序开发人员使用 VS 包可以方便地分组相似类型的项目中合并在一起[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]通过使用*项目嵌套*。 例如，企业级模板项目为类别使用嵌套的组项目到项目。 商业外观项目、 Web UI 项目等组合在一起在一个类别中。  
  
 在此方案中，是开发人员可以嵌套在每个父项目，下面的项目数没有限制过程，尽管开发人员可以以编程方式提供限制。 这种类型的分组还可以使可递归的在这种情况下为子项目的相同类型的项目可以嵌套在要成为子项目的子级的父级的子项目的子级。  
  
 项目嵌套不是内部函数的一部分[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]。 您必须编写代码来启用嵌套和子项目中的嵌套子项目。 父项目是一个特殊的 VSPackage 或项目类型，创建并注册其自己的 GUID 包括实现嵌套项目所需的代码。  
  
 C# Example.Nested 项目示例中，可以找到嵌套项目的示例。  
  
## <a name="nested-projects-example"></a>嵌套的项目的示例  
 ![嵌套项目解决方案](../../extensibility/internals/media/vsnestedprojects.gif "vsNestedProjects")  
嵌套的项目的示例  
  
## <a name="see-also"></a>请参阅  
 [如何：实现嵌套的项目](../../extensibility/internals/how-to-implement-nested-projects.md)   
 [有关卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)   
 [嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)   
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [实现嵌套项目的命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)   
 [筛选嵌套项目的 AddItem 对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)   
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [上下文参数](../../extensibility/internals/context-parameters.md)   
 [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
