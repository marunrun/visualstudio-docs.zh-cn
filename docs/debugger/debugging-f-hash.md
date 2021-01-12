---
title: 调试 F# | Microsoft Docs
description: 查看调试 F# 与调试 Visual Studio 中的其他托管语言之间的差异列表。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Debugging [F#]
- F#, debugging
ms.assetid: 20bcd51c-2d06-4281-9a1e-ef2b91d1a779
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f2dcacff924386cc279708c34d2232e50aa92c55
ms.sourcegitcommit: fcfd0fc7702a47c81832ea97cf721cca5173e930
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2020
ms.locfileid: "97728416"
---
# <a name="debugging-f"></a>调试 F\#
调试 F# 与调试任何托管语言类似，但有以下几种例外情况：

- “自动”窗口不显示 F# 变量。

- F# 不支持“编辑并继续”。 可以在调试会话期间编辑 F# 代码，但应避免这样做。 因为在调试会话期间无法应用代码更改，所以在调试期间编辑 F# 代码将导致源代码和正在调试的代码出现不匹配。

- 调试器无法识别 F# 表达式。 若要在 F# 调试期间在调试器窗口或对话框中输入表达式，必须将该表达式转换为 C# 语法。 在将 F# 表达式转换为 C# 时，请务必记住 C# 使用 == 作为比较运算符中的等号，而 F# 使用单个 =。

## <a name="see-also"></a>请参阅
- [调试托管代码](../debugger/debugging-managed-code.md)
