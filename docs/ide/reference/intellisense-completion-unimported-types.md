---
title: 针对未导入类型的 IntelliSense 完成
description: 如何使用 `using` 指令将 IntelliSense 完成用于尚未导入的类型。
ms.date: 03/10/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 04ea7c94d3dd24c1a511544adca9bfac3370cd71
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "79094252"
---
# <a name="intellisense-completion-for-unimported-types"></a>针对未导入类型的 IntelliSense 完成

此重构适用于：

- C#

- Visual Basic

**功能：** IntelliSense 提供针对未导入类型的完成功能。

**使用时机：** 想要添加已在项目中有依赖项的类型，但你尚未将导入语句添加到文件。 

操作原因：  无需手动将导入语句添加到文件。

## <a name="how-to"></a>操作说明

1. 开始使用在项目中有依赖项的类型后，IntelliSense 将为你提供建议。
2. 按 Tab 键。  

   导入语句将添加到文件。

   ![针对未导入类型的 IntelliSense 完成](media/intellisense-completion-unimported-types.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
