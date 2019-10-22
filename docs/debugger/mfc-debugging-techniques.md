---
title: MFC 调试技术 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- AfxEnableMemoryTracking
- CMemoryState
- delayFreeMemDF
- checkAlwaysMemDF
- vs.debug.mfc
- vs.debug.objects.dump
- vs.debug.memory.dump
- allocMemDF
- afxMemDF
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [MFC]
ms.assetid: b154fc31-5e90-4734-8cbd-58dd9fe1f750
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1380cf2cfd4d1ffe729fdd4a6ce9cfb2ba7d9ab6
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72435642"
---
# <a name="mfc-debugging-techniques"></a>MFC 调试方法
如果要调试 MFC 程序，这些调试技术可能会有用。

## <a name="BKMK_In_this_topic"></a> 在本主题中
[AfxDebugBreak](#BKMK_AfxDebugBreak)

[TRACE 宏](#BKMK_The_TRACE_macro)

[在 MFC 中检测内存泄漏](#BKMK_Memory_leak_detection_in_MFC)

- [跟踪内存分配](#BKMK_Tracking_memory_allocations)

- [启用内存诊断](#BKMK_Enabling_memory_diagnostics)

- [拍摄内存快照](#BKMK_Taking_memory_snapshots)

- [查看内存统计信息](#BKMK_Viewing_memory_statistics)

- [采用对象转储](#BKMK_Taking_object_dumps)

  - [解释内存转储](#BKMK_Interpreting_memory_dumps)

  - [自定义对象转储](#BKMK_Customizing_object_dumps)

  - [减小 MFC 调试生成的大小](#BKMK_Reducing_the_size_of_an_MFC_Debug_build)

  - [生成带有选定模块的调试信息的 MFC 应用程序](#BKMK_Building_an_MFC_app_with_debug_information_for_selected_modules)

## <a name="BKMK_AfxDebugBreak"></a> AfxDebugBreak
MFC 提供特殊的 [AfxDebugBreak](/cpp/mfc/reference/diagnostic-services#afxdebugbreak) 函数，以供在源代码中对断点进行硬编码：

```cpp
AfxDebugBreak( );
```

在 Intel 平台上， `AfxDebugBreak` 将生成以下代码，它在源代码而不是内核代码中中断：

```cpp
_asm int 3
```

在其他平台上， `AfxDebugBreak` 仅调用 `DebugBreak`。

确保在创建发布版本时移除 `AfxDebugBreak` 语句，或使用 `#ifdef _DEBUG` 环绕这些语句。

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_The_TRACE_macro"></a> TRACE 宏
若要在调试器的 [“输出”窗口](../ide/reference/output-window.md)中显示来自程序的消息，可以使用 [ATLTRACE](https://msdn.microsoft.com/Library/c796baa5-e2b9-4814-a27d-d800590b102e) 宏或 MFC [TRACE](https://msdn.microsoft.com/Library/7b6f42d8-b55a-4bba-ab04-c46251778e6f) 宏。 与 [断言](../debugger/c-cpp-assertions.md)类似，跟踪宏只在程序的“Debug”版本中起作用，在“Release”版本中编译时将消失。

下面的示例显示几种 **TRACE** 宏的用法。 与 `printf`类似， **TRACE** 宏可处理许多参数。

```cpp
int x = 1;
int y = 16;
float z = 32.0;
TRACE( "This is a TRACE statement\n" );

TRACE( "The value of x is %d\n", x );

TRACE( "x = %d and y = %d\n", x, y );

TRACE( "x = %d and y = %x and z = %f\n", x, y, z );
```

TRACE 宏会适当地处理 char \* 和 wchar_t \* 参数。 下面的示例说明如何将 TRACE 宏与不同字符串参数类型配合使用。

```cpp
TRACE( "This is a test of the TRACE macro that uses an ANSI string: %s %d\n", "The number is:", 2);

TRACE( L"This is a test of the TRACE macro that uses a UNICODE string: %s %d\n", L"The number is:", 2);

TRACE( _T("This is a test of the TRACE macro that uses a TCHAR string: %s %d\n"), _T("The number is:"), 2);
```

有关 **TRACE** 宏的更多信息，请参见 [诊断服务](/cpp/mfc/reference/diagnostic-services)。

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_Memory_leak_detection_in_MFC"></a> 在 MFC 中检测内存泄漏
MFC 提供一些类和函数来检测曾经被分配但从未释放的内存。

### <a name="BKMK_Tracking_memory_allocations"></a> 跟踪内存分配
在 MFC 中，可以使用 [DEBUG_NEW](https://msdn.microsoft.com/Library/9b379344-4093-4bec-a3eb-e0d8a63ada9d) 宏代替 **new** 运算符来帮助定位内存泄漏。 在程序的“Debug”版本中， `DEBUG_NEW` 将为所分配的每个对象跟踪文件名和行号。 当编译程序的“Release”版本时， `DEBUG_NEW` 将解析为不包含文件名和行号信息的简单 **new** 操作。 因此，在程序的“Release”版本中不会造成任何速度损失。

如果不想重写整个程序来使用 `DEBUG_NEW` 代替 **new**，则可以在源文件中定义下面的宏：

```cpp
#define new DEBUG_NEW
```

当进行 [对象转储](#BKMK_Taking_object_dumps)时，用 `DEBUG_NEW` 分配的每个对象均将显示被分配到的文件和行号，使你可以查明内存泄漏源。

MFC 框架的“Debug”版本自动使用 `DEBUG_NEW` ，但代码不自动使用它。 如果希望利用 `DEBUG_NEW`的好处，则必须显式使用 `DEBUG_NEW` 或 **#define new** ，如上所示。

[主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Enabling_memory_diagnostics"></a> 启用内存诊断
必须先启用诊断跟踪，然后才能使用内存诊断功能。

**启用或禁用内存诊断**

- 调用全局函数 [AfxEnableMemoryTracking](https://msdn.microsoft.com/Library/0a40e0c4-855d-46e2-9577-a8f2346f47db) 来启用或禁用诊断内存分配器。 由于默认情况下内存诊断在调试库中是打开的，所以通常会使用该函数暂时关闭内存诊断，这会提高程序执行速度并减少诊断输出。

  **使用 afxMemDF 选择特定内存诊断功能**

- 如果希望对内存诊断功能进行更精确的控制，可以通过设置 MFC 全局变量 [afxMemDF](https://msdn.microsoft.com/Library/cf117501-5446-4fce-81b3-f7194bc95086)的值，来有选择地打开和关闭单个内存诊断功能。 该变量可以具有下列值（由枚举类型 **afxMemDF**所指定）。

  |“值”|描述|
  |-----------|-----------------|
  |**allocMemDF**|打开诊断内存分配器（默认）。|
  |**delayFreeMemDF**|在调用 `delete` 或 `free` 时延迟释放内存，直到程序退出。 这将使你的程序分配可能的最大内存量。|
  |**checkAlwaysMemDF**|每次分配或释放内存时均调用 [AfxCheckMemory](/cpp/mfc/reference/diagnostic-services#afxcheckmemory) 。|

  可以通过执行逻辑 OR 操作来组合使用这些值，如下所示：

  ```C++
  afxMemDF = allocMemDF | delayFreeMemDF | checkAlwaysMemDF;
  ```

  [主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Taking_memory_snapshots"></a> 拍摄内存快照

1. 创建一个 [CMemoryState](/previous-versions/visualstudio/visual-studio-2010/2ads32e2(v=vs.100)) 对象并调用 [CMemoryState::Checkpoint](/cpp/mfc/reference/cmemorystate-structure#checkpoint) 成员函数。 这将创建第一个内存快照。

2. 在程序执行了其内存分配和释放操作以后，创建另一个 `CMemoryState` 对象，并为该对象调用 `Checkpoint` 。 这将得到内存使用的第二个快照。

3. 创建第三个 `CMemoryState` 对象，并调用其 [CMemoryState::Difference](/cpp/mfc/reference/cmemorystate-structure#difference) 成员函数，同时将前两个 `CMemoryState` 对象作为参数提供。 如果这两个内存状态之间有差异，则 `Difference` 函数将返回非零值。 这指示有些内存块尚未被释放。

    本示例显示相应的代码：

    ```cpp
    // Declare the variables needed
    #ifdef _DEBUG
        CMemoryState oldMemState, newMemState, diffMemState;
        oldMemState.Checkpoint();
    #endif

        // Do your memory allocations and deallocations.
        CString s("This is a frame variable");
        // The next object is a heap object.
        CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );

    #ifdef _DEBUG
        newMemState.Checkpoint();
        if( diffMemState.Difference( oldMemState, newMemState ) )
        {
            TRACE( "Memory leaked!\n" );
        }
    #endif
    ```

    请注意，内存检查语句由 **#ifdef _debug/#endif**块括起来，以便仅在程序的调试版本中进行编译。

    既然已经知道存在内存泄漏，便可以使用另一个成员函数 [CMemoryState::DumpStatistics](/cpp/mfc/reference/cmemorystate-structure#dumpstatistics) ，该函数将有助于对其进行定位。

    [主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Viewing_memory_statistics"></a> 查看内存统计信息
[CMemoryState::Difference](/cpp/mfc/reference/cmemorystate-structure#difference) 函数监视两个内存状态对象，并检测起始状态和结束状态之间未从堆释放的所有对象。 在拍摄内存快照并使用 `CMemoryState::Difference`对它们进行比较后，可以调用 [CMemoryState::DumpStatistics](/cpp/mfc/reference/cmemorystate-structure#dumpstatistics) 来获取有关尚未释放的对象的信息。

请看下面的示例：

```cpp
if( diffMemState.Difference( oldMemState, newMemState ) )
{
    TRACE( "Memory leaked!\n" );
    diffMemState.DumpStatistics();
}
```

从该示例得出的转储示例如下所示：

```cpp
0 bytes in 0 Free Blocks
22 bytes in 1 Object Blocks
45 bytes in 4 Non-Object Blocks
Largest number used: 67 bytes
Total allocations: 67 bytes
```

可用块是 `afxMemDF` 设置为 `delayFreeMemDF`时延迟释放的块。

第二行中显示的普通对象块仍在堆中保持分配状态。

非对象块包括通过 `new`分配的数组和结构。 在此例中，堆中分配了四个非对象块，但均未释放。

`Largest number used` 给出程序在任意时候所使用的最大内存。

`Total allocations` 给出程序所使用的内存总量。

[主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Taking_object_dumps"></a> 采用对象转储
在 MFC 程序中，可以使用[CMemoryState：:D umpallobjectssince](/cpp/mfc/reference/cmemorystate-structure#dumpallobjectssince)转储堆上尚未释放的所有对象的描述。 `DumpAllObjectsSince` 转储从最后一个 [CMemoryState::Checkpoint](/cpp/mfc/reference/cmemorystate-structure#checkpoint)。 如果未发生 `Checkpoint` 调用，则 `DumpAllObjectsSince` 将转储当前在内存中的所有对象和非对象。

> [!NOTE]
> 必须先 [启用诊断跟踪](#BKMK_Enabling_memory_diagnostics)，然后才能使用 MFC 对象转储。

> [!NOTE]
> 程序退出时 MFC 将自动转储所有泄漏的对象，因此不必创建代码在该点转储对象。

以下代码通过比较两个内存状态来测试内存泄漏，并在检测到泄漏时转储所有对象。

```cpp
if( diffMemState.Difference( oldMemState, newMemState ) )
{
    TRACE( "Memory leaked!\n" );
    diffMemState.DumpAllObjectsSince();
}
```

转储的内容如下所示：

```cmd
Dumping objects ->

{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long
{2} a CPerson at $51A4

Last Name: Smith
First Name: Alan
Phone #: 581-0215

{1} strcore.cpp(80) : non-object block at $00A7516E, 25 bytes long
```

大多数行开始处的大括号中的数字指定对象的分配顺序。 最近分配的对象具有最高编号，并显示在转储的顶部。

若要从对象转储获取最大信息量，可以重写 `Dump` 派生的任何对象的 `CObject`成员函数，以自定义对象转储。

通过将全局变量 `_afxBreakAlloc` 设置为大括号中显示的数字，可以在特定内存分配上设置断点。 如果重新运行程序，调试器将在该分配发生时中断执行。 然后可以查看调用堆栈，以了解程序是怎样到达该点的。

C 运行时库有一个类似的函数 [_CrtSetBreakAlloc](/cpp/c-runtime-library/reference/crtsetbreakalloc)，可用于 C 运行时分配。

[主题内容](#BKMK_In_this_topic)

#### <a name="BKMK_Interpreting_memory_dumps"></a> 解释内存转储
查看此对象转储的更详细信息：

```cmd
{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long
{2} a CPerson at $51A4

Last Name: Smith
First Name: Alan
Phone #: 581-0215

{1} strcore.cpp(80) : non-object block at $00A7516E, 25 bytes long
```

生成该转储的程序只有两个显式分配，一个在框架上，另一个在堆上：

```cpp
// Do your memory allocations and deallocations.
CString s("This is a frame variable");
// The next object is a heap object.
CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );
```

`CPerson` 构造函数取三个参数（指向 `char`的指针），用于初始化 `CString` 成员变量。 在内存转储中，可以看到 `CPerson` 对象以及三个非对象块（3、4 和 5）。 它们保存 `CString` 成员变量的字符，并且在调用 `CPerson` 对象析构函数时不会被删除。

块号 2 是 `CPerson` 对象本身。 `$51A4` 表示块地址，其后是对象内容，该内容在 `CPerson`DumpAllObjectsSince`Dump` 调用它时采用 [::](/cpp/mfc/reference/cmemorystate-structure#dumpallobjectssince)输出。

可以因为块号 1 的序号和大小（与框架 `CString` 变量中的字符数匹配）而猜测其与 `CString` 框架变量相关联。 框架上分配的变量在框架超出范围后自动释放。

**框架变量**

一般情况下，你不必担心与框架变量关联的堆对象，因为它们在框架变量超出范围后被自动释放。 为避免内存诊断转储混乱，应将对 `Checkpoint` 的调用定位在框架变量的范围以外。 例如，在前面的分配代码周围放置范围括号，如下所示：

```cpp
oldMemState.Checkpoint();
{
    // Do your memory allocations and deallocations ...
    CString s("This is a frame variable");
    // The next object is a heap object.
    CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );
}
newMemState.Checkpoint();
```

放置了范围括号后，该示例的内存转储如下所示：

```cmd
Dumping objects ->

{5} strcore.cpp(80) : non-object block at $00A7521A, 9 bytes long
{4} strcore.cpp(80) : non-object block at $00A751F8, 5 bytes long
{3} strcore.cpp(80) : non-object block at $00A751D6, 6 bytes long
{2} a CPerson at $51A4

Last Name: Smith
First Name: Alan
Phone #: 581-0215
```

**非对象分配**

请注意，一些分配是对象分配（如 `CPerson`），另外一些则是非对象分配。 “非对象分配”是针对不是派生自 `CObject` 的对象的分配，或者基元 C 类型（如 `char`、`int` 或 `long`）的分配。 如果 <strong>CObject</strong>派生的类分配额外的空间（例如用于内部缓冲区），则那些对象将既显示对象分配，也显示非对象分配。

**防止内存泄漏**

注意，在上面的代码中，与 `CString` 框架变量关联的内存块已自动释放，因而不作为内存泄漏显示。 与范围规则关联的自动释放负责处理与框架变量关联的大多数内存泄漏。

但对于在堆中分配的对象，则必须显式删除对象以防止内存泄漏。 若要清理上个示例中的最后一个内存泄漏，请删除堆中分配的 `CPerson` 对象，如下所示：

```cpp
{
    // Do your memory allocations and deallocations.
    CString s("This is a frame variable");
    // The next object is a heap object.
    CPerson* p = new CPerson( "Smith", "Alan", "581-0215" );
    delete p;
}
```

[主题内容](#BKMK_In_this_topic)

#### <a name="BKMK_Customizing_object_dumps"></a> 自定义对象转储
当从 [CObject](/cpp/mfc/reference/cobject-class)派生类时，在使用 `Dump` DumpAllObjectsSince [将对象转储到](/cpp/mfc/reference/cmemorystate-structure#dumpallobjectssince) “输出”窗口 [时，可以重写](../ide/reference/output-window.md)成员函数以提供附加信息。

`Dump` 函数将对象的成员变量的文本化表示形式写入转储上下文 ([CDumpContext](/cpp/mfc/reference/cdumpcontext-class))。 转储上下文类似于 I/O 流。 可以使用追加运算符 ( **<<** ) 向 `CDumpContext`。

重写 `Dump` 函数时，应先调用 `Dump` 的基类版本以转储基类对象的内容。 然后为派生类的每个成员变量输出文本化说明和值。

`Dump` 函数的声明如下所示：

```cpp
class CPerson : public CObject
{
public:
#ifdef _DEBUG
    virtual void Dump( CDumpContext& dc ) const;
#endif

    CString m_firstName;
    CString m_lastName;
    // And so on...
};
```

由于对象转储只在调试程序时有意义，所以 `Dump` 函数的声明用 **#ifdef _DEBUG / #endif** 块括起来。

在下面的示例中， `Dump` 函数先为其基类调用 `Dump` 函数。 然后，它将每个成员变量的简短说明与该成员的值一起写入诊断流。

```cpp
#ifdef _DEBUG
void CPerson::Dump( CDumpContext& dc ) const
{
    // Call the base class function first.
    CObject::Dump( dc );

    // Now do the stuff for our specific class.
    dc << "last name: " << m_lastName << "\n"
        << "first name: " << m_firstName << "\n";
}
#endif
```

必须提供 `CDumpContext` 参数以指定转储输出的目的地。 MFC 的“Debug”版本提供名为 `CDumpContext` 的预定义 `afxDump` 对象，它将输出发送到调试器。

```cpp
CPerson* pMyPerson = new CPerson;
// Set some fields of the CPerson object.
//...
// Now dump the contents.
#ifdef _DEBUG
pMyPerson->Dump( afxDump );
#endif
```

[主题内容](#BKMK_In_this_topic)

## <a name="BKMK_Reducing_the_size_of_an_MFC_Debug_build"></a> 减小 MFC 调试生成的大小
大型 MFC 应用程序的调试信息会占用大量磁盘空间。 你可以使用以下过程之一减小该大小：

1. 使用[/Z7、/zi、/zi （调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)选项而不是 **/Z7**来重新生成 MFC 库。 这些选项生成单个程序数据库 (PDB) 文件，该文件包含整个库的调试信息，减少了冗遇并节省了空间。

2. 重新生成不含调试信息的 MFC 库（无[/Z7、/zi、/zi （调试信息格式）](/cpp/build/reference/z7-zi-zi-debug-information-format)选项）。 在此情况下，缺少调试信息将妨碍你在 MFC 库代码内使用大多数调试器功能，但由于 MFC 库已完全调试，所以可能不会有问题。

3. 生成你自己的只带有选定模块的调试信息的应用程序，如下所述。

    [主题内容](#BKMK_In_this_topic)

### <a name="BKMK_Building_an_MFC_app_with_debug_information_for_selected_modules"></a> 生成带有选定模块的调试信息的 MFC 应用程序
生成带有 MFC 调试库的选定模块以后，你便可以在这些模块中使用单步执行和其他调试功能。 此过程使用项目的调试和发布配置，因此使得了以下步骤中所述的更改，并在需要完全发布版本时，还需要进行 "全部重新生成"。

1. 在“解决方案资源管理器”中，选择项目。

2. 从 **“视图”** 菜单中选定 **“属性页”** 。

3. 首先，将创建一个新的项目配置。

   1. 在“\<项目> 属性页”对话框中，单击“配置管理器”按钮。

   2. 在 [“配置管理器”对话框](/previous-versions/visualstudio/visual-studio-2010/t1hy4dhz(v=vs.100))中，在网格中定位你的项目。 在“配置”列中，选择“\<新建...>”。

   3. 在 [“新建项目配置”对话框](/previous-versions/visualstudio/visual-studio-2010/0eh8w4cf(v=vs.100))中的 **“项目配置名”** 框中键入新配置的名称，如“Partial Debug”（部分调试）。

   4. 在 **“从此处复制设置”** 列表中，选择 **“Release”** 。

   5. 单击 **"确定"** 以关闭 "**新建项目配置**" 对话框。

   6. 关闭 **“配置管理器”** 对话框。

4. 现在，将为整个项目设置选项。

   1. 在 **“属性页”** 对话框中的 **“配置属性”** 文件夹下选定 **“常规”** 类别。

   2. 在项目设置网格中展开 **“项目默认值”** （如有必要）。

   3. 在 **“项目默认值”** 下找到 **“MFC 的使用”** 。 当前设置将显示在网格的右列中。 单击当前设置并将它更改为 **“在静态库中使用 MFC”** 。

   4. 在 **“属性页”** 对话框的左窗格中，打开 **“C/C++”** 文件夹并选定 **“预处理器”** 。 在“属性”网格中找到 **“预处理器定义”** ，并用“_DEBUG”替换“NDEBUG”。

   5. 在 **“属性页”** 对话框的左窗格中，打开 **“链接器”** 文件夹并选定 **“输入”** 类别。 在“属性”网格中找到 **“附加依赖项”** 。 在 **“附加依赖项”** 设置中，键入“NAFXCWD.LIB”和“LIBCMT”。

   6. 单击 **“确定”** 以保存新的生成选项并关闭 **“属性页”** 对话框。

5. 从 **“生成”** 菜单中选定 **“重新生成”** 。 这将从模块中移除所有调试信息，但不影响 MFC 库。

6. 现在必须将调试信息添加回应用程序中的选定模块。 请记住，只能在已用调试信息编译了的模块中设置断点和执行其他调试器函数。 对于要包括调试信息的每个项目文件，执行以下步骤：

   1. 在“解决方案资源管理器”中，打开位于你的项目下的 **“源文件”** 文件夹。

   2. 选择要为其设置调试信息的文件。

   3. 从 **“视图”** 菜单中选定 **“属性页”** 。

   4. 在 **“属性页”** 对话框中的 **“配置设置”** 文件夹下，打开 **“C/C++”** 文件夹，然后选定 **“常规”** 类别。

   5. 在“属性”网格中找到 **“调试信息格式”.**

   6. 单击 **“调试信息格式”** 设置并为调试信息选择所需选项（通常为 **“/ZI”** ）。

   7. 如果要使用应用程序向导生成的应用程序或具有预编译头，则在编译其他模块以前必须关闭预编译头或重新编译预编译头。 否则，将收到警告 C4650 和错误消息 C2855。 通过更改“\<项目> 属性”对话框中的“创建/使用预编译标头”设置，可关闭预编译标头（该设置位于“配置属性”文件夹下的“C/C++”子文件夹中的“预编译标头”类别中）。

7. 从 **“生成”** 菜单中选定 **“生成”** 以重新生成已过期的项目文件。

   作为本主题中所描述技术的替换技术，可以使用外部生成文件为每个文件定义单个选项。 在这种情况下，若要链接 MFC 调试库，必须为每个模块都定义 [_DEBUG](/cpp/c-runtime-library/debug) 标志。 如果想使用 MFC 发布库，必须定义了 NDEBUG。 有关编写外部生成文件的更多信息，请参见 [NMAKE 参考](/cpp/build/running-nmake)。

   [主题内容](#BKMK_In_this_topic)

## <a name="see-also"></a>请参阅
[调试本机代码](../debugger/debugging-native-code.md)
