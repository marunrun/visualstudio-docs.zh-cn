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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 71cec79acfcc934f9ddd910006f32f5207b26c84
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654966"
---
# <a name="customizing-t4-text-transformation"></a>自定义 T4 文本转换
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本模板是 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的一项功能，它允许您通过转换过程生成程序代码或其他文本文件。 使用 [!INCLUDE[vssdk_current_short](../includes/vssdk-current-short-md.md)]，可以通过自定义文本模板指令处理器或文本模板宿主来扩展默认模板转换过程。

## <a name="in-this-section"></a>本节内容
 [文本模板转换过程](../modeling/the-text-template-transformation-process.md)描述文本转换的工作方式，并解释模板主机和指令处理器的角色。

 [创建自定义 T4 文本模板指令处理器](../modeling/creating-custom-t4-text-template-directive-processors.md)指令处理器处理模板中的指令，例如 `<#@template#>.` 在编译模板过程中运行，并且可以加载程序集和其他资源。 它还可插入将在运行时加载资源的代码。 通过定义自己的指令处理器，可以降低模板的复杂性。

 [在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)如果要编写 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展（如菜单命令或事件处理程序），则扩展可以使用文本模板化服务来转换任何文本模板。 可以使用 Session 对象将参数数据传递到模板，并使用 `<#@parameter#>` 指令从模板内获取值。

 [使用自定义宿主处理文本模板](../modeling/processing-text-templates-by-using-a-custom-host.md)当执行文本模板的代码时，主机提供对外部文件和应用程序状态的访问。 例如，在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中运行文本转换的宿主可以提供对解决方案资源管理器的访问。 它还在错误消息窗口中显示错误。 如果要在不同的上下文中运行文本转换，可以定义自己的主机，以便提供对该上下文中可用服务的访问权限。

 如果要编写 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展，请考虑使用现有的文本转换服务，而不是编写自己的主机。 有关详细信息，请参阅[在 VS 扩展中调用文本转换](../modeling/invoking-text-transformation-in-a-vs-extension.md)。

## <a name="reference"></a>参考
 [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)

 提供文本模板指令和控制块的语法。
