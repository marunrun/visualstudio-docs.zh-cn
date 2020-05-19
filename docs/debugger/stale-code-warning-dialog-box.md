---
title: “陈旧代码警告”对话框 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.ENC.stalecode
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Stale Code Warning dialog box
- code, stale code warning
- warnings, Stale Code Warning dialog box
- Edit and Continue, stale code
ms.assetid: 594b894c-e652-4e13-a980-9909473d5712
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dba38e5b5d9f7a2be710cad58d6f2297dd03a412
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729547"
---
# <a name="stale-code-warning-dialog-box"></a>“陈旧代码警告”对话框

当“编辑并继续”操作未能立即应用对本机代码所做的更改时，将显示此对话框。 因此，当前堆栈帧中的某些本机代码是过时的、陈旧的。 有关详细信息，请参阅[编辑并继续(C++)](edit-and-continue-visual-cpp.md)。

**不再显示此对话框**

如果选中此复选框，则“编辑并继续”以后将在不要求权限的情况下应用代码更改。 可以通过转到“选项”对话框，打开“调试”文件夹，单击“编辑并继续”页，然后选择“就陈旧的代码发出警告”来再次启用此警告。

## <a name="see-also"></a>请参阅

- [受支持的代码更改 (C++)](supported-code-changes-cpp.md)
- [“选项”对话框 ->“调试”->“编辑并继续”](edit-and-continue.md)