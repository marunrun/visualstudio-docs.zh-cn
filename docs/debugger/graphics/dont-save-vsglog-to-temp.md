---
title: DONT_SAVE_VSGLOG_TO_TEMP | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: f27ab0e6-9575-4ca0-9901-37d3e5c3a2f5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 40f3c3c22de6b4b0ebdbdf2dfc953f4cb1c9b5e6
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72736080"
---
# <a name="dont_save_vsglog_to_temp"></a>DONT_SAVE_VSGLOG_TO_TEMP
通过其存在定义图形日志文件是否保存到用户的临时文件目录。

## <a name="syntax"></a>语法

```C++
#define DONT_SAVE_VSGLOG_TO_TEMP
```

## <a name="value"></a>“值”
 一个预处理器符号，根据其是否存在来确定是否将图形日志文件保存到用户的临时文件目录中。 如果定义了此符号，则 `VSG_DEFAULT_RUN_FILENAME` 定义的文件名相对于捕获的应用的当前目录，或为绝对路径；否则，`VSG_DEFAULT_RUN_FILENAME` 定义的文件名相对于用户的临时文件目录，且不能是绝对路径。

## <a name="remarks"></a>备注
 根据用户权限的不同，可能无法将图形日志文件保存到任意位置。 如果不确定用户是否可以写入到你选择的位置，建议你最好将图形日志保存到用户的临时文件目录或其他已知良好的位置。

 若要防止将图形日志文件保存到临时文件目录，必须在包含 `vsgcapture.h` 之前定义 `DONT_SAVE_VSGLOG_TO_TEMP`。

## <a name="example"></a>示例
 此示例展示如何将图形日志文件保存到主机计算机上的绝对路径。

```cpp
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h
#define DONT_SAVE_VSGLOG_TO_TEMP
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"

#include <vsgcapture.h>
```

## <a name="see-also"></a>请参阅
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
