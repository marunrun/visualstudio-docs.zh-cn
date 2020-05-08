---
title: AddMessage | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 102a0404-a00c-4566-93f3-01bc8df63280
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 41a71a69c916bf2fff30b2dee8784d5d9997436b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62896349"
---
# <a name="addmessage"></a>AddMessage
将自定义消息添加到图形诊断 HUD（提醒显示）  。

## <a name="syntax"></a>语法

```C++
void AddMessage(
  wchar_t const * szMessage
);
```

#### <a name="parameters"></a>参数
 `szMessage` 要添加到 HUD 的消息。

## <a name="remarks"></a>备注
 图像诊断 HUD 显示在正在图形诊断下运行的应用的左上角。 它显示有关此应用和图形信息捕获的信息以及通过调用此函数添加的消息。

 若要将消息添加到 HUD，不必主动捕获图形信息 - 也就是说，消息可通过 `VsgDbg` 类的实例添加，但首先不要调用 [Init](init.md) 成员函数。 消息只显示在 HUD 中，而不会记录在图形日志文件中。