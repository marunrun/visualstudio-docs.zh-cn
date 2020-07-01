---
title: 自动换行
ms.date: 11/07/2018
ms.topic: how-to
helpviewer_keywords:
- word wrap
- editors, text viewing
- Code Editor, word wrap
ms.assetid: 442f33ef-9f52-4515-b55f-fb816d664645
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c4bf76643ce1ea6e2f449c54fbc31d441418becf
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770329"
---
# <a name="how-to-manage-word-wrap-in-the-editor"></a>如何：在编辑器中管理自动换行

可以设置和清除“自动换行”选项  。 如果设置了此选项，较长行中超出代码编辑器窗口当前宽度的部分将在下一行显示。 如果清除了此选项，例如，为方便使用行号，则可以向右滚动查看较长行的末尾。

> [!NOTE]
> 本主题适用于 Visual Studio  Windows 版。 有关 Visual Studio for Mac，请参阅[源编辑器：自动换行](/visualstudio/mac/source-editor#word-wrap)。

## <a name="to-set-word-wrap-preferences"></a>设置换行首选项

1. 在“工具”菜单上选择“选项”   。

2. 在“文本编辑器”文件夹的“所有语言”子文件夹中选择“常规”选项，在全局设置此选项    。

     — 或 —

     在编程所用的语言的子文件夹中选择“常规”选项  。

3. 在“设置”下，选择或清除“自动换行”选项   。

     选中“自动换行”选项将启用“显示可视的自动换行标志符号”选项   。

4. 如果希望在较长行换行到下一行的位置处显示回车箭头指示符，请选择“显示可视的自动换行标志符号”选项  。 如果不希望显示这些指示箭头，则清除此复选框。

    > [!NOTE]
    > 这些提醒箭头不会添加到代码中，它们仅用于显示。

## <a name="known-issues"></a>已知问题

如果熟悉 Notepad++、Sublime Text 或 Visual Studio Code 中的自动换行功能，请注意 Visual Studio 的行为在以下方面与其他编辑器的行为不同：

* [三次单击不会选择整行](https://developercommunity.visualstudio.com/content/problem/268989/triple-click-doesnt-select-whole-line-when-word-wr.html)
* [按两次 End 键不会将光标移动到行尾](https://developercommunity.visualstudio.com/content/problem/138274/pressing-end-key-twice-should-move-cursor-to-end-o.html)

## <a name="see-also"></a>请参阅

- [代码编辑器功能](../../ide/writing-code-in-the-code-and-text-editor.md)
