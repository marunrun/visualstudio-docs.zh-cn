---
title: 文本模板的安全性
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66159516c6b1360203130dedb56c0e6c192a118a
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62824015"
---
# <a name="security-of-text-templates"></a>文本模板的安全性
文本模板具有以下安全问题：

- 文本模板是任意代码插入到易受攻击。

- 如果主机用来查找指令处理器的机制不是安全的可以运行恶意的指令处理器。

## <a name="arbitrary-code"></a>任意代码
 在编写模板时，可以将之内的任何代码\<# # > 标记。 这允许在文本模板中执行任意代码。

 请确保从受信任的来源获取模板。 请确保你的应用程序无法执行不是来自受信任源的模板的最终用户，则发出警告。

## <a name="malicious-directive-processor"></a>恶意的指令处理器
 与转换主机和一个或多个指令处理器转换到的输出文件的模板文本，文本模板引擎进行交互。 有关详细信息，请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

 如果主机用来查找指令处理器的机制不是安全的它运行的运行恶意的指令处理器的风险。 恶意的指令处理器可以提供在中运行的代码`FullTrust`模式时运行该模板。 如果创建自定义文本模板转换主机，您必须使用一种安全机制，如注册表中，要找到指令处理器的引擎。