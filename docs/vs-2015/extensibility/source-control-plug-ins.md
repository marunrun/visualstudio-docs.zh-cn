---
title: 源代码管理插件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a5a99ebdf2366ce6a60a6a724afc7d742db7150f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705794"
---
# <a name="source-control-plug-ins"></a>源代码管理插件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

源代码控制插件 SDK 参考部分包含启用源代码管理系统集成的完整接口规范[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 它指定的语法和各种源代码管理插件必须实现到接口使用的函数和数据类型的语义[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]集成的开发环境 (IDE)。  
  
## <a name="in-this-section"></a>本节内容  
 [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)  
 列出必须由源代码管理插件为了遵守源控制插件 API 实现的函数。  
  
 [通过 IDE实现的回叫函数](../extensibility/callback-functions-implemented-by-the-ide.md)  
 介绍了源代码管理插件用于执行特定命令时，将信息传回给 IDE 的函数。  
  
 [枚举器](../extensibility/enumerators.md)  
 列出了源代码管理插件必须要知道源控制插件 API 中的枚举器的数据类型。  
  
 [功能标志](../extensibility/capability-flags.md)  
 介绍`SCC_CAP_xxx`标志，是指示提供程序的功能。  
  
 [特定命令使用的位标志](../extensibility/bitflags-used-by-specific-commands.md)  
 列出在特定命令的上下文中有用的标志。  
  
 [错误代码](../extensibility/error-codes.md)  
 列出了作为函数返回的常见错误值`SCCTRN`。  
  
 [作为用于查找源代码管理插件的密钥的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)  
 介绍用于访问注册表，以查找源代码管理插件的密钥。  
  
 [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)  
 介绍了一个客户端的文件，其中包含信息不透明的 IDE，但源代码管理插件使用，以在版本控制中找到解决方案或项目。  
  
 [实现源代码管理插件的最佳做法](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)  
 提供了一系列技术的重要提醒记住时要实现源控件插件 API。  
  
 [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)  
 描述源控件插件 API 中的限制上各种不同的函数中使用的字符串的长度。  
  
 [术语表](../extensibility/source-control-plug-in-glossary.md)  
 提供了有用的术语和用于读取源控制插件 SDK 文档及其定义。  
  
 [如何：关闭源代码管理插件的兼容性警告](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)  
 介绍如何禁用警告。  
  
## <a name="related-sections"></a>相关章节  
 [源控件插件示例](https://msdn.microsoft.com/61de7d2b-71db-451e-8e3e-d41b11c7a4ca)  
 提供的源代码管理插件功能的示例。  
  
 [源代码管理插件的测试指南](../extensibility/internals/test-guide-for-source-control-plug-ins.md)  
 介绍与源代码管理插件相关的测试过程。  
  
 [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)  
 讨论如何创建一个源代码管理插件，而使用提供的源代码管理功能[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]源代码管理用户界面 (UI)。  
  
 [Visual Studio SDK 引用](../extensibility/visual-studio-sdk-reference.md)  
 显示参考主题的列表。
