---
title: 创建PkgDef实用程序 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- package definition
- create pkgdef
- pkgdef
- createpkgdef
ms.assetid: c745cb76-47a6-49ff-9eed-16af0f748e35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 9f437eb3586dc16bb0b4b9eb60cd303eb90db6c3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709157"
---
# <a name="createpkgdef-utility"></a>创建PkgDef实用程序
将 Visual Studio 扩展名的 .dll 文件作为参数，并创建一个 *.pkgdef*文件来伴随 *.dll*文件。 *.pkgdef*文件包含安装扩展名时将写入系统注册表的所有信息。

> [!NOTE]
> Visual Studio SDK 中包含的大多数项目模板都会自动创建 *.pkgdef*文件，作为生成过程的一部分。 本文档适用于希望手动创建包或将现有包转换为使用 *.pkgdef*部署的用户。

## <a name="syntax"></a>语法

```
CreatePkgDef /out=<FileName> [/codebase] [/assembly] <AssemblyPath>
```

## <a name="arguments"></a>自变量
**/out=&lt;文件名&gt;**\
必需。 将 *.pkgdef*输出文件的名称设置到&lt;FileName&gt;。

**/代码库**\
可选。 强制使用**CodeBase**实用程序进行注册。

**/装配**\
强制向**装配实用程序**注册。

**&lt;装配路径&gt;**\
要从中生成 *.pkgdef*的 *.dll*文件的路径。

## <a name="remarks"></a>备注
使用 *.pkgdef*文件的扩展部署取代了早期版本的 Visual Studio 的注册表要求。

::: moniker range=">=vs-2019"

*.pkgdef*文件必须安装在以下位置之一：

- *%本地应用数据%%\微软_可视化工作室\16.0\扩展\\*

- *%vsinstalldir%\公共7_IDE_扩展\\*

如果安装文件夹是 *%localappdata%%\Microsoft_Visual Studio_16.0\\\扩展*，则 Visual Studio 会识别扩展，但默认情况下将禁用该扩展。 用户可以使用**管理扩展启用扩展**。

如果安装文件夹为 *%vsvsinstalldir%\Common7_IDE\扩展\\*，则默认情况下将启用扩展。

> [!NOTE]
> 除非扩展作为 VSIX 包的一部分安装，否则"**管理扩展"** 工具不能用于访问扩展。

::: moniker-end

::: moniker range="vs-2017"

*.pkgdef*文件必须安装在以下位置之一：

- *%本地应用数据%%\微软_可视化工作室\15.0\扩展\\*

- *%vsinstalldir%\公共7_IDE_扩展\\*

如果安装文件夹是 *%localappdata%%\Microsoft_Visual Studio_15.0\\\扩展*，则 Visual Studio 会识别扩展，但默认情况下将禁用该扩展。 用户可以使用**扩展和更新**启用扩展。

如果安装文件夹为 *%vsvsinstalldir%\Common7_IDE\扩展\\*，则默认情况下将启用扩展。

> [!NOTE]
> 扩展**和更新**工具不能用于访问扩展，除非它是作为 VSIX 包的一部分安装的。

::: moniker-end

## <a name="see-also"></a>请参阅
- [创建 ExpInstance 实用程序](../../extensibility/internals/createexpinstance-utility.md)
