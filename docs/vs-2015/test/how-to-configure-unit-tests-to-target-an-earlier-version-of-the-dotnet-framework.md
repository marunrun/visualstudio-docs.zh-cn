---
title: 如何：配置单元测试以面向 .NET Framework 的早期版本 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: adb6c011-5abd-41d2-8ead-08cd7579bf37
caps.latest.revision: 14
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: fd212eb304e6cba022b067b8b432cf00fc3f87ba
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660536"
---
# <a name="how-to-configure-unit-tests-to-target-an-earlier-version-of-the-net-framework"></a>如何：配置单元测试以面向 .NET Framework 的早期版本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Microsoft Visual Studio 中创建测试项目时，默认将 .NET Framework 的最新版本设为要面向的版本。 此外，如果从 Visual Studio 的早期版本升级测试项目，那么它们将被升级为面向 .NET Framework 的最新版本。 通过编辑项目属性，可以显式使项目重新面向 .NET Framework 的早期版本。

 可以创建面向 .NET Framework 的特定版本的单元测试项目。 所面向的版本必须为 3.5 或更高版本，并且不能为客户端版本。 Visual Studio 为面向特定版本的单元测试启用了以下基本支持：

- 可以创建单元测试项目，并使它们面向 .NET Framework 的特定版本。

- 可以在本地计算机上的 Visual Studio 中运行面向特定版本的 .NET Framework 的单元测试。

- 可以使用 MSTest.exe 从命令提示符处运行面向特定版本的 .NET Framework 的单元测试。

- 作为生成的一部分，可以在生成代理上运行单元测试。

  **测试 SharePoint 应用程序**

  上面列出的功能还支持使用 Visual Studio 为 SharePoint 应用程序编写单元测试和集成测试。 [!INCLUDE[crabout](../includes/crabout-md.md)]如何使用 Visual Studio 开发 SharePoint 应用程序，请参阅[创建 SharePoint 解决方案](https://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)、[生成和调试 SharePoint 解决方案](https://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae)和[验证和调试 SharePoint 代码](https://msdn.microsoft.com/library/b5f3bce2-6a51-41b1-a292-9e384bae420c)。

  **限制**

  将测试项目重新面向为使用早期版本的 .NET Framework 时，存在以下限制：

- 在 .NET Framework 3.5 中，只包含单元测试的测试项目支持多面向。 .NET Framework 3.5 不支持任何其他测试类型，如编码的 UI 测试或负载测试。 除了单元测试，其他测试类型均不支持重新面向。

- 仅默认的主机适配器支持面向 .NET Framework 的早期版本的测试的执行。 ASP.NET 主机适配器不支持。 需要在 ASP.NET 开发服务器环境中运行的 ASP.NET 应用程序必须与 .NET Framework 的当前版本兼容。

- 运行支持 .NET Framework 3.5 多面向的测试时，将禁用数据收集支持。 可以使用 Visual Studio 命令行工具来运行代码覆盖率。

- 无法在远程计算机上运行使用 .NET Framework 3.5 的单元测试。

- 无法使单元测试面向早期客户端版本的框架。

### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-basic-unit-test-projects"></a>针对 Visual Basic 单元测试项目重定目标为特定版本的 .NET Framework

1. 创建一个新的 Visual Basic 单元测试项目。 在“文件”菜单上选择“新建”，再选择“项目”。

     随即显示“新建项目”对话框。

2. 在“已安装的模板”下面展开“Visual Basic”。 选择“测试”，然后选择“测试项目”模板。

3. 在“名称”框中，键入 Visual Basic 测试项目名称，然后选择“确定”。

4. 在解决方案资源管理器中，从新的 Visual Basic 测试项目的快捷菜单中选择“属性”。

     随即显示 Visual Basic 测试项目的属性。

5. 在“编译”选项卡上选择“高级编译选项”，如下图所示。

     ![高级编译选项](../test/media/howtoconfigureunittest35frameworka.png "HowToConfigureUnitTest35FrameworkA")

6. 使用“目标框架 (所有配置)”下拉列表，将目标框架更改为 **.NET Framework 3.5**或更高版本，如下图中的标注 B 所示。 不应指定客户端版本。

     !["目标框架&#45;" 下拉列表](../test/media/howtoconfigureunitest35frameworkstepb.png "HowToConfigureUniTest35FrameworkStepB")

### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-visual-c-unit-test-projects"></a>针对 Visual C# 单元测试项目重定目标为特定版本的 .NET Framework

1. 创建一个新的 Visual C# 单元测试项目。 在“文件”菜单上选择“新建”，再选择“项目”。

     随即显示“新建项目”对话框。

2. 在“已安装的模板”下面展开“Visual C#”。 选择“测试”，然后选择“测试项目”模板。

3. 在“名称”文本框中，键入 Visual C# 测试项目名称，然后选择“确定”。

4. 在解决方案资源管理器中，从新的 Visual C# 测试项目的快捷菜单中选择“属性”。

     随即显示 Visual C# 测试项目的属性。

5. 在“应用程序”选项卡上选择“目标框架”，然后从下拉列表中选择“.NET Framework 3.5”或更高版本，以更改目标框架，如下图所示。 不应指定客户端版本。

     !["目标框架&#45;" 下拉列表](../test/media/howtoconfigureunittest35frameworkcsharp.png "HowToConfigureUnitTest35FrameworkCSharp")

### <a name="re-targeting-to-a-specific-version-of-the-net-framework-for-ccli-unit-test-projects"></a>针对 C++/CLI 单元测试项目重定目标为特定版本的 .NET Framework

1. 创建一个新的 C++ 单元测试项目。 在“文件”菜单上，选择“新建” ，然后单击“项目”。

     随即显示“新建项目”对话框。

    > [!WARNING]
    > 若要为以前版本的适用于 Visual C++ 的 .NET Framework 生成 C++/CLI 单元测试，则必须使用相应版本的 Visual Studio。 例如，若要面向 .NET Framework 3.5，必须安装 [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] 和 [!INCLUDE[vs_orcas_long](../includes/vs-orcas-long-md.md)] Service Pack 1。

2. 在“已安装的模板”下面展开“Visual C++”。 选择“测试”，然后选择“测试项目”模板。

3. 在“名称”文本框中，键入 Visual C++ 测试项目名称，然后选择“确定”。

4. 在解决方案资源管理器中，从新的 Visual C++ 测试项目中选择“卸载项目”。

5. 在解决方案资源管理器中，选择已卸载的 Visual C++ 测试项目，然后选择“编辑\<项目名称>.vcxproj”。

     即可在编辑器中打开 .vcxproj 文件。

6. 在标记为`"Globals"`的 `PropertyGroup` 中将 `TargetFrameworkVersion` 设为版本 3.5 或更高版本。 不应指定客户端版本：

    ```
    <PropertyGroup Label="Globals">
        <TargetName>DefaultTest</TargetName>
        <ProjectTypes>{3AC096D0-A1C2-E12C-1390-A8335801FDAB};{8BC9CEB8-8B4A-11D0-8D11-00A0C91BC942}</ProjectTypes>
        <ProjectGUID>{CE16D77A-E364-4ACD-948B-1EB6218B0EA3}</ProjectGUID>
        <TargetFrameworkVersion>3.5</TargetFrameworkVersion>
        <Keyword>ManagedCProj</Keyword>
        <RootNamespace>CPP_Test</RootNamespace>
      </PropertyGroup>

    ```

7. 保存并关闭 .vcxproj 文件。

8. 在解决方案资源管理器中，从新的 Visual C++ 测试项目的快捷菜单中选择“重载项目”。

## <a name="see-also"></a>请参阅
 [为现有代码创建和运行单元测试](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173)[创建 sharepoint 解决方案](https://msdn.microsoft.com/library/4bfb1e59-97c9-4594-93f8-3068b4eb9631)"[生成和调试 Sharepoint 解决方案](https://msdn.microsoft.com/library/c9e7c9ab-4eb3-40cd-a9b9-6c2a896f70ae)[高级编译器设置" 对话框（Visual Basic）](../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md)
