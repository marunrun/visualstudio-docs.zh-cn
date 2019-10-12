---
title: Clang 链接器属性 (Android C++)| Microsoft Docs
ms.custom: ''
ms.date: 10/23/2017
ms.technology: vs-ide-mobile
ms.topic: conceptual
ms.assetid: 66e88848-116c-4eb0-bc57-183394d35b57
author: corob-msft
ms.author: corob
manager: jillfra
f1_keywords:
- VC.Project.VCLinkerTool.OutputFile
- VC.Project.VCLinkerTool.ShowProgress
- VC.Project.VCLinkerTool.Version
- VC.Project.VCLinkerTool.VerboseOutput
- VC.Project.VCLinkerTool.IncrementalLink
- VC.Project.VCLinkerTool.SharedLibrarySearchPath
- VC.Project.VCLinkerTool.AdditionalLibraryDirectories
- VC.Project.VCLinkerTool.UnresolvedReferences
- VC.Project.VCLinkerTool.OptimizeForMemory
- VC.Project.VCLinkerTool.IgnoreDefaultLibraryNames
- VC.Project.VCLinkerTool.ForceSymbolReferences
- VC.Project.VCLinkerTool.ForceFileOutput
- VC.Project.VCLinkerTool.OmitDebuggerSymbolInformation
- VC.Project.VCLinkerTool.GenerateMapFile
- VC.Project.VCLinkerTool.Relocation
- VC.Project.VCLinkerTool.FunctionBinding
- VC.Project.VCLinkerTool.NoExecStackRequired
- VC.Project.WholeArchive
- VC.Project.AdditionalOptionsPage
- VC.Project.VCLinkerTool.AdditionalDependencies
- VC.Project.VCLinkerTool.LibraryDependencies
ms.workload:
- xplat-cplusplus
ms.openlocfilehash: e8f138b6c496f9dec32ad44dbdfa2064dd639990
ms.sourcegitcommit: 6ae0a289f1654dec63b412bfa22035511a2ef5ad
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71950680"
---
# <a name="clang-linker-properties-android-c"></a>Clang 链接器属性 (Android C++)

Property | 说明 | 选项
--- | ---| ---
输出文件 | 该选项可重写链接器创建的程序的默认名称和位置。 (-o)
显示进度 | 打印链接器进度消息。
Version | -version 选项让链接器将版本号置于可执行文件的标头中。
启用详细输出 | -verbose 选项通知链接器输出调试的详细消息。
启用增量链接 | 此选项通知链接器启用增量链接。
共享库搜索路径 | 允许用户填入共享库搜索路径。
附加库目录 | 允许用户重写环境库路径。 （-L 文件夹）。
报告未解析的符号引用 | 启用此选项将报告未解析的符号引用。
优化内存使用率 | 如有必要，通过重读符号表优化内存使用率。
忽略特定默认库 | 指定一个或多个要忽略的默认库的名称。
强制符号引用 | 强制将符号作为未定义符号输入到输出文件中。
调试器符号信息 | 输出文件中的调试程序符号信息。 | 全部包含 <br>忽略不需要的符号以进行重定位处理 <br>仅忽略调试器符号信息 <br>忽略所有符号信息 <br>
打包调试器符号信息 | 在打包之前剥离调试器符号信息。  使用原始二进制文件的副本进行调试。
映射文件名 | “映射”选项通知链接器使用用户指定的名称创建映射文件。
重定位之后将变量标记为只读 | 此选项在重定位之后将变量标记为只读。
启用即时函数绑定 | 此选项标记用于即时函数绑定的对象。
需要可执行堆栈 | 此选项将输出标记为不需要可执行堆栈。
整个存档 | 整个存档使用来自源和其他依赖项的所有代码。
附加选项 | 附加选项。
附加依赖项 | 指定要添加到链接命令行的附加项。
库依赖项 | 此选项可指定要添加到链接器命令行的附加库。 附加库会添加到链接器命令行末尾，并以“lib”  开头，以“.a”  或“.so”  扩展名结尾。  (-lFILE)
