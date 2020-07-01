---
title: 在正则字符串文本和逐字字符串文本之间转换
ms.date: 06/08/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: 7e8e239f53f92727072a2fcd6573d6957b7cd3ec
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290771"
---
# <a name="convert-between-regular-string-and-verbatim-string-literals-refactoring"></a>在正则字符串文本和逐字字符串文本重构之间转换

此重构适用于：

- C#

**功能：** 允许在正则字符串文本和逐字字符串文本之间转换。

**使用时机：** 需要在代码中节省空间或提高清晰度。

操作原因：将逐字字符串文本转换为常规字符串文本可以帮助节省空间。 将正则字符串文本转换为逐字字符串文本可提高清晰度。

## <a name="how-to"></a>操作说明

1. 将插入符号放置在正则字符串文本或逐字字符串文本上：

2. 按“Ctrl”+ **。** 触发“快速操作和重构”菜单。

3. 选择以下选项之一： 

    选择“转换为规则字符串”。

    ![转换为正则字符串](media/convert-to-regular-string.png)

    选择“转换为逐字字符串”。

    ![转换为逐字字符串](media/convert-to-verbatim-string.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)