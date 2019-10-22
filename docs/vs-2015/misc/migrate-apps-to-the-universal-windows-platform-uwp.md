---
title: 将应用迁移到通用 Windows 平台（UWP） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 5279ab9b-71d9-4be5-81f6-a1f24b06f5fb
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 76590f55b21f1609a20c6fd8eb041a41a0f82131
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656031"
---
# <a name="migrate-apps-to-the-universal-windows-platform-uwp"></a>将应用迁移到通用 Windows 平台 (UWP)
对使用 Visual Studio 2015 RC 创建的 Windows Store 8.1 应用、Windows Phone 8.1 应用或通用 Windows 应用的现有项目文件进行必要的手动更改，以便它们能与 Visual Studio 2015 RTM 一起使用。 （如果你的 Windows 8.1 通用应用同时具有 Windows 应用项目和 Windows Phone 项目，则需要按照以下步骤迁移每个项目。）

 使用通用 Windows 平台，你现在能使你的应用面向一个或多个设备系列。 若要了解有关通用 Windows 应用的详细信息，请参阅此 [平台指南](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx)。

- [迁移现有 C#/VB Windows 应用商店 8.1 或 Windows Phone 8.1 应用](#MigrateCSharp) 以使用通用 Windows 平台。

- [迁移现有 C++ Windows 应用商店 8.1 或 Windows Phone 8.1 应用](#MigrateCPlusPlus) 以使用通用 Windows 平台。

- [使用 Visual Studio 2015 RC 创建的现有通用 Windows 应用所需的更改](#PreviousVersions)。

- [使用 Visual Studio 2015 RC 创建的通用 Windows 应用的现有单元测试项目所需的更改](#MigrateUnitTest)。

  如果你不想进行所有这些更改，请了解如何 [移植现有应用](https://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) 到新的通用 Windows 项目。

## <a name="MigrateCSharp"></a>将C#/VB Windows 应用商店8.1 或 Windows Phone 8.1 应用迁移到使用通用 Windows 平台

#### <a name="migrate-your-cvb-project-files"></a>迁移 C#/VB 项目文件

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

     ![打开文件夹以查看安装的版本](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     可以安装多个版本的通用 Windows 平台。 建议对你的应用使用最新版本。

2. 使用文件资源管理器，转到存储 UWP 项目的文件夹。 在此文件夹中创建 .json 文件。 将该文件命名为 project.json，然后将以下内容添加到此文件：

    ```json
    {
      "dependencies": {
        "Microsoft.ApplicationInsights": "1.0.0",
        "Microsoft.ApplicationInsights.PersistenceChannel": "1.0.0",
        "Microsoft.ApplicationInsights.WindowsApps": "1.0.0",
        "Microsoft.NETCore.UniversalWindowsPlatform": "5.0.0"
      },
      "frameworks": {
        "uap10.0": {}
      },
      "runtimes": {
        "win10-arm": {},
        "win10-arm-aot": {},
        "win10-x86": {},
        "win10-x86-aot": {},
        "win10-x64": {},
        "win10-x64-aot": {}
      }
    }

    ```

3. 创建名为 default.rd.xml 且包含以下内容的文件。 如果具有 VB 项目，请将此文件添加到项目的“我的项目”目录中。 如果具有 C# 项目，请将此文件添加到项目的“属性”目录中。

    ```xml
    <?xml version="1.0"?>
    <!-- This file contains Runtime Directives used by .NET Native. The defaults here are suitable for most developers. However, you can modify these parameters to modify the behavior of the .NET Native optimizer. Runtime Directives are documented at http://go.microsoft.com/fwlink/?LinkID=391919 To fully enable reflection for App1.MyClass and all of its public/private members <Type Name="App1.MyClass" Dynamic="Required All"/> To enable dynamic creation of the specific instantiation of AppClass<T> over System.Int32 <TypeInstantiation Name="App1.AppClass" Arguments="System.Int32" Activate="Required Public" /> Using the Namespace directive to apply reflection policy to all the types in a particular namespace <Namespace Name="DataClasses.ViewModels" Seralize="All" /> -->
    <Directives xmlns="http://schemas.microsoft.com/netfx/2013/01/metadata"><Application>
    <!-- An Assembly element with Name="*Application*" applies to all assemblies in the application package. The asterisks are not wildcards. -->
    <Assembly Dynamic="Required All" Name="*Application*"/>
    <!-- Add your application specific runtime directives here. -->
    </Application></Directives>
    ```

4. 在 Visual Studio 中打开包含你现有 Windows 应用商店 8.1 应用或 Windows Phone 8.1 应用的解决方案。

5. 在解决方案资源管理器中右键单击你应用的现有项目，然后选择 **“卸载项目”** 。 卸载项目后，再次右键单击项目文件，然后选择编辑 .csproj 或 .vbproj 文件。

     ![右键单击该项目，然后选择 "编辑"](../misc/media/uap-editproject.png "UAP_EditProject")

6. 查找包含值为8.1 的 \<TargetPlatformVersion > 元素 \<PropertyGroup > 元素。 为此 \<PropertyGroup > 元素执行以下步骤：

    1. 将 \<Platform > 元素的值设置为： **x86**。

    2. 添加一个 \<TargetPlatformIdentifier > 元素，并将其值设置为： **UAP**。

    3. 将 \<TargetPlatformVersion > 元素的现有值更改为你安装的通用 Windows 平台版本的值。 还要添加一个 \<TargetPlatformMinVersion > 元素，并为其指定相同的值。

    4. 将 \<MinimumVisualStudioVersion > 元素的值更改为： **14**。

    5. 将 \<ProjectTypeGuids > 元素，如下所示：

         对于 C#：

        ```xml
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
        ```

         对于 VB：

        ```xml
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>
        ```

    6. 添加一个 \<EnableDotNetNativeCompatibleProfile > 元素，并将其值设置为 " **true**"。

    7. 通用 Windows 应用的默认资产规模为 200。 如果你的项目包括未在200缩放的资产，则你需要添加一个 \<UapDefaultAssetScale > 元素，并将资产规模的值添加到此 PropertyGroup。 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

         现在，\<PropertyGroup > 元素应类似于以下示例：

        ```xml
        <PropertyGroup>
            …
             <Platform Condition=" '$(Platform)' == '' ">x86</Platform>
             <TargetPlatformVersion>10.0.10240.0</TargetPlatformVersion>
             <TargetPlatformMinVersion>10.0.10240.0</TargetPlatformMinVersion>
             <TargetPlatformIdentifier>UAP</TargetPlatformIdentifier>
             <MinimumVisualStudioVersion>14</MinimumVisualStudioVersion>
             <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
        <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>
             <UapDefaultAssetScale>100</UapDefaultAssetScale>
             …
        </PropertyGroup>
        ```

7. 将 12.0 的所有实例替换为 14.0，以反映你现在使用的 Visual Studio 版本。 如以下实例：

    ```xml
    <Project Tools Version="14.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    ```

    ```
    <PropertyGroup Condition=" '$(VisualStudioVersion)' == '' or '$(VisualStudioVersion)' < '14.0' ">
        <VisualStudioVersion>14.0</VisualStudioVersion>
    ```

8. @No__t_0PropertyGroup 查找为 AnyCPU 平台配置的 > 元素，作为 Condition 特性的一部分。 删除这些元素及其所有子元素。 在 Visual Studio 2015 中，Windows 10 应用不支持 AnyCPU。 例如，应删除 \<PropertyGroup > 元素，如下所示：

    ```xml
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
        <PlatformTarget>AnyCPU</PlatformTarget>
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineConstants>DEBUG;TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
        <PlatformTarget>AnyCPU</PlatformTarget>
        <DebugType>pdbonly</DebugType>
        <Optimize>true</Optimize>
        <OutputPath>bin\Release\</OutputPath>
        <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
        <ErrorReport>prompt</ErrorReport>
        <WarningLevel>4</WarningLevel>
      </PropertyGroup>
    ```

9. 对于剩余的每个 \<PropertyGroup > 元素，请检查元素是否具有具有发布配置的 Condition 特性。 如果是这样，但它不包含 \<UseDotNetNativeToolchain > 元素，则添加一个。 将 \<UseDotNetNativeToolchain > 元素的值设置为 true，如下所示：

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|x64'">
        <OutputPath>bin\x64\Release\</OutputPath>
        <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
        <Optimize>true</Optimize>
        <NoWarn>;2008</NoWarn>
        <DebugType>pdbonly</DebugType>
        <PlatformTarget>x64</PlatformTarget>
        <UseVSHostingProcess>false</UseVSHostingProcess>
        <ErrorReport>prompt</ErrorReport>
        <Prefer32Bit>true</Prefer32Bit>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>
    ```

10. 对于 Windows Phone 项目，请删除包含值为 WindowsPhoneApp 的 \<TargetPlatformIdentifier > 元素的 \<PropertyGroup > 元素。 同时删除此元素的任何子级：

    ```xml
    <PropertyGroup Condition=" '$(TargetPlatformIdentifier)' == '' ">
      <TargetPlatformIdentifier>WindowsPhoneApp</TargetPlatformIdentifier>
    </PropertyGroup>
    ```

11. 查找包含 \<AppxManifest > 元素 \<ItemGroup > 元素。 将以下 \<None > 元素添加为 \<ItemGroup > 元素的子元素：

    ```xml
    <None Include="project.json" />
    ```

12. 查找 \<ItemGroup > 元素，该元素包含添加到项目中的其他资产，如徽标 .png 文件（\<Content Include = "Assets\Logo.scale-100.png"/>）。 将以下 \<Content > 子元素添加到此 \<ItemGroup > 元素：

     **对于C#：**

    ```xml
    <Content Include="Properties\default.rd.xml" />
    ```

     **对于 VB：**

    ```xml
    <Content Include="My Project\default.rd.xml" />
    ```

13. 查找包含 NuGet 包 \<Reference > 子元素的 \<ItemGroup > 元素。 记下你使用的 NuGet 包，因为在重新加载项目后你将需要使用 NuGet 包管理器下载它们。 删除此 \<ItemGroup 与其子项 >。 例如，UWP 项目可能具有以下需要删除的 NuGet 包：

    ```xml
    <ItemGroup>
        <Reference Include="Microsoft.ApplicationInsights, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
          <HintPath>..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="Microsoft.ApplicationInsights.Extensibility.Windows, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
          <HintPath>..\packages\Microsoft.ApplicationInsights.WindowsApps.0.14.3-build00177\lib\win81\Microsoft.ApplicationInsights.Extensibility.Windows.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="Microsoft.ApplicationInsights.PersistenceChannel, Version=0.14.3.186, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
          <HintPath>..\packages\Microsoft.ApplicationInsights.PersistenceChannel.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.PersistenceChannel.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="System.Numerics.Vectors, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.dll</HintPath>
          <Private>True</Private>
        </Reference>
        <Reference Include="System.Numerics.Vectors.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
          <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.WindowsRuntime.dll</HintPath>
          <Private>True</Private>
        </Reference>
      </ItemGroup>
    ```

14. 保存更改。

15. 关闭 .csproj 或 .vbproj 文件。

16. 在解决方案资源管理器中右键单击你的项目，然后从上下文菜单中选择“重新加载项目”。 项目中的所有文件现在都应显示在解决方案资源管理器中。

17. 使用 NuGet 管理器将在之前步骤中删除的包添加回来。

     现在需要遵循相关步骤，为你的所有 Windows Store 8.1 或 Windows Phone 8.1 项目 [更新包清单文件](#PackageManifest) 。

## <a name="MigrateCPlusPlus"></a>迁移C++ Windows 应用商店8.1 或 Windows Phone 8.1 应用以使用通用 Windows 平台

#### <a name="migrate-your-c-project-files"></a>迁移 C++ 项目文件

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

     ![打开文件夹以查看安装的版本](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     可以安装多个版本的通用 Windows 平台。 建议对你的应用使用最新版本。

2. 在 Visual Studio 中打开包含现有 C++ Windows 应用商店 8.1 应用或 Windows Phone 8.1 应用的解决方案。

     在解决方案资源管理器中右键单击现有项目，然后选择“卸载项目”。 卸载项目后，再次右键单击项目文件，并选择编辑 .vcxproj 文件。

     ![右键&#45;单击项目文件并选择 "编辑"](../misc/media/uap-editcplusproject.png "UAP_EditCPlusProject")

3. 查找包含值为8.1 的 \<ApplicationTypeRevision > 元素 \<PropertyGroup > 元素。 为此 \<PropertyGroup > 元素执行以下步骤：

    1. 添加一个 \<WindowsTargetPlatformVersion > 元素和一个 \<WindowsTargetPlatformMinVersion > 元素，并为其指定所安装通用 Windows 平台版本的值。

    2. 将 ApplicationTypeRevision 元素的值从 8.1 更新为 10.0。

    3. 将 \<MinimumVisualStudioVersion > 元素的值更改为：14。

    4. 添加一个 \<EnableDotNetNativeCompatibleProfile > 元素，并将其值设置为 "true"。

    5. 通用 Windows 应用的默认资产规模为 200。 如果你的项目包括未在200缩放的资产，则你需要添加一个 \<UapDefaultAssetScale > 元素，并将资产规模的值添加到此 PropertyGroup。 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

    6. 对于 Windows Phone 项目，请将 \<ApplicationType > 的值从 Windows Phone 更改为 Windows 应用商店。

         现在，\<PropertyGroup > 元素应类似于以下示例：

        ```xml
        <PropertyGroup>
            …
                  <WindowsTargetPlatformVersion>10.0.10240.0</WindowsTargetPlatformVersion>
        <WindowsTargetPlatformMinVersion>10.0.10240.0</WindowsTargetPlatformMinVersion>
             <ApplicationType>Windows Store</ApplicationType>
             <ApplicationTypeRevision>10.0</ApplicationTypeRevision>
             <MinimumVisualStudioVersion>14</MinimumVisualStudioVersion>
             <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>
             <UapDefaultAssetScale>100</UapDefaultAssetScale>
             …
        </PropertyGroup>
        ```

4. 将 \<PlatformToolset > 元素的所有实例更改为具有 v140 值。 例如:

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>
    ```

5. 对于剩余的每个 \<PropertyGroup > 元素，请检查元素是否具有具有发布配置的 Condition 特性。 如果是这样，但它不包含 \<UseDotNetNativeToolchain > 元素，则添加一个。 将 \<UseDotNetNativeToolchain > 元素的值设置为 true，如下所示：

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|X64'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>

    ```

6. 保存更改。 然后关闭项目文件。

7. 在解决方案资源管理器中右键单击项目文件，然后从上下文菜单中选择“重新加载项目”。 项目中的所有文件现在都应显示在解决方案资源管理器中。

     现在需要遵循相关步骤，为你的所有 Windows Store 8.1 或 Windows Phone 8.1 项目 [更新包清单文件](#PackageManifest) 。

## <a name="PackageManifest"></a>更新所有 Windows 应用商店8.1 或 Windows Phone 8.1 项目的包清单文件
 必须更新解决方案中每个项目的包清单文件。

#### <a name="update-your-package-manifest-file"></a>更新包清单文件

1. 在项目中打开 package.appxmanifest 文件。 需要编辑每个 Windows 应用商店项目和 Windows Phone 项目的 Package.AppxManifest 文件。

2. 需要根据现有的项目类型，将 \<Package > 元素更新为新的架构。 首先根据你使用的是 Windows 应用商店项目还是 Windows Phone 项目删除以下架构。

    **Windows 应用商店项目的旧版本：** @No__t_1Package > 元素将与此类似。

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"
       xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest">

   ```

    **Windows Phone 项目的旧版本：** @No__t_1Package > 元素将与此类似。

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"
   xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest"
   xmlns:m3="http://schemas.microsoft.com/appx/2014/manifest"
   xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest">
   ```

    **通用 Windows 平台的新内容：** 将下面的架构添加到 \<Package > 元素。 从刚才删除的架构的元素中删除任何关联的命名空间标识符前缀。 将 IgnorableNamespaces 属性更新为：uap mp。 新的 \<Package > 元素应该与此类似。

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
       xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
       xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
      IgnorableNamespaces= "uap mp">

   ```

3. 将 \<Dependencies > 子元素添加到 \<Package > 元素。 然后，将 \<TargetDeviceFamily > 子元素添加到此 \<Dependencies > 具有 Name、MinVersion 和 MaxVersionTested 属性的元素。 为 Name 属性赋予值：Windows.Universal。 为 MinVersion 和 MaxVersionTested 赋予已安装通用 Windows 平台版本的值。 此元素应类似于：

   ```xml
   <Dependencies>
   <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10069.0" MaxVersionTested="10.0.10069.0" />
   </Dependencies>
   ```

4. **仅适用于 Windows 应用商店：** 需要将 \<mp:P honeIdentity > 子元素添加到 \<Package > 元素。 添加 PhoneProductId 属性和 PhonePublisherId 属性。 将 PhoneProductId 设置为具有与 \<Identity > 元素中的 Name 属性相同的值。 将 PhonePublishedId 值设置为：00000000-0000-0000-0000-000000000000。 如：

   ```xml
   <Identity Name="aa3815a1-2d97-4c71-8c99-578135b28cd8" Publisher="CN=xxxxxxxx" Version="1.0.0.0" />
   <mp:PhoneIdentity PhoneProductId="aa3815a1-2d97-4c71-8c99-578135b28cd8" PhonePublisherId="00000000-0000-0000-0000-000000000000"/>
   ```

5. 查找 \<Prerequisites > 元素，并删除此元素及其具有的任何子元素。

6. 将**uap**命名空间添加到以下 \<Resource > 元素： Scale、DXFeatureLevel。 例如:

   ```xml
   <Resources>
     <Resource Language="en-us"/>
    <Resource uap:Scale="180"/>
    <Resource uap:DXFeatureLevel="dx11"/>
   </Resources>

   ```

7. 将**uap**命名空间添加到以下 \<Capability > 元素： DocumentsLibrary、PicturesLibrary、VideosLibrary、MusicLibrary、EnterpriseAuthentication、SharedUserCertificates、removableStorage、约会和联系人。 例如:

   ```xml
   <Capabilities>
     <uap:Capability Name="documentsLibrary"/>
     <uap:Capability Name="removableStorage"/>
   </Capabilities>

   ```

8. 将**uap**命名空间添加到 \<VisualElements > 元素及其任何子元素。 例如:

   ```xml
   <uap:VisualElements
       DisplayName="My WWA App"
       Square150x150Logo="images/150x150.png"
       Square44x44Logo="images/44x44.png"
       Description="My WWA App"
       BackgroundColor="#777777">
     <uap:SplashScreen Image="images/splash.png"/>
   </uap:VisualElements>

   ```

    **仅适用于 Windows 应用商店：** 磁贴大小名称已更改。 更改 \<VisualElements > 元素中的属性，以反映新的汇聚磁贴大小。 70x70 变为 71x71，30x30 变为 44x44。

    **旧：** 磁贴大小名称

   ```xml
   <m2:VisualElements
       …
       Square30x30Logo="Assets\SmallLogo.png"
       …>
    <m2:DefaultTile
         …
         Square70x70Logo="images/70x70.png">
   </m2:VisualElements>

   ```

    **新：** 磁贴大小名称

   ```xml
   <uap:VisualElements
       …
       Square44x44Logo="Assets\SmallLogo.png"
       …>
    <uap:DefaultTile
         …
         Square71x71Logo="images/70x70.png">
   </uap:VisualElements>

   ```

9. 将**uap**命名空间添加到 \<ApplicationContentUriRules > 及其所有子元素。 例如:

    ```xml
    <uap:ApplicationContentUriRules>
      <uap:Rule Type="include" Match="https://www.microsoft.com/"/>
      <uap:Rule Type="exclude" Match="*.pdf"/>
    </uap:ApplicationContentUriRules>

    ```

10. 将**uap**命名空间添加到以下 \<Extension > 元素及其所有子元素： AccountPictureProvide、AutoPlayDevice、appointmentsProvider AutoPlayContent、）。cachedFileUpdate、cameraSettings、fileOpenPicker、fileTypeAssociation、fileSavePicke、lockScreenCall、printTaskSettings、shareTarget、windows.、windows.、windows.。 例如:

    ```xml
    <Extensions>
      <uap:Extension Category="windows.alarm"/>
      <uap:Extension Category="windows.search" EntryPoint="MyActivateableClassId.baz"/>
      <uap:Extension Category="windows.protocol">
        <uap:Protocol Name="mailto" DesiredView="useHalf">
         <uap:DisplayName>MailTo Protocol</uap:DisplayName>
        </uap:Protocol>
      </uap:Extension>
    </Extensions>

    ```

11. 将“uap” 命名空间添加到 chatMessageNotification 类型的后台任务。 例如:

    ```xml
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">
     <BackgroundTasks ServerName="MyBackgroundTasks">
        <uap:Task Type="chatMessageNotification"/>
      </BackgroundTasks>
    </Extension>

    ```

12. 更改框架依赖项。 将发布者名称添加到所有 \<PackageDependency > 元素，并指定 "MinVersion" （如果尚未指定）。

     **旧：** \<PackageDependency > 元素

    ```xml
    <Dependencies>
     <PackageDependency Name="Microsoft.VCLibs.120.00" />
    </Dependencies>

    ```

     **NEW：** \<PackageDependency > 元素

    ```xml
    <Dependencies>
     <PackageDependency
          Name="Microsoft.VCLibs.120.00"
          Publisher="CN=Microsoft Corporation, O=Microsoft Corporation, L=Redmond, S=Washington, C=US"
          MinVersion="12.0.30113.0" />
    </Dependencies>

    ```

     使用你正在使用的实际框架的相应发布者和 MinVersion 值。 请注意，对于 Windows 10，这些名称可能会更改。

13. 将 gattCharacteristicNotification 和 rfcommConnection 后台类型任务替换为蓝牙类型任务。 例如:

     **原来**

    ```xml
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">
    <BackgroundTasks ServerName="MyBackgroundTasks">
                <Task Type="rfcommConnection"/>
               <Task Type="gattCharacteristicNotification"/>
    </BackgroundTasks>
    </Extension>
    ```

     **新：** 使用蓝牙类型任务。

    ```xml
    <Extension Category="windows.backgroundTasks" EntryPoint="Fabrikam.BackgroundTask" Executable="MyBackground.exe">
    <BackgroundTasks ServerName="MyBackgroundTasks">
               <Task Type="bluetooth"/>
    </BackgroundTasks>
    </Extension>
    ```

14. 将蓝牙设备功能 bluetooth.rfcomm 和 bluetooth.genericAttributeProfile 替换为泛型蓝牙功能。 例如:

     **原来**

    ```xml
    <Capabilities>
      <m2:DeviceCapability Name="bluetooth.rfcomm">
        <m2:Device Id="any">
         <m2:Function Type="serviceId:34B1CF4D-1069-4AD6-89B6-E161D79BE4D8"/>
        </m2:Device>
      </m2:DeviceCapability>
      <m2:DeviceCapability Name="bluetooth.genericAttributeProfile">
        <m2:Device Id="any">
         <m2:Function Type="name:heartRate"/>
        </m2:Device>
      </m2:DeviceCapability>
    </Capabilities>
    ```

     **新：** 已替换为泛型蓝牙功能。

    ```xml
    <Capabilities>
      <uap:DeviceCapability Name="bluetooth"/>
    </Capabilities>

    ```

15. 删除任何已弃用的元素。

    1. @No__t_0VisualElements > 的这些属性已弃用，应将其删除：

       - @No__t_0VisualElements > 属性： ForegroundText、ToastCapable

       - @No__t_0DefaultTile > 属性 DefaultSize

       - @No__t_0ApplicationView > 元素

         例如:

       ```xml
       <m2:VisualElements
           …
           ForegroundText="dark"
           ToastCapable="true">
       <m2:DefaultTile DefaultSize="square150x150Logo"/>
         <m2:ApplicationView MinWidth="width320"/>
       </m2:VisualElements>

       ```

    2. 删除 Windows.contact 和 windows.contactPicker 扩展以及它们下面的所有元素。

16. 保存 Package.appxmanifest 文件。 然后关闭 Visual Studio。

17. 需要删除某些隐藏文件，才能重新打开解决方案。

    1. 打开文件资源管理器，单击工具栏中的“视图” ，然后选择“已隐藏项” 和“文件名扩展”。 在计算机上打开此文件夹： > \\ 的解决方案位置 \<path。 vs \\ {Project Name} \v14。 如果存在具有 .suo 文件扩展名的文件，请将其删除。

    2. 现在返回解决方案所在的文件夹。 打开解决方案中存在的项目的任何文件夹。 如果任何这些项目文件夹中的文件具有 .csproj.user 或 .vbproj.user 扩展名，请将其删除。

         现在可以在 Visual Studio 中重新打开解决方案。 现在你可以使用通用 Windows 平台对应用程序进行编码、编译和调试。

         了解如何 [调整代码](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx) 以利用通用 Windows 平台的新增功能。

## <a name="PreviousVersions"></a>用 Visual Studio 2015 RC 创建的现有通用 Windows 应用所需的更改
 如果你使用 Visual Studio 2015 RC 创建了 Windows 10 通用应用，则需重定项目的目标，以使用随最新版 Visual Studio 2015 一起安装的通用 Windows 平台的版本。 不支持任何以前的版本。 所需更改因用于创建应用的语言而异：

- [C#/VB 应用](#RCUpdate10CSharp)

- [C++应用](#RCUpdate10CPlusPlus)

### <a name="RCUpdate10CSharp"></a>更新C#/VB 项目以使用最新通用 Windows 平台
 为现有应用打开解决方案时，你将看到你的应用需要更新：

 ![查看解决方案资源管理器中的项目](../misc/media/uwp-updaterequired.png "UWP_UpdateRequired")

 如果选择从解决方案资源管理器重新加载此项目，你将看到此对话框：

 ![重定向你的应用以使用正确的 SDK](../misc/media/missingsdkforuap.png "MissingSDKforUAP")

 因为你项目的通用 Windows 平台 SDK 目前暂不受支持，因此无法进行安装。 请单击“确定”，然后执行以下操作。

##### <a name="update-your-cvb-projects-to-use-the-latest-universal-windows-platform"></a>更新 C#/VB 项目以使用最新的通用 Windows 平台

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

    ![打开文件夹以查看安装的版本](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

    可以安装多个版本的通用 Windows 平台。 建议对你的应用使用最新版本。

2. 使用文件资源管理器，转到存储 UWP 项目的文件夹。 删除文件 packages.config，并在此文件夹中创建一个新的 .json 文件。 将该文件命名为 project.json，然后将以下内容添加到此文件：

   ```json

   {
     "dependencies": {
       "Microsoft.ApplicationInsights": "1.0.0",
       "Microsoft.ApplicationInsights.PersistenceChannel": "1.0.0",
       "Microsoft.ApplicationInsights.WindowsApps": "1.0.0",
       "Microsoft.NETCore.UniversalWindowsPlatform": "5.0.0"
     },
     "frameworks": {
       "uap10.0": {}
     },
     "runtimes": {
       "win10-arm": {},
       "win10-arm-aot": {},
       "win10-x86": {},
       "win10-x86-aot": {},
       "win10-x64": {},
       "win10-x64-aot": {}
     }
   }

   ```

3. 使用 Visual Studio 打开包含 C#/VB 通用 Windows 应用的解决方案。 你将看到项目文件（.csproj 或 .vbproj 文件）需要更新。 右键单击项目文件并选择编辑该文件。

    ![右键单击该项目，然后选择 "编辑"](../misc/media/uap-editproject.png "UAP_EditProject")

4. 查找 \<PropertyGroup > 包含 \<TargetPlatformVersion > 和 \<TargetPlatformMinVersion 元素的元素。 将 \<TargetPlatformVersion > 的现有值更改为，并 \<TargetPlatformMinVersion > 元素设置为已安装的通用 Windows 平台的相同版本。

    通用 Windows 应用的默认资产规模为 200。 使用 Visual Studio 2015 RC 创建的项目所包含的资产在100进行了调整，需要将值为100的 \<UapDefaultAssetScale > 元素添加到此 PropertyGroup 中。 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

5. 如果添加了对 UWP 扩展 SDK 的任意引用（例如 Windows Mobile SDK），你将需要更新该 SDK 版本。 例如，此 \<SDKReference > 元素：

   ```xml
   <SDKReference Include="WindowsMobile, Version=10.0.0.1">
         <Name>Microsoft Mobile Extension SDK for Universal App Platform</Name>
   </SDKReference>

   ```

    应更改为：

   ```xml
   <SDKReference Include="WindowsMobile, Version=10.0.10240.0">
         <Name>Microsoft Mobile Extension SDK for Universal App Platform</Name>
   </SDKReference>

   ```

6. 使用具有以下值的 name 特性查找 \<Target > 元素： EnsureNuGetPackageBuildImports。 删除此元素及其所有子级。

   ```xml
   <Target Name="EnsureNuGetPackageBuildImports" BeforeTargets="PrepareForBuild">
       <PropertyGroup>
         <ErrorText>This project references NuGet package(s) that are missing on this computer. Use NuGet Package Restore to download them.  For more information, see http://go.microsoft.com/fwlink/?LinkID=322105. The missing file is {0}.</ErrorText>
       </PropertyGroup>
       <Error Condition="!Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets'))" />
       <Error Condition="!Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets'))" />
   </Target>
   ```

7. 查找并删除具有引用 applicationinsights.config 和的项目和条件特性的 \<Import > 元素，如下所示：

   ```xml
   <Import Project="..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets" Condition="Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" />
   <Import Project="..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets" Condition="Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" />

   ```

8. 查找 \<ItemGroup >，它已将 \<Reference 的子元素 > 到 NuGet 包。 记下引用的 NuGet 包，因为在后续步骤中将需要此信息。 Visual Studio 2015 RC 与 Visual Studio 2015 RTM 在 Windows 10 项目格式上的其中一个显著区别是 RTM 格式使用 [NuGet](http://docs.nuget.org/) 版本 3。

    删除 \<ItemGroup > 及其所有子项。 例如，使用 Visual Studio RC 创建的 UWP 项目可能具有以下需要删除的 NuGet 包：

   ```xml
   <ItemGroup>
       <Reference Include="Microsoft.ApplicationInsights, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
         <HintPath>..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="Microsoft.ApplicationInsights.Extensibility.Windows, Version=0.14.3.177, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
         <HintPath>..\packages\Microsoft.ApplicationInsights.WindowsApps.0.14.3-build00177\lib\win81\Microsoft.ApplicationInsights.Extensibility.Windows.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="Microsoft.ApplicationInsights.PersistenceChannel, Version=0.14.3.186, Culture=neutral, PublicKeyToken=31bf3856ad364e35, processorArchitecture=MSIL">
         <HintPath>..\packages\Microsoft.ApplicationInsights.PersistenceChannel.0.14.3-build00177\lib\portable-win81+wpa81\Microsoft.ApplicationInsights.PersistenceChannel.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="System.Numerics.Vectors, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
         <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.dll</HintPath>
         <Private>True</Private>
       </Reference>
       <Reference Include="System.Numerics.Vectors.WindowsRuntime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a, processorArchitecture=MSIL">
         <HintPath>..\packages\System.Numerics.Vectors.4.0.0\lib\win8\System.Numerics.Vectors.WindowsRuntime.dll</HintPath>
         <Private>True</Private>
       </Reference>
     </ItemGroup>

   ```

9. 查找 \<ItemGroup > 包含 \<AppxManifest > 元素的元素。 如果有一个 \<None > 元素的 Include 特性设置为： machine.config，请将其删除。 此外，添加包含特性的 \<None > 元素，并将其值设置为： "。

10. 保存更改。 然后关闭项目文件。

11. 在解决方案资源管理器中右键单击项目文件，然后从上下文菜单中选择“重新加载项目”。 项目中的所有文件现在都应显示在解决方案资源管理器中。

12. 在解决方案资源管理器中，选择文件 ApplicationInsights.config 并打开其属性。 将“生成操作”属性更改为“内容”，并将“复制到输出目录”属性更改为“如果较新则复制”。

13. 在项目中打开 package.appxmanifest 文件。

    1. 查找 \<TargetDeviceFamily > 元素。 更改其 MinVersion 和 MaxVersionTested 特性，使其与已安装的通用 Windows 平台版本相对应。 如：

        ```xml
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />
        ```

    2. 保存更改。

14. 使用 NuGet 管理器添加你在之前步骤中删除的包。 Visual Studio 2015 RC 与 Visual Studio 2015 RTM 在 Windows 10 项目格式上的其中一个显著区别是 RTM 格式使用 [NuGet](http://docs.nuget.org/) 版本 3。

    现在可以对应用进行编码、编译和调试。

    如果你有针对通用 Windows 应用的单元测试项目，也必须遵循 [这些步骤](#MigrateUnitTest)。

### <a name="RCUpdate10CPlusPlus"></a>更新C++项目以使用最新通用 Windows 平台

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

     ![打开文件夹以查看安装的版本](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     可以安装多个版本的通用 Windows 平台。 建议对你的应用使用最新版本。

2. 打开包含 C++ 通用 Windows 应用的解决方案。 右键单击项目 .vcxproj 文件，然后选择卸载项目文件。 卸载项目后，再次右键单击项目文件，并选择编辑它。

     ![卸载项目，然后编辑项目文件](../misc/media/uap-editearliercplus.png "UAP_EditEarlierCPlus")

3. 查找不包含 Condition 特性但包含 \<ApplicationTypeRevision > 元素的任何 \<PropertyGroup > 元素。 将 ApplicationTypeRevision 值从 8.2 更新为 10.0。 添加一个 \<WindowsTargetPlatformVersion > 和一个 \<WindowsTargetPlatformMinVersion > 元素，并将其值设置为所安装通用 Windows 平台版本的值。

     添加一个 \<EnableDotNetNativeCompatibleProfile > 元素，并将其值设置为 true （如果该元素尚不存在）。

     通用 Windows 应用的默认资产规模为 200。 使用 Visual Studio 2015 RC 创建的项目所包含的资产在100进行了调整，需要将值为100的 \<UapDefaultAssetScale > 元素添加到此 PropertyGroup 中。 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

     这 \<PropertyGroup > 元素现在如下所示：

    ```xml
    <PropertyGroup Label="Globals">
        …
        <MinimumVisualStudioVersion>14.0</MinimumVisualStudioVersion>
        <ApplicationType>Windows Store</ApplicationType>
        <ApplicationTypeRevision>10.0</ApplicationTypeRevision>
        <WindowsTargetPlatformVersion>10.0.10240.0</WindowsTargetPlatformVersion>
        <WindowsTargetPlatformMinVersion>10.0.10240.0</WindowsTargetPlatformMinVersion>
        <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>
        <UapDefaultAssetScale>100</UapDefaultAssetScale>
      </PropertyGroup>

    ```

4. 对于剩余的每个 \<PropertyGroup > 元素，请检查元素是否具有具有发布配置的 Condition 特性。 如果是这样，但它不包含 \<UseDotNetNativeToolchain > 元素，则添加一个。 将 \<UseDotNetNativeToolchain > 元素的值设置为 true，如下所示：

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>

    ```

5. 需要更新 \<EnableDotNetNativeCompatibleProfile > 元素和 \<UseDotNetNativeToolchain > 元素以启用 .NET Native，但C++模板中未启用 .NET Native。

     保存更改。 然后关闭项目文件。

6. 在解决方案资源管理器中右键单击项目文件，然后从上下文菜单中选择“重新加载项目”。 项目中的所有文件现在都应显示在解决方案资源管理器中。

7. 在项目中打开 package.appxmanifest 文件。

    1. 查找 \<TargetDeviceFamily > 元素。 更改其 MinVersion 和 MaxVersionTested 特性，使其与已安装的通用 Windows 平台版本相对应。 如：

        ```xml
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />
        ```

    2. 保存更改。

         现在可以对应用进行编码、编译和调试。

         如果你有针对通用 Windows 应用的单元测试项目，也必须遵循 [这些步骤](#MigrateUnitTest)。

## <a name="MigrateUnitTest"></a>用 Visual Studio 2015 RC 创建的通用 Windows 应用的现有单元测试项目所需的更改
 如果你使用 Visual Studio 2015 RC 创建了针对 Windows 10 通用应用的单元测试项目，则需要对你的项目文件进行这些额外更改，以将这些测试项目与最新版 Visual Studio 2015 一起使用。 所需更改因用于创建应用的语言而异：

- [C#/VB 应用](#UnitTestRCUpdate10CSharp)

- [C++应用](#UnitTestRCUpdate10CPlusPlus)

### <a name="UnitTestRCUpdate10CSharp"></a>更新你C#的/VB 单元测试项目

1. 使用 Visual Studio，打开包含 C#/VB 单元测试项目的解决方案。 将 \<OuttputType > 元素的值更改为： AppContainerExe。

   ```xml

   <OutputType>AppContainerExe</OutputType>

   ```

2. 将此元素 \<EnableCoreRuntime > false \</EnableCoreRuntime > 替换为以下元素：

   ```xml

   <EnableDotNetNativeCompatibleProfile>true</EnableDotNetNativeCompatibleProfile>

   ```

3. 删除以下各行：

   ```xml

   <PropertyGroup>
       <AppXPackage>True</AppXPackage>
       <AppxPackageIncludePrivateSymbols>true</AppxPackageIncludePrivateSymbols>
    </PropertyGroup>
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
    <PlatformTarget>AnyCPU</PlatformTarget>
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <Optimize>false</Optimize>
    <OutputPath>bin\Debug\</OutputPath>
    <DefineConstants>DEBUG;TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    </PropertyGroup>
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
       <PlatformTarget>AnyCPU</PlatformTarget>
       <DebugType>pdbonly</DebugType>
       <Optimize>true</Optimize>
       <OutputPath>bin\Release\</OutputPath>
       <DefineConstants>TRACE;NETFX_CORE;WINDOWS_UAP</DefineConstants>
       <ErrorReport>prompt</ErrorReport>
       <WarningLevel>4</WarningLevel>
    </PropertyGroup>

   ```

4. 添加此元素 \<UseDotNetNativeToolchain > true \</UseDotNetNativeToolchain > 作为这些属性组的子元素：

   ```xml

   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|ARM'">
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X86'">
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X64'">

   ```

5. 删除以下 \<ItemGroup > 元素：

   ```xml

   <ItemGroup>
      <Compile Include="Properties\AssemblyInfo.cs" />
      <Compile Include="UnitTest.cs" />
   </ItemGroup>
   <ItemGroup>
      <AppxManifest Include="Package.appxmanifest">
         <SubType>Designer</SubType>
      </AppxManifest>
      <None Include="packages.config" />
      <None Include="UnitTestProject1_TemporaryKey.pfx" />
   </ItemGroup>
   <ItemGroup>
      <Content Include="Properties\Default.rd.xml" />
      <Content Include="Assets\Logo.scale-240.png" />
      <Content Include="Assets\SmallLogo.scale-240.png" />
      <Content Include="Assets\SplashScreen.scale-240.png" />
      <Content Include="Assets\Square71x71Logo.scale-240.png" />
      <Content Include="Assets\StoreLogo.scale-240.png" />
      <Content Include="Assets\WideLogo.scale-240.png" />
   </ItemGroup>

   ```

    将它们替换为以下元素：

   ```xml

   <ItemGroup>
      <Compile Include="Properties\AssemblyInfo.cs" />
      <Compile Include="UnitTestApp.xaml.cs">
         <DependentUpon>UnitTestApp.xaml</DependentUpon>
      </Compile>
      <Compile Include="UnitTest.cs" />
   </ItemGroup>
   <ItemGroup>
      <ApplicationDefinition Include="UnitTestApp.xaml">
         <Generator>MSBuild:Compile</Generator>
         <SubType>Designer</SubType>
      </ApplicationDefinition>
   </ItemGroup>
   <ItemGroup>
      <AppxManifest Include="Package.appxmanifest">
         <SubType>Designer</SubType>
      </AppxManifest>
      <None Include="UnitTestProject1_TemporaryKey.pfx" />
   </ItemGroup>
   <ItemGroup>
      <Content Include="Properties\UnitTestApp.rd.xml" />
      <Content Include="Assets\LockScreenLogo.scale-200.png" />
      <Content Include="Assets\SplashScreen.scale-200.png" />
      <Content Include="Assets\Square150x150Logo.scale-200.png" />
      <Content Include="Assets\Square44x44Logo.scale-200.png" />
      <Content Include="Assets\Square44x44Logo.targetsize-24_altform-unplated.png" />
      <Content Include="Assets\StoreLogo.png" />
      <Content Include="Assets\Wide310x150Logo.scale-200.png" />
   </ItemGroup>
   ```

6. 创建新的单元测试项目，并将 UnitTestApp.xaml 和 UnitTestApp.xaml.cs 文件从新项目复制到你要更新的现有单元测试项目。

7. 将 UnitTestApp.rd.xml 文件从新单元测试项目的 Properties 文件夹复制到要更新的现有单元测试项目的 Properties 文件夹。

8. 在项目中打开 package.appxmanifest 文件。 然后从中删除这些元素：

   ```xml

   <Applications>
      <Application Id="vstest.executionengine.universal.App"
            Executable="vstest.executionengine.appcontainer.uap.exe"
            EntryPoint="Microsoft.VisualStudio.TestPlatform.TestExecutor.AppContainer.App">
         <uap:VisualElements
            DisplayName="UnitTestProject1"
            Square150x150Logo="Assets\Logo.png"
            Square44x44Logo="Assets\SmallLogo.png"
            Description="UnitTestProject1"
            BackgroundColor="#464646">
            <uap:SplashScreen Image="Assets\SplashScreen.png" />
         </uap:VisualElements>
      </Application>
   </Applications>
   <Capabilities>
      <Capability Name="internetClientServer" />
   </Capabilities>
   ```

    将已删除的这些元素替换为以下元素。 根据的你项目名称而不是以下元素中的 UnitTestProject1，使用 ProjectName 的适当值：

   ```xml

   <Applications>
      <Application Id="vstest.executionengine.universal.App"
            Executable="$targetnametoken$.exe"
            EntryPoint="UnitTestProject1.App">
         <uap:VisualElements
               DisplayName="UnitTestProject1"
               Square150x150Logo="Assets\Square150x150Logo.png"
               Square44x44Logo="Assets\Square44x44Logo.png"
               Description="UnitTestProject1"
               BackgroundColor="transparent">
            <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png"/>
            <uap:SplashScreen Image="Assets\SplashScreen.png" />
         </uap:VisualElements>
      </Application>
   </Applications>
   <Capabilities>
      <Capability Name="internetClient" />
   </Capabilities>
   ```

   现在可以运行你的单元测试。

### <a name="UnitTestRCUpdate10CPlusPlus"></a>更新C++项目以使用最新通用 Windows 平台

1. 使用 Visual Studio，打开包含你 C++ 单元测试项目的解决方案。 删除下列元素：

    ```xml

    <TestApplication>true</TestApplication>
    <AppxPackage>True</AppxPackage>
    <CppWindowsStoreUnitTestLibraryType>true</CppWindowsStoreUnitTestLibraryType>
    <EnableCoreRuntime>false</EnableCoreRuntime>

    ```

2. 如果此元素下的以下 \<ProjectConfiguration > 元素 \<ItemGroup Label = "ProjectConfigurations" > （如果它们尚不在此填充中）：

    ```xml

    <ProjectConfiguration Include="Debug|x64">
       <Configuration>Debug</Configuration>
       <Platform>x64</Platform>
    </ProjectConfiguration>
    <ProjectConfiguration Include="Release|x64">
       <Configuration>Release</Configuration>
       <Platform>x64</Platform>
    </ProjectConfiguration>

    ```

3. 替换此元素的每个匹配项：

    ```xml

    <ConfigurationType>DynamicLibrary</ConfigurationType>

    ```

     替换为以下内容：

    ```xml

    <ConfigurationType>Application</ConfigurationType>

    ```

4. 如果文件中尚不存在这些 \<PropertyGroup > 元素，则添加这些元素：

    ```xml

    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'" Label="Configuration">
       <ConfigurationType>Application</ConfigurationType>
       <UseDebugLibraries>true</UseDebugLibraries>
       <PlatformToolset>v140</PlatformToolset>
    </PropertyGroup>
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'" Label="Configuration">
       <ConfigurationType>Application</ConfigurationType>
       <UseDebugLibraries>false</UseDebugLibraries>
       <WholeProgramOptimization>true</WholeProgramOptimization>
       <PlatformToolset>v140</PlatformToolset>
       <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
    </PropertyGroup>

    ```

5. 替换此元素的每个匹配项：

    ```xml

    <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
    ```

     替换为以下内容：

    ```xml

    <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>

    ```

6. 替换此元素的每个匹配项：

    ```xml

    <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\Lib;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>

    ```

     替换为以下内容：

    ```xml

    <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>

    ```

7. 将这些 \<ItemDefinitionGroup > 元素添加到已包含其他 \<ItemDefinitionGroup > 元素的部分中：

    ```xml

    <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Debug|x64'">
       <ClCompile>
          <AdditionalOptions>/bigobj %(AdditionalOptions)</AdditionalOptions>
          <DisableSpecificWarnings>4453;28204</DisableSpecificWarnings>
          <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%     (AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
       </ClCompile>
    <Link>
       <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>
    </Link>
    </ItemDefinitionGroup>
    <ItemDefinitionGroup Condition="'$(Configuration)|$(Platform)'=='Release|x64'">
       <ClCompile>
          <AdditionalOptions>/bigobj %(AdditionalOptions)</AdditionalOptions>
          <DisableSpecificWarnings>4453;28204</DisableSpecificWarnings>
          <AdditionalIncludeDirectories>$(VCInstallDir)UnitTest\include\UWP;$(ProjectDir);$(IntermediateOutputPath);%(AdditionalIncludeDirectories)</AdditionalIncludeDirectories>
       </ClCompile>
       <Link>
          <AdditionalLibraryDirectories>$(VCInstallDir)UnitTest\lib\UWP;%(AdditionalLibraryDirectories)</AdditionalLibraryDirectories>
       </Link>
    </ItemDefinitionGroup>

    ```

8. 删除以下 \< ItemGroup > 元素：

    ```xml

    <ItemGroup>
       <Image Include="Assets\Logo.scale-100.png" />
       <Image Include="Assets\SmallLogo.scale-100.png" />
       <Image Include="Assets\StoreLogo.scale-100.png" />
       <Image Include="Assets\SplashScreen.scale-100.png" />
       <Image Include="Assets\WideLogo.scale-100.png" />
    </ItemGroup>

    ```

     将其替换为此 \<ItemGroup > 元素：

    ```xml

    <ItemGroup>
       <Image Include="Assets\LockScreenLogo.scale-200.png" />
       <Image Include="Assets\SplashScreen.scale-200.png" />
       <Image Include="Assets\Square44x44Logo.scale-200.png" />
       <Image Include="Assets\Square44x44Logo.targetsize-24_altform-unplated.png" />
       <Image Include="Assets\Square150x150Logo.scale-200.png" />
       <Image Include="Assets\StoreLogo.png" />
       <Image Include="Assets\Wide310x150Logo.scale-200.png" />
    </ItemGroup>

    ```

9. 删除以下 \< ItemGroup > 元素：

    ```xml

    <ItemGroup>
       <ClInclude Include="pch.h" />
    </ItemGroup>
    ```

     将其替换为这些 \<ItemGroup > 元素：

    ```xml

    <ItemGroup>
       <ClInclude Include="pch.h" />
       <ClInclude Include="UnitTestApp.xaml.h">
          <DependentUpon>UnitTestApp.xaml</DependentUpon>
       </ClInclude>
    </ItemGroup>
    <ItemGroup>
       <ApplicationDefinition Include="UnitTestApp.xaml">
          <SubType>Designer</SubType>
       </ApplicationDefinition>
    </ItemGroup>

    ```

10. 删除以下元素：

    ```xml
    <ClCompile Include="UnitTest.cpp"/>
    ```

     将其替换为这些 \<CICompile > 元素：

    ```xml

    <ClCompile Include="UnitTestApp.xaml.cpp">
       <DependentUpon>UnitTestApp.xaml</DependentUpon>
    </ClCompile>
    <ClCompile Include="UnitTest.cpp"/>

    ```

11. 添加此元素：

    ```xml
    <Import Project="$(VCTargetsPath)\Microsoft.Cpp.targets" />
    ```

     在文件中的此元素上：

    ```xml

    <ItemGroup>
       <Xml Include="UnitTestApp.rd.xml" />
    </ItemGroup>
    ```

12. 创建新的单元测试 C++ 项目，并将 UnitTestApp.xaml、UnitTestApp.xaml.cpp、UnitTestApp.xaml.h 和 UnitTestApp.rd.xml 文件从该项目复制到你要更新的现有项目。

13. 在项目中打开 package.appxmanifest 文件。 然后从中删除这些元素：

    ```xml

    <Applications>
       <Application Id="vstest.executionengine.universal.App"
             Executable="vstest.executionengine.appcontainer.uap.exe"
             EntryPoint="Microsoft.VisualStudio.TestPlatform.TestExecutor.AppContainer.App">
          <uap:VisualElements
             DisplayName="UnitTestProject1"
             Square150x150Logo="Assets\Logo.png"
             Square44x44Logo="Assets\SmallLogo.png"
             Description="UnitTestProject1"
             BackgroundColor="#464646">
             <uap:SplashScreen Image="Assets\SplashScreen.png" />
          </uap:VisualElements>
       </Application>
    </Applications>
    <Capabilities>
       <Capability Name="internetClientServer" />
    </Capabilities>

    ```

     将已删除的这些元素替换为以下元素。 根据的你项目名称而不是以下元素中的 UnitTestProject1，使用 ProjectName 的适当值：

    ```xml

    <Applications>
       <Application Id="vstest.executionengine.universal.App"
                Executable="$targetnametoken$.exe"
                EntryPoint="UnitTestProject1.App">
          <uap:VisualElements
                DisplayName="UnitTestProject1"
                Square150x150Logo="Assets\Square150x150Logo.png"
                Square44x44Logo="Assets\Square44x44Logo.png"
                Description="UnitTestProject1"
                BackgroundColor="transparent">
                <uap:DefaultTile Wide310x150Logo="Assets\Wide310x150Logo.png"/>
                <uap:SplashScreen Image="Assets\SplashScreen.png" />
          </uap:VisualElements>
       </Application>
    </Applications>
    <Capabilities>
       <Capability Name="internetClient" />
    </Capabilities>

    ```