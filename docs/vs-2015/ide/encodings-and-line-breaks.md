---
title: 编码和换行符 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
f1_keywords:
- vs.Encoding
helpviewer_keywords:
- line breaks
- encoding
- Visual Studio, encoding
- editors, line breaks
- line break characters
- Visual Studio, line break characters
ms.assetid: 8f9b3ffc-7b8d-44f4-87cb-dc29105be12d
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2e1b13cc101ea4d7609633fd9c11bf87946d7b7d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665723"
---
# <a name="encodings-and-line-breaks"></a>编码和换行符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可使用“文件”/“高级保存选项”设置来确定所需的换行符类型。 还可使用相同的设置更改文件的编码。

> [!NOTE]
> 如果已具有特定类型的开发设置（Visual Basic、F#、Web 开发），则菜单上可能不会出现“高级保存选项”。 若要更改设置（例如更改为“常规”），请打开“工具”/“导入和导出设置”。 有关详细信息，请参阅[在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。

 在 Visual Studio 中，以下字符将解释为换行符：

- CRLF：回车符 + 换行符，Unicode 字符 000D + 000A

- LF：换行符，Unicode 字符 000A

- NEL：下一行，Unicode 字符 0085

- LS：行分隔符，Unicode 字符 2028

- PS：段落分隔符，Unicode 字符 2029

  从其他应用程序复制的文本将保留原始编码和换行符。 例如，当从记事本复制文本并将其粘贴到 Visual Studio 中的文本文件时，此文本的设置仍与在记事本中的设置相同。

  当打开包含不同换行符的文件时，可能会看到一个对话框，询问是否应规范化不一致的换行符以及要选择哪一种换行类型。
