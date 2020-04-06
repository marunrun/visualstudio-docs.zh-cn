---
title: 源代码管理插件 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699893"
---
# <a name="source-control-plug-ins"></a>源代码管理插件
源代码管理插件 SDK 参考部分包含完整的接口规范，使源代码管理系统能够与[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]集成。 它指定源代码管理插件必须实现的各种函数和数据类型的语法和语义，以便与[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]集成开发环境 （IDE） 接口。

## <a name="in-this-section"></a>本节内容
- [源代码管理插件 API 功能](../extensibility/source-control-plug-in-api-functions.md)列出源代码管理插件必须实现的函数，以便符合源代码管理插件 API。

- [IDE 实现的回调函数](../extensibility/callback-functions-implemented-by-the-ide.md)描述源代码管理插件在执行某些命令时用于将信息传回 IDE 的功能。

- [枚举器](../extensibility/enumerators.md)在源代码管理插件 API 中列出源控件插件 API 中的枚举器数据类型，源代码管理插件必须了解这些数据类型。

- [功能标志](../extensibility/capability-flags.md)描述`SCC_CAP_xxx`标志，这些标志表示提供程序的功能。

- [特定命令使用的比特标志](../extensibility/bitflags-used-by-specific-commands.md)列出在特定命令的上下文中有用的标志。

- [错误代码](../extensibility/error-codes.md)将函数返回的常见错误值列为`SCCTRN`。

- [用作查找源代码管理插件的键](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)描述访问注册表以查找源代码管理插件的键。

- [MSSCCPRJ.SCC 文件](../extensibility/mssccprj-scc-file.md)描述包含对 IDE 不透明的信息，但源代码管理插件用于在版本控制中查找解决方案或项目的信息的客户端文件。

- [实现源代码管理插件的最佳做法](../extensibility/best-practices-for-implementing-a-source-control-plug-in.md)提供在实现源代码管理插件 API 时要记住的重要技术提醒的集合。

- [字符串长度的限制](../extensibility/restrictions-on-string-lengths.md)描述源代码管理插件 API 中对各种函数中使用的字符串长度的限制。

- [词汇表](../extensibility/source-control-plug-in-glossary.md)提供了用于阅读源代码管理插件 SDK 文档的有用术语及其定义。

- [如何：关闭源代码管理插件的兼容性警告](../extensibility/how-to-turn-off-compatibility-warnings-for-source-control-plug-ins.md)描述如何禁用警告。

## <a name="related-sections"></a>相关章节
- [源代码管理插件示例](https://www.microsoft.com/download/details.aspx?id=55984)提供源代码管理插件功能的示例。

- [源代码管理插件测试指南](../extensibility/internals/test-guide-for-source-control-plug-ins.md)描述与源代码管理插件相关的测试过程。

- [创建源代码管理插件](../extensibility/internals/creating-a-source-control-plug-in.md)讨论如何在使用源代码管理用户界面 （UI） 时创建提供源代码管理功能的[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]源代码管理插件。

- [可视化工作室 SDK 参考](../extensibility/visual-studio-sdk-reference.md)显示参考主题的列表。
