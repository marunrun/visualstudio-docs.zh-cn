---
title: WaitStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 6c737177-2dfb-4150-963e-a49ac9aaa591
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6307dcad45b7e2c8164aa892c4598d577e4ea464
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62998964"
---
# <a name="waitstart"></a>WaitStart
仅当探查器已初始化，或已超过指定秒数时，WaitStart 选项才使 VSPerfCmd.exe Start 子命令返回。 默认情况下，Start 命令将立即返回。 如果 Start 子命令在未初始化探查器的情况下就返回，则将返回一个错误。 如果未指定秒数，Start 命令将无限期等待。

 WaitStart 选项在批处理文件中十分有用，可确保探查器已经过初始化。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName[Options] /StartWait[:Seconds]
```

#### <a name="parameters"></a>参数
 `Seconds` 从 Start 子命令返回前要等待的秒数。

## <a name="required-options"></a>必需选项
 WaitStart 选项仅可与 Start 子命令一起使用。

 **输出：**`filename` 指定输出文件名。

## <a name="remarks"></a>备注

## <a name="example"></a>示例
 在此批处理示例中，Start 命令将等待 5 秒，探查器才会初始化。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /WaitStart:5
if not %errorlevel% 0 goto :error_tag
VSPerfCmd.exe /Launch:TestApp.exe
goto :end
:error_tag
@echo Could not start Profiler!
@echo Error %errorlevel%
:end
```