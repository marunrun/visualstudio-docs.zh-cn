---
title: 网站支持 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects
ms.assetid: ce9f4266-bb64-4c09-be88-4bd6413f60d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 22047ad1b0709cefa200656e61f8e0d39ace94c9
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703445"
---
# <a name="web-site-support"></a>网站支持
网站项目系统是创建 Web 项目的项目系统。 Web 项目反过来创建 Web 应用程序。 网站项目为具有关联代码的每个网页生成一个可执行文件。 其他可执行文件从 /App_Code 文件夹中的源代码文件生成。

 网站项目系统是通过向现有项目系统添加模板和注册属性来创建的。 这些属性之一为语言选择 IntelliSense 提供程序。 当请求未缓存的智能 Web 页时，IntelliSense 提供程序实现处理引用并调用语言编译器。

 编译网页的语言编译器必须注册到[!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]。 您可以在 Web.config 文件中使用[\<编译器>元素](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element)来注册编译器，如以下示例所示：

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>本节内容
- [网站支持模板](../../extensibility/internals/web-site-support-templates.md)

 列出可用于创建新网站项目和相关项的模板。

- [网站支持属性](../../extensibility/internals/web-site-support-attributes.md)

 显示将网站项目连接到[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]和[!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)]的注册属性。

## <a name="related-sections"></a>相关章节
- [Web 项目](../../extensibility/internals/web-projects.md)

 概述了两种类型的 Web 项目，即网站项目和 Web 应用程序项目。
