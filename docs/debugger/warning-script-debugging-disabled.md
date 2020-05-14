---
title: 警告：脚本调试被禁用 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.scriptdisabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 323d2b1d-52a4-42f7-b4ad-96b4b0c23b8d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 15de1a1e516cb3d84c24428ef04dd87baedaed9e
ms.sourcegitcommit: ade07bd1cf69b8b494d171ae648cfdd54f7800d3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2020
ms.locfileid: "81648505"
---
# <a name="warning-script-debugging-disabled"></a>警告：脚本调试已禁用
脚本调试当前在 Internet Explorer 中禁用

 尝试在未在 Internet Explorer 中启用脚本调试的情况下调试脚本时，会出现此警告。 出于安全考虑，默认情况下，Internet Explorer 禁用脚本调试。

### <a name="to-enable-script-debugging-in-internet-explorer"></a>在 Internet Explorer 中启用脚本调试

1. 在 Internet Explorer 的“工具”菜单上选择“Internet 选项”   。

2. 在“Internet 选项”  对话框中，单击“高级”  选项卡。

3. 在“高级”选项卡上，在“设置”框中查找“浏览”类别    。

4. 清除“禁用脚本调试(Internet Explorer)”  。

5. 单击 **“确定”** 。

6. 退出并重新启动 Internet Explorer。

     新设置现在将生效。

## <a name="see-also"></a>请参阅
- [如何：附加到脚本](attach-to-running-processes-with-the-visual-studio-debugger.md)