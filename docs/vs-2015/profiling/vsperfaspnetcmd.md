---
title: VSPerfASPNetCmd | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools,VSPerfASPNETCmd
- VSPerfASPNETCmd
ms.assetid: f9e9f895-57bb-41e8-8bd1-cdaa738ec220
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9cb81f17abd1e7891dc3f78a85d6d1276991f070
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68145277"
---
# <a name="vsperfaspnetcmd"></a>VSPerfASPNetCmd
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**VSPerfASPNetCmd.exe** 命令行使你无需设置环境变量或重新启动计算机，就能分析 ASP.NET 网站。 在分析 ASP.NET 网站时，使用 **VSPerfASPNetCmd.exe** 而非 [VSPerfCmd](../profiling/vsperfcmd.md)，并且无需使用 **VSPerCmd** 提供的其他功能。 有关 **VSPerfASPNetCmd**的详细信息，请参阅 [通过 VSPerfASPNetCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)。 **VSPerfASPNetCmd** 是使用独立探查器分析 ASP.NET 网站时要使用的首选命令行工具。  
  
## <a name="syntax"></a>语法  
 **vsperfaspnetcmd** [/*Options*] *Website*  
  
## <a name="options"></a>选项  
  
|选项|描述|  
|------------|-----------------|  
|**/Sample** 或 **/s**|使用采样方法分析网站。 **/Sample** 是默认方法。 /Sample 不能与 **/Trace** 一起使用。|  
|**/Trace** 或 **/t**|使用检测方法分析网站。 /Trace 不能与 **/Sample** 一起使用。|  
|**/Memory**[ **:** `Type`] 或 **/m**[ **:** {**a**&#124;**l**}]|分析内存分配，还可以选择分析对象生存期（垃圾回收）。 **/Memory** 可用于采样或检测方法。<br /><br /> *Type* 可以是下列类型之一：<br /><br /> -   **allocation**（或 **a**）只收集内存分配数据。<br />-   **lifetime**（或 **l**）同时收集内存分配数据和对象生存期数据。<br /><br /> 默认的 `Type` 是 **allocation**。|  
|**/Tip** 或 **/i**|将详细的 ASP.NET 请求和 ADO.NET 调用信息添加到分析数据。 **/Tip** 可用于采样或检测方法，还可与 **/Memory** 选项一起使用。|  
|**/Output:** `File` or   **/o:** `File`|指定分析数据 (.vsp) 文件的路径和文件名。|  
|**/NoWait** 或 **/n**|立即返回命令提示符，以便在命令提示符窗口中使用其他命令。 必须在单独的命令行上键入 **VSPerfASPNETCmd /Shutdown**，以关闭分析。|  
|**/PackSymbols**[:{**on**&#124;**off**} 或 **/p**[:{**on**&#124;**off**}|在分析数据 (.vsp) 文件中嵌入符号（函数和参数名称等）。|  
|**/Shutdown:** `Website`or   **/d:** `Website`|关闭分析。 在使用 **/NoWait** 选项启动分析后，或探查器意外结束时，在命令行上将其作为唯一选项使用。 指定与在原始 **VSPerfASPNETCmd** 命令中使用的 URL 相同的 URL。|  
|`Website`|要分析的网站的 URL。|  
  
## <a name="see-also"></a>另请参阅  
 [通过 VSPerfASPNETCmd 进行快速网站分析](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md)   
 [分析 ASP.NET Web 应用程序](../profiling/command-line-profiling-of-aspnet-web-applications.md)
