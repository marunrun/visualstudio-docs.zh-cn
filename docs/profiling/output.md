---
title: Output | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 5e286e61-4548-42cf-a635-e608c5edbe2b
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 78d5b39908bc0ffa39533c22ea4effcbe97397b7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62794212"
---
# <a name="output"></a>Output
“Output”选项指定用于性能会话的分析数据文件的名称。 “Output”必须与“Start”选项配合使用。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Start:Method /Output:FileName [Options]
```

#### <a name="parameters"></a>参数
 `FileName` 数据文件的名称。 接受完整和部分路径。 如果未指定路径，则在当前目录中创建该文件。

## <a name="required-options"></a>必需选项
 “Output”选项必须与“Start”选项一起使用。

 **Start：**`Method` 指定输出文件名。

## <a name="example"></a>示例
 在下例中，分析数据文件是在当前目录中创建的。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)