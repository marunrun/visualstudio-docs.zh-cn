---
title: 更改 F1 帮助键
description: 介绍如何重新映射或删除 F1 键映射
ms.date: 08/20/2020
ms.topic: how-to
ms.custom: contperfq1
robots: noindex,nofollow
manager: jillfra
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: debf469248a8ec1906f3692c37835d9f96476f54
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88802289"
---
# <a name="change-the-f1-help-key-in-visual-studio"></a>在 Visual Studio 中更改 F1 帮助键

如果需要将 F1 键用于除 F1 帮助服务外的其他功能，或者你只是想禁用使用 F1 的帮助，可以删除或修改键映射。

> [!IMPORTANT]
> 如果是由于性能问题而需要禁用 F1 帮助，建议临时修改键映射，这样就可以测试 Visual Studio 更新中对 F1 帮助服务的改进。 在大多数情况下，可以通过 F1 轻松地从代码编辑器中打开语言关键字和 API 的参考页面，或者打开与 IDE 中的窗口或 UI 元素相关联的帮助页面。 如果禁用它，则会禁用它在 Visual Studio 中的所有功能。

禁用 F1 帮助的步骤：

1. 在 Visual Studio 中，选择“工具” > “选项”，然后在“环境”下，选择“键盘”。

1. 在“显示命令包含”文本框中，输入 Help.f1 以筛选命令的视图。

   ![禁用 F1 帮助](../not-in-toc/media/disable-f1-help-key.png)

1. 选择“删除”以删除键映射。

1. 选择“按快捷键”文本框。

1. 在键盘上，按下用于 F1 帮助的新键或键组合（如 Alt + F1），选择“分配”，然后选择“确定”。

有关设置键盘快捷方式的详细信息，请参阅[标识并自定义键盘快捷方式](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)。
