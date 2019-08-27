---
title: 控制台 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e825ba66-1383-46ad-8712-396bc9c14036
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 74a5cecbdf3bba942c888a5cde3d49236047f4ee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62553183"
---
# <a name="console"></a>控制台
VSPerfCmd.exe“Console”选项在新的命令提示符窗口中启动指定的应用程序。 “Console”只能与 VSPerfCmd“Launch”选项一起使用。 如果应用程序不是命令行应用程序，“Console”不起作用。

## <a name="syntax"></a>语法

```cmd
VSPerfCmd.exe /Launch:AppName /Console
```

#### <a name="parameters"></a>参数
 None

## <a name="required-options"></a>必需选项
 只能在同时包含“Launch”选项的命令行上指定“Console”。

 **Launch:**`AppName` 启动探查器以及由 `AppName` 指定的应用程序。

## <a name="see-also"></a>请参阅
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [分析独立应用程序](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [分析服务](../profiling/command-line-profiling-of-services.md)