---
title: Link 任务 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
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
- MSBuild (Visual C++), Link task
- Link task (MSBuild (Visual C++))
ms.assetid: 0a61f168-3113-4fa7-83a3-d9142e2a33f8
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 930cec012bfda49c61116ada2ba6df10c3a48f51
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MTE95
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75851000"
---
# <a name="link-task"></a>Link 任务
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包装 Visual C++ 链接器工具 link.exe。 链接器工具将通用对象文件格式 (COFF) 对象文件和库链接起来，以创建可执行 (.exe) 文件或动态链接库 (DLL)。 有关详细信息，请参阅[链接器选项](https://msdn.microsoft.com/library/c1d51b8a-bd23-416d-81e4-900e02b2c129)。  
  
## <a name="parameters"></a>参数  
 下表描述了 **Link** 任务的参数。 大多数任务参数和若干组参数都对应于命令行选项。  
  
- **AdditionalDependencies**  
  
   可选 **String []** 参数。  
  
   指定要添加到命令的输入文件的列表。  
  
   有关详细信息，请参阅 [LINK 输入文件](https://msdn.microsoft.com/library/bb26fcc5-509a-4620-bc3e-b6c6e603a412)。  
  
- **AdditionalLibraryDirectories**  
  
   可选 **String []** 参数。  
  
   重写环境库路径。 指定目录名。  
  
   有关详细信息，请参阅 [/LIBPATH（附加的 Libpath）](https://msdn.microsoft.com/library/7240af0b-9a3d-4d53-8169-2a92cd6958ba)。  
  
- **AdditionalManifestDependencies**  
  
   可选 **String []** 参数。  
  
   指定将放入清单文件的 `dependency` 节的属性。  
  
   有关详细信息，请参阅 [/MANIFESTDEPENDENCY（指定清单依赖项）](https://msdn.microsoft.com/library/e4b68313-33a2-4c3e-908e-ac2b9f7d6a73)。 另请参阅 [MSDN](https://msdn.microsoft.com/) 网站上的“发布服务器配置文件”。  
  
- **AdditionalOptions**  
  
   可选 **String** 参数。  
  
   在命令行上指定的链接器选项列表。 例如， **"** _/option1 /option2 /option#_ "。 使用此参数可指定未由任何其他 **Link** 任务参数表示的链接器选项。  
  
   有关详细信息，请参阅[链接器选项](https://msdn.microsoft.com/library/c1d51b8a-bd23-416d-81e4-900e02b2c129)。  
  
- **AddModuleNamesToAssembly**  
  
   可选 **String []** 参数。  
  
   向程序集添加模块引用。  
  
   有关详细信息，请参阅 [/ASSEMBLYMODULE（向程序集添加 MSIL 模块）](https://msdn.microsoft.com/library/67357da8-e4b6-49fd-932c-329a5777f143)。  
  
- **AllowIsolation**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则将导致操作系统进行清单查找和加载。 如果为 `false`，则指示将加载 DLL，仿佛没有清单一样。  
  
   有关详细信息，请参阅 [/ALLOWISOLATION（清单查找）](https://msdn.microsoft.com/library/6d41851e-b3c1-4bdf-beaa-031773089d6f)。  
  
- **AssemblyDebug**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则发出 **DebuggableAttribute** 属性以及调试信息跟踪，并禁用 JIT 优化。 如果为 `false`，则发出 **DebuggableAttribute** 属性，但禁用调试信息跟踪，启用 JIT 优化。  
  
   有关详细信息，请参阅 [/ASSEMBLYDEBUG（添加 DebuggableAttribute）](https://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982)。  
  
- **AssemblyLinkResource**  
  
   可选 **String []** 参数。  
  
   创建指向输出文件中的 .NET Framework 资源的链接；资源文件不会放入输出文件中。 指定资源的名称。  
  
   有关详细信息，请参阅 [/ASSEMBLYLINKRESOURCE（链接到 .NET Framework 资源）](https://msdn.microsoft.com/library/8b6ad184-1b33-47a4-8513-4803cf915b64)。  
  
- **AttributeFileTracking**  
  
   隐式 **Boolean** 参数。  
  
   启用更深层次的文件跟踪，以捕获链接增量的行为。 始终返回 `true`。  
  
- **BaseAddress**  
  
   可选 **String** 参数。  
  
   为正在生成的程序或 DLL 设置基址。 指定 `{address[,size] | @filename,key}`。  
  
   有关详细信息，请参阅 [/BASE（基址）](https://msdn.microsoft.com/library/00b9f6fe-0bd2-4772-a69c-7365eb199069)。  
  
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
  
    有关详细信息，请参阅 [/CLRIMAGETYPE（指定 CLR 映像的类型）](https://msdn.microsoft.com/library/04c60ee6-9dd7-4391-bc03-6926ad0fa116)。  
  
- **CLRSupportLastError**  
  
   可选 **String** 参数。  
  
   保留通过 P/Invoke 机制调用的函数的上一个错误代码。  
  
   指定以下值之一，其中每个值对应于一个链接器选项。  
  
  - **Enabled** -  **/CLRSupportLastError**  
  
  - **Disabled** -  **/CLRSupportLastError:NO**  
  
  - **SystemDlls** -  **/CLRSupportLastError:SYSTEMDLL**  
  
    有关详细信息，请参阅 [/CLRSUPPORTLASTERROR（为 PInvoke 调用保留上次的错误代码）](https://msdn.microsoft.com/library/b7057990-4154-4b1d-9fc9-6236f7be7575)。  
  
- **CLRThreadAttribute**  
  
   可选 **String** 参数。  
  
   显式指定用于 CLR 程序入口点的线程特性。  
  
   指定以下值之一，其中每个值对应于一个链接器选项。  
  
  - **DefaultThreadingAttribute** -  **/CLRTHREADATTRIBUTE:NONE**  
  
  - **MTAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:MTA**  
  
  - **STAThreadingAttribute** -  **/CLRTHREADATTRIBUTE:STA**  
  
    有关详细信息，请参阅 [/CLRTHREADATTRIBUTE（设置 CLR 线程特性）](https://msdn.microsoft.com/library/4907e9ef-5031-446c-aecf-0a0b32fae1e8)。  
  
- **CLRUnmanagedCodeCheck**  
  
   可选 **Boolean** 参数。  
  
   指定链接器是否将 **SuppressUnmanagedCodeSecurityAttribute** 应用到链接器生成的从托管代码到本机 DLL 的 P/Invoke 调用。  
  
   有关详细信息，请参阅 [/CLRUNMANAGEDCODECHECK（添加 SuppressUnmanagedCodeSecurityAttribute）](https://msdn.microsoft.com/library/73abc426-dab0-45e2-be85-0f9a14206cc2)。  
  
- **CreateHotPatchableImage**  
  
   可选 **String** 参数。  
  
   准备映像以进行热修补。  
  
   指定以下值之一，它对应于一个链接器选项。  
  
  - **Enabled** -  **/FUNCTIONPADMIN**  
  
  - **X86Image** -  **/FUNCTIONPADMIN:5**  
  
  - **X64Image** -  **/FUNCTIONPADMIN:6**  
  
  - **ItaniumImage** -  **/FUNCTIONPADMIN:16**  
  
    有关详细信息，请参阅 [/FUNCTIONPADMIN（创建可热修补的映像）](https://msdn.microsoft.com/library/25b02c13-1add-4fbd-add9-fcb30eb2cae7)。  
  
- **DataExecutionPrevention**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指示可执行文件已经就是否与 Windows 数据执行保护功能兼容进行了测试。  
  
   有关详细信息，请参阅 [/NXCOMPAT（与数据执行保护兼容）](https://msdn.microsoft.com/library/5858e7ff-24d3-4ac3-9046-af2c9e220d9b)。  
  
- **DelayLoadDLLs**  
  
   可选 **String []** 参数。  
  
   此参数导致 DLL *延迟加载*。 指定要延迟加载的 DLL 的名称。  
  
   有关详细信息，请参阅 [/DELAYLOAD（延迟加载导入）](https://msdn.microsoft.com/library/39ea0f1e-5c01-450f-9c75-2d9761ff9b28)。  
  
- **DelaySign**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则对程序集进行部分签名。 默认情况下，该值为 `false`。  
  
   有关详细信息，请参阅 [/DELAYSIGN（对程序集进行部分签名）](https://msdn.microsoft.com/library/15244d30-3ecb-492f-a408-ffe81f38de20)。  
  
- **Driver**  
  
   可选 **String** 参数。  
  
   指定此参数以生成 Windows NT 内核模式驱动程序。  
  
   指定以下值之一，其中每个值对应于一个链接器选项。  
  
  - **NotSet** -  *\<none>*  
  
  - **Driver** -  **/Driver**  
  
  - **UpOnly** -  **/DRIVER:UPONLY**  
  
  - **WDM** -  **/DRIVER:WDM**  
  
    有关详细信息，请参阅 [/DRIVER（Windows NT 内核模式驱动程序）](https://msdn.microsoft.com/library/aeee8e28-5d97-40f5-ba16-9f370fe8a1b8)。  
  
- **EmbedManagedResourceFile**  
  
   可选 **String []** 参数。  
  
   将资源文件嵌入程序集。 指定所需的资源文件名。 （可选）指定用于加载资源的逻辑名称，和指示在程序集清单中该资源文件为私有的 **PRIVATE** 选项。  
  
   有关详细信息，请参阅 [/ASSEMBLYRESOURCE（嵌入托管资源）](https://msdn.microsoft.com/library/0ce6e1fb-921b-4b1b-a59c-d35388d789f2)。  
  
- **EnableCOMDATFolding**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则启用相同的 COMDAT 折叠。  
  
   有关详细信息，请参阅 [/OPT（优化）](https://msdn.microsoft.com/library/8f229863-5f53-48a8-9478-243a647093ac)的 `ICF[= iterations]` 参数。  
  
- **EnableUAC**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指定将用户帐户控制 (UAC) 信息嵌入到程序清单中。  
  
   有关详细信息，请参阅 [/MANIFESTUAC（将 UAC 信息嵌入到清单中）](https://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a)。  
  
- **EntryPointSymbol**  
  
   可选 **String** 参数。  
  
   将某个入口点函数指定为 .exe 文件或 DLL 的起始地址。 将函数名称指定为参数值。  
  
   有关详细信息，请参阅 [/ENTRY（入口点符号）](https://msdn.microsoft.com/library/26c62ba2-4f52-4882-a7bd-7046a0abf445)。  
  
- **FixedBaseAddress**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则创建只能在其首选基址加载的程序或 DLL。  
  
   有关详细信息，请参阅 [/FIXED（固定基址）](https://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5)。  
  
- **ForceFileOutput**  
  
   可选 **String** 参数。  
  
   告知链接器创建有效的 .exe 文件或 DLL，即使引用的符号未经定义或多次定义也是如此。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **Enabled** -  **/FORCE**  
  
  - **MultiplyDefinedSymbolOnly** -  **/FORCE:MULTIPLE**  
  
  - **UndefinedSymbolOnly** -  **/FORCE:UNRESOLVED**  
  
    有关详细信息，请参阅 [/FORCE（强制文件输出）](https://msdn.microsoft.com/library/b1e9a218-a5eb-4e60-a4a4-65b4be15e5da)。  
  
- **ForceSymbolReferences**  
  
   可选 **String []** 参数。  
  
   此参数告知链接器将指定的符号添加到符号表中。  
  
   有关详细信息，请参阅 [/INCLUDE（强制符号引用）](https://msdn.microsoft.com/library/4a039677-360a-480f-bd0b-448e239b449c)。  
  
- **FunctionOrder**  
  
   可选 **String** 参数。  
  
   此参数通过将指定的已打包函数 (COMDATs) 按预定顺序放置到映像中，来优化程序。  
  
   有关详细信息，请参阅 [/ORDER（按顺序放置函数）](https://msdn.microsoft.com/library/ecf5eb3e-e404-4e86-9a91-4e5ec157261a)。  
  
- **GenerateDebugInformation**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则为 .exe 文件或 DLL 创建调试信息。  
  
   有关详细信息，请参阅 [/DEBUG（生成调试信息）](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103)。  
  
- **GenerateManifest**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则创建并行清单文件。  
  
   有关详细信息，请参阅 [/MANIFEST（创建并行程序集清单）](https://msdn.microsoft.com/library/98c52e1e-712c-4f49-b149-4d0a3501b600)。  
  
- **GenerateMapFile**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则创建*映射文件*。 映射文件的文件扩展名为 .map。  
  
   有关详细信息，请参阅 [/MAP（生成映射文件）](https://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63)。  
  
- **HeapCommitSize**  
  
   可选 **String** 参数。  
  
   指定在堆上一次性分配的物理内存量。  
  
   有关详细信息，请参阅 [/HEAP（设置堆大小）](https://msdn.microsoft.com/library/a3f71927-7f1d-492c-9fdb-dfccb1a043da)中的 `commit` 参数。 另请参阅 **HeapReserveSize** 参数。  
  
- **HeapReserveSize**  
  
   可选 **String** 参数。  
  
   指定虚拟内存中的堆分配总量。  
  
   有关详细信息，请参阅 [/HEAP（设置堆大小）](https://msdn.microsoft.com/library/a3f71927-7f1d-492c-9fdb-dfccb1a043da)中的 `reserve` 参数。 另请参阅此表格中的 **HeapCommitSize** 参数。  
  
- **IgnoreAllDefaultLibraries**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则告知链接器从其在解析外部引用时搜索的库列表中移除一个或多个默认库。  
  
   有关详细信息，请参阅 [/NODEFAULTLIB（忽略库）](https://msdn.microsoft.com/library/7270b673-6711-468e-97a7-c2925ac2be6e)。  
  
- **IgnoreEmbeddedIDL**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指定不应将源代码中的任何 IDL 属性处理到 .idl 文件中。  
  
   有关详细信息，请参阅 [/IGNOREIDL（不将属性处理到 MIDL 中）](https://msdn.microsoft.com/library/29514098-6a1c-4317-af2f-1dc268972780)。  
  
- **IgnoreImportLibrary**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指定不应将由此配置生成的导入库导入到依赖项目中。  
  
   此参数不与任何链接器选项对应。  
  
- **IgnoreSpecificDefaultLibraries**  
  
   可选 **String []** 参数。  
  
   指定一个或多个要忽略的默认库的名称。 使用分号分隔多个库。  
  
   有关详细信息，请参阅 [/NODEFAULTLIB（忽略库）](https://msdn.microsoft.com/library/7270b673-6711-468e-97a7-c2925ac2be6e)。  
  
- **ImageHasSafeExceptionHandlers**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则仅当链接器还可以生成映像安全异常处理程序的表时，才生成映像。  
  
   有关详细信息，请参阅 [/SAFESEH（映像具有安全异常处理程序）](https://msdn.microsoft.com/library/7722ff99-b833-4c65-a855-aaca902ffcb7)。  
  
- **ImportLibrary**  
  
   替换默认库名称的用户指定的导入库名称。  
  
   有关详细信息，请参阅 [/IMPLIB（命名导入库）](https://msdn.microsoft.com/library/fe8f71ab-7055-41b5-8ef8-2b97cfa4a432)。  
  
- **KeyContainer**  
  
   可选 **String** 参数。  
  
   包含已签名程序集的密钥的容器。  
  
   有关详细信息，请参阅 [/KEYCONTAINER（指定密钥容器以便为程序集签名）](https://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e)。 另请参阅此表格中的 **KeyFile** 参数。  
  
- **KeyFile**  
  
   可选 **String** 参数。  
  
   指定包含已签名程序集的密钥的文件。  
  
   有关详细信息，请参阅 [/KEYFILE（指定密钥或密钥对以便为程序集签名）](https://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06)。 另请参阅 **KeyContainer** 参数。  
  
- **LargeAddressAware**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则应用程序可以处理大于 2 GB 的地址。  
  
   有关详细信息，请参阅 [/LARGEADDRESSAWARE（处理大地址）](https://msdn.microsoft.com/library/a29756c8-e893-47a9-9750-1f0d25359385)。  
  
- **LinkDLL**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则将 DLL 作为主输出文件生成。  
  
   有关详细信息，请参阅 [/DLL（生成 DLL）](https://msdn.microsoft.com/library/c7685aec-31d0-490f-9503-fb5171a23609)。  
  
- **LinkErrorReporting**  
  
   可选 **String** 参数。  
  
   允许你直接向 Microsoft 提供内部编译器错误 (ICE) 信息。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **NoErrorReport** -  **/ERRORREPORT:NONE**  
  
  - **PromptImmediately** -  **/ERRORREPORT:PROMPT**  
  
  - **QueueForNextLogin** -  **/ERRORREPORT:QUEUE**  
  
  - **SendErrorReport** -  **/ERRORREPORT:SEND**  
  
    有关详细信息，请参阅 [/ERRORREPORT（报告内部链接器错误）](https://msdn.microsoft.com/library/f5fab595-a2f1-4eb0-ab5c-1c0fbd3d8c28)。  
  
- **LinkIncremental**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则启用增量链接。  
  
   有关详细信息，请参阅 [/INCREMENTAL（增量链接）](https://msdn.microsoft.com/library/135656ff-94fa-4ad4-a613-22e1a2a5d16b)。  
  
- **LinkLibraryDependencies**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，指定自动链接项目依赖项中的库输出。  
  
   此参数不与任何链接器选项对应。  
  
- **LinkStatus**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指定链接器显示用来指示链接完成百分比的进度指示器。  
  
   有关详细信息，请参阅 [/LTCG（链接时间代码生成）](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2)的 `STATUS` 参数。  
  
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
  
    有关详细信息，请参阅 [/LTCG（链接时间代码生成）](https://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2)。  
  
- **ManifestFile**  
  
   可选 **String** 参数。  
  
   将默认清单文件名更改为指定的文件名。  
  
   有关详细信息，请参阅 [/MANIFESTFILE（命名清单文件）](https://msdn.microsoft.com/library/befa5ab2-a9cf-4c9b-969a-e7b4a930f08d)。  
  
- **MapExports**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则告知链接器将导出的函数包括在映射文件中。  
  
   有关详细信息，请参阅 [/MAPINFO（将信息包括在映射文件中）](https://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b)中的 `EXPORTS` 参数。  
  
- **MapFileName**  
  
   可选 **String** 参数。  
  
   将默认映射文件名更改为指定的文件名。  
  
- **MergedIDLBaseFileName**  
  
   可选 **String** 参数。  
  
   指定 .idl 文件的文件名和文件扩展名。  
  
   有关详细信息，请参阅 [/IDLOUT（命名 MIDL 输出文件）](https://msdn.microsoft.com/library/10d00a6a-85b4-4de1-8732-e422c6931509)。  
  
- **MergeSections**  
  
   可选 **String** 参数。  
  
   合并映像中的节。 指定 `from-section=to-section`。  
  
   有关详细信息，请参阅 [/MERGE（合并节）](https://msdn.microsoft.com/library/10fb20c2-0b3f-4c8d-98a8-f69aedf03d52)。  
  
- **MidlCommandFile**  
  
   可选 **String** 参数。  
  
   指定包含 MIDL 命令行选项的文件的名称。  
  
   有关详细信息，请参阅 [/MIDL（指定 MIDL 命令行选项）](https://msdn.microsoft.com/library/22dc259e-b34c-4ed3-a380-4beb734482c1)。  
  
- **MinimumRequiredVersion**  
  
   可选 **String** 参数。  
  
   指定子系统所需的最低版本。 该参数是介于 0 到 65535 之间的十进制数字。  
  
- **ModuleDefinitionFile**  
  
   可选 **String** 参数。  
  
   指定[模块定义文件](https://msdn.microsoft.com/library/08c0bc28-c5d2-47aa-9624-7fc68bcaa4d8)的名称。  
  
   有关详细信息，请参阅 [/DEF（指定模块定义文件）](https://msdn.microsoft.com/library/6497fa68-65f0-48ca-8f66-b87166fc631a)。  
  
- **MSDOSStubFileName**  
  
   可选 **String** 参数。  
  
   将指定的 MS-DOS 存根程序附加到 Win32 程序。  
  
   有关详细信息，请参阅 [/STUB（MS-DOS 存根文件名）](https://msdn.microsoft.com/library/65221ffe-4f9a-4a14-ac69-3cfb79b40b5f)。  
  
- **NoEntryPoint**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指定纯资源 DLL。  
  
   有关详细信息，请参阅 [/NOENTRY（无入口点）](https://msdn.microsoft.com/library/0214dd41-35ad-43ab-b892-e636e038621a)。  
  
- **ObjectFiles**  
  
   隐式 **String []** 参数。  
  
   指定已链接的对象文件。  
  
- **OptimizeReferences**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则清除从未引用过的函数和/或数据。  
  
   有关详细信息，请参阅 [/OPT （优化）](https://msdn.microsoft.com/library/8f229863-5f53-48a8-9478-243a647093ac) 中的 `REF` 参数。  
  
- **OutputFile**  
  
   可选 **String** 参数。  
  
   覆盖链接器所创建程序的默认名称和位置。  
  
   有关详细信息，请参阅 [/OUT（输出文件名）](https://msdn.microsoft.com/library/976210a4-e51f-4cfb-af5e-c16344455834)。  
  
- **PerUserRedirection**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，且启用了“注册输出”，则强制注册表向 **HKEY_CLASSES_ROOT** 写入内容以重定向到 **HKEY_CURRENT_USER**。  
  
- **PreprocessOutput**  
  
   可选 `ITaskItem[]` 参数。  
  
   定义可以由任务使用和发出的预处理器输出项的数组。  
  
- **PreventDllBinding**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则向 Bind.exe 指示不应绑定已链接映像。  
  
   有关详细信息，请参阅 [/ALLOWBIND（禁止 DLL 绑定）](https://msdn.microsoft.com/library/30e37e24-12e4-407e-988a-39d357403598)。  
  
- **Profile**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则生成一个可与“性能工具”  探查器结合使用的输出文件。  
  
   有关详细信息，请参阅 [/PROFILE（性能工具探查器）](https://msdn.microsoft.com/library/e676baa1-5063-47a3-a357-ba0d1f0d1699)。  
  
- **ProfileGuidedDatabase**  
  
   可选 **String** 参数。  
  
   指定将用于保存有关运行中程序的信息的 .pgd 文件的名称  
  
   有关详细信息，请参阅 [/PGD（指定数据库以按配置文件优化）](https://msdn.microsoft.com/library/9f312498-493b-461f-886f-92652257e443)。  
  
- **ProgramDatabaseFile**  
  
   可选 **String** 参数。  
  
   指定链接器所创建程序数据库 (PDB) 的名称。  
  
   有关详细信息，请参阅 [/PDB（使用程序数据库）](https://msdn.microsoft.com/library/d23db0ce-10cb-427a-bc60-d6b2a852723d)。  
  
- **RandomizedBaseAddress**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则使用 Windows 的*地址空间布局随机化* (ASLR) 功能，生成可在加载时随机变基的可执行映像。  
  
   有关详细信息，请参阅 [/DYNAMICBASE（使用地址空间布局随机化）](https://msdn.microsoft.com/library/6c0ced8e-fe9c-4b63-b956-eb8a55fbceb2)。  
  
- **RegisterOutput**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则注册此生成的主输出。  
  
- **SectionAlignment**  
  
   可选 **Integer** 参数。  
  
   指定程序的线性地址空间内每节的对齐方式。 该参数值是字节单位数，并且是 2 的幂。  
  
   有关详细信息，请参阅 [/ALIGN（节对齐）](https://msdn.microsoft.com/library/f2f8ac24-e90e-4bea-8205-f2960a3b1740)。  
  
- **SetChecksum**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则在 .exe 文件的标头中设置校验和。  
  
   有关详细信息，请参阅 [/RELEASE（设置校验和）](https://msdn.microsoft.com/library/93bcadf4-29ac-4824-914b-6997e3751d22)。  
  
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
  
    有关详细信息，请参阅 [/VERBOSE（打印进度消息）](https://msdn.microsoft.com/library/9c347d98-4c37-4724-a39e-0983934693ab)。  
  
- **Sources**  
  
   必选 `ITaskItem[]` 参数。  
  
   定义可以被任务使用和发出的 MSBuild 源文件项的数组。  
  
- **SpecifySectionAttributes**  
  
   可选 **String** 参数。  
  
   指定节的属性。 这将覆盖在编译节的 .obj 文件时所设置的属性。  
  
   有关详细信息，请参阅 [/SECTION（指定节属性）](https://msdn.microsoft.com/library/92b69d81-e421-462e-b46f-7d0dff9b9d16)。  
  
- **StackCommitSize**  
  
   可选 **String** 参数。  
  
   指定分配额外内存时，每次分配的物理内存量。  
  
   有关详细信息，请参阅 [/STACK（堆栈分配）](https://msdn.microsoft.com/library/73283660-e4bd-47cc-b5ca-04c5d739034c)的 `commit` 参数。  
  
- **StackReserveSize**  
  
   可选 **String** 参数。  
  
   指定虚拟内存中的堆栈分配总大小。  
  
   有关详细信息，请参阅 [/STACK（堆栈分配）](https://msdn.microsoft.com/library/73283660-e4bd-47cc-b5ca-04c5d739034c)的 `reserve` 参数。  
  
- **StripPrivateSymbols**  
  
   可选 **String** 参数。  
  
   创建第二个程序数据库 (PDB) 文件，该文件将省略你不希望向客户分布的符号。 指定第二个 PDB 文件的名称。  
  
   有关详细信息，请参阅 [/PDBSTRIPPED（去除私有符号）](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55)。  
  
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
  
    有关详细信息，请参阅 [/SUBSYSTEM（指定子系统）](https://msdn.microsoft.com/library/d7b133cf-cf22-4da8-ab46-6552702c0b9b)。  
  
- **SupportNobindOfDelayLoadedDLL**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则告知链接器不要在最终映像中包含可绑定的导入地址表 (IAT)。  
  
   有关详细信息，请参阅 [/DELAY（延迟加载导入设置）](https://msdn.microsoft.com/library/9334b332-cc58-4dae-b10f-a4c75972d50c)的 `NOBIND` 参数。  
  
- **SupportUnloadOfDelayLoadedDLL**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则告知延迟加载 Helper 函数支持 DLL 的显式卸载。  
  
   有关详细信息，请参阅 [/DELAY（延迟加载导入设置）](https://msdn.microsoft.com/library/9334b332-cc58-4dae-b10f-a4c75972d50c)的 `UNLOAD` 参数。  
  
- **SuppressStartupBanner**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则在任务开始时阻止显示版权和版本号消息。  
  
   有关详细信息，请参阅 [/NOLOGO（取消显示启动版权标志）（链接器）](https://msdn.microsoft.com/library/3b20dddd-eca6-4545-a331-9f70bf720197)。  
  
- **SwapRunFromCD**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则告知操作系统首先将连接器输出复制到交换文件，然后从那里运行映像。  
  
   有关详细信息，请参阅 [/SWAPRUN（将链接器输出加载到交换文件）](https://msdn.microsoft.com/library/4a1e7f46-4399-4161-8dfc-d6a71beaf683)的 `CD` 参数。 另请参阅 **SwapRunFromNET** 参数。  
  
- **SwapRunFromNET**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则告知操作系统首先将连接器输出复制到交换文件，然后从那里运行映像。  
  
   有关详细信息，请参阅 [/SWAPRUN（将链接器输出加载到交换文件）](https://msdn.microsoft.com/library/4a1e7f46-4399-4161-8dfc-d6a71beaf683)的 `NET` 参数。 另请参阅此表格中的 **SwapRunFromCD** 参数。  
  
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
  
    有关详细信息，请参阅 [/MACHINE（指定目标平台）](https://msdn.microsoft.com/library/8d41bf4b-7e53-4ab9-9085-d852b08d31c2)。  
  
- **TerminalServerAware**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则在程序映像的可选标头中的 IMAGE_OPTIONAL_HEADER DllCharacteristics 字段中设置一个标志。 当设置此标志后，终端服务器将不会向应用程序进行某些更改。  
  
   有关详细信息，请参阅 [/TSAWARE（创建终端服务器感知应用程序）](https://msdn.microsoft.com/library/fe1c1846-de5b-4839-b562-93fbfe36cd29)。  
  
- **TrackerLogDirectory**  
  
   可选 **String** 参数。  
  
   指定跟踪器日志的目录。  
  
- **TreatLinkerWarningAsErrors**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则指示在链接器生成警告的情况下不生成任何输出文件。  
  
   有关详细信息，请参阅 [/WX（将链接器警告视为错误）](https://msdn.microsoft.com/library/e4ba97c7-93f7-43ae-a4bb-d866790926c9)。  
  
- **TurnOffAssemblyGeneration**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则创建当前输出文件的映像，但不包含 .NET Framework 程序集。  
  
   有关详细信息，请参阅 [/NOASSEMBLY（创建 MSIL 模块）](https://msdn.microsoft.com/library/3cea4e70-f451-4395-a626-1930b1b127fe)。  
  
- **TypeLibraryFile**  
  
   可选 **String** 参数。  
  
   指定 .tlb 文件的文件名和文件扩展名。 指定文件名，或者路径和文件名。  
  
   有关详细信息，请参阅 [/TLBOUT（命名 .TLB 文件）](https://msdn.microsoft.com/library/0df6d078-2e48-46c9-a1a5-02674d85dce8)。  
  
- **TypeLibraryResourceID**  
  
   可选 **Integer** 参数。  
  
   指定链接器所创建类型库的用户指定值。 指定一个介于 1 和 65535 之间的值。  
  
   有关详细信息，请参阅 [/TLBID（指定类型库的资源 ID）](https://msdn.microsoft.com/library/434b28a2-4656-4d52-ac82-8b18bf486fb2)。  
  
- **UACExecutionLevel**  
  
   可选 **String** 参数。  
  
   指定在用户帐户控制下运行时为应用程序请求的执行级别。  
  
   指定以下值之一，其中每个值对应于一个命令行选项。  
  
  - **AsInvoker** - `level='asInvoker'`  
  
  - **HighestAvailable** - `level='highestAvailable'`  
  
  - **RequireAdministrator** - `level='requireAdministrator'`  
  
    有关详细信息，请参阅 [/MANIFESTUAC（将 UAC 信息嵌入到清单中）](https://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a)的 `level` 参数。  
  
- **UACUIAccess**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则应用程序绕过用户界面保护级别并将输入引导到桌面上的更高权限窗口；否则为 `false`。  
  
   有关详细信息，请参阅 [/MANIFESTUAC（将 UAC 信息嵌入到清单中）](https://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a)的 `uiAccess` 参数。  
  
- **UseLibraryDependencyInputs**  
  
   可选 **Boolean** 参数。  
  
   如果为 `true`，则在对项目依赖项的库输出进行链接时，使用对库管理员工具的输入，而不使用库文件本身。  
  
- **Version**  
  
   可选 **String** 参数。  
  
   在 .exe 或 .dll 文件的标头中放置一个版本号。 指定 "`major[.minor]`"。 `major` 和 `minor` 参数是介于 0 到 65535 之间的十进制数字。  
  
   有关详细信息，请参阅 [/VERSION（版本信息）](https://msdn.microsoft.com/library/b86d0e86-dca6-4316-aee2-d863ccb9f223)。  
  
## <a name="see-also"></a>另请参阅  
 [任务参考](../msbuild/msbuild-task-reference.md)
