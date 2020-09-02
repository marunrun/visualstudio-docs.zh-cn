---
title: 通过 VSIX v3 在 extension 文件夹外安装 |Microsoft Docs
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa2c7d97dda9bba139ec613b367eedbc6307848a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80700185"
---
# <a name="install-outside-the-extensions-folder"></a>在扩展文件夹外进行安装

从 Visual Studio 2017 和 VSIX v3 开始 (版本 3) ，可以在 extension 文件夹外部安装扩展资产。 目前，以下位置将作为 (的有效安装位置启用，其中 [INSTALLDIR] 映射到 Visual Studio 实例的安装目录) ：

* [INSTALLDIR] \MSBuild
* [INSTALLDIR] \Xml\Schemas
* [INSTALLDIR] \Common7\IDE\PublicAssemblies
* [INSTALLDIR] \Licenses
* [INSTALLDIR] \Common7\IDE\ReferenceAssemblies
* [INSTALLDIR] \Common7\IDE\RemoteDebugger
* [INSTALLDIR] \Common7\IDE\VC\VCTargets (仅支持 Visual Studio 2017;Visual Studio 2019 和更高版本中已弃用) 

> [!NOTE]
> VSIX 格式不允许在 Visual Studio 安装文件夹结构的外部安装。 

若要支持安装到这些目录，必须在 "每个实例每台计算机" 上安装 VSIX。 可以通过选中 source.extension.vsixmanifest 设计器中的 "所有用户" 复选框来启用此功能：

![检查所有用户](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>如何设置 InstallRoot

若要设置安装目录，可以使用 Visual Studio 中的 " **属性** " 窗口。 例如，可以将 `InstallRoot` 项目引用的属性设置为上述位置之一：

![安装根属性](media/install-root-properties.png)

这会将某些元数据添加到 `ProjectReference` VSIX 项目的 .csproj 文件中的相应属性：

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 如果愿意，可以直接编辑 .csproj 文件。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>如何在 InstallRoot 下设置子路径

如果要将安装到下的子路径 `InstallRoot` ，可以通过设置属性来实现此操作，就 `VsixSubPath` 像属性一样 `InstallRoot` 。 例如，假设我们要将项目引用的输出安装到 "[INSTALLDIR] \MSBuild\MyCompany\MySDK\1.0"。 可以通过属性设计器轻松实现此目的：

![设置子路径](media/set-subpath.png)

对应的 .csproj 更改将如下所示：

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>额外的信息

属性设计器的更改仅适用于项目引用;你 `InstallRoot` 还可以使用上述) 的相同方法，设置项目内项的元数据 (。
