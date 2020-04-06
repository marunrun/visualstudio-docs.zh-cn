---
title: 网站支持属性 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef75f99480145475278357a552f3ac74c0289800
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703499"
---
# <a name="web-site-support-attributes"></a>网站支持属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]可以扩展网站项目，为 Web 编程语言提供支持。 语言必须注册[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]自身，以便项目模板在选择语言时可以显示在 **"新建网站"** 对话框中。

IronPython 工作室示例包括网站支持。 该示例包含以下属性类，用于将 IronPython 注册为新 Web 项目的代码背后语言。

## <a name="websiteprojectattribute"></a>网站项目属性
 此属性放置在语言项目上。 它将语言添加到 **"新建网站"** 对话框中 **"语言**"列表中的 Web 编程语言列表中。 例如，以下代码将 IronPython 添加到列表中：

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 此属性还将模板路径设置以指向模板文件夹。 有关模板文件夹位置的详细信息，请参阅[网站支持模板](../../extensibility/internals/web-site-support-templates.md)。

## <a name="websiteprojectrelatedfilesattribute"></a>网站项目相关文件属性
 此属性放置在语言项目上。 它允许网站项目嵌套一个文件类型（相关）在**解决方案资源管理器**中的另一个文件类型（主文件类型）。

 例如，以下代码指定 IronPython 代码背后文件与 .aspx 文件相关。 在 IronPython 网站解决方案中创建新的 .aspx Web 页时，将生成新的 .py 源文件，并显示为 .aspx 页的子节点。

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>提供感知提供程序属性
 此属性放置在语言项目包上。 它为语言选择 IntelliSense 提供程序。

 例如，以下代码指定应按需创建 PythonIntellisenseProvider<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>的实例来提供语言服务。

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 IVsIntellisenseProject 在请求包含代码的 Web 页但不缓存时处理引用并调用语言编译器。

## <a name="see-also"></a>请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)
