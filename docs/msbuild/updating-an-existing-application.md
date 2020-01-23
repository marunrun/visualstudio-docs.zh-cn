---
title: 将现有的应用程序更新到 MSBuild 15 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8d4e7d84768307964b495e8c5e97e7731b0622a1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75597134"
---
# <a name="update-an-existing-application-for-msbuild-15"></a>将现有的应用程序更新到 MSBuild 15

在 15.0 之前的 MSBuild 版本中，是从全局程序集缓存 (GAC) 加载 MSBuild ，并在注册表中安装 MSBuild 扩展的。 这样确保了所有应用程序使用相同版本的 MSBuild 和访问相同的工具集，但阻止了 Visual Studio 不同版本的并行安装。

为支持更快、更小的并行安装，Visual Studio 2017 及更高版本不再将 MSBuild 放置在 GAC 中或修改注册表。 遗憾的是，这意味着希望使用 MSBuild API 评估或生成项目的应用程序不能隐式依赖于 Visual Studio 安装。

## <a name="use-msbuild-from-visual-studio"></a>从 Visual Studio 使用 MSBuild

为确保以编程方式从应用程序生成的项目与 Visual Studio 或 MSBuild.exe 中生成的项目相匹配，请从 Visual Studio 加载 MSBuild 程序集，并使用 Visual Studio 中提供的 SDK。  Microsoft.Build.Locator NuGet 包简化了这一过程。

## <a name="use-microsoftbuildlocator"></a>使用 Microsoft.Build.Locator

如果将 Microsoft.Build.Locator.dll  与应用程序一起重新分发，则无需分发其他 MSBuild 程序集。

若要更新项目以使用 MSBuild 15 和定位符 API，需要对项目进行一些更改，如下所述。 若要查看更新项目所需更改的示例，请参阅[在 MSBuildLocator 存储库中对示例项目进行的提交](https://github.com/Microsoft/MSBuildLocator/commits/example-updating-to-msbuild-15)。

### <a name="change-msbuild-references"></a>更改 MSBuild 引用

为确保从中心位置加载 MSBuild，请勿将其程序集与应用程序一起分发。

更改项目以避免从中心位置加载 MSBuild 的机制取决于引用 MSBuild 的方式。

#### <a name="use-nuget-packages-preferred"></a>使用 NuGet 包（首选）

这些说明假定用户使用 [PackageReference 样式 NuGet 引用](/nuget/consume-packages/package-references-in-project-files)。

将项目文件更改为从 NuGet 包中引用 MSBuild 程序集。 指定 `ExcludeAssets=runtime` 以告知 NuGet 仅在生成期间需要程序集，不应将其复制到输出目录。

MSBuild 包的主要版本和次要版本须低于或等于希望支持的 Visual Studio 的最低版本。 例如，如果想要支持 Visual Studio 2017 和更高版本，请引用包版本 `15.1.548`。

例如，可以使用此 XML：

```xml
<ItemGroup>
  <PackageReference Include="Microsoft.Build" Version="15.1.548" ExcludeAssets="runtime" />
  <PackageReference Include="Microsoft.Build.Utilities.Core" Version="15.1.548" ExcludeAssets="runtime" />
</ItemGroup>
```

#### <a name="use-extension-assemblies"></a>使用扩展程序集

如果不能使用 NuGet 包，则可以引用随 Visual Studio 一起分发的 MSBuild 程序集。 如果直接引用 MSBuild，请通过将 `Copy Local` 设置为 `False` 确保不会将其复制到输出目录。 在项目文件中，此设置将如以下代码所示：

```xml
    <Reference Include="Microsoft.Build, Version=15.1.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
      <Private>False</Private>
    </Reference>
```

#### <a name="binding-redirects"></a>绑定重定向

引用 Microsoft.Build.Locator 包会自动让应用程序使用所需的绑定重定向到 15.1.0.0 版本。 绑定重定向到此版本支持 MSBuild 15 和 MSBuild 16。

### <a name="ensure-output-is-clean"></a>确保输出清洁

生成项目并检查输出目录，以确保它不包含任何 Microsoft.Build.\*.dll 程序集（除 Microsoft.Build.Locator.dll 以外，它在下一步中添加）。  

### <a name="add-package-reference-for-microsoftbuildlocator"></a>为 Microsoft.Build.Locator 添加包引用

为 [Microsoft.Build.Locator](https://www.nuget.org/packages/Microsoft.Build.Locator/) 添加 NuGet 包引用。

```xml
    <PackageReference Include="Microsoft.Build.Locator">
      <Version>1.1.2</Version>
    </PackageReference>
```

请勿为 Microsoft.Build.Locator 包指定 `ExcludeAssets=runtime`。

### <a name="register-instance-before-calling-msbuild"></a>在调用 MSBuild 之前注册实例

在调用任何使用 MSBuild 的方法之前，添加对 Locator API 的调用。

添加对 Locator API 的调用的最简单方法是：在应用程序启动代码中

```csharp
MSBuildLocator.RegisterDefaults();
```

添加对以上内容的调用。

如果希望更精细地控制 MSBuild 的加载，可以选择将 `MSBuildLocator.QueryVisualStudioInstances()` 的结果手动传递给 `MSBuildLocator.RegisterInstance()`，但通常不需要这样做。
