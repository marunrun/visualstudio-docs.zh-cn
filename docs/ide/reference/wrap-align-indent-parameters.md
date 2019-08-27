---
title: 自动换行、缩进、对齐参数
ms.date: 02/13/2019
ms.topic: reference
author: kendrahavens
ms.author: kehavens
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: ccdf29e3a4cda2bf5d527a2b712878c1fbd76197
ms.sourcegitcommit: cd21b38eefdea2cdefb53e68e7a30b868e78dd6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2019
ms.locfileid: "66037586"
---
# <a name="wrap-indent-and-align-parameters-or-arguments"></a>换行、缩进和对齐参数

此重构适用于：

- C#

- Visual Basic

**功能：** 允许你换行、缩进或对齐参数。

**使用时机：** 有具有多个参数的方法声明或调用。

操作原因：根据用户偏好换行或缩进时，读取一长串参数会更容易。

## <a name="how-to"></a>操作说明

1. 请将光标放置在参数列表中。
2. 按“Ctrl”+**。** 触发“快速操作和重构”菜单。

   ![自动换行、缩进和对齐参数](media/wrap-parameters.png)

3. 按 Enter 接受重构。

   ![应用的换行、缩进和对齐参数](media/wrap-parameters-completed.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
