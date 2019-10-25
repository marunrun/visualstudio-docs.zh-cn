---
title: COM 和 ActiveX 调试 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.com
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- COM, debugging
- debugging ActiveX applications
- debugging [Visual Studio], COM
- debugging COM containers
- ActiveX controls, debugging
ms.assetid: 3260b2a7-3239-493d-9271-aedf705c13c7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f6dc69a18aa09536e5735431aa451bc2dd3933ee
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745683"
---
# <a name="com-and-activex-debugging"></a>调试 COM 和 ActiveX
本节提供有关调试 COM 应用程序和 ActiveX 控件的提示。

## <a name="in-this-section"></a>本节内容
 [COM 服务器和容器调试](../debugger/com-server-and-container-debugging.md)提到了调试 COM 应用程序时的特殊注意事项。 问题包括：使用同一解决方案中的两个项目来调试 COM 服务器和容器，跟踪到跨越进程边界的调用中，在回调函数中设置断点，以及单步通过和单步执行容器和服务器。

 [如何：调试 ActiveX 控件](../debugger/how-to-debug-an-activex-control.md)包含有关调试 ActiveX 控件的信息。 这包括：为调试会话指定容器以查看 ActiveX 控件中的代码的执行方式，调试数据绑定 ActiveX 控件，模拟特定容器，以及单步执行容器的代码。

 [COM 调试工具](../debugger/com-debugging-tools.md)列出在调试 COM 应用程序时可能有用的查看器和示例应用程序。

## <a name="related-sections"></a>相关章节
 [首先查看调试器](../debugger/debugger-feature-tour.md)提供指向调试文档的较大章节的链接。 信息包括：调试器的新增功能、设置和准备、断点、处理异常、编辑并继续、调试托管代码、调试C++项目、调试 COM 和 ActiveX、调试 dll、调试 SQL 和用户接口引用。

## <a name="see-also"></a>请参阅

- [调试器安全](../debugger/debugger-security.md)
- [COM 简介](/cpp/atl/introduction-to-com)
- [ActiveX 控件](/cpp/mfc/activex-controls)
- [SDI 服务器应用程序](../debugger/sdi-server-applications.md)