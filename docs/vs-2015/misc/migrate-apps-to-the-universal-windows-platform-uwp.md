---
title: Migrate apps to the Universal Windows Platform (UWP) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
ms.assetid: 5279ab9b-71d9-4be5-81f6-a1f24b06f5fb
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5794aa5ab7dc14932c65a9156ea9252e71731155
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299470"
---
# <a name="migrate-apps-to-the-universal-windows-platform-uwp"></a>将应用迁移到通用 Windows 平台 (UWP)
对使用 Visual Studio 2015 RC 创建的 Windows Store 8.1 应用、Windows Phone 8.1 应用或通用 Windows 应用的现有项目文件进行必要的手动更改，以便它们能与 Visual Studio 2015 RTM 一起使用。 （如果你的 Windows 8.1 通用应用同时具有 Windows 应用项目和 Windows Phone 项目，则需要按照以下步骤迁移每个项目。）

 使用通用 Windows 平台，你现在能使你的应用面向一个或多个设备系列。 若要了解有关通用 Windows 应用的详细信息，请参阅此 [平台指南](https://msdn.microsoft.com/library/windows/apps/dn894631.aspx)。

- [迁移现有 C#/VB Windows 应用商店 8.1 或 Windows Phone 8.1 应用](#MigrateCSharp) 以使用通用 Windows 平台。

- [迁移现有 C++ Windows 应用商店 8.1 或 Windows Phone 8.1 应用](#MigrateCPlusPlus) 以使用通用 Windows 平台。

- [使用 Visual Studio 2015 RC 创建的现有通用 Windows 应用所需的更改](#PreviousVersions)。

- [使用 Visual Studio 2015 RC 创建的通用 Windows 应用的现有单元测试项目所需的更改](#MigrateUnitTest)。

  如果你不想进行所有这些更改，请了解如何 [移植现有应用](https://msdn.microsoft.com/library/windows/apps/xaml/mt238321.aspx) 到新的通用 Windows 项目。

## <a name="MigrateCSharp"></a> Migrate your C#/VB Windows Store 8.1 or Windows Phone 8.1 apps to use the Universal Windows Platform

#### <a name="migrate-your-cvb-project-files"></a>迁移 C#/VB 项目文件

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

     ![Open the folder to view the versions installed](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

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

     ![Right click the project and choose Edit](../misc/media/uap-editproject.png "UAP_EditProject")

6. Find the \<PropertyGroup> element that contains the \<TargetPlatformVersion> element with a value of 8.1. Do the following steps for this \<PropertyGroup> element:

    1. Set the value of the \<Platform> element to: **x86**.

    2. Add a \<TargetPlatformIdentifier> element and set its value to: **UAP**.

    3. Change the existing value of the \<TargetPlatformVersion> element to be the value of the Universal Windows Platform version that you installed. Also add a \<TargetPlatformMinVersion> element and give it the same value.

    4. Change the value of the \<MinimumVisualStudioVersion> element to: **14**.

    5. Replace the \<ProjectTypeGuids> element as shown below:

         对于 C#：

        ```xml
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}</ProjectTypeGuids>
        ```

         对于 VB：

        ```xml
        <ProjectTypeGuids>{A5A43C5B-DE2A-4C0C-9213-0A381AF9435A};{F184B08F-C81C-45F6-A57F-5ABD9991F28F}</ProjectTypeGuids>
        ```

    6. Add an \<EnableDotNetNativeCompatibleProfile> element and set its value to: **true**.

    7. 通用 Windows 应用的默认资产规模为 200。 If your project includes assets not scaled at 200, you will need to add a \<UapDefaultAssetScale> element with the value of the scale of your assets to this PropertyGroup. 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

         Now your \<PropertyGroup> element should look similar to this example:

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

8. Find \<PropertyGroup> elements that are configured for the AnyCPU platform as part of the Condition attribute. 删除这些元素及其所有子元素。 在 Visual Studio 2015 中，Windows 10 应用不支持 AnyCPU。 For example, you should remove \<PropertyGroup> elements like these ones:

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

9. For each remaining \<PropertyGroup> element, check if the element has a Condition attribute with a Release configuration. If it does, but it does not contain a \<UseDotNetNativeToolchain> element, then add one. Set the value for the \<UseDotNetNativeToolchain> element to true, like this:

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

10. For Windows Phone projects only, remove the \<PropertyGroup> element that contains a \<TargetPlatformIdentifier> element with a value of WindowsPhoneApp. 同时删除此元素的任何子级：

    ```xml
    <PropertyGroup Condition=" '$(TargetPlatformIdentifier)' == '' ">
      <TargetPlatformIdentifier>WindowsPhoneApp</TargetPlatformIdentifier>
    </PropertyGroup>
    ```

11. Find the \<ItemGroup> element that contains the \<AppxManifest> element. Add the following \<None> element as a child of the \<ItemGroup> element:

    ```xml
    <None Include="project.json" />
    ```

12. Find the \<ItemGroup> element that contains other assets that are added to your project such as logo .png files (\<Content Include="Assets\Logo.scale-100.png" />). Add the following \<Content> child element to this \<ItemGroup> element:

     **For C#:**

    ```xml
    <Content Include="Properties\default.rd.xml" />
    ```

     **For VB:**

    ```xml
    <Content Include="My Project\default.rd.xml" />
    ```

13. Find the \<ItemGroup> element that includes \<Reference> children elements to NuGet packages. 记下你使用的 NuGet 包，因为在重新加载项目后你将需要使用 NuGet 包管理器下载它们。 Remove this \<ItemGroup> along with its children. 例如，UWP 项目可能具有以下需要删除的 NuGet 包：

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

## <a name="MigrateCPlusPlus"></a> Migrate your C++ Windows Store 8.1 or Windows Phone 8.1 apps to use the Universal Windows Platform

#### <a name="migrate-your-c-project-files"></a>迁移 C++ 项目文件

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

     ![Open the folder to view the versions installed](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     可以安装多个版本的通用 Windows 平台。 建议对你的应用使用最新版本。

2. 在 Visual Studio 中打开包含现有 C++ Windows 应用商店 8.1 应用或 Windows Phone 8.1 应用的解决方案。

     在解决方案资源管理器中右键单击现有项目，然后选择“卸载项目”。 卸载项目后，再次右键单击项目文件，并选择编辑 .vcxproj 文件。

     ![Right&#45;click project file and choose to edit](../misc/media/uap-editcplusproject.png "UAP_EditCPlusProject")

3. Find the \<PropertyGroup> element that contains the \<ApplicationTypeRevision> element with a value of 8.1. Do the following steps for this \<PropertyGroup> element:

    1. Add a \<WindowsTargetPlatformVersion> element and a \<WindowsTargetPlatformMinVersion> element and give them the value of the Universal Windows Platform version that you installed.

    2. 将 ApplicationTypeRevision 元素的值从 8.1 更新为 10.0。

    3. Change the value of the \<MinimumVisualStudioVersion> element to: 14.

    4. Add an \<EnableDotNetNativeCompatibleProfile> element and set its value to: true.

    5. 通用 Windows 应用的默认资产规模为 200。 If your project includes assets not scaled at 200, you will need to add a \<UapDefaultAssetScale> element with the value of the scale of your assets to this PropertyGroup. 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

    6. For Windows Phone projects only, change the value of \<ApplicationType> from Windows Phone to Windows Store.

         Now your \<PropertyGroup> element should look similar to this example:

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

4. Change all instances of the \<PlatformToolset> element to have the value v140. 例如:

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>
    ```

5. For each remaining \<PropertyGroup> element, check if the element has a Condition attribute with a Release configuration. If it does, but it does not contain a \<UseDotNetNativeToolchain> element, then add one. Set the value for the \<UseDotNetNativeToolchain> element to true, like this:

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

## <a name="PackageManifest"></a> Update your package manifest file for all your Windows Store 8.1 or Windows Phone 8.1 projects
 必须更新解决方案中每个项目的包清单文件。

#### <a name="update-your-package-manifest-file"></a>更新包清单文件

1. 在项目中打开 package.appxmanifest 文件。 需要编辑每个 Windows 应用商店项目和 Windows Phone 项目的 Package.AppxManifest 文件。

2. You need to update the \<Package> element with the new schemas based on your existing project type. 首先根据你使用的是 Windows 应用商店项目还是 Windows Phone 项目删除以下架构。

    **OLD for Windows Store project:** Your \<Package> element will look similar to this one.

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"
       xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest">

   ```

    **OLD for Windows Phone project:** Your \<Package> element will look similar to this one.

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/2010/manifest"
   xmlns:m2="http://schemas.microsoft.com/appx/2013/manifest"
   xmlns:m3="http://schemas.microsoft.com/appx/2014/manifest"
   xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest">
   ```

    **NEW for Universal Windows Platform:** Add the schemas below to your \<Package> element. 从刚才删除的架构的元素中删除任何关联的命名空间标识符前缀。 将 IgnorableNamespaces 属性更新为：uap mp。 Your new \<Package> element should look similar to this one.

   ```xml
   <Package
       xmlns="http://schemas.microsoft.com/appx/manifest/foundation/windows10"
       xmlns:uap="http://schemas.microsoft.com/appx/manifest/uap/windows10"
       xmlns:mp="http://schemas.microsoft.com/appx/2014/phone/manifest"
      IgnorableNamespaces= "uap mp">

   ```

3. Add a \<Dependencies> child element to the \<Package> element. Then add a \<TargetDeviceFamily> child element to this \<Dependencies> element with Name, MinVersion, and MaxVersionTested attributes. 为 Name 属性赋予值：Windows.Universal。 为 MinVersion 和 MaxVersionTested 赋予已安装通用 Windows 平台版本的值。 此元素应类似于：

   ```xml
   <Dependencies>
   <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10069.0" MaxVersionTested="10.0.10069.0" />
   </Dependencies>
   ```

4. **For Windows Store only:** You need to add a \<mp:PhoneIdentity> child element to the \<Package> element. 添加 PhoneProductId 属性和 PhonePublisherId 属性。 Set the PhoneProductId to have the same value as the Name attribute in the \<Identity> element. 将 PhonePublishedId 值设置为：00000000-0000-0000-0000-000000000000。 如：

   ```xml
   <Identity Name="aa3815a1-2d97-4c71-8c99-578135b28cd8" Publisher="CN=xxxxxxxx" Version="1.0.0.0" />
   <mp:PhoneIdentity PhoneProductId="aa3815a1-2d97-4c71-8c99-578135b28cd8" PhonePublisherId="00000000-0000-0000-0000-000000000000"/>
   ```

5. Find the \<Prerequisites> element and delete this element and any child elements that it has.

6. Add the **uap** namespace to the following \<Resource> elements: Scale, DXFeatureLevel. 例如:

   ```xml
   <Resources>
     <Resource Language="en-us"/>
    <Resource uap:Scale="180"/>
    <Resource uap:DXFeatureLevel="dx11"/>
   </Resources>

   ```

7. Add the **uap** namespace to the following \<Capability> elements: documentsLibrary, picturesLibrary, videosLibrary, musicLibrary, enterpriseAuthentication, sharedUserCertificates, removableStorage, appointments, and contacts. 例如:

   ```xml
   <Capabilities>
     <uap:Capability Name="documentsLibrary"/>
     <uap:Capability Name="removableStorage"/>
   </Capabilities>

   ```

8. Add the **uap** namespace to the \<VisualElements> element and any of its child elements. 例如:

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

    **仅适用于 Windows 应用商店：** 磁贴大小名称已更改。 Change the attributes in the \<VisualElements> element to reflect the new converged tile sizes. 70x70 变为 71x71，30x30 变为 44x44。

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

9. Add the **uap** namespace to the \<ApplicationContentUriRules> and all its child elements. 例如:

    ```xml
    <uap:ApplicationContentUriRules>
      <uap:Rule Type="include" Match="https://www.microsoft.com/"/>
      <uap:Rule Type="exclude" Match="*.pdf"/>
    </uap:ApplicationContentUriRules>

    ```

10. Add the **uap** namespace to the following \<Extension> elements and all of its child elements: windows.accountPictureProvide,  windows.alarm, windows.appointmentsProvider windows.autoPlayContent,  windows.autoPlayDevice, windows.cachedFileUpdate, windows.cameraSettings, windows.fileOpenPicker, windows.fileTypeAssociation, windows.fileSavePicke, windows.lockScreenCall, windows.printTaskSettings, windows.protocol, windows.search, windows.shareTarget. 例如:

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

12. 更改框架依赖项。 Add a Publisher name to all \<PackageDependency> elements, and specify a MinVersion if it’s not already specified.

     **OLD:** \<PackageDependency> element

    ```xml
    <Dependencies>
     <PackageDependency Name="Microsoft.VCLibs.120.00" />
    </Dependencies>

    ```

     **NEW:** \<PackageDependency> element

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

     **OLD:**

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

     **OLD:**

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

    1. These attributes for \<VisualElements> are deprecated and should be removed:

       - The \<VisualElements> attributes: ForegroundText, ToastCapable

       - The \<DefaultTile> attribute DefaultSize

       - The \<ApplicationView> element

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

    1. 打开文件资源管理器，单击工具栏中的“视图” ，然后选择“已隐藏项” 和“文件名扩展”。 Open this folder on your machine: \<path for the location of your solution>\\.vs\\{Project Name}\v14. 如果存在具有 .suo 文件扩展名的文件，请将其删除。

    2. 现在返回解决方案所在的文件夹。 打开解决方案中存在的项目的任何文件夹。 如果任何这些项目文件夹中的文件具有 .csproj.user 或 .vbproj.user 扩展名，请将其删除。

         现在可以在 Visual Studio 中重新打开解决方案。 现在你可以使用通用 Windows 平台对应用程序进行编码、编译和调试。

         了解如何 [调整代码](https://msdn.microsoft.com/library/windows/apps/dn954974.aspx) 以利用通用 Windows 平台的新增功能。

## <a name="PreviousVersions"></a> Changes required for existing Universal Windows apps created with Visual Studio 2015 RC
 如果你使用 Visual Studio 2015 RC 创建了 Windows 10 通用应用，则需重定项目的目标，以使用随最新版 Visual Studio 2015 一起安装的通用 Windows 平台的版本。 不支持任何以前的版本。 所需更改因用于创建应用的语言而异：

- [C#/VB apps](#RCUpdate10CSharp)

- [C++ apps](#RCUpdate10CPlusPlus)

### <a name="RCUpdate10CSharp"></a> Update your C#/VB projects to use the latest Universal Windows Platform
 为现有应用打开解决方案时，你将看到你的应用需要更新：

 ![View your project in Solution Explorer](../misc/media/uwp-updaterequired.png "UWP_UpdateRequired")

 如果选择从解决方案资源管理器重新加载此项目，你将看到此对话框：

 ![Retarget your app to use the correct SDK](../misc/media/missingsdkforuap.png "MissingSDKforUAP")

 因为你项目的通用 Windows 平台 SDK 目前暂不受支持，因此无法进行安装。 请单击“确定”，然后执行以下操作。

##### <a name="update-your-cvb-projects-to-use-the-latest-universal-windows-platform"></a>更新 C#/VB 项目以使用最新的通用 Windows 平台

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

    ![Open the folder to view the versions installed](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

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

    ![Right click the project and choose Edit](../misc/media/uap-editproject.png "UAP_EditProject")

4. Find the \<PropertyGroup> element that contains the \<TargetPlatformVersion> and \<TargetPlatformMinVersion> elements. Change the existing value of the \<TargetPlatformVersion> and \<TargetPlatformMinVersion> elements to be the same version of the Universal Windows Platform that you have installed.

    通用 Windows 应用的默认资产规模为 200。 Projects created with Visual Studio 2015 RC included assets scaled at 100, you will need to add a \<UapDefaultAssetScale> element with a value of 100 to this PropertyGroup. 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

5. 如果添加了对 UWP 扩展 SDK 的任意引用（例如 Windows Mobile SDK），你将需要更新该 SDK 版本。 For example this \<SDKReference> element:

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

6. Find the \<Target> element with a name attribute that has the value: EnsureNuGetPackageBuildImports. 删除此元素及其所有子级。

   ```xml
   <Target Name="EnsureNuGetPackageBuildImports" BeforeTargets="PrepareForBuild">
       <PropertyGroup>
         <ErrorText>This project references NuGet package(s) that are missing on this computer. Use NuGet Package Restore to download them.  For more information, see http://go.microsoft.com/fwlink/?LinkID=322105. The missing file is {0}.</ErrorText>
       </PropertyGroup>
       <Error Condition="!Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets'))" />
       <Error Condition="!Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" Text="$([System.String]::Format('$(ErrorText)', '..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets'))" />
   </Target>
   ```

7. Find and delete the \<Import> elements with Project and Condition attributes that reference Microsoft.Diagnostics.Tracing.EventSource and Microsoft.ApplicationInsights, like this:

   ```xml
   <Import Project="..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets" Condition="Exists('..\packages\Microsoft.Diagnostics.Tracing.EventSource.Redist.1.1.16-beta\build\portable-net45+win8+wpa81\Microsoft.Diagnostics.Tracing.EventSource.Redist.targets')" />
   <Import Project="..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets" Condition="Exists('..\packages\Microsoft.ApplicationInsights.0.14.3-build00177\build\portable-win81+wpa81\Microsoft.ApplicationInsights.targets')" />

   ```

8. Find the \<ItemGroup> that has \<Reference> children elements to NuGet packages. 记下引用的 NuGet 包，因为在后续步骤中将需要此信息。 Visual Studio 2015 RC 与 Visual Studio 2015 RTM 在 Windows 10 项目格式上的其中一个显著区别是 RTM 格式使用 [NuGet](https://docs.microsoft.com/nuget/) 版本 3。

    Remove the \<ItemGroup> and all its children. 例如，使用 Visual Studio RC 创建的 UWP 项目可能具有以下需要删除的 NuGet 包：

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

9. Find the \<ItemGroup> element that contains an \<AppxManifest> element. If there is a \<None> element with an Include attribute set to: packages.config, delete it. Also, add a \<None> element with an Include attribute and set its value to: project.json.

10. 保存更改。 然后关闭项目文件。

11. 在解决方案资源管理器中右键单击项目文件，然后从上下文菜单中选择“重新加载项目”。 项目中的所有文件现在都应显示在解决方案资源管理器中。

12. 在解决方案资源管理器中，选择文件 ApplicationInsights.config 并打开其属性。 将“生成操作”属性更改为“内容”，并将“复制到输出目录”属性更改为“如果较新则复制”。

13. 在项目中打开 package.appxmanifest 文件。

    1. Find the \<TargetDeviceFamily> element. 更改其 MinVersion 和 MaxVersionTested 特性，使其与已安装的通用 Windows 平台版本相对应。 如：

        ```xml
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />
        ```

    2. 保存更改。

14. 使用 NuGet 管理器添加你在之前步骤中删除的包。 Visual Studio 2015 RC 与 Visual Studio 2015 RTM 在 Windows 10 项目格式上的其中一个显著区别是 RTM 格式使用 [NuGet](https://docs.microsoft.com/nuget/) 版本 3。

    现在可以对应用进行编码、编译和调试。

    如果你有针对通用 Windows 应用的单元测试项目，也必须遵循 [这些步骤](#MigrateUnitTest)。

### <a name="RCUpdate10CPlusPlus"></a> Update your C++ projects to use the latest Universal Windows Platform

1. 若要了解已安装的通用 Windows 平台，请打开此文件夹： **\Program Files (x86)\Windows Kits\10\Platforms\UAP**。 它包含每个已安装通用 Windows 平台的文件夹列表。 文件夹名称是已安装的通用 Windows 平台版本。 例如，此 Windows 10 设备安装了 10.0.10240.0 版的通用 Windows 平台。

     ![Open the folder to view the versions installed](../misc/media/uap-uwpversions.png "UAP_UWPVersions")

     可以安装多个版本的通用 Windows 平台。 建议对你的应用使用最新版本。

2. 打开包含 C++ 通用 Windows 应用的解决方案。 右键单击项目 .vcxproj 文件，然后选择卸载项目文件。 卸载项目后，再次右键单击项目文件，并选择编辑它。

     ![Unload the project, then edit the project file](../misc/media/uap-editearliercplus.png "UAP_EditEarlierCPlus")

3. Find any \<PropertyGroup> elements that do not contain a Condition attribute but do contain an \<ApplicationTypeRevision> element. 将 ApplicationTypeRevision 值从 8.2 更新为 10.0。 Add a \<WindowsTargetPlatformVersion> and a \<WindowsTargetPlatformMinVersion> element and set their values to be the value of the Universal Windows Platform version that you installed.

     Add an \<EnableDotNetNativeCompatibleProfile> element and set its value to true if the element does not already exist.

     通用 Windows 应用的默认资产规模为 200。 Projects created with Visual Studio 2015 RC included assets scaled at 100, you will need to add a \<UapDefaultAssetScale> element with a value of 100 to this PropertyGroup. 了解有关 [资产和规模](https://msdn.microsoft.com/library/jj679352.aspx)的详细信息。

     So this \<PropertyGroup> element will now be similar to this:

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

4. For each remaining \<PropertyGroup> element, check if the element has a Condition attribute with a Release configuration. If it does, but it does not contain a \<UseDotNetNativeToolchain> element, then add one. Set the value for the \<UseDotNetNativeToolchain> element to true, like this:

    ```xml
    <PropertyGroup Condition="'$(Configuration)|$(Platform)'=='Release|Win32'" Label="Configuration">
        <ConfigurationType>Application</ConfigurationType>
        <UseDebugLibraries>false</UseDebugLibraries>
        <WholeProgramOptimization>true</WholeProgramOptimization>
        <PlatformToolset>v140</PlatformToolset>
        <UseDotNetNativeToolchain>true</UseDotNetNativeToolchain>
      </PropertyGroup>

    ```

5. You need to update the \<EnableDotNetNativeCompatibleProfile> element and the \<UseDotNetNativeToolchain> element to enable .NET Native, but .NET Native is not enabled in the C++ templates.

     保存更改。 然后关闭项目文件。

6. 在解决方案资源管理器中右键单击项目文件，然后从上下文菜单中选择“重新加载项目”。 项目中的所有文件现在都应显示在解决方案资源管理器中。

7. 在项目中打开 package.appxmanifest 文件。

    1. Find the \<TargetDeviceFamily> element. 更改其 MinVersion 和 MaxVersionTested 特性，使其与已安装的通用 Windows 平台版本相对应。 如：

        ```xml
        <TargetDeviceFamily Name="Windows.Universal" MinVersion="10.0.10240.0" MaxVersionTested="10.0.10240.0" />
        ```

    2. 保存更改。

         现在可以对应用进行编码、编译和调试。

         如果你有针对通用 Windows 应用的单元测试项目，也必须遵循 [这些步骤](#MigrateUnitTest)。

## <a name="MigrateUnitTest"></a> Changes required for existing unit test projects for Universal Windows apps created with Visual Studio 2015 RC
 如果你使用 Visual Studio 2015 RC 创建了针对 Windows 10 通用应用的单元测试项目，则需要对你的项目文件进行这些额外更改，以将这些测试项目与最新版 Visual Studio 2015 一起使用。 所需更改因用于创建应用的语言而异：

- [C#/VB apps](#UnitTestRCUpdate10CSharp)

- [C++ apps](#UnitTestRCUpdate10CPlusPlus)

### <a name="UnitTestRCUpdate10CSharp"></a> Update your C#/VB unit test projects

1. 使用 Visual Studio，打开包含 C#/VB 单元测试项目的解决方案。 Change the value of the \<OuttputType> element to: AppContainerExe.

   ```xml

   <OutputType>AppContainerExe</OutputType>

   ```

2. Replace this element \<EnableCoreRuntime>false\</EnableCoreRuntime> with the following element:

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

4. Add this element \<UseDotNetNativeToolchain>true\</UseDotNetNativeToolchain> as a child element to these property groups:

   ```xml

   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|ARM'">
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X86'">
   <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|X64'">

   ```

5. Delete the following \<ItemGroup> elements:

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

### <a name="UnitTestRCUpdate10CPlusPlus"></a> Update your C++ projects to use the latest Universal Windows Platform

1. 使用 Visual Studio，打开包含你 C++ 单元测试项目的解决方案。 删除下列元素：

    ```xml

    <TestApplication>true</TestApplication>
    <AppxPackage>True</AppxPackage>
    <CppWindowsStoreUnitTestLibraryType>true</CppWindowsStoreUnitTestLibraryType>
    <EnableCoreRuntime>false</EnableCoreRuntime>

    ```

2. Add the following \<ProjectConfiguration> elements below this element \<ItemGroup Label="ProjectConfigurations"> if they are not already in this fille:

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

4. Add these \<PropertyGroup> elements if they are not already in the file:

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

7. Add these \<ItemDefinitionGroup> elements in the section that already contains other \<ItemDefinitionGroup> elements:

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

8. Delete the following \< ItemGroup> element:

    ```xml

    <ItemGroup>
       <Image Include="Assets\Logo.scale-100.png" />
       <Image Include="Assets\SmallLogo.scale-100.png" />
       <Image Include="Assets\StoreLogo.scale-100.png" />
       <Image Include="Assets\SplashScreen.scale-100.png" />
       <Image Include="Assets\WideLogo.scale-100.png" />
    </ItemGroup>

    ```

     Replace it with this \<ItemGroup> element:

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

9. Delete the following \< ItemGroup> element:

    ```xml

    <ItemGroup>
       <ClInclude Include="pch.h" />
    </ItemGroup>
    ```

     Replace it with these \<ItemGroup> elements:

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

     Replace it with these \<CICompile> elements:

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