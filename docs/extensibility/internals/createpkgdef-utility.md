---
title: CreatePkgDef 实用程序 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80709157"
---
# <a name="createpkgdef-utility"></a>CreatePkgDef 实用程序
将 Visual Studio 扩展的 .dll 文件作为参数，并创建 *.pkgdef* 文件以伴随 *.dll* 文件。 *.Pkgdef*文件包含在安装扩展后将写入系统注册表的所有信息。

> [!NOTE]
> Visual Studio SDK 中包含的大多数项目模板会自动在生成过程中创建 *.pkgdef* 文件。 本文档适用于想要手动创建包的人员，或将现有包转换为使用 *.pkgdef*  部署。

## <a name="syntax"></a>语法

```
CreatePkgDef /out=<FileName> [/codebase] [/assembly] <AssemblyPath>
```

## <a name="arguments"></a>参数
**/out = &lt; FileName&gt;**\
必需。 将 *.pkgdef* 输出文件的名称设置为 &lt; FileName &gt; 。

**/codebase**\
可选。 强制注册到 **CodeBase** 实用工具。

**/assembly**\
强制对 **程序集** 实用程序进行注册。

**&lt;AssemblyPath&gt;**\
要从中生成 *. .pkgdef*的 *.dll*文件的路径。

## <a name="remarks"></a>备注
使用 *.pkgdef* 文件的扩展部署将替换 Visual Studio 早期版本的注册表要求。

::: moniker range=">=vs-2019"

*.Pkgdef*文件必须安装在下列位置之一：

- *%localappdata%\Microsoft\Visual Studio\16.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

如果安装文件夹为 *%Localappdata%\Microsoft\Visual Studio\16.0\Extensions \\ *，则 Visual Studio 会识别该扩展，但默认情况下禁用该扩展。 用户可以使用 " **管理扩展**" 来启用该扩展。

如果安装文件夹为 *%vsinstalldir%\Common7\IDE\Extensions \\ *，则默认情况下将启用该扩展。

> [!NOTE]
> " **管理扩展** " 工具不能用于访问扩展，除非它作为 VSIX 包的一部分进行安装。

::: moniker-end

::: moniker range="vs-2017"

*.Pkgdef*文件必须安装在下列位置之一：

- *%localappdata%\Microsoft\Visual Studio\15.0\Extensions\\*

- *%vsinstalldir%\Common7\IDE\Extensions\\*

如果安装文件夹为 *%Localappdata%\Microsoft\Visual Studio\15.0\Extensions \\ *，则 Visual Studio 会识别该扩展，但默认情况下禁用该扩展。 用户可以通过使用 " **扩展和更新**" 来启用该扩展。

如果安装文件夹为 *%vsinstalldir%\Common7\IDE\Extensions \\ *，则默认情况下将启用该扩展。

> [!NOTE]
> " **扩展和更新** " 工具不能用于访问扩展，除非它作为 VSIX 包的一部分进行安装。

::: moniker-end

## <a name="see-also"></a>另请参阅
- [CreateExpInstance 实用程序](../../extensibility/internals/createexpinstance-utility.md)
