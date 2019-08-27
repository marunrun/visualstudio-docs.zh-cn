---
title: 标准和自定义工具集配置 | Microsoft Docs
ms.date: 01/31/2018
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, custom toolset configurations
- MSBuild, msbuild.exe.config
ms.assetid: 15a048c8-5ad3-448e-b6e9-e3c5d7147ed2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a8d3e78e4bd49c36174280c62ca8f24cdbd7f648
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63440037"
---
# <a name="standard-and-custom-toolset-configurations"></a>标准和自定义工具集配置
MSBuild 工具集包含对可用来生成应用程序项目的任务、目标和工具的引用。 MSBuild 包括标准工具集，但也可以创建自定义工具集。 有关如何指定工具集的信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)

## <a name="standard-toolset-configurations"></a>标准工具集配置

::: moniker range=">=vs-2019"
 MSBuild 16.0 内附有以下标准工具集：

|ToolsVersion|工具集路径（如 MSBuildToolsPath 或 MSBuildBinPath 生成属性中所指定）|
|------------------| - |
|2.0|\<Windows installation path\Microsoft.Net\Framework\v2.0.50727\\|
|3.5|\<Windows installation path>\Microsoft.NET\Framework\v3.5\\|
|4.0|\<Windows installation path>\Microsoft.NET\Framework\v4.0.30319\\|
|当前|\<Visual Studio installation path>\MSBuild\Current\bin|

 `ToolsVersion` 值确定 Visual Studio 生成的项目使用哪个工具集。 在 Visual Studio 2019 中，默认值为“Current”（不管在项目文件中指定了哪个版本），但可在命令提示符处使用 /toolsversion 开关重写该属性。 有关此属性和其他指定 `ToolsVersion` 的方式的信息，请参阅[重写 ToolsVersion 设置](../msbuild/overriding-toolsversion-settings.md)。

 ::: moniker-end

::: moniker range="vs-2017"
 MSBuild 15.0 内附有以下标准工具集：

|ToolsVersion|工具集路径（如 MSBuildToolsPath 或 MSBuildBinPath 生成属性中所指定）|
|------------------| - |
|2.0|\<Windows installation path\Microsoft.Net\Framework\v2.0.50727\\|
|3.5|\<Windows installation path>\Microsoft.NET\Framework\v3.5\\|
|4.0|\<Windows installation path>\Microsoft.NET\Framework\v4.0.30319\\|
|15.0|\<Visual Studio installation path>\MSBuild\15.0\bin|

 `ToolsVersion` 值确定 Visual Studio 生成的项目使用哪个工具集。 在 Visual Studio 2017 中，默认值为“15.0”（不管在项目文件中指定了哪个版本），但可在命令提示符处使用 /toolsversion 开关重写该属性。 有关此属性和其他指定 `ToolsVersion` 的方式的信息，请参阅[重写 ToolsVersion 设置](../msbuild/overriding-toolsversion-settings.md)。
 ::: moniker-end

Visual Studio 2017 及更高版本不对 MSBuild 路径使用注册表项。 对于随附 Visual Studio 2017 安装的 15.0 之前的 MSBuild 版本，以下注册表项指定了 MSBuild.exe 的安装路径。

|注册表项|项名称|字符串键值|
|------------------|--------------|----------------------|
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\2.0\\ |MSBuildToolsPath|.NET Framework 2.0 安装路径|
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\3.5\\ |MSBuildToolsPath|.NET Framework 3.5 安装路径|
|\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ MSBuild\ToolsVersions\4.0\\ |MSBuildToolsPath|.NET Framework 4 安装路径|

### <a name="sub-toolsets"></a>子工具集
 如果上表中的注册表项有一个子项，MSBuild 会使用它确定子工具集的路径是否有可能重写父工具集中的路径。 下面是一个示例子项：

 \HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSBuild\ToolsVersions\12.0\12.0

 如果基本工具集和选定的子工具集中均定义了某个属性，则使用子工具集中的属性定义。 例如，MSBuild 4.0 工具集将 `SDK40ToolsPath` 定义为指向 7.0A SDK，但是 MSBuild 4.0\11.0 工具集将同一属性定义为指向 8.0A SDK。 如果取消设置 `VisualStudioVersion`，`SDK40ToolsPath` 将指向 7.0A，但如果将 `VisualStudioVersion` 设置为 11.0，该属性将改为指向 8.0A。

 `VisualStudioVersion` 生成属性指示子工具集是否变为活动状态。 例如，`VisualStudioVersion` 值“12.0”指定 MSBuild 12.0 子工具集。 有关详细信息，请参阅[工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md) 的“子工具集”一节。

> [!NOTE]
> 建议避免更改这些设置。 不过，还是可以添加自己的设置并定义计算机范围内的自定义工具集定义，这将在下一节中进行介绍。

## <a name="custom-toolset-definitions"></a>自定义工具集定义
 当标准工具集不满足生成要求时，可以创建自定义工具集。 例如，你可能有一套生成实验室方案，方案中必须有一个单独的系统用于生成 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 项目。 通过使用自定义工具集，可在创建项目或运行 MSBuild.exe 时将自定义值指定为 `ToolsVersion` 属性。 这样，也可以使用 `$(MSBuildToolsPath)` 属性从该目录导入 .targets 文件，以及定义自己的自定义工具集属性，该属性可用于任何使用该工具集的项目。

 在 MSBuild.exe 或托管 MSBuild 引擎的自定义工具（如果正在使用的话）的配置文件中指定自定义工具集。 例如，如果想要定义名为 MyCustomToolset 的工具集，MSBuild.exe 的配置文件可以包含以下工具集定义。

```xml
<msbuildToolsets default="MyCustomToolset">
   <toolset toolsVersion="MyCustomToolset">
      <property name="MSBuildToolsPath"
        value="C:\SpecialPath" />
   </toolset>
</msbuildToolsets>
```

 还必须在配置文件中定义 `<msbuildToolsets>`，如下所示。

```xml
<configSections>
   <section name="msbuildToolsets"
       Type="Microsoft.Build.BuildEngine.ToolsetConfigurationSection,
       Microsoft.Build, Version=15.1.0.0, Culture=neutral,
       PublicKeyToken=b03f5f7f11d50a3a"
   </section>
</configSections>
```

> [!NOTE]
> 若要正确读取，`<configSections>` 必须是 `<configuration>` 部分中的第一个子节。

 `ToolsetConfigurationSection` 是一个可供任意 MSBuild 主机用于自定义配置的自定义配置部分。 如果使用自定义工具集，则主机除了提供配置文件项外，无需再执行任何其他操作便可初始化生成引擎。 通过在注册表中定义这些项，可指定计算机范围内的、适用于 MSBuild.exe、[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 及所有 MSBuild 主机的工具集。

> [!NOTE]
> 如果已在注册表中定义了 `ToolsVersion` 的设置，而后又在配置文件中对其进行了定义，则这两个定义并不会合并。 配置文件中的定义具有优先权，而注册表中的 `ToolsVersion` 设置则会被忽略。

 下列属性特定于项目中所用的 `ToolsVersion` 的值：

- **$(MSBuildBinPath)** 设置为 `ToolsPath` 值，该值在定义 `ToolsVersion` 的注册表或配置文件中指定。 注册表或配置文件中的 `$(MSBuildToolsPath)` 设置指定核心任务和目标的位置。 在项目文件中，此值映射到 $(MSBuildBinPath) 属性和 $(MSBuildToolsPath) 属性。

- `$(MSBuildToolsPath)` 是一个由在配置文件中指定的 MSBuildToolsPath 属性提供的保留属性。 （此属性取代了 `$(MSBuildBinPath)`。 但是，`$(MSBuildBinPath)` 的目的是实现兼容性。）自定义工具集必须定义 `$(MSBuildToolsPath)` 或 `$(MSBuildBinPath)`，但不能同时定义二者，除非它们具有相同的值。

  还可以使用添加 MSBuildToolsPath 属性时所用的语法向配置文件添加特定于 ToolsVersion 的自定义属性。 如果要使这些自定义属性可在项目文件中使用，请使用与配置文件中指定的值相同的名称。 可以在配置文件中定义工具集但不能定义子工具集。

## <a name="see-also"></a>请参阅
- [工具集 (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)