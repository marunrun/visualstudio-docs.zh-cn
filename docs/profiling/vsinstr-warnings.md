---
title: VSInstr 警告 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- instrumentation, VSInstr tool
- warnings
- VSInstr tool
- warnings, VSInstr tool
- performance tools, VSInstr tool
ms.assetid: 47512bc9-a8e9-4628-883a-d9888edab786
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 259b4089e4a54dbde4cc8b30a3da2899ad37a85a
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73189295"
---
# <a name="vsinstr-warnings"></a>VSInstr 警告
下表列出了由 VSInstr.exe 工具发出的警告  。 可使用 NOWARN 选项及警告编号来禁止显示警告。

|警告编号|说明|
|--------------------|-----------------|
|**VSP1026**|不引用 MSCorLib 的库不支持覆盖率。 这通常是可移植库会遇到的情况。<br /><br />.NET Core 需要 [/EnableCodeCoverage](../test/vstest-console-options.md) 命令行选项。|
|**VSP2000**|内部错误。 无法获取此可执行文件的模块文件名。|
|**VSP2001**|\<程序集名称> 是强名称程序集。 必须先对其重新签名，然后才能执行它。<br /><br /> 当检测到签名程序集时，将发出此警告。 可使用 sn.exe 工具重新签名二进制，或暂时关闭强名称要求  。 有关详细信息，请参阅 [Sn.exe （强名称工具）](/dotnet/framework/tools/sn-exe-strong-name-tool)。|
|**VSP2002**|未能在文件 \<文件名> 中找到函数 \<函数名><br /><br /> 如果无法在指定文件中找到某个函数，将出现此警告。|
|**VSP2003**|未能在文件 \<文件名> 中找到任何指向函数 \<函数名> 的交叉跳转。<br /><br /> 如果 VSInstr 无法置空交叉跳转，将出现此警告。 交叉跳转用于代码优化。|
|**VSP2004**|已通过 EXCLUDE 命令行开关排除了函数 \<函数名>，但因为该函数包含交叉跳转，所以仍需要它。<br /><br /> 如果使用 EXCLUDE 选项排除了函数，但在检测过程中仍需要该函数，则将出现此警告。 探查器会自动包括所需的函数。|
|**VSP2005**|内部检测错误 \<错误文本><br /><br /> 如果无法执行检测，将发出此警告。 查看错误文本，确定是否可进行更正。|
|**VSP2006**|未能找到 \<名称> 的 PDB<br /><br /> 如果 PDB 文件在搜索路径上不存在，或不匹配二进制文件，则将出现此警告。|
|**VSP2007**|\<文件名> 不包含可检测的代码。<br /><br /> 如果二进制文件中所有函数都被排除，或如果指定的文件仅包含资源，则将发出此警告。|
|**VSP2008**|无法从 \<名称> 获取安全特性。 错误代码 \<代码><br /><br /> 如果用户没有 READ_DAC 权限，将出现此警告。 在检测过程中，探查器尝试保留二进制的原始 DACL。 由于原始二进制文件替换为了新的二进制文件，因此必须复制来自原始二进制文件的 DACL，并将其应用于新的二进制文件。 如果用户没有对原始二进制文件的 READ_DAC 访问权限，此操作可能失败。|
|**VSP2009**|无法在 \<名称> 上设置安全特性。 错误代码为 \<错误号><br /><br /> 如果用户没有 WRITE_DAC 权限，将出现此警告。 在检测过程中，探查器尝试保留二进制的原始 DACL。 由于原始二进制文件替换为了新的二进制文件，因此必须复制来自原始二进制文件的 DACL，并将其应用于新的二进制文件。 如果用户没有对新二进制文件的 WRITE_DAC 访问权限，此操作可能失败。|
|**VSP2010**|由于 -INCLUDE/-EXCLUDE 选项，没有专门为检测选择任何函数|
|**VSP2011**|Include/Exclude funcspec \<名称> 与任何函数都不匹配|
|**VSP2012**|该映像不包含任何可进行代码覆盖率检测的代码。<br /><br /> 探查器不检测以下类型的代码：<br /><br /> - 静态 CRT 函数<br />- 具有 NonUserCodeAttribute 特性的托管方法<br />- 具有 DebuggerHiddenAttribute 特性的托管方法<br />- MASM 块<br /><br /> 如果在此筛选后没有剩余代码，则将生成此警告。|
|**VSP2013**|检测此映像需要它以 32 位进程运行。 已更新了 CLR 标头标志以反映这一情况。<br /><br /> 探查器修改二进制文件，以便 64 位操作系统可以在 WOW64 仿真器中打开 32 位进程。 对于库 (DLL)，如果是在现有 64 位进程中加载这些库，则上述操作可能失败。 此警告会向用户通知依赖项。|
|**VSP2014**|检测后得到的映像似乎无效，可能无法运行。<br /><br /> 当最终检测程序集具有无效的 PE 头时，将出现此消息。|

## <a name="see-also"></a>请参阅
- [VSInstr](../profiling/vsinstr.md)