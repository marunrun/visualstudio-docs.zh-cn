---
title: 文本模板的安全性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 25815bcb7f027501fb849dcd29d14b040c24d7fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "75591965"
---
# <a name="security-of-text-templates"></a>文本模板的安全性
文本模板具有以下安全问题：

- 文本模板容易出现任意代码插入。

- 如果主机用于查找指令处理器的机制不安全，则可能会运行恶意指令处理器。

## <a name="arbitrary-code"></a>任意代码
 编写模板时，可以将任何代码放在 \<# #> 标记中。 这允许从文本模板中执行任意代码。

 请确保从受信任的源获取模板。 请确保警告应用程序的最终用户不执行不来自受信任的源的模板。

## <a name="malicious-directive-processor"></a>恶意指令处理器
 文本模板引擎与转换主机和一个或多个指令处理器进行交互，以将模板文本转换为输出文件。 有关详细信息，请参阅 [文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

 如果主机用于查找指令处理器的机制不安全，则会运行运行恶意指令处理器的风险。 恶意指令处理器可能会提供 `FullTrust` 运行模板时在模式下运行的代码。 如果创建自定义文本模板转换主机，则必须使用安全机制（如注册表）来查找指令处理器。
