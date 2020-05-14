---
title: 旧语言服务中的自动格式 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a11e9c1fdef60e71f46cee9986d925e876dcac35
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709983"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>旧语言服务中的自动格式设置
使用自动格式，当用户开始键入已知代码构造时，语言服务会自动插入代码段。

## <a name="automatic-formatting-behavior"></a>自动格式化行为
 例如，当您键入*if，* 语言服务会自动插入匹配的大括号，或者如果按 ENTER 键时，语言服务会强制新行上的插入点到相应的缩进级别，具体取决于前面的行是否打开新作用域。

 用于其余语言服务的命令筛选器也可用于自动格式化。 您还可以通过调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A>突出显示匹配的大括号。

## <a name="see-also"></a>请参阅
- [开发传统语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
