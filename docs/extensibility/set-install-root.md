---
title: 使用 VSIX v3 在扩展文件夹外安装 |微软文档
ms.date: 11/09/2016
ms.topic: conceptual
ms.assetid: 913c3745-8aa9-4260-886e-a05aecfb2225
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: aa2c7d97dda9bba139ec613b367eedbc6307848a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80700185"
---
# <a name="install-outside-the-extensions-folder"></a>在扩展文件夹外进行安装

从 Visual Studio 2017 和 VSIX v3（版本 3）开始，可以在扩展文件夹之外安装扩展资产。 目前，以下位置已启用为有效的安装位置（其中 [INSTALLDIR] 映射到 Visual Studio 实例的安装目录）：

* [INSTALLDIR]_MSBuild
* [INSTALLDIR]\Xml_Schema
* [INSTALLDIR]_公共7_IDE_公共程序集
* [INSTALLDIR]=许可证
* [INSTALLDIR]=通用7_IDE_参考程序集
* [INSTALLDIR]_公共7_IDE_远程调试器
* [INSTALLDIR]_通用7_IDE_VC目标（仅适用于 2017 年视觉工作室;2019 年及以后用于视觉工作室）

> [!NOTE]
> VSIX 格式不允许在 Visual Studio 安装文件夹结构之外安装。 

为了支持安装到这些目录，VSIX 必须"每台计算机按实例安装"。 这可以通过选中扩展中的"所有用户"复选框来启用。

![检查所有用户](media/check-all-users.png)

## <a name="how-to-set-the-installroot"></a>如何设置安装根

要设置安装目录，可以使用 Visual Studio 中的 **"属性**"窗口。 例如，您可以将项目引用`InstallRoot`的属性设置为上述位置之一：

![安装根属性](media/install-root-properties.png)

这将在 VSIX 项目的`ProjectReference`.csproj 文件内向相应的属性添加一些元数据：

```xml
 <ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
        <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
        <Name>ClassLibrary1</Name>
        <InstallRoot>PublicAssemblies</InstallRoot>
 </ProjectReference>
```

> [!NOTE]
> 如果您愿意，可以直接编辑 .csproj 文件。

## <a name="how-to-set-a-subpath-under-the-installroot"></a>如何在"安装根"下设置子路径

如果要安装到 下面的子路径，`InstallRoot`可以通过设置`VsixSubPath`属性与`InstallRoot`属性类似来执行此操作。 例如，假设我们希望项目引用的输出安装到'[INSTALLDIR]MSBuild_MyCompany_MySDK_1.0'。 我们可以轻松地与属性设计师一起执行此操作：

![设置子路径](media/set-subpath.png)

相应的 .csproj 更改如下所示：

```xml
<ProjectReference Include="..\ClassLibrary1\ClassLibrary1.csproj">
       <Project>{69a979f1-eba2-43e7-9346-0e56e803508b}</Project>
       <Name>ClassLibrary1</Name>
       <InstallRoot>MSBuild</InstallRoot>
       <VSIXSubPath>MyCompany\MySDK\1.0</VSIXSubPath>
</ProjectReference>
```

## <a name="extra-information"></a>额外信息

属性设计器更改不仅适用于项目引用，还应用于项目引用。也可以设置项目内`InstallRoot`项目的元数据（使用上述相同的方法）。
