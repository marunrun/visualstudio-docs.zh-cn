---
title: VSPerfASPNetCmd | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
ms.assetid: f9e9f895-57bb-41e8-8bd1-cdaa738ec220
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8c9bf465b4da7f305e97a18099a7e27db8eab6b4
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2019
ms.locfileid: "74778006"
---
# <a name="vsperfaspnetcmd"></a>VSPerfASPNetCmd
通过 VSPerfASPNetCmd.exe  命令行，无需设置环境变量或重启计算机即可分析 ASP.NET 网站。 在分析 ASP.NET 网站时，使用 VSPerfASPNetCmd.exe  而非 [VSPerfCmd](../profiling/vsperfcmd.md)，并且无需使用 VSPerfCmd  提供的其他功能。 有关 VSPerfASPNetCmd  的详细信息，请参阅[使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)。 VSPerfASPNetCmd  是使用独立探查器分析 ASP.NET 网站时的首选命令行工具。

## <a name="syntax"></a>语法
 **vsperfaspnetcmd** [/*Options*] *Website*

## <a name="options"></a>选项

|选项|说明|
|------------|-----------------|
|**/Sample** 或 **/s**|使用采样方法分析网站。 **/Sample** 是默认方法。 /Sample 不能与 **/Trace** 一起使用。|
|**/Trace** 或 **/t**|使用检测方法分析网站。 /Trace 不能与 **/Sample** 一起使用。|
|**/Memory**[ **:** `Type`] 或 **/m**[ **:** {**a**&#124;**l**}]|分析内存分配，还可以选择分析对象生存期（垃圾回收）。 **/Memory** 可用于采样或检测方法。<br /><br /> *Type* 可以是下列类型之一：<br /><br /> -   **allocation**（或 **a**）只收集内存分配数据。<br />-   **lifetime**（或 **l**）同时收集内存分配数据和对象生存期数据。<br /><br /> 默认的 `Type` 是 **allocation**。|
|**/Tip** 或 **/i**|将详细的 ASP.NET 请求和 ADO.NET 调用信息添加到分析数据。 **/Tip** 可用于采样或检测方法，还可与 **/Memory** 选项一起使用。|
|**/Output:** `File` 或 **/o:** `File`|指定分析数据 (.vsp) 文件的路径和文件名  。|
|**/NoWait** 或 **/n**|立即返回命令提示符，以便在命令提示符窗口中使用其他命令。 必须在单独的命令行上键入 **VSPerfASPNETCmd /Shutdown**，以关闭分析。|
|**/PackSymbols**[:{**on**&#124;**off**} 或 **/p**[:{**on**&#124;**off**}|在分析数据 (.vsp) 文件中嵌入符号（函数和参数名称等）  。|
|**/Shutdown:** `Website` 或 **/d:** `Website`|关闭分析。 在使用 **/NoWait** 选项启动分析后，或探查器意外结束时，在命令行上将其作为唯一选项使用。 指定与在原始 **VSPerfASPNETCmd** 命令中使用的 URL 相同的 URL。|
|`Website`|要分析的网站的 URL。|

## <a name="see-also"></a>请参阅
- [使用 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)
- [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
