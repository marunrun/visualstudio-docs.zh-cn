---
title: 枚举器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, enumerators
ms.assetid: a60030c5-e1d1-47e1-84bb-cbfe838ab479
caps.latest.revision: 20
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 65a03a8dc741ec86aca3137f49cd753722ede215
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204566"
---
# <a name="enumerators"></a>枚举数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本部分列出了源代码管理插件必须要知道源控制插件 API 中的枚举器的数据类型。  
  
## <a name="in-this-section"></a>本节内容  
 [命令代码](../extensibility/command-code-enumerator.md)  
 枚举的选项[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)并[SccPopulateList](../extensibility/sccpopulatelist-function.md)函数。  
  
 [消息](../extensibility/message-enumerator.md)  
 枚举用于打印的回叫，使用标志[LPTEXTOUTPROC](../extensibility/lptextoutproc.md)。  
  
 [文件状态代码](../extensibility/file-status-code-enumerator.md)  
 包含已命名的常量值用于指定源代码管理下的文件的状态。  
  
 [目录状态代码](../extensibility/directory-status-code-enumerator.md)  
 包含已命名的常量值用于指定源代码管理下的目录的状态。  
  
## <a name="related-sections"></a>相关章节  
 [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)  
 定义源控制插件 SDK 并介绍了包含的资源。  
  
 [SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)  
 提示用户输入给定命令的高级选项。  
  
 [SccPopulateList](../extensibility/sccpopulatelist-function.md)  
 检查以了解其当前状态的文件的列表。 此外，使用`pfnPopulate`函数，以通知调用方，当文件不匹配的条件时`nCommand`。  
  
 [LPTEXTOUTPROC](../extensibility/lptextoutproc.md)  
 描述使用的回调函数[SccOpenProject](../extensibility/sccopenproject-function.md)以显示从源代码管理插件通过 IDE 的消息。  
  
 [源代码管理插件](../extensibility/source-control-plug-ins.md)  
 提供源控制插件 API 中的所有元素的完整列表。
