---
title: 设置代码书签
description: 了解如何使用书签标记代码行，以便能够快速返回到特定位置，或者在不同位置间来回跳转。
ms.custom: SEO-VS-2020
ms.date: 02/23/2018
ms.topic: conceptual
f1_keywords:
- VS.BookmarkWindow
ms.assetid: a752ed5f-5cf9-4bf2-865a-2131ca600ed5
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ded48fcea0630bf07311cbb92ed2e258cdf4afb1
ms.sourcegitcommit: bbed6a0b41ac4c4a24e8581ff3b34d96345ddb00
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2020
ms.locfileid: "96560858"
---
# <a name="set-bookmarks-in-code"></a>在代码中设置书签

可以使用书签标记代码行，以便能够快速返回到特定位置，或者在不同位置间来回跳转。 有两个位置提供书签命令和图标：“书签窗口”（“视图” > “书签窗口”）和文本编辑器工具栏。

![书签工具栏](media/bookmark-toolbar.png)

![“书签”窗口](media/bookmark-window.png)

## <a name="manage-bookmarks"></a>管理书签

若要添加书签，请将光标置于要添加书签的行上。 选择“切换书签”按钮，或者按 Ctrl+K、Ctrl+K。 这样便可添加书签。 如果再次选择“切换书签”按钮（或按 Ctrl+K、Ctrl+K），将删除该书签。

若要一目了然地了解特定书签的用途，可在右键单击或上下文菜单中的“书签窗口”中对其进行重命名。 也可以选择书签窗口中的“删除”按钮来删除书签。

> [!IMPORTANT]
> 书签设置在行号上，而不是代码上。 如果修改代码，书签会保留在行号上，不会随代码移动。

使用书签窗口中的“下一书签”和“上一书签”按钮，可以切换浏览不同书签。

选择书签窗口中的“新建文件夹”，然后将选定书签拖入新文件夹，可以将书签整理存放到虚拟文件夹中。

选择书签窗口中的“禁用所有书签”按钮，可以关闭书签（但不会删除书签）。 选择同一按钮（现在称为“启用所有书签”），可以重新启用书签。

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../ide/writing-code-in-the-code-and-text-editor.md)
