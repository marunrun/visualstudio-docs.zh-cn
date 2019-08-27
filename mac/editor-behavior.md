---
title: 代码格式设置
description: 本文介绍可用于修改 Visual Studio for Mac 中的文本编辑器行为的各种选项
author: cobey
ms.author: cobey
ms.date: 05/06/2018
ms.assetid: 81EE4460-26EB-4BB0-9297-932E1F88E4B8
ms.openlocfilehash: 20363d5497ea5897cb2685ca838da44b8c21d3df
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823177"
---
# <a name="editor-behavior"></a>编辑器行为

可将编辑器行为设置为允许代码的格式与写入方式相同。 可在“Visual Studio”>“首选项”>“文本编辑器”>“行为”下设置这些操作，以下介绍了一些常用的功能： 

![编辑器行为选项](media/source-editor-image9.png)

* 创建新的类、方法或属性时，会自动将匹配的右大括号添加到代码。 选中此选项时，键入 `{` 将自动添加 `}`。
* 按下分号或大括号等字符会触发即时生成的代码格式，模拟已设置的格式首选项。
* 也可以选择在保存文件时设置其格式，该方法允许按需写入代码，让 IDE 负责按现有的首选项设置代码格式。
* 可将缩进设置为“无”、“自动”或“智能”。 这些设置会执行以下操作：
  * 无 - 将脱字号设置到下一行的起始位置
  * 自动 - 将脱字号设置到下一行的同一列
  * 智能 - 基于代码在下一行缩进
* 不同 OS 有不同的断字行为，出于导航目的，文本编辑器需要知道字开始或结束的位置。 可以将格式设置为 Unix 或 Windows。

也可以为 XML、CSS、HTML 和 JSON 设置格式规则。

## <a name="see-also"></a>请参阅

- [代码样式首选项（Windows 上的 Visual Studio）](/visualstudio/ide/code-styles-and-quick-actions)
