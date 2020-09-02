---
title: 编辑 XSLT 样式表 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 080bed0f-0ca9-4be7-aecd-6bdaebc04007
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3e1669affa89c91ca3ae1958c22ff3ec4d56bb8c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670957"
---
# <a name="editing-xslt-style-sheets"></a>编辑 XSLT 样式表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“XML 编辑器”还可以用于编辑 XSLT 样式表。 可以利用默认的编辑器功能，例如 IntelliSense、大纲、XML 代码段等。 此外，还提供了一些新功能，使 XSLT 中的开发更加容易。

## <a name="xslt-features"></a>XSLT 功能
 下表介绍使用 XSLT 样式表时的特定功能。

 **语法着色** XSLT 关键字（例如、 `template` `match` 等）以 " **字体和颜色** " 设置指定的 xslt 关键字颜色显示。

 **波浪下划线** "XML 编辑器" 使用已安装的 xslt .xsd 文件来验证 XSLT 样式表。 验证错误以蓝色的波浪形下划线显示。 “XML 编辑器”还在后台编译样式表，并使用相应的波浪形下划线报告编译器错误或警告。

 **支持脚本块** XSLT 调试程序支持脚本块中的代码，因此你可以设置断点并逐行执行脚本块代码。

 **查看 XSLT 输出** 您可以执行 XSL 转换，并从 "XML 编辑器" 查看输出。 有关详细信息，请参阅 [如何：从 XML 编辑器执行 XSLT 转换](../xml-tools/how-to-execute-an-xslt-transformation-from-the-xml-editor.md)。

 **调试 XSLT** 可以从 "XML 编辑器" 中的 XSLT 文件启动 XSLT 调试程序。 调试程序支持在 XSLT 文件中设置断点、查看 XSLT 执行状态等。 将光标置于 XSLT 变量上，可以显示包含变量值的工具提示。 调试程序可以用于调试样式表，也可以用于调试从另一个应用程序调用的已编译 XSLT 转换。 有关详细信息，请参阅[调试 XSLT](../xml-tools/debugging-xslt.md)。

## <a name="see-also"></a>另请参阅
 [XML 编辑器](../xml-tools/xml-editor.md)
