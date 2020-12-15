---
title: 网站支持 |Microsoft Docs
description: 了解网站项目系统，这些系统是通过将模板和注册属性添加到现有项目系统创建的。
ms.custom: SEO-VS-2020
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
ms.openlocfilehash: 06f8ffdd504182dd82b11d4b5ce5f57e0a7629c3
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487837"
---
# <a name="web-site-support"></a>网站支持
网站项目系统是用于创建 Web 项目的项目系统。 Web 项目，然后创建 Web 应用程序。 网站项目为每个包含关联代码的网页生成一个可执行文件。 其他可执行文件是从/App_Code 文件夹中的源代码文件生成的。

 网站项目系统是通过将模板和注册属性添加到现有项目系统创建的。 其中一个属性选择语言的 IntelliSense 提供程序。 当请求未缓存的智能网页时，IntelliSense 提供程序实现会处理引用并调用语言编译器。

 用于编译网页的语言编译器必须注册到 [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] 。 您可以使用 Web.config 文件中的[ \<compiler> 元素](/dotnet/framework/configure-apps/file-schema/compiler/compiler-element)来注册编译器，如以下示例中所示：

```
<system.codedom>  <compilers>    <compiler language="py;IronPython" extension=".py"       type="IronPython.CodeDom.PythonProvider, IronPython,       Version=1.0.2391.18146, Culture=neutral,       PublicKeyToken=b03f5f7f11d50a3a" />  </compilers></system.codedom>
```

## <a name="in-this-section"></a>本节内容
- [网站支持模板](../../extensibility/internals/web-site-support-templates.md)

 列出了可用于创建新的网站项目和关联项的模板。

- [网站支持属性](../../extensibility/internals/web-site-support-attributes.md)

 显示将网站项目连接到和的注册属性 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] [!INCLUDE[vstecasp](../../code-quality/includes/vstecasp_md.md)] 。

## <a name="related-sections"></a>相关章节
- [Web 项目](../../extensibility/internals/web-projects.md)

 概括介绍了两种 Web 项目、网站项目和 Web 应用程序项目。
