---
title: 网站支持 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a9f6e287a2cd91b0a5eb0d04130627faa787ccac
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323181"
---
# <a name="web-site-support"></a>网站支持
网站项目系统是创建 Web 项目的项目系统。 反过来，web 项目创建 Web 应用程序。 网站项目会生成一个可执行文件，每个网页关联的代码。 其他可执行文件是从 /App_Code 文件夹中的源代码文件生成的。

 通过将模板和注册属性添加到现有的项目系统创建网站项目系统。 其中一个属性选择的语言的 IntelliSense 提供程序。 IntelliSense 提供程序实现处理引用，并请求未缓存智能 Web 页时调用的语言编译器。

 必须已注册的语言编译器用于编译网页[!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]。 可以使用[\<编译器 > 元素](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element)在 Web.config 文件以注册的编译器，如以下示例所示：

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>本节内容
- [网站支持模板](../../extensibility/internals/web-site-support-templates.md)

 列出可用于创建新网站项目和关联的项的模板。

- [网站支持属性](../../extensibility/internals/web-site-support-attributes.md)

 显示连接到的网站项目的注册属性[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和[!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]。

## <a name="related-sections"></a>相关章节
- [Web 项目](../../extensibility/internals/web-projects.md)

 概述了两种类型的 Web 项目、 网站项目和 Web 应用程序项目。