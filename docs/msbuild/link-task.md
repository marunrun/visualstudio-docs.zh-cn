---
title: Link 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- VC.Project.VCLinkerTool.ForceFileOutput
- VC.Project.VCLinkerTool.LinkStatus
- VC.Project.VCLinkerTool.CLRUnmanagedCodeCheck
- VC.Project.VCLinkerTool.SpecifySectionAttributes
- VC.Project.VCLinkerTool.SupportNobindOfDelayLoadedDLL
- VC.Project.VCLinkerTool.MinimumRequiredVersion
- VC.Project.VCLinkerTool.PerUserRedirection
- VC.Project.VCLinkerTool.CreateHotPatchableImage
- VC.Project.VCLinkerTool.DataExecutionPrevention
- VC.Project.VCLinkerTool.TreatLinkerWarningsAsErrors
- vc.task.link
- VC.Project.VCLinkerTool.ImageHasSafeExceptionHandlers
- VC.Project.VCLinkerTool.CLRSupportLastError
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (C++), Link task
- Link task (MSBuild (C++))
ms.assetid: 0a61f168-3113-4fa7-83a3-d9142e2a33f8
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 31bad6dfd0c336e4535e446d1167cb9fd6874972
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592199"
---
# <a name="link-task"></a>Link 任务
包装 Microsoft C++ 链接器工具，link.exe  。 链接器工具将通用对象文件格式 (COFF) 对象文件和库链接起来，以创建可执行 (.exe) 文件或动态链接库 (DLL)  。 有关详细信息，请参阅[链接器选项](/cpp/build/reference/linker-options)。

## <a name="parameters"></a>参数
 下表描述了 Link 任务的参数  。 大多数任务参数和若干组参数都对应于命令行选项。

- **AdditionalDependencies**

  可选 **String []** 参数。

  指定要添加到命令的输入文件的列表。

  有关详细信息，请参阅 [LINK 输入文件](/cpp/build/reference/link-input-files)。

- **AdditionalLibraryDirectories**

  可选 **String []** 参数。

  重写环境库路径。 指定目录名。

  有关详细信息，请参阅 [/LIBPATH（附加的 Libpath）](/cpp/build/reference/libpath-additional-libpath)。

- **AdditionalManifestDependencies**

  可选 **String []** 参数。

  指定将放入清单文件的 `dependency` 节的属性。

  有关详细信息，请参阅 [/MANIFESTDEPENDENCY（指定清单依赖项）](/cpp/build/reference/manifestdependency-specify-manifest-dependencies)。 另请参阅 [Publisher configuration files（发布服务器配置文件）](/windows/desktop/SbsCs/publisher-configuration-files)。

- **AdditionalOptions**

  可选 **String** 参数。

  在命令行上指定的链接器选项列表。 例如，/\<option1> /\<option2> /\<option#>。 使用此参数可指定未由任何其他 **Link** 任务参数表示的链接器选项。

  有关详细信息，请参阅[链接器选项](/cpp/build/reference/linker-options)。

- **AddModuleNamesToAssembly**

  可选 **String []** 参数。

  向程序集添加模块引用。

  有关详细信息，请参阅 [/ASSEMBLYMODULE（向程序集添加 MSIL 模块）](/cpp/build/reference/assemblymodule-add-a-msil-module-to-the-assembly)。

- **AllowIsolation**

  可选 **Boolean** 参数。

  如果为 `true`，则将导致操作系统进行清单查找和加载。 如果为 `false`，则指示将加载 DLL，仿佛没有清单一样。

  有关详细信息，请参阅 [/ALLOWISOLATION（清单查找）](/cpp/build/reference/allowisolation-manifest-lookup)。

- **AssemblyDebug**

  可选 **Boolean** 参数。

  如果为 `true`，则发出 **DebuggableAttribute** 属性以及调试信息跟踪，并禁用 JIT 优化。 如果为 `false`，则发出 **DebuggableAttribute** 属性，但禁用调试信息跟踪，启用 JIT 优化。

  有关详细信息，请参阅 [/ASSEMBLYDEBUG（添加 DebuggableAttribute）](/cpp/build/reference/assemblydebug-add-debuggableattribute)。

- **AssemblyLinkResource**

  可选 **String []** 参数。

  创建指向输出文件中的 .NET Framework 资源的链接；资源文件不会放入输出文件中。 指定资源的名称。

  有关详细信息，请参阅 [/ASSEMBLYLINKRESOURCE（链接到 .NET Framework 资源）](/cpp/build/reference/assemblylinkresource-link-to-dotnet-framework-resource)。

- **AttributeFileTracking**

  隐式 **Boolean** 参数。

  启用更深层次的文件跟踪，以捕获链接增量的行为。 始终返回 `true`。

- **BaseAddress**

  可选 **String** 参数。

  为正在生成的程序或 DLL 设置基址。 指定 `{address[,size] | @filename,key}`。

  有关详细信息，请参阅 [/BASE（基址）](/cpp/build/reference/base-base-address)。

- **BuildingInIDE**

  可选 **Boolean** 参数。

  如果为 true，则指示 MSBuild 是从 IDE 调用的。 否则指示 MSBuild 是从命令行调用的。

  此参数没有等效的链接器选项。

- **CLRImageType**

  可选 **String** 参数。

  设置公共语言运行时 (CLR) 映像的类型。

  指定以下值之一，其中每个值对应于一个链接器选项。

  - **Default** -  *\<none>*

  - **ForceIJWImage** -  **/CLRIMAGETYPE:IJW**

  - **ForcePureILImage** -  **/CLRIMAGETYPE:PURE**

  - **ForceSafeILImage** -  **/CLRIMAGETYPE:SAFE**

  有关详细信息，请参阅 [/CLRIMAGETYPE（指定 CLR 映像的类型）](/cpp/build/reference/clrimagetype-specify-type-of-clr-image)。

- **CLRSupportLastError**

  可选 **String** 参数。

  保留通过 P/Invoke 机制调用的函数的上一个错误代码。

  指定以下值之一，其中每个值对应于一个链接器选项。

  - **Enabled** -  **/CLRSupportLastError**

  - **Disabled** -  **/CLRSupportLastError:NO**

  - **SystemDlls** -  **/CLRSupportLastError:SYSTEMDLL**

  有关详细信息，请参阅 [/CLRSUPPORTLASTERROR（为 PInvoke 调用保留上次的错误代码）](/cpp/build/reference/clrsupportlasterror-preserve-last-error-code-for-pinvoke-calls)。

- **CLRThreadAttribute**

  可选 **String** 参数。

  显式指定用于 CLR 程序入口点的线程特性。

  指定以下值之一，其中每个值对应于一个链接器选项。

  - **DefaultThreadingAttribute** -  **/CLRTHREADATTRIBUTE:NONE**

  - **MTAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:MTA**

  - **STAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:STA**

  有关详细信息，请参阅 [/CLRTHREADATTRIBUTE（设置 CLR 线程特性）](/cpp/build/reference/clrthreadattribute-set-clr-thread-attribute)。

- **CLRUnmanagedCodeCheck**

  可选 **Boolean** 参数。

  指定链接器是否将 **SuppressUnmanagedCodeSecurityAttribute** 应用到链接器生成的从托管代码到本机 DLL 的 P/Invoke 调用。

  有关详细信息，请参阅 [/CLRUNMANAGEDCODECHECK（添加 SuppressUnmanagedCodeSecurityAttribute）](/cpp/build/reference/clrunmanagedcodecheck-add-suppressunmanagedcodesecurityattribute)。

- **CreateHotPatchableImage**

  可选 **String** 参数。

  准备映像以进行热修补。

  指定以下值之一，它对应于一个链接器选项。

  - **Enabled** -  **/FUNCTIONPADMIN**

  - **X86Image** -  **/FUNCTIONPADMIN:5**

  - **X64Image** -  **/FUNCTIONPADMIN:6**

  - **ItaniumImage** -  **/FUNCTIONPADMIN:16**

  有关详细信息，请参阅 [/FUNCTIONPADMIN（创建可热修补的映像）](/cpp/build/reference/functionpadmin-create-hotpatchable-image)。

- **DataExecutionPrevention**

  可选 **Boolean** 参数。

  如果为 `true`，则指示可执行文件已经就是否与 Windows 数据执行保护功能兼容进行了测试。

  有关详细信息，请参阅 [/NXCOMPAT（与数据执行保护兼容）](/cpp/build/reference/nxcompat-compatible-with-data-execution-prevention)。

- **DelayLoadDLLs**

  可选 **String []** 参数。

  此参数导致 DLL *延迟加载*。 指定要延迟加载的 DLL 的名称。

  有关详细信息，请参阅 [/DELAYLOAD（延迟加载导入）](/cpp/build/reference/delayload-delay-load-import)。

- **DelaySign**

  可选 **Boolean** 参数。

  如果为 `true`，则对程序集进行部分签名。 默认情况下，该值为 `false`。

  有关详细信息，请参阅 [/DELAYSIGN（对程序集进行部分签名）](/cpp/build/reference/delaysign-partially-sign-an-assembly)。

- **Driver**

  可选 **String** 参数。

  指定此参数以生成 Windows NT 内核模式驱动程序。

  指定以下值之一，其中每个值对应于一个链接器选项。

  - **NotSet** -  *\<none>*

  - **Driver** -  **/Driver**

  - **UpOnly** -  **/DRIVER:UPONLY**

  - **WDM** -  **/DRIVER:WDM**

  有关详细信息，请参阅 [/DRIVER（Windows NT 内核模式驱动程序）](/cpp/build/reference/driver-windows-nt-kernel-mode-driver)。

- **EmbedManagedResourceFile**

  可选 **String []** 参数。

  将资源文件嵌入程序集。 指定所需的资源文件名。 （可选）指定用于加载资源的逻辑名称，和指示在程序集清单中该资源文件为私有的 **PRIVATE** 选项。

  有关详细信息，请参阅 [/ASSEMBLYRESOURCE（嵌入托管资源）](/cpp/build/reference/assemblyresource-embed-a-managed-resource)。

- **EnableCOMDATFolding**

  可选 **Boolean** 参数。

  如果为 `true`，则启用相同的 COMDAT 折叠。

  有关详细信息，请参阅 [/OPT（优化）](/cpp/build/reference/opt-optimizations)的 `ICF[= iterations]` 参数。

- **EnableUAC**

  可选 **Boolean** 参数。

  如果为 `true`，则指定将用户帐户控制 (UAC) 信息嵌入到程序清单中。

  有关详细信息，请参阅 [/MANIFESTUAC（将 UAC 信息嵌入到清单中）](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest)。

- **EntryPointSymbol**

  可选 **String** 参数。

  将某个入口点函数指定为 .exe 文件或 DLL 的起始地址  。 将函数名称指定为参数值。

  有关详细信息，请参阅 [/ENTRY（入口点符号）](/cpp/build/reference/entry-entry-point-symbol)。

- **FixedBaseAddress**

  可选 **Boolean** 参数。

  如果为 `true`，则创建只能在其首选基址加载的程序或 DLL。

  有关详细信息，请参阅 [/FIXED（固定基址）](/cpp/build/reference/fixed-fixed-base-address)。

- **ForceFileOutput**

  可选 **String** 参数。

  告知链接器创建有效的 .exe 文件或 DLL，即使引用的符号未经定义或多次定义也是如此  。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **Enabled** -  **/FORCE**

  - **MultiplyDefinedSymbolOnly** -  **/FORCE:MULTIPLE**

  - **UndefinedSymbolOnly** -  **/FORCE:UNRESOLVED**

  有关详细信息，请参阅 [/FORCE（强制文件输出）](/cpp/build/reference/force-force-file-output)。

- **ForceSymbolReferences**

  可选 **String []** 参数。

  此参数告知链接器将指定的符号添加到符号表中。

  有关详细信息，请参阅 [/INCLUDE（强制符号引用）](/cpp/build/reference/include-force-symbol-references)。

- **FunctionOrder**

  可选 **String** 参数。

  此参数通过将指定的已打包函数 (COMDATs) 按预定顺序放置到映像中，来优化程序。

  有关详细信息，请参阅 [/ORDER（按顺序放置函数）](/cpp/build/reference/order-put-functions-in-order)。

- **GenerateDebugInformation**

  可选 **Boolean** 参数。

  如果为 `true`，则为 .exe 文件或 DLL 创建调试信息  。

  有关详细信息，请参阅 [/DEBUG（生成调试信息）](/cpp/build/reference/debug-generate-debug-info)。

- **GenerateManifest**

  可选 **Boolean** 参数。

  如果为 `true`，则创建并行清单文件。

  有关详细信息，请参阅 [/MANIFEST（创建并行程序集清单）](/cpp/build/reference/manifest-create-side-by-side-assembly-manifest)。

- **GenerateMapFile**

  可选 **Boolean** 参数。

  如果为 `true`，则创建*映射文件*。 映射文件的文件扩展名为 .map  。

  有关详细信息，请参阅 [/MAP（生成映射文件）](/cpp/build/reference/map-generate-mapfile)。

- **HeapCommitSize**

  可选 **String** 参数。

  指定在堆上一次性分配的物理内存量。

  有关详细信息，请参阅 [/HEAP（设置堆大小）](/cpp/build/reference/heap-set-heap-size)中的 `commit` 参数。 另请参阅 **HeapReserveSize** 参数。

- **HeapReserveSize**

  可选 **String** 参数。

  指定虚拟内存中的堆分配总量。

  有关详细信息，请参阅 [/HEAP（设置堆大小）](/cpp/build/reference/heap-set-heap-size)中的 `reserve` 参数。 另请参阅此表格中的 **HeapCommitSize** 参数。

- **IgnoreAllDefaultLibraries**

  可选 **Boolean** 参数。

  如果为 `true`，则告知链接器从其在解析外部引用时搜索的库列表中移除一个或多个默认库。

  有关详细信息，请参阅 [/NODEFAULTLIB（忽略库）](/cpp/build/reference/nodefaultlib-ignore-libraries)。

- **IgnoreEmbeddedIDL**

  可选 **Boolean** 参数。

  如果为 `true`，则指定不应将源代码中的任何 IDL 属性处理到 .idl 文件中  。

  有关详细信息，请参阅 [/IGNOREIDL（不将属性处理到 MIDL 中）](/cpp/build/reference/ignoreidl-don-t-process-attributes-into-midl)。

- **IgnoreImportLibrary**

  可选 **Boolean** 参数。

  如果为 `true`，则指定不应将由此配置生成的导入库导入到依赖项目中。

  此参数不与任何链接器选项对应。

- **IgnoreSpecificDefaultLibraries**

  可选 **String []** 参数。

  指定一个或多个要忽略的默认库的名称。 使用分号分隔多个库。

  有关详细信息，请参阅 [/NODEFAULTLIB（忽略库）](/cpp/build/reference/nodefaultlib-ignore-libraries)。

- **ImageHasSafeExceptionHandlers**

  可选 **Boolean** 参数。

  如果为 `true`，则仅当链接器还可以生成映像安全异常处理程序的表时，才生成映像。

  有关详细信息，请参阅 [/SAFESEH（映像具有安全异常处理程序）](/cpp/build/reference/safeseh-image-has-safe-exception-handlers)。

- **ImportLibrary**

  替换默认库名称的用户指定的导入库名称。

  有关详细信息，请参阅 [/IMPLIB（命名导入库）](/cpp/build/reference/implib-name-import-library)。

- **KeyContainer**

  可选 **String** 参数。

  包含已签名程序集的密钥的容器。

  有关详细信息，请参阅 [/KEYCONTAINER（指定密钥容器以便为程序集签名）](/cpp/build/reference/keycontainer-specify-a-key-container-to-sign-an-assembly)。 另请参阅此表格中的 **KeyFile** 参数。

- **KeyFile**

  可选 **String** 参数。

  指定包含已签名程序集的密钥的文件。

  有关详细信息，请参阅 [/KEYFILE（指定密钥或密钥对以便为程序集签名）](/cpp/build/reference/keyfile-specify-key-or-key-pair-to-sign-an-assembly)。 另请参阅 **KeyContainer** 参数。

- **LargeAddressAware**

  可选 **Boolean** 参数。

  如果为 `true`，则应用程序可以处理大于 2 GB 的地址。

  有关详细信息，请参阅 [/LARGEADDRESSAWARE（处理大地址）](/cpp/build/reference/largeaddressaware-handle-large-addresses)。

- **LinkDLL**

  可选 **Boolean** 参数。

  如果为 `true`，则将 DLL 作为主输出文件生成。

  有关详细信息，请参阅 [/DLL（生成 DLL）](/cpp/build/reference/dll-build-a-dll)。

- **LinkErrorReporting**

  可选 **String** 参数。

  允许你直接向 Microsoft 提供内部编译器错误 (ICE) 信息。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **NoErrorReport** -  **/ERRORREPORT:NONE**

  - **PromptImmediately** -  **/ERRORREPORT:PROMPT**

  - **QueueForNextLogin** -  **/ERRORREPORT:QUEUE**

  - **SendErrorReport** -  **/ERRORREPORT:SEND**

  有关详细信息，请参阅 [/ERRORREPORT（报告内部链接器错误）](/cpp/build/reference/errorreport-report-internal-linker-errors)。

- **LinkIncremental**

  可选 **Boolean** 参数。

  如果为 `true`，则启用增量链接。

  有关详细信息，请参阅 [/INCREMENTAL（增量链接）](/cpp/build/reference/incremental-link-incrementally)。

- **LinkLibraryDependencies**

  可选 **Boolean** 参数。

  如果为 `true`，指定自动链接项目依赖项中的库输出。

  此参数不与任何链接器选项对应。

- **LinkStatus**

  可选 **Boolean** 参数。

  如果为 `true`，则指定链接器显示用来指示链接完成百分比的进度指示器。

  有关详细信息，请参阅 [/LTCG（链接时间代码生成）](/cpp/build/reference/ltcg-link-time-code-generation)的 `STATUS` 参数。

- **LinkTimeCodeGeneration**

  可选 **String** 参数。

  指定用于按配置文件优化的选项。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **Default** -  *\<none>*

  - **UseLinkTimeCodeGeneration** -  **/LTCG**

  - **PGInstrument** -  **/LTCG:PGInstrument**

  - **PGOptimization** -  **/LTCG:PGOptimize**

  - **PGUpdate**

    \- **/LTCG:PGUpdate**

  有关详细信息，请参阅 [/LTCG（链接时间代码生成）](/cpp/build/reference/ltcg-link-time-code-generation)。

- **ManifestFile**

  可选 **String** 参数。

  将默认清单文件名更改为指定的文件名。

  有关详细信息，请参阅 [/MANIFESTFILE（命名清单文件）](/cpp/build/reference/manifestfile-name-manifest-file)。

- **MapExports**

  可选 **Boolean** 参数。

  如果为 `true`，则告知链接器将导出的函数包括在映射文件中。

  有关详细信息，请参阅 [/MAPINFO（将信息包括在映射文件中）](/cpp/build/reference/mapinfo-include-information-in-mapfile)中的 `EXPORTS` 参数。

- **MapFileName**

  可选 **String** 参数。

  将默认映射文件名更改为指定的文件名。

- **MergedIDLBaseFileName**

  可选 **String** 参数。

  指定 .idl 文件的文件名和文件扩展名  。

  有关详细信息，请参阅 [/IDLOUT（命名 MIDL 输出文件）](/cpp/build/reference/idlout-name-midl-output-files)。

- **MergeSections**

  可选 **String** 参数。

  合并映像中的节。 指定 `from-section=to-section`。

  有关详细信息，请参阅 [/MERGE（合并节）](/cpp/build/reference/merge-combine-sections)。

- **MidlCommandFile**

  可选 **String** 参数。

  指定包含 MIDL 命令行选项的文件的名称。

  有关详细信息，请参阅 [/MIDL（指定 MIDL 命令行选项）](/cpp/build/reference/midl-specify-midl-command-line-options)。

- **MinimumRequiredVersion**

  可选 **String** 参数。

  指定子系统所需的最低版本。 该参数是介于 0 到 65535 之间的十进制数字。

- **ModuleDefinitionFile**

  可选 **String** 参数。

  指定[模块定义文件](/cpp/build/reference/module-definition-dot-def-files)的名称。

  有关详细信息，请参阅 [/DEF（指定模块定义文件）](/cpp/build/reference/def-specify-module-definition-file)。

- **MSDOSStubFileName**

  可选 **String** 参数。

  将指定的 MS-DOS 存根程序附加到 Win32 程序。

  有关详细信息，请参阅 [/STUB（MS-DOS 存根文件名）](/cpp/build/reference/stub-ms-dos-stub-file-name)。

- **NoEntryPoint**

  可选 **Boolean** 参数。

  如果为 `true`，则指定纯资源 DLL。

  有关详细信息，请参阅 [/NOENTRY（无入口点）](/cpp/build/reference/noentry-no-entry-point)。

- **ObjectFiles**

  隐式 **String []** 参数。

  指定已链接的对象文件。

- **OptimizeReferences**

  可选 **Boolean** 参数。

  如果为 `true`，则清除从未引用过的函数和/或数据。

  有关详细信息，请参阅 [/OPT （优化）](/cpp/build/reference/opt-optimizations) 中的 `REF` 参数。

- **OutputFile**

  可选 **String** 参数。

  覆盖链接器所创建程序的默认名称和位置。

  有关详细信息，请参阅 [/OUT（输出文件名）](/cpp/build/reference/out-output-file-name)。

- **PerUserRedirection**

  可选 **Boolean** 参数。

  如果为 `true`，且启用了“注册输出”，则强制注册表向 **HKEY_CLASSES_ROOT** 写入内容以重定向到 **HKEY_CURRENT_USER**。

- **PreprocessOutput**

  可选 `ITaskItem[]` 参数。

  定义可以由任务使用和发出的预处理器输出项的数组。

- **PreventDllBinding**

  可选 **Boolean** 参数。

  如果为 `true`，则向 Bind.exe 指示不应绑定已链接映像  。

  有关详细信息，请参阅 [/ALLOWBIND（禁止 DLL 绑定）](/cpp/build/reference/allowbind-prevent-dll-binding)。

- **Profile**

  可选 **Boolean** 参数。

  如果为 `true`，则生成一个可与“性能工具”  探查器结合使用的输出文件。

  有关详细信息，请参阅 [/PROFILE（性能工具探查器）](/cpp/build/reference/profile-performance-tools-profiler)。

- **ProfileGuidedDatabase**

  可选 **String** 参数。

  指定将用于保存有关运行中程序的信息的 .pgd 文件的名称 

  有关详细信息，请参阅 [/PGD（指定数据库以按配置文件优化）](/cpp/build/reference/pgd-specify-database-for-profile-guided-optimizations)。

- **ProgramDatabaseFile**

  可选 **String** 参数。

  指定链接器所创建程序数据库 (PDB) 的名称。

  有关详细信息，请参阅 [/PDB（使用程序数据库）](/cpp/build/reference/pdb-use-program-database)。

- **RandomizedBaseAddress**

  可选 **Boolean** 参数。

  如果为 `true`，则使用 Windows 的*地址空间布局随机化* (ASLR) 功能，生成可在加载时随机变基的可执行映像。

  有关详细信息，请参阅 [/DYNAMICBASE（使用地址空间布局随机化）](/cpp/build/reference/dynamicbase-use-address-space-layout-randomization)。

- **RegisterOutput**

  可选 **Boolean** 参数。

  如果为 `true`，则注册此生成的主输出。

- **SectionAlignment**

  可选 **Integer** 参数。

  指定程序的线性地址空间内每节的对齐方式。 该参数值是字节单位数，并且是 2 的幂。

  有关详细信息，请参阅 [/ALIGN（节对齐）](/cpp/build/reference/align-section-alignment)。

- **SetChecksum**

  可选 **Boolean** 参数。

  如果为 `true`，则在 .exe 文件的标头中设置校验和  。

  有关详细信息，请参阅 [/RELEASE（设置校验和）](/cpp/build/reference/release-set-the-checksum)。

- **ShowProgress**

  可选 **String** 参数。

  指定链接操作的进度报告的详细级别。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **NotSet** -  *\<none>*

  - **LinkVerbose** -  **/VERBOSE**

  - **LinkVerboseLib** -  **/VERBOSE:Lib**

  - **LinkVerboseICF** -  **/VERBOSE:ICF**

  - **LinkVerboseREF** -  **/VERBOSE:REF**

  - **LinkVerboseSAFESEH** -  **/VERBOSE:SAFESEH**

  - **LinkVerboseCLR** -  **/VERBOSE:CLR**

  有关详细信息，请参阅 [/VERBOSE（打印进度消息）](/cpp/build/reference/verbose-print-progress-messages)。

- **Sources**

  必选 `ITaskItem[]` 参数。

  定义可以被任务使用和发出的 MSBuild 源文件项的数组。

- **SpecifySectionAttributes**

  可选 **String** 参数。

  指定节的属性。 这将覆盖在编译节的 .obj 文件时所设置的属性  。

  有关详细信息，请参阅 [/SECTION（指定节属性）](/cpp/build/reference/section-specify-section-attributes)。

- **StackCommitSize**

  可选 **String** 参数。

  指定分配额外内存时，每次分配的物理内存量。

  有关详细信息，请参阅 [/STACK（堆栈分配）](/cpp/build/reference/stack-stack-allocations)的 `commit` 参数。

- **StackReserveSize**

  可选 **String** 参数。

  指定虚拟内存中的堆栈分配总大小。

  有关详细信息，请参阅 [/STACK（堆栈分配）](/cpp/build/reference/stack-stack-allocations)的 `reserve` 参数。

- **StripPrivateSymbols**

  可选 **String** 参数。

  创建第二个程序数据库 (PDB) 文件，该文件将省略你不希望向客户分布的符号。 指定第二个 PDB 文件的名称。

  有关详细信息，请参阅 [/PDBSTRIPPED（去除私有符号）](/cpp/build/reference/pdbstripped-strip-private-symbols)。

- **SubSystem**

  可选 **String** 参数。

  为可执行文件指定环境。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **NotSet** -  *\<none>*

  - **Console** -  **/SUBSYSTEM:CONSOLE**

  - **Windows** -  **/SUBSYSTEM:WINDOWS**

  - **Native** -  **/SUBSYSTEM:NATIVE**

  - **EFI Application** -  **/SUBSYSTEM:EFI_APPLICATION**

  - **EFI Boot Service Driver** -  **/SUBSYSTEM:EFI_BOOT_SERVICE_DRIVER**

  - **EFI ROM** -  **/SUBSYSTEM:EFI_ROM**

  - **EFI Runtime** -  **/SUBSYSTEM:EFI_RUNTIME_DRIVER**

  - **WindowsCE** -  **/SUBSYSTEM:WINDOWSCE**

  - **POSIX** -  **/SUBSYSTEM:POSIX**

  有关详细信息，请参阅 [/SUBSYSTEM（指定子系统）](/cpp/build/reference/subsystem-specify-subsystem)。

- **SupportNobindOfDelayLoadedDLL**

  可选 **Boolean** 参数。

  如果为 `true`，则告知链接器不要在最终映像中包含可绑定的导入地址表 (IAT)。

  有关详细信息，请参阅 [/DELAY（延迟加载导入设置）](/cpp/build/reference/delay-delay-load-import-settings)的 `NOBIND` 参数。

- **SupportUnloadOfDelayLoadedDLL**

  可选 **Boolean** 参数。

  如果为 `true`，则告知延迟加载 Helper 函数支持 DLL 的显式卸载。

  有关详细信息，请参阅 [/DELAY（延迟加载导入设置）](/cpp/build/reference/delay-delay-load-import-settings)的 `UNLOAD` 参数。

- **SuppressStartupBanner**

  可选 **Boolean** 参数。

  如果为 `true`，则在任务开始时阻止显示版权和版本号消息。

  有关详细信息，请参阅 [/NOLOGO（取消显示启动版权标志）（链接器）](/cpp/build/reference/nologo-suppress-startup-banner-linker)。

- **SwapRunFromCD**

  可选 **Boolean** 参数。

  如果为 `true`，则告知操作系统首先将连接器输出复制到交换文件，然后从那里运行映像。

  有关详细信息，请参阅 [/SWAPRUN（将链接器输出加载到交换文件）](/cpp/build/reference/swaprun-load-linker-output-to-swap-file)的 `CD` 参数。 另请参阅 **SwapRunFromNET** 参数。

- **SwapRunFromNET**

  可选 **Boolean** 参数。

  如果为 `true`，则告知操作系统首先将连接器输出复制到交换文件，然后从那里运行映像。

  有关详细信息，请参阅 [/SWAPRUN（将链接器输出加载到交换文件）](/cpp/build/reference/swaprun-load-linker-output-to-swap-file)的 `NET` 参数。 另请参阅此表格中的 **SwapRunFromCD** 参数。

- **TargetMachine**

  可选 **String** 参数。

  指定程序或 DLL 的目标平台。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **NotSet** -  *\<none>*

  - **MachineARM** -  **/MACHINE:ARM**

  - **MachineEBC** -  **/MACHINE:EBC**

  - **MachineIA64** -  **/MACHINE:IA64**

  - **MachineMIPS** -  **/MACHINE:MIPS**

  - **MachineMIPS16** -  **/MACHINE:MIPS16**

  - **MachineMIPSFPU** -  **/MACHINE:MIPSFPU**

  - **MachineMIPSFPU16** -  **/MACHINE:MIPSFPU16**

  - **MachineSH4** -  **/MACHINE:SH4**

  - **MachineTHUMB** -  **/MACHINE:THUMB**

  - **MachineX64** -  **/MACHINE:X64**

  - **MachineX86** -  **/MACHINE:X86**

  有关详细信息，请参阅 [/MACHINE（指定目标平台）](/cpp/build/reference/machine-specify-target-platform)。

- **TerminalServerAware**

  可选 **Boolean** 参数。

  如果为 `true`，则在程序映像的可选标头中的 IMAGE_OPTIONAL_HEADER DllCharacteristics 字段中设置一个标志。 当设置此标志后，终端服务器将不会向应用程序进行某些更改。

  有关详细信息，请参阅 [/TSAWARE（创建终端服务器感知应用程序）](/cpp/build/reference/tsaware-create-terminal-server-aware-application)。

- **TrackerLogDirectory**

  可选 **String** 参数。

  指定跟踪器日志的目录。

- **TreatLinkerWarningAsErrors**

  可选 **Boolean** 参数。

  如果为 `true`，则指示在链接器生成警告的情况下不生成任何输出文件。

  有关详细信息，请参阅 [/WX（将链接器警告视为错误）](/cpp/build/reference/wx-treat-linker-warnings-as-errors)。

- **TurnOffAssemblyGeneration**

  可选 **Boolean** 参数。

  如果为 `true`，则创建当前输出文件的映像，但不包含 .NET Framework 程序集。

  有关详细信息，请参阅 [/NOASSEMBLY（创建 MSIL 模块）](/cpp/build/reference/noassembly-create-a-msil-module)。

- **TypeLibraryFile**

  可选 **String** 参数。

  指定 .tlb 文件的文件名和文件扩展名  。 指定文件名，或者路径和文件名。

  有关详细信息，请参阅 [/TLBOUT（命名 .tlb 文件）](/cpp/build/reference/tlbout-name-dot-tlb-file)。

- **TypeLibraryResourceID**

  可选 **Integer** 参数。

  指定链接器所创建类型库的用户指定值。 指定一个介于 1 和 65535 之间的值。

  有关详细信息，请参阅 [/TLBID（指定类型库的资源 ID）](/cpp/build/reference/tlbid-specify-resource-id-for-typelib)。

- **UACExecutionLevel**

  可选 **String** 参数。

  指定在用户帐户控制下运行时为应用程序请求的执行级别。

  指定以下值之一，其中每个值对应于一个命令行选项。

  - **AsInvoker** - `level='asInvoker'`

  - **HighestAvailable** - `level='highestAvailable'`

  - **RequireAdministrator** - `level='requireAdministrator'`

  有关详细信息，请参阅 [/MANIFESTUAC（将 UAC 信息嵌入到清单中）](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest)的 `level` 参数。

- **UACUIAccess**

  可选 **Boolean** 参数。

  如果为 `true`，则应用程序绕过用户界面保护级别并将输入引导到桌面上的更高权限窗口；否则为 `false`。

  有关详细信息，请参阅 [/MANIFESTUAC（将 UAC 信息嵌入到清单中）](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest)的 `uiAccess` 参数。

- **UseLibraryDependencyInputs**

  可选 **Boolean** 参数。

  如果为 `true`，则在对项目依赖项的库输出进行链接时，使用对库管理员工具的输入，而不使用库文件本身。

- **Version**

  可选 **String** 参数。

  在 .exe 或 .dll 文件的标头中放置一个版本号   。 指定 "`major[.minor]`"。 `major` 和 `minor` 参数是介于 0 到 65535 之间的十进制数字。

  有关详细信息，请参阅 [/VERSION（版本信息）](/cpp/build/reference/version-version-information)。

## <a name="see-also"></a>请参阅
- [任务参考](../msbuild/msbuild-task-reference.md)
