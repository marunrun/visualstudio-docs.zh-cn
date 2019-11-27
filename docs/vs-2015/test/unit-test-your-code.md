---
title: 单元测试代码 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio, unit tests
- unit tests, verifying code with
- testing code, automated tests
ms.assetid: c191de3e-3f3b-471e-b828-29ec24e80e2c
caps.latest.revision: 64
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8c861099ac5253c9610e8ae75d3c429a5ce88a9d
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301437"
---
# <a name="unit-test-your-code"></a>单元测试代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通过单元测试，开发人员和测试人员可以快速查找 [!INCLUDE[csharp_current_short](../includes/csharp-current-short-md.md)]、[!INCLUDE[vb_current_short](../includes/vb-current-short-md.md)] 和 [!INCLUDE[cpp_current_short](../includes/cpp-current-short-md.md)] 项目中各个类的方法中的逻辑错误。

 单元测试工具包括：

1. **测试资源管理器。** 使用“测试资源管理器”可运行单元测试并查看结果。 “测试资源管理器”可以使用任何单元测试框架，包括具有该资源管理器的适配器的第三方框架。

2. **托管代码的 Microsoft 单元测试框架。** 托管代码的 Microsoft 单元测试框架随 Visual Studio 安装并提供测试 .NET 代码的框架。

3. **C++ 的 Microsoft 单元测试框架。** C++ 的 Microsoft 单元测试框架随 Visual Studio 安装并提供测试本机代码的框架。

4. **代码覆盖率工具。** 你可以确定单元测试从“测试资源管理器”中的一个命令执行的产品代码数量。

5. **Microsoft Fakes 隔离框架。** Microsoft Fakes 隔离框架可以为创建所测试代码中的依赖关系的产品和系统代码创建替代类和方法。 通过实施函数的假委托，可以控制依赖对象的行为和输出。

   还可以使用 [IntelliTest](../test/generate-unit-tests-for-your-code-with-intellitest.md) 浏览 .NET 代码，以生成测试数据和单元测试套件。 对于代码中的每个语句，将生成执行该语句的测试输入。 为代码中的每个条件分支执行案例分析。

## <a name="key-tasks"></a>关键任务
 下面的主题可帮助你了解和创建单元测试：

|任务|相关主题|
|-----------|-----------------------|
|**快速入门和演练：** 借助以下主题从代码示例中学习 Visual Studio 中的单元测试。|-   [演练：创建并运行托管代码的单元测试](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)<br />-   [快速入门：通过测试资源管理器进行测试驱动开发](../test/quick-start-test-driven-development-with-test-explorer.md)<br />-   [向现有的 C++ 应用程序添加单元测试](../test/unit-testing-existing-cpp-applications-with-test-explorer.md)<br />-   [使用测试资源管理器对本机代码进行单元测试](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c)|
|**使用“测试资源管理器”进行单元测试：** 了解“测试资源管理器”如何帮助创建成效和效率更高的单元测试。|-   [单元测试基础](../test/unit-test-basics.md)<br />-   [创建单元测试项目](../test/create-a-unit-test-project.md)<br />-   [使用测试资源管理器运行单元测试](../test/run-unit-tests-with-test-explorer.md)<br />-   [安装第三方单元测试框架](../test/install-third-party-unit-test-frameworks.md)<br />-   [从 Visual Studio 2010 升级单元测试](https://msdn.microsoft.com/9bb75856-f68a-4de2-a084-b08a947a1172)|
|**对托管代码进行单元测试：**|-   [用 Microsoft 适用于托管代码的单元测试框架编写 .NET Framework 的单元测试](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)|
|**对 C++ 代码进行单元测试**|-   [用适用于 C++ 的 Microsoft 单元测试框架编写 C/C++ 单元测试](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)|
|**隔离单元测试**|-   [用 Microsoft Fakes 隔离测试代码](../test/isolating-code-under-test-with-microsoft-fakes.md)|
|**使用代码覆盖率确定通过单元测试进行测试的项目代码的比例：** 了解 [!INCLUDE[vsprvsts](../includes/vsprvsts-md.md)] 测试工具的代码覆盖率功能。|-   [使用代码覆盖率确定所测试的代码量](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)|
|**通过对单元测试使用负载测试来执行压力和性能分析**：可以创建负载测试并向其添加单元测试，以帮助隔离应用程序中的性能和压力问题。 **注意：** 创建和使用负载测试需要 Visual Studio Enterprise。|-   [创建和编辑负载测试](https://msdn.microsoft.com/e2985d15-60a7-4177-93b4-f986c2936337)<br />-   [如何：将 Web 性能测试和单元测试添加到负载测试方案](https://msdn.microsoft.com/03cc073e-9bdf-4530-ae46-504a51884594)<br />-   [如何：从负载测试方案中删除 Web 测试和单元测试](https://msdn.microsoft.com/3d6128d2-82b0-42fc-bda2-23a8aa03be07)|
|**设置和强制实施质量要求**：可以创建质量要求以在签入代码之前强制运行测试，从而帮助确保代码质量。|-   [设置和强制实施质量要求](https://msdn.microsoft.com/library/bdc5666e-6cf0-45b2-a0a1-133c3f61e852)|
|**扩展单元测试类型：** 可以向可能不在单元测试框架内的测试添加功能。 例如，可以添加一个指定某个测试是否应以普通用户身份运行的测试属性。 也可以扩展框架，将行特性添加到某个方法并在测试内使用该行中的数据。|有关如何扩展单元测试框架的示例代码，请参见以下 [Microsoft 网站](https://go.microsoft.com/fwlink/?LinkId=185591)。|
|**设置测试选项：** 例如，可以指定测试结果的存储位置。|[使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)|

## <a name="related-tasks"></a>相关任务
 [在 Microsoft 测试管理器中查看测试结果](https://msdn.microsoft.com/9fb3e429-78df-4fe2-89ed-0ad1db0738f4)

 介绍测试结果及其处理方法，包括如何查看、保存和删除它们。

 [使用 Microsoft Visual Studio 运行系统测试](https://msdn.microsoft.com/library/19fae5c4-5798-4c4c-b531-3e8f901b1130)

 提供指向关于使用 Visual Studio 而不是使用 [!INCLUDE[TCMext](../includes/tcmext-md.md)]来运行自动测试的信息的链接。

## <a name="reference"></a>引用
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting> 描述 UnitTesting 命名空间，该命名空间提供特性、异常、断言和其他支持单元测试的类。

 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Web> 描述 UnitTesting 命名空间，该命名空间通过提供对 [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] 和 Web 服务单元测试的支持扩展了 UnitTesting 命名空间。

## <a name="external-resources"></a>外部资源

### <a name="videos"></a>视频
 [第 9 频道：对使用 XAML 编写的 Windows 应用商店应用进行单元测试](https://go.microsoft.com/fwlink/?LinkId=226285)

### <a name="forums"></a>论坛
 [Visual Studio 单元测试](https://go.microsoft.com/fwlink/?LinkId=224477)

### <a name="guidance"></a>指导
 [使用 Visual Studio 2012 对连续交付进行测试 - 第 2 章：单元测试：测试内部](https://go.microsoft.com/fwlink/?LinkID=255188)

### <a name="reference"></a>引用
 [Content Index for Unit Tests](https://go.microsoft.com/fwlink/?LinkID=254719)（单元测试的内容索引）

## <a name="see-also"></a>请参阅
 [提高](https://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)[测试应用程序的](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)代码质量
