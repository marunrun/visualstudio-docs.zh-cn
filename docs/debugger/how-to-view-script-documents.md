---
title: 查看脚本文档 | Microsoft Docs
description: 了解如何使用解决方案资源管理器在 Visual Studio 中查看 JavaScript 服务器端脚本文档。
ms.custom: SEO-VS-2020
ms.date: 11/05/2019
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Script Explorer
ms.assetid: 8b621e53-4508-4b4a-9995-70995b0b9ac8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 91c2e1c0438ebf8fad69f985f62a976ff6710a81
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98150478"
---
# <a name="how-to-view-script-documents-javascript"></a>如何：查看脚本文档 (JavaScript)

服务器端脚本文件在解决方案资源管理器中可见。 客户端脚本文件仅在调试模式或中断模式下显示。 客户端脚本文件显示在“脚本文档”节点中。

对于某些动态生成页面的应用程序类型，当你从浏览器中加载的脚本文档设置断点时，更容易进入中断模式并进行调试。 同样，可以从加载的脚本文档中添加 `debugger` 语句，以进入中断模式。 本文将介绍如何查看这些文档。

> [!NOTE]
> 在 [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] 之前，从服务器端脚本生成的客户端脚本文件显示在“脚本资源管理器”窗口中。

### <a name="to-view-a-server-side-script-document"></a>查看服务器端脚本文档

1. 在“解决方案资源管理器”中，打开 \<Website Pathname> 节点 。

2. 双击要查看的脚本文件。

     服务器端脚本文件在源窗口中打开。

### <a name="to-view-a-client-side-script-document"></a>查看客户端脚本文档

1. 在“解决方案资源管理器”中，打开“脚本文档”节点 。

2. 双击要查看的脚本文件。

     客户端脚本文件在源窗口中打开。

## <a name="see-also"></a>请参阅
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)