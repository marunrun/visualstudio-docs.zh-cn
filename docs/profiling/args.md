---
title: 参数 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 20c35949-1f29-4282-ac75-4e6c237d71bc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 036b13a7fea5d64e23e2b7d5ccbd8a7b17f91176
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62777045"
---
# <a name="args"></a>参数
VSPerfCmd.exe **参数**选项指定传递给 **Launch** 子命令的目标应用程序的参数列表。

 只有在命令行上还指定了 **Launch** 时才可使用**参数**。 指定 **Launch** 时，**参数**为可选。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Launch:AppName /Args:Arguments [Options]
```

#### <a name="parameters"></a>参数
 `Arguments` Launch 命令的目标应用程序的参数列表。

## <a name="required-options"></a>必需选项
 **Launch:**`AppName` 启动指定的应用程序并开始使用采样方法进行分析。

## <a name="example"></a>示例
 以下示例使用**参数**选项将参数传递给 TestApp.exe。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp
VSPerfCmd.exe /Launch:TestApp.exe /Args:"123, 'Hello World'"
```

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)