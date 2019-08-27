---
title: 自定义 T4 文本转换 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, API
- text templates, custom hosts
ms.assetid: 62cd9a3c-a6e1-4b29-93f5-f2a0cf47dc92
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ea2881cfebaf10d7a72e8651214cf3a6f64debae
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68164676"
---
# <a name="customizing-t4-text-transformation"></a>自定义 T4 文本转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本模板是一项功能的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，可以生成程序代码或其他文本文件通过转换过程。 使用[!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]，可以通过自定义文本模板指令处理器或文本模板宿主扩展默认模板转换过程。  
  
## <a name="in-this-section"></a>本节内容  
 [文本模板转换过程](../modeling/the-text-template-transformation-process.md)  
 描述文本转换的工作方式，并说明了模板宿主和指令处理器的角色。  
  
 [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)  
 指令处理器处理指令在你的模板，如`<#@template#>.`它运行的模板，在编译过程，并可以加载程序集和其他资源。 它还可以插入代码将加载在运行时的资源。 通过定义指令处理器，可以减少您的模板的复杂性。  
  
 [在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)  
 如果你正在编写[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]如菜单命令或事件处理程序的扩展，您的扩展插件可以使用文本模板化服务来转换任何文本模板。 可以将参数数据传递到模板，通过使用 Session 对象，并通过获取从模板中的值`<#@parameter#>`指令。  
  
 [使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)  
 文本模板的代码执行时，主机可以访问外部文件和应用程序的状态。 例如，主机在运行文本转换的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]可提供对解决方案资源管理器访问。 它还在错误消息窗口中显示错误。 如果你想要在不同的上下文中运行文本转换，则可以定义您自己提供对在该上下文中可用的服务的访问的主机。  
  
 如果你正在编写[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展，请考虑使用现有的文本转换服务而不编写您自己的主机。 有关详细信息，请参阅[VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。  
  
## <a name="reference"></a>参考  
 [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)  
  
 提供文本模板指令和控制块的语法。
