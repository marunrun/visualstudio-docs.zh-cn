---
title: 源代码管理插件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 01e7a0ca8a509d430a0794a2cedb4b2e9d869585
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66331826"
---
# <a name="source-control-plug-ins"></a>源代码管理插件
源代码控制插件 SDK 参考部分包含启用源代码管理系统集成的完整接口规范[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]。 它指定的语法和各种源代码管理插件必须实现到接口使用的函数和数据类型的语义[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]集成的开发环境 (IDE)。

## <a name="in-this-section"></a>本节内容
- [源控件插件 API 函数](../extensibility/source-control-plug-in-api-functions.md)列出必须由源代码管理插件为了遵守源控制插件 API 实现的函数。

- [通过 IDE 的回调函数实现](../extensibility/callback-functions-implemented-by-the-ide.md)介绍了源代码管理插件用于执行特定命令时，将信息传回给 IDE 的函数。

- [枚举器](../extensibility/enumerators.md)列出了源代码管理插件必须要知道源控制插件 API 中的枚举器的数据类型。

- [功能标志](../extensibility/capability-flags.md)描述`SCC_CAP_xxx`标志，是指示提供程序的功能。

- [位标志由特定命令](../extensibility/bitflags-used-by-specific-commands.md)列出在特定命令的上下文中有用的标志。

- [错误代码](../extensibility/error-codes.md)列出了作为函数返回的常见错误值`SCCTRN`。

- [使用字符串作为键用于查找源代码管理插件](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)介绍用于访问注册表，以查找源代码管理插件的密钥。

- [MSSCCPRJ。SCC 文件](../extensibility/mssccprj-scc-file.md)介绍了一个客户端的文件，其中包含信息不透明的 IDE，但源代码管理插件使用，以在版本控制中找到解决方案或项目。

- [实现源代码管理插件的最佳实践](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)提供了一系列技术的重要提醒记住时要实现源控件插件 API。

- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md)上各种不同的函数中使用的字符串的长度描述源控件插件 API 中的限制。

- [术语表](../extensibility/source-control-plug-in-glossary.md)提供有用的术语和用于读取源控制插件 SDK 文档及其定义。

- [如何：打开关闭的兼容性警告源代码管理插件](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)介绍如何禁用警告。

## <a name="related-sections"></a>相关章节
- [源控件插件示例](https://www.microsoft.com/download/details.aspx?id=55984)提供了一个示例的源代码管理插件功能。

- [测试的源代码管理插件的指南](../extensibility/internals/test-guide-for-source-control-plug-ins.md)介绍与源代码管理插件相关的测试过程。

- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)介绍了如何创建一个源代码管理插件，而使用提供的源代码管理功能[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]源代码管理用户界面 (UI)。

- [Visual Studio SDK 引用](../extensibility/visual-studio-sdk-reference.md)显示参考主题的列表。