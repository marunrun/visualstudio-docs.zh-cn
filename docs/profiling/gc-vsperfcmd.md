---
title: GC (VSPerfCmd) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7c81e88b-a748-4cf5-a7a1-3429608e1b54
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: e14fef1cfdc2dfc5f0d737ac09a08d90ab1de309
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74776974"
---
# <a name="gc-vsperfcmd"></a>GC (VSPerfCmd)
“GC”  选项启用 .NET Framework 内存分配数据和对象生存期数据的收集。 “GC”  选项只能用于采样分析方法，且只能与“Launch”  选项一起使用。

 使用“GC”  选项时，不需要 VSPerfClrEnv /sampleon  命令。

 如果未指定任何参数，或者如果指定了 Allocation  参数，则只会收集 .NET Framework 内存分配数据。 如果指定了 Lifetime  参数，则会同时收集 .NET Framework 内存分配数据和 .NET Framework 对象生存期数据。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Launch:AppName /GC[:{Allocation|Lifetime}] [Options]
```

#### <a name="parameters"></a>参数
 **Allocation** 默认。 收集 .NET Framework 内存分配数据。

 **Lifetime** 同时收集 .NET Framework 内存分配数据和 .NET Framework 对象生存期数据。

## <a name="required-options"></a>必需选项
  “GC”选项只能与“Launch”  选项一起使用。

 **Launch:** `AppName` 启动指定的应用程序并开始使用采样方法进行分析。

## <a name="example"></a>示例
 以下示例启动一个应用程序，并收集 .NET Framework 内存分配数据。

```cmd
VSPerfCmd.exe /Launch:TestApp.exe /gc
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)
