---
title: 警告：脚本调试被禁用 | Microsoft Docs
description: 尝试在未在 Internet Explorer 中启用脚本调试的情况下调试脚本时，出现“脚本调试被禁用”警告。 查看启用脚本调试的步骤。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 7cc2e03a4efcf9a88675fd3c80f374ff78ba35bb
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "98149555"
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