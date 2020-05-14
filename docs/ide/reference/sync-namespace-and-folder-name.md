---
title: 同步命名空间和文件夹名称
ms.date: 06/12/2019
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
dev_langs:
- CSharp
ms.workload:
- dotnet
ms.openlocfilehash: d7073edaf6ecc261c58bf1e5607323b9214c5ed0
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "67160753"
---
# <a name="sync-namespace-and-folder-name"></a>同步命名空间和文件夹名称

此重构适用于：

- C#

**功能：** 同步命名空间和文件夹名称。

**使用时机：** 你想要通过将文件拖动到新文件夹重构部分解决方案。 

操作原因：  你想要确保你的命名空间中的新文件夹结构保持最新。

## <a name="how-to"></a>操作说明

1. 请将光标置于命名空间名称中。
2. 按“Ctrl”  + **。** 触发“快速操作和重构”  菜单。
3. 选择“将命名空间更改为 \<文件夹名称>”  。

   ![同步命名空间和文件夹名称](media/sync-namespace-and-folder-name.png)

## <a name="see-also"></a>请参阅

- [重构](../refactoring-in-visual-studio.md)
