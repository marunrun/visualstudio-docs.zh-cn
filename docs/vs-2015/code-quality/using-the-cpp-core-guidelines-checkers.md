---
title: 使用C++核心准则检查 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: a2098fd9-8334-4e95-9b8d-bc3da689d9e3
caps.latest.revision: 11
author: mikeblome
ms.author: mblome
manager: jillfra
ms.openlocfilehash: ccc44b77c4524e7d707ce3fe407d204d729017ff
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74291240"
---
# <a name="using-the-c-core-guidelines-checkers"></a>使用 C++ 核心准则检查程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C++核心指导原则是有关C++专家和设计人员所C++创建的编码的一组可移植指导原则、规则和最佳实践。  Visual Studio 现在支持外接程序包，这些包可为代码分析工具创建其他规则，以检查代码是否符合C++核心准则和建议改进。  
  
## <a name="the-c-core-guidelines-project"></a>C++核心准则项目  
 由 Bjarne Stroustrup 和其他人创建， C++核心准则是使用新式C++安全有效的指南。 这些指南强调了静态类型安全和资源安全性。 它们确定了消除或最小化语言中最容易出错的部分的方法，并建议如何以可靠的方式使代码更简单、更具性能。 这些准则由标准C++基础维护。 若要了解详细信息，请参阅[GitHub](https://github.com/isocpp/CppCoreGuidelines)上的文档、 [ C++核心准则](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)和访问C++核心准则文档项目文件。  
  
 Microsoft 通过生成C++ C++可使用 Nuget 包添加到项目的核心检查代码分析规则集来支持核心准则工作。 此包的名称为 CppCoreCheck，可[https://www.nuget.org/packages/Microsoft.CppCoreCheck](https://www.nuget.org/packages/Microsoft.CppCoreCheck)。 此程序包需要至少安装了 Visual Studio 2015 Update 1。  
  
 该包还会安装另一个包作为依赖项，即仅标头的准则支持库（GSL）。 [https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL)上还提供了 GitHub 上的 GSL。  
  
## <a name="enable-the-c-core-check-guidelines-in-code-analysis"></a>启用代码C++分析中的核心检查指南  
 若要启用C++核心检查代码分析工具，请将 CppCoreCheck NuGet 包安装到要在C++ Visual Studio 中检查的每个项目。  
  
#### <a name="to-add-the-microsoftcppcorecheck-package-to-your-project"></a>将 CppCoreCheck 包添加到项目中  
  
1. 在**解决方案资源管理器**中，右键单击以打开要将包添加到的解决方案中项目的上下文菜单。 选择 "**管理 Nuget 包**"，打开**NuGet 包管理器**。  
  
2. 在 " **NuGet 包管理器**" 窗口中，搜索 CppCoreCheck。  
  
    !["Nuget 包管理器" 窗口显示 CppCoreCheck 包](../code-quality/media/cppcorecheck-nuget-window.PNG "CPPCoreCheck_Nuget_Window")  
  
3. 选择 CppCoreCheck 包，然后选择 "**安装**" 按钮，将规则添加到项目。  
  
   在项目中启用代码分析后，NuGet 包会向项目添加一个附加的 MSBuild 文件。 此 .targets 文件将C++核心检查规则作为附加扩展添加到 Visual Studio 代码分析工具。  
  
   可以通过在项目的 "**属性页**" 对话框的 "**代码分析**" 部分中选择 "**生成时启用代码分析**" 复选框，对项目启用代码分析。  
  
   ![代码分析常规设置的属性页](../code-quality/media/cppcorecheck-codeanalysis-general.png "CPPCoreCheck_CodeAnalysis_General")  
  
   C++核心检查规则成为启用代码分析时运行的默认规则集的一部分。 由于C++核心检查规则正在开发中，某些规则可能无法在所有代码上使用，但可能会在开发过程中提供信息。 这些规则作为实验性发布。 你可以选择是在项目的属性中运行已发布规则还是实验性规则。  
  
   ![代码分析扩展插件设置的属性页](../code-quality/media/cppcorecheck-codeanalysis-extensions.png "CPPCoreCheck_CodeAnalysis_Extensions")  
  
   若要启用或禁用C++核心检查规则集，请打开项目的 "**属性页**" 对话框。 在 "**配置属性**" 下，展开 "**代码分析**" 和 "**扩展**"。 在 "**启用C++核心检查（已发布）** " 或 "  **C++启用核心检查（实验）** " 旁边的下拉列表中，选择 **"是" 或 "** **否**"。 选择 **"确定" 或 "** **应用**" 保存更改。  
  
## <a name="check-types-bounds-and-lifetimes"></a>检查类型、边界和生存期  
 C++核心检查包当前包含[类型安全](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-type)、[边界安全](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-bounds)和[生存期安全](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#SS-lifetime)配置文件的检查程序。  
  
 下面是C++核心检查规则可以发现的问题类型的示例：  
  
```cpp  
// CoreCheckExample.cpp  
// Add CppCoreCheck package and enable code analysis in build for warnings.  
  
int main()  
{  
    int arr[10];           // warning C26494  
    int* p = arr;          // warning C26485  
  
    [[gsl::suppress(bounds.1)]] // This attribute suppresses Bounds rule #1  
    {  
        int* q = p + 1;    // warning C26481 (suppressed)  
        p = q++;           // warning C26481 (suppressed)  
    }  
  
    return 0;  
}  
```  
  
 此示例演示C++核心检查规则可以发现的几个警告：  
  
- C26494 是规则类型。5：始终初始化对象。  
  
- C26485 是规则界限。3：没有数组到指针的衰减。  
  
- C26481 是规则界限。1：不要使用指针算法。 请改用 `span` 。  
  
  如果编译C++此代码时安装并启用了核心检查代码分析规则集，则会输出前两个警告，但会禁止显示第三个警告。 下面是示例代码的生成输出：  
  
**1 >------已启动生成：项目： CoreCheckExample，配置： Debug Win32--**  
**----**  
**1 > CoreCheckExample .cpp**  
**1 > CoreCheckExample .vcxproj-> C:\Users\username\documents\visual studio 2015 \ P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.exe**  
**1 > CoreCheckExample .vcxproj-> C:\Users\username\documents\visual studio 2015 \ P**  
**rojects\CoreCheckExample\Debug\CoreCheckExample.pdb （完整 PDB）**  
**c:\users\username\documents\visual studio 2015 \ projects\corecheckexample\coreche**  
**ckexample\corecheckexample.cpp （6）： warning C26494：变量 "arr" 为 uninitializ**  
**ed。始终初始化一个对象。（类型为5： https://go.microsoft.com/fwlink/p/?Link**  
**ID = 620421）**  
**c:\users\username\documents\visual studio 2015 \ projects\corecheckexample\coreche**  
**ckexample\corecheckexample.cpp （7）： warning C26485： Expression "arr"：无数组到**  
**指针衰减。（边界：3： https://go.microsoft.com/fwlink/p/?LinkID=620415)**  
= = = = = = = = = = =**生成：1成功，0失败，0最新，0已跳过 =** = = = = = = = = =C++核心准则可帮助您编写更好和更安全的代码。 但是，如果你有一个不应应用规则或配置文件的实例，则可以轻松地直接在代码中将其取消。 你可以使用 `gsl::suppress` 特性来防止C++核心检查检测和报告以下代码块中的任何规则冲突。 您可以标记各个语句以禁止显示特定规则。 甚至可以通过编写 `[[gsl::suppress(bounds)]]` 来禁止整个边界配置文件，而无需包含特定的规则号。  
  
## <a name="use-the-guideline-support-library"></a>使用准则支持库  
 CppCoreCheck NuGet 包还会安装一个包，其中包含 Microsoft 的准则支持库（GSL）的实现。 GSL 在[http://www.nuget.org/packages/Microsoft.Gsl](https://www.nuget.org/packages/Microsoft.Gsl)也以独立形式提供。 如果要遵循核心准则，此库将非常有用。 GSL 包括一些定义，使你可以用更安全的替代方法替换容易出错的构造。 例如，您可以使用 `span<T>` 类型替换 `T*, length` 参数对。 GSL 是开源的，因此，如果想要查看库源、评论或贡献，可以在[https://github.com/Microsoft/GSL](https://github.com/Microsoft/GSL)找到该项目。
