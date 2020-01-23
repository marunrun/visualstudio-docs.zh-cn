---
title: 为项目和 NuGet 包取消显示编译器警告
ms.date: 01/24/2018
ms.technology: vs-ide-compile
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b604f6a1392353d304897a233b74c0d81fc258df
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76114509"
---
# <a name="how-to-suppress-compiler-warnings"></a>如何：取消编译器警告

通过筛选出一个或多个类型的编译器警告，可以整理一个生成日志。 例如，可能只想查看在将生成日志详细信息设置为“正常”、“详细信息”或“诊断”时生成的某些输出    。 有关详细程度的详细信息，请参见[如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)。

## <a name="suppress-specific-warnings-for-visual-c-or-f"></a>取消显示特定的 Visual C# 或 F\# 警告

使用“生成”  属性页可取消显示特定的 C# 和 F# 项目警告。

1. 在**解决方案资源管理器**中，选择想要取消显示警告的项目。

1. 在菜单栏上，依次选择“查看”   > “属性页”  。

1. 选择“生成”页。 

1. 在“取消显示警告”  框中，指定想要取消显示的警告的错误代码，使用分号分隔。

1. 重新生成解决方案。

## <a name="suppress-specific-warnings-for-c"></a>取消显示特定的 C++ 警告

使用“配置属性”  属性页可取消显示特定的 C++ 项目警告。

1. 在**解决方案资源管理器**中，选择想要取消显示警告的项目或源文件。

1. 在菜单栏上，依次选择“查看”   > “属性页”  。

1. 依次选择“配置属性”  类别、“C/C++”  类别和“高级”  页。

1. 执行以下步骤之一：

    - 在“禁用特定警告”  框中，指定想要取消显示的警告的错误代码，并使用分号分隔。

    - 在“禁用特定警告”  框中，选择“编辑”  以显示更多选项。

1. 选择“确定”按钮，然后重新生成解决方案。 

## <a name="suppress-warnings-for-visual-basic"></a>取消显示 Visual Basic 警告

可以通过编辑项目的 .vbproj  文件，隐藏 Visual Basic 的特定编译器警告。 若要按“类别”  取消显示警告，可以使用[编译属性页](../ide/reference/compile-page-project-designer-visual-basic.md)。 有关详细信息，请参阅[在 Visual Basic 中配置警告](../ide/configuring-warnings-in-visual-basic.md)。

### <a name="to-suppress-specific-warnings-for-visual-basic"></a>要取消显示特定的 Visual Basic 警告

此示例演示如何编辑 .vbproj  文件以取消显示特定的编译器警告。

1. 在**解决方案资源管理器**中，选择想要取消显示警告的项目。

1. 在菜单栏上，依次选择“项目”   > “卸载项目”  。

1. 在“解决方案资源管理器”中，打开项目的右键单击菜单或快捷菜单，然后选择“编辑 \<ProjectName>.vbproj”   。

    该 XML 项目文件将在代码编辑器中打开。

1. 找到正在生成的用于生成配置的 `<NoWarn>` 元素，并添加一个或多个警告编号作为 `<NoWarn>` 元素的值。 如果指定多个警告编号，请使用逗号分隔。

     以下示例显示了在 x86 平台上的“调试”  生成配置的 `<NoWarn>` 元素，其中取消显示了两个编译器警告：

    ```xml
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
        <PlatformTarget>x86</PlatformTarget>
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineDebug>true</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <ErrorReport>prompt</ErrorReport>
        <NoWarn>40059,42024</NoWarn>
        <WarningLevel>1</WarningLevel>
      </PropertyGroup>
    ```

   > [!NOTE]
   > 在默认情况下，.NET Core 项目不包含生成配置属性组。 若要取消显示 .NET Core 项目中的警告，请将生成配置部分手动添加到文件。 例如：
   >
   > ```xml
   > <Project Sdk="Microsoft.NET.Sdk">
   >   <PropertyGroup>
   >     <OutputType>Exe</OutputType>
   >     <TargetFramework>netcoreapp2.0</TargetFramework>
   >     <RootNamespace>VBDotNetCore_1</RootNamespace>
   >   </PropertyGroup>
   >   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
   >     <NoWarn>42016,41999,42017</NoWarn>
   >   </PropertyGroup>
   > </Project>
   > ```

1. 保存对 .vbproj  文件所做的更改。

1. 在菜单栏上，依次选择“项目”   > “重载项目”  。

1. 在菜单栏上，依次选择“生成”   > “重新生成解决方案”  。

    “输出”窗口不再显示指定的警告。 

有关详细信息，请参阅 Visual Basic 命令行编译器的 [/nowarn 编译器选项](/dotnet/visual-basic/reference/command-line-compiler/nowarn)。

## <a name="suppress-warnings-for-nuget-packages"></a>取消显示 NuGet 包警告

在某些情况下，你可能希望取消显示单个 NuGet 包的 NuGet 编译器警告（而不是整个项目）。 警告是有意义的，因此，你不希望在项目级别取消显示它。 例如，其中的一个 NuGet 警告告诉你，这个包可能不完全兼容与你的项目。 如果在项目级别取消显示该警告并稍后添加其他 NuGet 包，则将永远无法了解它是否会生成兼容性警告。

### <a name="to-suppress-a-specific-warning-for-a-single-nuget-package"></a>取消显示单个 NuGet 包的特定警告

1. 在解决方案资源管理器  中，选择想要为其取消显示编译器警告的 NuGet 包。

   ![解决方案资源管理器中的 NuGet 包](media/nuget-package-with-warning.png)

1. 在右键菜单或上下文菜单中，选择“属性”  。

1. 在包属性的“NoWarn”  框中，输入想要为此包取消显示的警告编号。 如果想要取消显示多个警告，请使用逗号分隔警告编号。

   ![NuGet 包属性](media/nuget-properties-nowarn.png)

   警告已从解决方案资源管理器  和错误列表  消失。

## <a name="see-also"></a>请参阅

- [演练：构建应用程序](../ide/walkthrough-building-an-application.md)
- [如何：查看、保存和配置生成日志文件](../ide/how-to-view-save-and-configure-build-log-files.md)
- [编译和生成](../ide/compiling-and-building-in-visual-studio.md)
