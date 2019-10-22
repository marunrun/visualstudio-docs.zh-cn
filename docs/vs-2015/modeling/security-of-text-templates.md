---
title: 文本模板的安全性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
ms.assetid: 567a2383-7d43-4acc-af4a-cd70b7a0151e
caps.latest.revision: 25
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e24a90d4e7af351fc4ba5807d2af7830edede9cb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671219"
---
# <a name="security-of-text-templates"></a>文本模板的安全性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

文本模板具有以下安全问题：

- 文本模板容易出现任意代码插入。

- 如果主机用于查找指令处理器的机制不安全，则可能会运行恶意指令处理器。

## <a name="arbitrary-code"></a>任意代码
 编写模板时，可以在 \< # # > 标记中添加任何代码。 这允许从文本模板中执行任意代码。

 请确保从受信任的源获取模板。 请确保警告应用程序的最终用户不执行不来自受信任的源的模板。

## <a name="malicious-directive-processor"></a>恶意指令处理器
 文本模板引擎与转换主机和一个或多个指令处理器进行交互，以将模板文本转换为输出文件。 有关详细信息，请参阅[文本模板转换过程](../modeling/the-text-template-transformation-process.md)。

 如果主机用于查找指令处理器的机制不安全，则会运行运行恶意指令处理器的风险。 在运行模板时，恶意指令处理器可能会提供在 `FullTrust` 模式下运行的代码。 如果创建自定义文本模板转换主机，则必须使用安全机制（如注册表）来查找指令处理器。
