---
title: 多个插入点编辑
description: 在 Visual Studio for Mac 中编辑代码时，将文本插入多个位置。
author: cobey
ms.author: cobey
ms.date: 08/19/2019
ms.openlocfilehash: a21bebda057a772017fa1481e18f9801d1fbcbdf
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "75439048"
---
# <a name="multi-caret-editing"></a>多个插入点编辑

多个插入点编辑允许一次添加 n  个插入点数。 在多个插入点模式下，你可以通过单击鼠标或通过键盘命令将其他插入点添加到文档中。 主插入点由红色光标表示，辅助插入点则显示为浅蓝色。 可以通过 `ESC` 键禁用多个插入点编辑模式。

## <a name="enabling-multi-caret-editing"></a>启用多个插入点编辑

### <a name="keyboard"></a>键盘

可以通过键盘以多种方式启用多个插入点模式。 下表提供了可用于进入多个插入点编辑的特定模式的键盘快捷键：

| 热键  | 操作                        | 
|---------| ------------------------------|
|  ⌥⇧.   | 插入下一个匹配的插入点    | 
|  ⌥⇧;   | 在所有匹配位置插入插入点 | 
|  ⌥⇧,   | 删除最后一个插入点             | 
|  ⌥⇧/   | 下移最后一个插入点          | 

调用命令时，这些行为都将锚定到插入点的当前位置。 例如，如果插入点位于单词“name”的开头，并且你调用“在所有匹配位置插入插入点”(⌥⇧;)，当前文档中“name”一词的每个实例都将在单词的开头插入一个插入点。 同样，如果调用命令“插入下一个匹配的插入点”(⌥⇧.)，则会在下一个单词“name”的实例中放置一个插入点。 可以多次调用此命令。

![多个插入点键盘](media/multi-caret-keyboard.gif)

## <a name="mousetouchpad"></a>鼠标/触摸板

通过使用光标，可以为多个插入点自由选择特定插入点。 将键盘快捷键绑定到匹配字符串时，可以使用光标在文档中的任何位置手动插入插入点。 设置插入点后，每个插入点都将回显你在键盘上键入的键项。

若要使用鼠标插入多个插入点，必须按住 ⌘⌥，并单击要输入插入点的位置。 只要按住 ⌘⌥ 键，就会处于插入模式。 如果在不正确的位置插入插入点，则可以通过继续按住 ⌘⌥ 并再次单击同一区域来删除插入点。 将所有插入点定位到所需位置之后，停止按 ⌘⌥ 键并开始键入。 以下 GIF 演示了如何选择一组插入点以及删除错误设置的点。

![多个插入点鼠标](media/multi-caret-mouse.gif)

## <a name="see-also"></a>另请参阅

- [快速操作（Windows 上的 Visual Studio）](/visualstudio/ide/quick-actions)
- [重构代码（Windows 上的 Visual Studio）](/visualstudio/ide/refactoring-in-visual-studio)
