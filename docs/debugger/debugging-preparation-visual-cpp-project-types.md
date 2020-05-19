---
title: 准备调试 C++ 项目 | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- project templates, debugging
- C++ projects, debugging
- debug builds, project settings
- debugging [C++]
ms.assetid: 912b4ba2-7719-43d5-b087-db33e3f9329a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: dc663115e98d7553e03a186874d59b75eb68cb90
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916311"
---
# <a name="debugging-preparation-c-project-types"></a>调试准备：C++ 项目类型
本节描述如何调试用 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 项目模板创建的基本项目类型。

 请注意，那些将 DLL 作为其输出创建的项目类型由于其共同的特性已被分组到[调试 DLL 项目](../debugger/debugging-dll-projects.md)。

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> 在本主题中
 [建议的属性设置](#BKMK_Recommended_Property_Settings)

 [Win32 项目](#BKMK_Win32_Projects)

- [调试 C 或 C++ Win32 应用程序](#BKMK_To_debug_a_C_or_C___Win32_application)

- [手动设置调试配置](#BKMK_To_manually_set_a_Debug_configuration)

  [Windows 窗体应用程序 (.NET)](#BKMK_Windows_Forms_Applications___NET_)

## <a name="recommended-property-settings"></a><a name="BKMK_Recommended_Property_Settings"></a>建议的属性设置
 应以相同的方式设置所有非托管调试方案的某些属性。 以下各表显示了建议的属性设置。 未在此处列出的设置可能有各种不同的非托管项目类型。 有关详细信息，请参阅 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

### <a name="configuration-properties-124-cc-124-optimization-node"></a>配置属性 &#124; C/C++ &#124; 优化节点

|属性名|设置|
|-------------------|-------------|
|**优化**|设置为“禁用(/0d)”。 优化代码更难调试，因为生成的指令与源代码并不直接对应。 如果发现程序具有只出现在优化代码中的 bug，则可以打开此设置，但应记住“反汇编”窗口中显示的代码是从可能与在源窗口中见到的内容不匹配的优化源生成的。 其他功能（如单步执行）可能不会像预期的那样执行。|

### <a name="configuration-properties-124-linker-124-debugging-node"></a>配置属性 &#124; 链接器 &#124; 调试节点

|属性名|设置|
|-------------------|-------------|
|**生成调试信息**|应始终将此选项设置为“是(/DEBUG)”以创建调试所需的调试符号和文件。 在应用程序进入成品阶段时，可以将其设置为关闭。|

 [在本主题中](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)

## <a name="win32-projects"></a><a name="BKMK_Win32_Projects"></a>Win32 项目
 Win32 应用程序是用 C 或 C++ 编写的传统 Windows 程序。 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中调试此类应用程序非常简单。

 Win32 应用程序包括 MFC 应用程序和 ATL 项目。 Win32 应用程序使用 Windows API，也可使用 MFC 或 ATL，但不使用公共语言运行时 (CLR)。 但是，它们可以调用使用 CLR 的托管代码。

 下面的过程解释如何在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中调试 Win32 项目。 调试 Win32 应用程序的另一种方法是在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 之外启动并附加到该应用程序。 有关详细信息，请参阅[附加到运行中的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

### <a name="to-debug-a-c-or-c-win32-application"></a><a name="BKMK_To_debug_a_C_or_C___Win32_application"></a>调试 C 或 C++ Win32 应用程序

1. 在 Visual Studio 中打开项目。

2. 在“调试”菜单上选择“启动” 。

3. 使用 [初步了解调试器](../debugger/debugger-feature-tour.md) 中讨论的技术进行调试。

### <a name="to-manually-set-a-debug-configuration"></a><a name="BKMK_To_manually_set_a_Debug_configuration"></a>手动设置调试配置

1. 在“视图”菜单上，单击“属性页” 。

2. 如果“配置属性”节点尚未打开，则单击以打开该节点

3. 选择“常规”，并将“输出”行的值设置为“调试”  。

4. 打开“C/C++”节点，然后选择“常规” 。

    在“调试”行指定要由编译器生成的调试信息的类型。 可以选择的值包括“程序数据库(/Zi)”或“用于‘编辑并继续’的程序数据库(/ZI)” 。

5. 选择“优化”，然后在“优化”行的下拉列表中选择“禁用(/0d)”  。

    优化代码更难调试，因为生成的指令与源代码并不直接对应。 如果发现程序具有只出现在优化代码中的 bug，则可以打开此设置，但应记住“反汇编”窗口中显示的代码是从可能与在源窗口中见到的内容不匹配的优化源生成的。 有些功能（如单步执行）显示的断点和执行点有可能不正确。

6. 打开“链接器”节点，然后选择“调试” 。 在第一个“常规”行的下拉列表中，选择“是(/DEBUG)” 。 调试期间应始终这样设置。

   有关详细信息，请参阅 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

   [在本主题中](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)

## <a name="windows-forms-applications-net"></a><a name="BKMK_Windows_Forms_Applications___NET_"></a>Windows 窗体应用程序 (.NET)
 “Windows 窗体应用程序 (.NET)”模板可创建 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)]Windows 窗体应用程序。 有关详细信息，请参阅[如何：创建一个 Windows 应用程序项目](/previous-versions/visualstudio/visual-studio-2010/42wc9kk5(v=vs.100))。

 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中调试此类应用程序类似于在托管的 Windows 窗体应用程序中进行调试。

 用项目模板创建 Windows 窗体项目时，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 将自动为调试和发布配置创建所需的设置。 如有必要，可在“\<项目名称> 属性页”对话框中更改这些设置。 有关详细信息，请参阅[调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)。

 有关详细信息，请参阅 [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)。

 调试 Windows 窗体应用程序的另一种方法是从 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 外部启动应用程序并附加到它上面。 有关详细信息，请参阅[附加到正在运行的程序或多个程序](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)。

 [在本主题中](../debugger/debugging-preparation-visual-cpp-project-types.md#BKMK_In_this_topic)

## <a name="see-also"></a>请参阅
- [初探调试器](../debugger/debugger-feature-tour.md)
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)
- [附加到正在运行的程序或多个程序](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
- [调试和发布配置](../debugger/how-to-set-debug-and-release-configurations.md)
- [如何：创建一个 Windows 应用程序项目](/previous-versions/visualstudio/visual-studio-2010/42wc9kk5(v=vs.100))