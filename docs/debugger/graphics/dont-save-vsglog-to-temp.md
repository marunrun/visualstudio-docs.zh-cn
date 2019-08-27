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
ms.openlocfilehash: 501a054ddb1d3ab20a10f99bb30a0c3439004eb3
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62848689"
---
# <a name="dontsavevsglogtotemp"></a>DONT_SAVE_VSGLOG_TO_TEMP
通过其存在定义图形日志文件是否保存到用户的临时文件目录。

## <a name="syntax"></a>语法

```C++
#define DONT_SAVE_VSGLOG_TO_TEMP
```

## <a name="value"></a>“值”
 预处理器符号，其存在情况确定是否图形日志文件保存到用户的临时文件目录。 如果定义此符号，则由定义的文件的名称`VSG_DEFAULT_RUN_FILENAME`是捕获应用程序的当前目录的相对或绝对路径; 否则为的文件的名称定义`VSG_DEFAULT_RUN_FILENAME`是相对于用户的临时文件目录，不能为绝对路径。

## <a name="remarks"></a>备注
 具体取决于用户的权限，图形日志文件可能不能保存在任意位置。 我们建议您希望在将图形日志保存到用户的临时文件目录或其他已知的正确位置，如果您不确定是否将选择的位置可以写入到用户。

 若要防止图形日志文件保存到临时文件目录，必须定义`DONT_SAVE_VSGLOG_TO_TEMP`包含之前`vsgcapture.h`。

## <a name="example"></a>示例
 此示例演示如何在主机上将图形日志文件保存到的绝对路径。

```cpp
// Define DONT_SAVE_VSGLOG_TO_TEMP and VSG_DEFAULT_RUN_FILENAME before including vsgcapture.h
#define DONT_SAVE_VSGLOG_TO_TEMP
#define VSG_DEFAULT_RUN_FILENAME L"C:\\Graphics Diagnostics Captures\\default.vsglog"

#include <vsgcapture.h>
```

## <a name="see-also"></a>请参阅
- [VSG_DEFAULT_RUN_FILENAME](vsg-default-run-filename.md)
