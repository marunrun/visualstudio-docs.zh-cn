---
title: 旧版语言服务中的自动格式设置 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b69419e917a5ab5293af15b21822ca6473a9e292
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66344924"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>自动格式设置在旧版语言服务
使用自动设置格式语言服务会自动插入代码片段时在用户开始键入已知的代码构造。

## <a name="automatic-formatting-behavior"></a>自动格式设置行为
 例如，键入*如果*、 语言服务将自动插入匹配大括号，或按 ENTER 键时，如果语言服务将强制插入点置于新行到适当的缩进级别，具体取决于是否在前面的行可打开新的作用域。

 命令筛选器的语言服务的其余部分使用，还可用于自动格式设置。 此外可以突出显示匹配大括号显示通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A>。

## <a name="see-also"></a>请参阅
- [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)