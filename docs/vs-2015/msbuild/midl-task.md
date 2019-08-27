---
title: MIDL 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCMidlTool.ServerStubFile
- VC.Project.VCMidlTool.ApplicationConfigurationMode
- VC.Project.VCMidlTool.GenerateServerFiles
- VC.Project.VCMidlTool.ClientStubFile
- VC.Project.VCMidlTool.LocaleID
- VC.Project.VCMidlTool.GenerateClientFiles
- VC.Project.VCMidlTool.SuppressCompilerWarnings
- VC.Project.VCMidlTool.TypeLibFormat
- vc.task.midl
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (Visual C++), MIDL task
- MIDL task (MSBuild (Visual C++))
ms.assetid: 727efa8c-3336-40b8-8bef-ae6cbd77a422
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c1404ae5fce31eb59d2bb484ce1d97956f4cfefc
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68191563"
---
# <a name="midl-task"></a>MIDL 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包装 Microsoft 接口定义语言 (MIDL) 编译器工具 midl.exe。 有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上的“MIDL 命令行参考”。  
  
## <a name="parameters"></a>参数  
 下表描述了 **MIDL** 任务的参数。 大多数任务参数和若干组参数都对应于命令行选项。  
  
- **AdditionalIncludeDirectories**  
  
     可选 **String []** 参数。  
  
     将目录添加目录列表中，用于搜索导入的 IDL 文件，包含的头文件和应用程序配置文件 (ACF)。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/I** 选项。  
  
- **AdditionalOptions**  
  
     可选 **String** 参数。  
  
     命令行选项列表。 例如， **"** _/option1 /option2 /option#_ "。 使用此参数可指定未由任何其他 MIDL 任务参数表示的命令行选项。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上的“MIDL 命令行参考”。  
  
- **ApplicationConfigurationMode**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则表示允许在 IDL 文件中使用某些 ACF 关键字。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/app_config** 选项。  
  
- **ClientStubFile**  
  
     可选 **String** 参数。  
  
     指定 RPC 接口的客户端存根文件的名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/cstub** 选项。 另请参阅此表格中的 **ServerStubFile** 参数。  
  
- **CPreprocessOptions**  
  
     可选 **String** 参数。  
  
     指定要传递给 C/C++ 预处理器的选项。 指定用空格分隔的预处理器选项列表。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/cpp_opt** 选项。  
  
- **DefaultCharType**  
  
     可选 **String** 参数。  
  
     指定 C 编译器将用来编译生成代码的默认字符类型。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**Signed**|**/char signed**|  
    |**Unsigned**|**/char unsigned**|  
    |**Ascii**|**/char ascii7**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/char** 选项。  
  
- **DllDataFileName**  
  
     可选 **String** 参数。  
  
     指定代理 DLL 的生成的 *dlldata* 文件的文件名。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/dlldata** 选项。  
  
- **EnableErrorChecks**  
  
     可选 **String** 参数。  
  
     指定生成的存根在运行时将执行的错误检查类型。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**无**|**/error none**|  
    |**EnableCustom**|**/error**|  
    |**All**|**/error all**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/error** 选项。  
  
- **ErrorCheckAllocations**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则检查内存不足错误。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/error allocation** 选项。  
  
- **ErrorCheckBounds**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则根据传输长度规范检查变化符合数组和变化数组的大小。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/error bounds_check** 选项。  
  
- **ErrorCheckEnumRange**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则检查枚举值是否在允许的范围内。  
  
     有关详细信息，请参阅 midl.exe 命令行帮助 ( **/?** ) 中的 **/error enum** 选项。  
  
- **ErrorCheckRefPointers**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则检查没有任何空引用指针传递到客户端存根。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/error ref** 选项。  
  
- **ErrorCheckStubData**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则生成一个在服务器端捕获拆收处理异常的存根，并将这些异常传回客户端。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/error stub_data** 选项。  
  
- **GenerateClientFiles**  
  
     可选 **String** 参数。  
  
     指定编译器是否为 RPC 接口生成客户端 C 源文件。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**无**|**/client none**|  
    |**Stub**|**/client stub**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/client** 选项。  
  
- **GenerateServerFiles**  
  
     可选 **String** 参数。  
  
     指定编译器是否为 RPC 接口生成服务器端 C 源文件。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**无**|**/server none**|  
    |**Stub**|**/server stub**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/server** 选项。  
  
- **GenerateStublessProxies**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则为对象接口生成完全解析存根以及无存根代理。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/Oicf** 选项。  
  
- **GenerateTypeLibrary**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则不会生成类型库 (.tlb) 文件。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/notlb** 选项。  
  
- **HeaderFileName**  
  
     可选 **String** 参数。  
  
     指定所生成的头文件的名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/h** 或 **/header** 选项。  
  
- **IgnoreStandardIncludePath**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则 MIDL 任务只搜索使用 **additionalincludedirectories** 开关指定的目录，并忽略当前目录和 INCLUDE 环境变量指定的目录。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/no_def_idir** 选项。  
  
- **InterfaceIdentifierFileName**  
  
     可选 **String** 参数。  
  
     指定 COM 接口的*接口标识符文件*的名称。 这会覆盖通过将“_i.c”添加到 IDL 文件名所获取的默认名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/iid** 选项。  
  
- **LocaleID**  
  
     可选 **int** 参数。  
  
     指定在输入文件、文件名和目录路径中启用国际字符的*区域设置标识符*。 指定十进制区域设置标识符。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/lcid** 选项。 另请参阅 MSDN 上的“Microsoft 分配的区域设置 ID”。  
  
- **MkTypLibCompatible**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则要求输入文件的格式与 mktyplib.exe 版本 2.03 匹配。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/mktyplib203** 选项。 另请参阅 MSDN 网站上的“ODL 文件语法”。  
  
- **OutputDirectory**  
  
     可选 **String** 参数。  
  
     指定 MIDL 任务编写输出文件的默认目录。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/out** 选项。  
  
- **PreprocessorDefinitions**  
  
     可选 **String []** 参数。  
  
     指定一个或多个*定义*，即要传递给 C 预处理器的名称和可选值，就如通过 `#define` 指令所指示那样。 每个定义的形式为 *name[=value]* 。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/D** 选项。 另请参阅此表中的 **UndefinePreprocessorDefinitions** 参数。  
  
- **ProxyFileName**  
  
     可选 **String** 参数。  
  
     指定 COM 接口的接口代理文件的名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/proxy** 选项。  
  
- **RedirectOutputAndErrors**  
  
     可选 **String** 参数。  
  
     将错误消息和警告等输出从标准输出重定向到指定的文件。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/o** 选项。  
  
- **ServerStubFile**  
  
     可选 **String** 参数。  
  
     指定 RPC 接口的服务器存根文件的名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/sstub** 选项。 另请参阅此表格中的 **ClientStubFile** 参数。  
  
- **Source**  
  
     必选 `ITaskItem[]` 参数。  
  
     指定用空格分隔的源文件列表。  
  
- **StructMemberAlignment**  
  
     可选 **String** 参数。  
  
     指定目标系统中结构的对齐方式（*封装级别*）。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**NotSet**|*\<none>*|  
    |**1**|**/Zp1**|  
    |**2**|**/Zp2**|  
    |**4**|**/Zp4**|  
    |**8**|**/Zp8**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/Zp** 选项。 **/Zp** 选项相当于 **/pack** 选项以及较早的 **/align** 选项。  
  
- **SuppressCompilerWarnings**  
  
     可选 **Boolean** 参数。  
  
     如果为 `true`，则禁止 MIDL 任务的警告消息。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/no_warn** 选项。  
  
- **SuppressStartupBanner**  
  
     可选 `Boolean` 参数。  
  
     如果为 `true`，则在任务开始时阻止显示版权和版本号消息。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/nologo** 选项。  
  
- **TargetEnvironment**  
  
     可选 **String** 参数。  
  
     指定应用程序运行的环境。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**NotSet**|*\<none>*|  
    |**Win32**|**/env win32**|  
    |**Itanium**|**/env ia64**|  
    |**X64**|**/env x64**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/env** 选项。  
  
- **TrackerLogDirectory**  
  
     可选 `String` 参数。  
  
     指定存储此任务跟踪日志的中间目录。  
  
- **TypeLibFormat**  
  
     可选 **String** 参数。  
  
     指定类型库文件的格式。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**NewFormat**|**/newtlb**|  
    |**OldFormat**|**/oldtlb**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/newtlb** 和 **/oldtlb** 选项。  
  
- **TypeLibraryName**  
  
     可选 **String** 参数。  
  
     指定类型库文件的名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/tlb** 选项。  
  
- **UndefinePreprocessorDefinitions**  
  
     可选 **String []** 参数。  
  
     通过将名称传递到 C 预处理器，删除任何之前的名称定义，就如通过 `#undefine` 所指示那样。 指定一个或多个以前定义的名称。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/U** 选项。 另请参阅此表中的 **PreprocessorDefinitions** 参数。  
  
- **ValidateAllParameters**  
  
     可选 `Boolean` 参数。  
  
     如果为 `true`，则生成用于在运行时执行完整性检查的其他错误检查信息。 如果为 `false`，则不会生成错误检查信息。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/robust** 和 **/no_robust** 选项。  
  
- **WarnAsError**  
  
     可选 `Boolean` 参数。  
  
     如果为 `true`，则将所有警告视为错误。  
  
     如果未指定 **WarningLevel** MIDL 任务参数，则将默认级别和级别 1 的警告视为错误。  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/WX** 选项。 另请参阅此表格中的 **WarningLevel** 参数。  
  
- **WarningLevel**  
  
     可选 **String** 参数。  
  
     指定要发出的警告的严重性（*警告等级*）。 若值为 0，则不发出任何警告。 否则，如果警告等级数小于或等于指定的值，将发出警告。  
  
     指定以下值之一，其中每个值对应于一个命令行选项。  
  
    |值|命令行选项|  
    |-----------|--------------------------|  
    |**0**|**/W0**|  
    |**1**|**/W1**|  
    |**2**|**/W2**|  
    |**3**|**/W3**|  
    |**4**|**/W4**|  
  
     有关详细信息，请参阅 [MSDN](http://go.microsoft.com/fwlink/?LinkId=737) 网站上“MIDL 命令行参考”中的 **/W** 选项。 另请参阅此表格中的 **WarnAsError** 参数。  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>另请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)
