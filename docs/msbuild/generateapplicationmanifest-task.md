---
title: GenerateApplicationManifest 任务 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/msbuild/2003#GenerateApplicationManifest
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild, GenerateApplicationManifest task
- HostInBrowser property (MSBuild)
- GenerateApplicationManifest task [MSBuild]
ms.assetid: a494102b-0cb2-4755-8e2a-d2c0f39fac1d
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f77420c5ab269e1b0052ce6102c4e3196a3be52b
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/18/2020
ms.locfileid: "77634092"
---
# <a name="generateapplicationmanifest-task"></a>GenerateApplicationManifest 任务

生成 ClickOnce 应用程序清单或本机清单。 本机清单通过为组件定义唯一标识，并标识组成该组件的所有程序集和文件来描述组件。 ClickOnce 应用程序清单通过指示应用程序的入口点并指定应用程序安全级别来扩展本机清单。

## <a name="parameters"></a>参数

下表描述了 `GenerateApplicationManifest` 任务的参数。

| 参数 | 描述 |
|---------------------------------| - |
| `AssemblyName` | 可选 `String` 参数。<br /><br /> 指定生成的清单的程序集标识的 `Name` 字段。 如果未指定此参数，则从 `EntryPoint` 或 `InputManifest` 参数中推断名称。 如果无法创建任何名称，该任务将引发错误。 |
| `AssemblyVersion` | 可选 `String` 参数。<br /><br /> 指定生成的清单的程序集标识的 `Version` 字段。 如果未指定此参数，请使用默认值“1.0.0.0”。 |
| `ClrVersion` | 可选 `String` 参数。<br /><br /> 指定应用程序所需的公共语言运行时 (CLR) 的最低版本。 默认值是生成系统正在使用的 CLR 版本。 如果任务正在生成本机清单，将忽略此参数。 |
| `ConfigFile` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定包含应用程序配置文件的项。 如果任务正在生成本机清单，将忽略此参数。 |
| `Dependencies` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定为生成的清单定义依赖程序集集的项列表。 项元数据可更详细地描述每个项，指示更多部署状态和依赖项类型。 有关详细信息，请参阅[项元数据](#item-metadata)。 |
| `Description` | 可选 `String` 参数。<br /><br /> 指定应用程序或组件的说明。 |
| `EntryPoint` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定一个项，用于指示生成的清单程序集的入口点。<br /><br /> 对于 ClickOnce 应用程序清单，此参数指定在应用程序运行时启动的程序集。 |
| `ErrorReportUrl` | 可选 <xref:System.String?displayProperty=fullName> 参数。<br /><br /> 指定在安装 ClickOnce 时发出错误报告期间，对话框中显示的网页的 URL。 |
| `FileAssociations` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定与 ClickOnce 部署清单关联的一个或多个文件类型的列表。<br /><br /> 文件关联只在面向 .NET Framework 3.5 或更高版本时才有效。 |
| `Files` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 要包含在清单中的文件。 指定每个文件的完整路径。 |
| `HostInBrowser` | 可选 <xref:System.Boolean> 参数。<br /><br /> 如果为 `true`，则应用程序托管在浏览器中（与 WPF Web 浏览器应用程序一样）。 |
| `IconFile` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指示应用程序图标文件。 应用程序图标在生成的应用程序清单中表示，可用于“开始”菜单和“添加/删除程序”对话框   。 如果未指定此输入，将使用默认图标。 如果任务正在生成本机清单，将忽略此参数。 |
| `InputManifest` | 可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指示输入 XML 文档，使其充当清单生成器的基础。 这使得结构数据（如应用程序安全或自定义清单定义）可反映在输出清单中。 XML 文档中的根元素必须是 asmv1 命名空间中的程序集节点。 |
| `IsolatedComReferences` | 可选 <xref:Microsoft.Build.Framework.ITaskItem>`[]` 参数。<br /><br /> 指定要在生成清单中隔离的 COM 组件。 此参数支持隔离 COM 组件以实现“免注册 COM”部署。 方法是通过自动生成具有标准 COM 注册定义的清单。 但为了保证组件正常工作，必须在生成计算机上注册这些 COM 组件。 |
| `ManifestType` | 可选 `String` 参数。<br /><br /> 指定要生成的清单类型。 此参数可以具有下列值：<br /><br /> -   `Native`<br />-   `ClickOnce`<br /><br /> 如果未指定此参数，则该任务默认为 `ClickOnce`。 |
| `MaxTargetPath` | 可选 `String` 参数。<br /><br /> 指定 ClickOnce 应用程序部署中允许的最大文件路径长度。 如果指定此值，则将针对此限制检查应用程序中每个文件路径的长度。 超出该限制的任何项都会引发一条生成警告。 如果此输入未指定或为零，则不会执行任何检查。 如果任务正在生成本机清单，将忽略此参数。 |
| `OSVersion` | 可选 `String` 参数。<br /><br /> 指定应用程序所需的最低操作系统 (OS) 版本。 例如，值“5.1.2600.0”表示操作系统为 Windows XP。 如果未指定此参数，则使用值“4.10.0.0”，表示 Windows 98 Second Edition，即 .NET Framework 支持的最低 OS 版本。 如果任务正在生成本机清单，将忽略此输入。 |
| `OutputManifest` | 可选 <xref:Microsoft.Build.Framework.ITaskItem> 输出参数。<br /><br /> 指定所生成的输出清单文件的名称。 如果未指定此参数，则将从生成的清单的标识中推断输出文件的名称。 |
| `Platform` | 可选 `String` 参数。<br /><br /> 指定应用程序的目标平台。 此参数可以具有下列值：<br /><br /> -   `AnyCPU`<br />-   `x86`<br />-   `x64`<br />-   `Itanium`<br /><br /> 如果未指定此参数，则该任务默认为 `AnyCPU`。 |
| `Product` | 可选 `String` 参数。<br /><br /> 指定应用程序的名称。 如果未指定此参数，则将从生成的清单的标识中推断该名称。 该名称将用作“开始”菜单上的快捷名称，且将作为“添加或删除程序”对话框中显示的名称的一部分   。 |
| `Publisher` | 可选 `String` 参数。<br /><br /> 指定应用程序的发布者。 如果未指定此参数，则将从注册的用户或生成的清单的标识中推断该名称。 该名称将用作“开始”菜单上的文件夹名称，且将作为“添加或删除程序”对话框中显示的名称的一部分   。 |
| `RequiresMinimumFramework35SP1` | 可选 `Boolean` 参数。<br /><br /> 如果为 true，则该应用程序要求 .NET Framework 3.5 SP1 或更新的版本。 |
| `TargetCulture` | 可选 `String` 参数。<br /><br /> 标识应用程序的区域性，并指定生成的清单的程序集标识的 `Language` 字段。 如果未指定此参数，则会假定该应用程序的区域性是固定的。 |
| `TargetFrameworkMoniker` | 可选 `String` 参数。<br /><br /> 指定目标框架名字对象。 |
| `TargetFrameworkProfile` | 可选 `String` 参数。<br /><br /> 指定目标框架配置文件。 |
| `TargetFrameworkSubset` | 可选 `String` 参数。<br /><br /> 指定要面向的 .NET Framework 子集的名称。 |
| `TargetFrameworkVersion` | 可选 `String` 参数。<br /><br /> 指定项目的目标 .NET Framework。 |
| `TrustInfoFile` | 可选 <xref:Microsoft.Build.Framework.ITaskItem> 参数。<br /><br /> 指示用于指定应用程序安全性的 XML 文档。 XML 文档中的根元素必须是 asmv2 命名空间中的 trustInfo 节点。 如果任务正在生成本机清单，将忽略此参数。 |
| `UseApplicationTrust` | 可选 `Boolean` 参数。<br /><br /> 如果为 true，则将 `Product`、`Publisher` 和 `SupportUrl` 属性写入应用程序清单中。 |

## <a name="remarks"></a>备注

除上面列出的参数外，此任务还从 <xref:Microsoft.Build.Tasks.GenerateManifestBase> 类继承参数，后者自身继承自 <xref:Microsoft.Build.Utilities.Task> 类。 有关任务类的参数列表，请参阅[任务基类](../msbuild/task-base-class.md)。

有关如何使用 `GenerateDeploymentManifest` 任务的信息，请参阅 [GenerateApplicationManifest 任务](../msbuild/generateapplicationmanifest-task.md)。

可使用项元数据进一步修饰依赖项和文件的输入，为每个项指定其他部署状态。

## <a name="item-metadata"></a>项元数据

|元数据名称|描述|
|-------------------|-----------------|
|`DependencyType`|指示依赖项是随应用程序一起发布并安装还是一个必备组件。 此元数据对所有依赖项均有效，但不可用于文件。 可用于此元数据的值有：<br /><br /> -   `Install`<br />-   `Prerequisite`<br /><br /> Install 是默认值。|
|`AssemblyType`|指示依赖项是托管程序集还是本机程序集。 此元数据对所有依赖项均有效，但不可用于文件。 可用于此元数据的值有：<br /><br /> -   `Managed`<br />-   `Native`<br />-   `Unspecified`<br /><br /> `Unspecified` 是默认值，指示清单生成器将自动确定程序集类型。|
|`Group`|指示按需下载其他文件的组。 组名由应用程序定义，可以是任何字符串。 默认值是空字符串，表示该文件不属于下载组。 不在组中的文件属于初始应用程序下载。 只有当应用程序使用 <xref:System.Deployment.Application> 提出显式请求时才下载组中的文件。<br /><br /> 此元数据对于 `IsDataFile` 为 `false` 的所有文件以及 `DependencyType` 为 `Install` 的所有依赖项均有效。|
|`TargetPath`|指定应如何在生成的清单中定义该路径。 此属性对所有文件均有效。 如果未指定此属性，将使用项规范。 此属性对所有文件以及 `DependencyType` 值为 `Install` 的依赖项均有效。|
|`IsDataFile`|指示文件是否为数据文件的 `Boolean` 元数据值。 数据文件的特殊性在于它可以在应用程序更新之间迁移。 此元数据仅对文件有效。 默认值为 `False`。|

## <a name="example"></a>示例

此示例针对具有单个程序集的应用程序，使用 `GenerateApplicationManifest` 任务生成 ClickOnce 应用程序清单，并使用 `GenerateDeploymentManifest` 任务生成部署清单。 然后，使用 `SignFile` 任务对这些清单进行签名。

上文说明了最简单的清单生成方案，其中为单个程序生成了 ClickOnce 清单。 根据清单的程序集可以推断出默认的名称和标识。

> [!NOTE]
> 在下面的示例中，为将重点放在清单生成方面上，预先生成了所有应用程序二进制文件。 此示例会生成一个完全可用的 ClickOnce 部署。
>
> [!NOTE]
> 有关在此示例的 `SignFile` 任务中使用的 `Thumbprint` 属性的详细信息，请参阅 [SignFile 任务](../msbuild/signfile-task.md)。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe" />
    </ItemGroup>

    <PropertyGroup>
        <Thumbprint>
             <!-- Insert generated thumbprint here -->
        </Thumbprint>
    </PropertyGroup>

    <Target Name="Build">

        <GenerateApplicationManifest
            EntryPoint="@(EntryPoint)">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

        <GenerateDeploymentManifest
            EntryPoint="@(ApplicationManifest)">
            <Output
                ItemName="DeployManifest"
                TaskParameter="OutputManifest"/>
        </GenerateDeploymentManifest>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(ApplicationManifest)"/>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(DeployManifest)"/>

    </Target>
</Project>
```

## <a name="example"></a>示例

此示例针对具有单个程序集的应用程序，分别使用 `GenerateApplicationManifest` 和 `GenerateDeploymentManifest` 任务生成 ClickOnce 应用程序清单和部署清单，指定了清单的名称和标识。

此示例除显式指定清单的名称和标识之外，其他方面均与上一个示例类似。 此外，此示例还被配置为联机应用程序，而不是安装的应用程序。

> [!NOTE]
> 在下面的示例中，为将重点放在清单生成方面上，预先生成了所有应用程序二进制文件。 此示例会生成一个完全可用的 ClickOnce 部署。
>
> [!NOTE]
> 有关在此示例的 `SignFile` 任务中使用的 `Thumbprint` 属性的详细信息，请参阅 [SignFile 任务](../msbuild/signfile-task.md)。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe" />
    </ItemGroup>

    <PropertyGroup>
        <Thumbprint>
             <!-- Insert generated thumbprint here -->
        </Thumbprint>
    </PropertyGroup>

    <Target Name="Build">

        <GenerateApplicationManifest
            AssemblyName="SimpleWinApp.exe"
            AssemblyVersion="1.0.0.0"
            EntryPoint="@(EntryPoint)"
            OutputManifest="SimpleWinApp.exe.manifest">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

        <GenerateDeploymentManifest
                AssemblyName="SimpleWinApp.application"
                AssemblyVersion="1.0.0.0"
                EntryPoint="@(ApplicationManifest)"
                Install="false"
                OutputManifest="SimpleWinApp.application">
                <Output
                    ItemName="DeployManifest"
                    TaskParameter="OutputManifest"/>
        </GenerateDeploymentManifest>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(ApplicationManifest)"/>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(DeployManifest)"/>

    </Target>
</Project>
```

## <a name="example"></a>示例

此示例针对具有多个文件和程序集的应用程序，分别使用 `GenerateApplicationManifest` 和 `GenerateDeploymentManifest` 任务生成 ClickOnce 应用程序清单和部署清单。

> [!NOTE]
> 在下面的示例中，为将重点放在清单生成方面上，预先生成了所有应用程序二进制文件。 此示例会生成一个完全可用的 ClickOnce 部署。
>
> [!NOTE]
> 有关在此示例的 `SignFile` 任务中使用的 `Thumbprint` 属性的详细信息，请参阅 [SignFile 任务](../msbuild/signfile-task.md)。

```xml
<Project DefaultTargets="Build"
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe" />
    </ItemGroup>

    <PropertyGroup>
        <Thumbprint>
             <!-- Insert generated thumbprint here -->
        </Thumbprint>
        <DeployUrl>
            <!-- Insert the deployment URL here -->
        </DeployUrl>
        <SupportUrl>
            <!-- Insert the support URL here -->
        </SupportUrl>
    </PropertyGroup>

    <Target Name="Build">

    <ItemGroup>
        <EntryPoint Include="SimpleWinApp.exe"/>
        <Dependency Include="ClassLibrary1.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Install</DependencyType>
        </Dependency>
        <Dependency Include="ClassLibrary2.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Install</DependencyType>
            <Group>Secondary</Group>
        </Dependency>
        <Dependency Include="MyAddIn1.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Install</DependencyType>
            <TargetPath>Addins\MyAddIn1.dll</TargetPath>
        </Dependency>
        <Dependency Include="ClassLibrary3.dll">
            <AssemblyType>Managed</AssemblyType>
            <DependencyType>Prerequisite</DependencyType>
        </Dependency>

        <File Include="Text1.txt">
            <TargetPath>Text\Text1.txt</TargetPath>
            <Group>Text</Group>
        </File>
        <File Include="DataFile1.xml ">
            <TargetPath>Data\DataFile1.xml</TargetPath>
            <IsDataFile>true</IsDataFile>
        </File>

        <IconFile Include="Heart.ico"/>
        <ConfigFile Include="app.config">
            <TargetPath>SimpleWinApp.exe.config</TargetPath>
        </ConfigFile>
        <BaseManifest Include="app.manifest"/>
    </ItemGroup>

    <Target Name="Build">

        <GenerateApplicationManifest
            AssemblyName="SimpleWinApp.exe"
            AssemblyVersion="1.0.0.0"
            ConfigFile="@(ConfigFile)"
            Dependencies="@(Dependency)"
            Description="TestApp"
            EntryPoint="@(EntryPoint)"
            Files="@(File)"
            IconFile="@(IconFile)"
            InputManifest="@(BaseManifest)"
            OutputManifest="SimpleWinApp.exe.manifest">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

        <GenerateDeploymentManifest
            AssemblyName="SimpleWinApp.application"
            AssemblyVersion="1.0.0.0"
            DeploymentUrl="$(DeployToUrl)"
            Description="TestDeploy"
            EntryPoint="@(ApplicationManifest)"
            Install="true"
            OutputManifest="SimpleWinApp.application"
            Product="SimpleWinApp"
            Publisher="Microsoft"
            SupportUrl="$(SupportUrl)"
            UpdateEnabled="true"
            UpdateInterval="3"
            UpdateMode="Background"
            UpdateUnit="weeks">
            <Output
                ItemName="DeployManifest"
                TaskParameter="OutputManifest"/>
        </GenerateDeploymentManifest>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(ApplicationManifest)"/>

        <SignFile
            CertificateThumbprint="$(Thumbprint)"
            SigningTarget="@(DeployManifest)"/>

    </Target>
</Project>
```

## <a name="example"></a>示例

此示例使用 `GenerateApplicationManifest` 任务为应用程序 Test.exe 生成本机清单，引用本机组件 Alpha.dll 和独立的 COM 组件 Bravo.dll    。

此示例生成 Test.exe.manifest，使该应用程序可借助“免注册 COM”进行 XCOPY 部署  。

> [!NOTE]
> 在下面的示例中，为将重点放在清单生成方面上，预先生成了所有应用程序二进制文件。 此示例会生成一个完全可用的 ClickOnce 部署。

```xml
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

    <ItemGroup>
        <File Include="Test.exe" />
        <Dependency Include="Alpha.dll">
            <AssemblyType>Native</AssemblyType>
            <DependencyType>Install</DependencyType>
        </Dependency>
        <ComComponent Include="Bravo.dll" />
    </ItemGroup>

    <Target Name="Build">
        <GenerateApplicationManifest
            AssemblyName="Test.exe"
            AssemblyVersion="1.0.0.0"
            Dependencies="@(Dependency)"
            Files="@(File)"
            IsolatedComReferences="@(ComComponent)"
            ManifestType="Native">
            <Output
                ItemName="ApplicationManifest"
                TaskParameter="OutputManifest"/>
        </GenerateApplicationManifest>

    </Target>
</Project>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [GenerateDeploymentManifest 任务](../msbuild/generatedeploymentmanifest-task.md)
- [SignFile 任务](../msbuild/signfile-task.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
