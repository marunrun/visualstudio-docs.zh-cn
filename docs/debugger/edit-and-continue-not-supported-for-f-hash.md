---
title: F# 不支持“编辑并继续”| Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Edit and Continue [F#]
- Debugging [F#], Edit and Continue
ms.assetid: 40ec77bb-07e3-4b58-9254-ae015009441c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ceb0ca767b1ac6364e103925fb86ed639c3d321d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62851164"
---
# <a name="edit-and-continue-not-supported-for-f"></a>F# 不支持“编辑并继续” #
在调试 F# 代码时不支持“编辑并继续”。 在调试会话期间编辑 F# 代码是可以的，但应避免这样做。 在调试会话期间不能应用代码更改。 因此，在调试期间对 F# 代码所做的任何编辑将导致源代码与正在调试的代码不匹配。
