---
title: 受支持的代码更改 (C++) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Edit and Continue, limitations
- supported code changes
- object files, limitations of Edit and Continue
- C++ language, supported code changes
- coding, supported code changes
- resource files, limitations of Edit and Continue
- code changes, handling in Edit and Continue
- what's new [C++], supported code changes
- code changes
ms.assetid: f5754363-8a56-417b-b904-b05d9dd26d03
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f167b3e9d27145284defa2ff491bb9ce0085f2a3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684915"
---
# <a name="supported-code-changes-c"></a>受支持的代码更改 (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual C++ 的“编辑并继续”处理大多数类型的代码更改。 但是，在程序执行期间，某些更改无法应用。 若要应用这些更改，您必须停止执行并生成新版本的代码。  
  
 有关在 Visual Studio 中使用 C++ 编辑并继续的信息，请参阅 [Edit and Continue (Visual C++)](../debugger/edit-and-continue-visual-cpp.md) 。  
  
## <a name="unsupported-changes"></a><a name="BKMK_Unsupported_changes"></a> 不支持的更改  

在调试会话期间，不能应用下列 C/C++ 更改：  
  
- 对全局或静态数据的大多数更改。  
  
- 对从其他计算机复制并且未在本地生成的可执行文件的更改。  
  
- 对影响对象（如类的数据成员）的布局的数据类型的更改。  
  
- 添加 64k 字节以上的新代码或数据。  
  
- 添加要求在指令指针前存在构造函数的变量。  
  
- 影响需要运行时初始化的代码的更改。  
  
- 在某些实例中，添加异常处理程序。  
  
- 对资源文件的更改。  
  
- 对只读文件中的代码的更改。  
  
- 对没有相应的 PDB 文件的代码的更改。  
  
- 对没有对象文件的代码的更改。  
  
如果进行了上面某项更改，然后尝试应用代码更改，则 **“输出”** 窗口中会出现错误或警告消息。  
  
- “编辑并继续”不更新静态库。 如果您更改了静态库，则会继续执行老版本，且不发出任何警告。  
  
## <a name="unsupported-scenarios"></a><a name="BKMK_Unsupported_scenarios"></a> 不支持的方案  
 在以下调试方案中，C/C++ 的“编辑并继续”不可用：  
  
- 调试使用 [/Zo（增强优化调试）](https://msdn.microsoft.com/library/eea8d89a-7fe0-4fe1-86b2-7689bbebbd7f)编译的本机应用  
  
- 在 Visual Studio 2015 Update 1 之前的 Visual Studio 版本中，调试 Windows 应用商店应用或组件。 从 Visual Studio 2015 Update 1 开始，便可在 Windows 应用商店 C++ 应用和 DirectX 应用中使用“编辑并继续”，因为它现在支持 `/ZI` 编译器开关与  `/bigobj` 开关。 你还可以使用具有二进制文件（使用 `/FASTLINK` 开关。  
  
- 在 Windows 98 上进行调试。  
  
- 混合模式（本机/托管）调试。  
  
- Javascript 调试。  
  
- SQL 调试。  
  
- 调试转储文件。  
  
- 在未选择 **“在未经处理的异常上展开调用堆栈”** 选项的情况下，在发生未经处理的异常之后编辑代码。  
  
- 使用 **连接到** 来调试应用程序，而不是选择 **调试** 菜单上的 **开始** 来运行应用程序。  
  
- 调试优化后的代码。  
  
- 如果由于生成错误无法生成新版本的代码，则对旧版本的代码进行调试。  
  
## <a name="linking-limitations"></a><a name="BKMK_Linking_limitations"></a> 链接限制  
  
### <a name="linker-options-that-disable-edit-and-continue"></a><a name="BKMK_Linker_options_that_disable_Edit_and_Continue"></a> 禁用“编辑并继续”的链接器选项  
 下列链接器选项可禁用“编辑并继续”：  
  
- 设置 **/OPT:REF**、 **/OPT:ICF**或 **/INCREMENTAL:NO** 将禁用“编辑并继续”并发出以下警告：  
  
     LINK : warning LNK4075: ignoring /EDITANDCONTINUE due to /OPT  
  
     specification  
  
- 设置 **/ORDER**、 **/RELEASE**或 **/FORCE** 将禁用“编辑并继续”并发出以下警告：  
  
     LINK : warning LNK4075: ignoring /INCREMENTAL due to /option  
  
     specification  
  
- 设置任何禁止创建程序数据库 (.pdb) 文件的选项都会禁用“编辑并继续”，但不给出任何特定警告。  
  
### <a name="auto-relinking-limitations"></a><a name="BKMK_Auto_relinking_limitations"></a> 自动重新链接限制  
 默认情况下，“编辑并继续”在调试会话结束时重新链接到程序，以创建最新的可执行文件。  
  
 如果正在从原始生成位置以外的位置调试，“编辑并继续”不能重新链接程序。 有消息通知您需要手动重新生成。  
  
 “编辑并继续”不重新生成静态库。 如果使用“编辑并继续”更改静态库，需要使用“编辑并继续”手动重新生成库并重新链接应用程序。  
  
 “编辑并继续”不调用自定义生成步骤。 如果程序使用自定义生成步骤，则可能要手动重新生成这些步骤才能调用它们。 在这种情况下，可以在“编辑并继续”后禁用重新链接，以确保系统会提示您手动重新生成。  
  
 **在“编辑并继续”之后禁用重新链接**  
  
1. 在 **“调试”** 菜单上，选择 **“选项和设置”** 。  
  
2. 在 **选项** 对话框中，在 **调试** 节点下，选择 **编辑并继续** 节点。  
  
3. 清除 **“调试后重新链接代码更改”** 复选框。  
  
## <a name="precompiled-header-limitations"></a><a name="BKMK_Precompiled_Header_Limitations"></a> 预编译头限制  
 默认情况下，“编辑并继续”在后台加载并处理预编译头，以加速对代码更改的处理。 加载预编译头需要分配物理内存，如果您正在一台 RAM 有限的计算机上进行编译，这可能会是一个问题。 在调试时，您可以使用 Windows 任务管理器来确定可用的物理内存量，以确定这是否可能有问题。 如果此数量大于预编译头的大小，则“编辑并继续”应没有问题。 如果此数量小于预编译头的大小，可以禁止“编辑并继续”在后台加载预编译头。  
  
 **对“编辑并继续”禁用预编译头的后台加载**  
  
1. 在 **“调试”** 菜单上，选择 **“选项和设置”** 。  
  
2. 在 **选项** 对话框中，在 **调试** 节点下，选择 **编辑并继续** 节点。  
  
3. 清除 **“允许预编译”** 复选框。  
  
## <a name="idl-attribute-limitations"></a><a name="BKMK_IDL_Attribute_Limitations"></a> IDL 特性限制  
 “编辑并继续”不重新生成接口定义 (IDL) 文件。 因此，调试时不反映对 IDL 特性的更改。 若要查看对 IDL 特性更改的结果，必须停止调试并重新生成应用程序。 如果 IDL 特性已更改，“编辑并继续”不生成错误或警告。 有关更多信息，请参见 [IDL 特性](https://msdn.microsoft.com/library/04c596f4-c97b-4952-8053-316678b1d0b6)。  
  
## <a name="see-also"></a>另请参阅  
 [编辑并继续 (Visual C++) ](../debugger/edit-and-continue-visual-cpp.md)
