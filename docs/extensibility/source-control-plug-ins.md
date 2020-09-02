---
title: 源代码管理插件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, reference
ms.assetid: 964980ca-21c5-4706-8535-6ea23e1c9cc9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cc5f092e0ae93109d071af0b1a67999947e73e90
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699893"
---
# <a name="source-control-plug-ins"></a>源代码管理插件
源代码管理插件 SDK 参考部分包含完整的接口规范，使源代码管理系统能够与进行集成 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 它指定源代码管理插件必须实现的各种函数和数据类型的语法和语义，以与 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] (IDE) 的集成开发环境交互。

## <a name="in-this-section"></a>本节内容
- [源代码管理插件 API 函数](../extensibility/source-control-plug-in-api-functions.md) 列出必须由源代码管理插件实现的函数，才能遵从源代码管理插件 API。

- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md) 描述在执行特定命令时源代码管理插件用来将信息传递回 IDE 的函数。

- [枚举](../extensibility/enumerators.md) 器列出源代码管理插件 API 中源代码管理插件必须知道的枚举器数据类型。

- [功能标志](../extensibility/capability-flags.md) 介绍 `SCC_CAP_xxx` 标志，指示提供程序的功能。

- [特定命令使用的 Bitflags](../extensibility/bitflags-used-by-specific-commands.md) 列出在特定命令上下文中有用的标志。

- [错误代码](../extensibility/error-codes.md) 列出了由函数返回的常见错误值 `SCCTRN` 。

- [用作查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md) 描述用于访问注册表以查找源代码管理插件的键。

- [Mssccprj.scc。SCC 文件](../extensibility/mssccprj-scc-file.md) 描述了包含 IDE 的信息不透明的客户端文件，但源代码管理插件使用此文件在版本控制中查找解决方案或项目。

- [实现源代码管理插件的最佳实践](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md) 提供在实现源代码管理插件 API 时要记住的重要技术提醒的集合。

- [字符串长度限制](../extensibility/restrictions-on-string-lengths.md) 介绍源代码管理插件 API 对各种函数中使用的字符串长度的限制。

- [术语表](../extensibility/source-control-plug-in-glossary.md) 提供用于读取源代码管理插件 SDK 文档的有用术语及其定义。

- [如何：关闭源代码管理插件的兼容性警告](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md) 描述如何禁用警告。

## <a name="related-sections"></a>相关章节
- [源代码管理插件示例](https://www.microsoft.com/download/details.aspx?id=55984) 提供源代码管理插件功能的示例。

- [源代码管理插件的测试指南](../extensibility/internals/test-guide-for-source-control-plug-ins.md) 介绍与源代码管理插件相关的测试过程。

- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md) 讨论在使用 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 源代码管理用户界面 (UI) 时，如何创建提供源代码管理功能的源代码管理插件。

- [Visual STUDIO SDK 参考](../extensibility/visual-studio-sdk-reference.md) 显示参考主题的列表。
