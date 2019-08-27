---
title: 网站支持属性 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- web site projects, registration
ms.assetid: 46d52e2c-ca2a-4bbd-8500-5b0129768aec
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1a508acaf174e5e4e4b4b615e5f38c600f0669ed
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66323384"
---
# <a name="web-site-support-attributes"></a>网站支持属性
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 网站项目可以进行扩展以提供对 Web 的支持编程语言。 语言必须注册自行向[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]，以便项目模板可以出现在**新的 Web 站点**对话框时选择的语言。

IronPython Studio 示例包括 web 站点的支持。 该示例包含以下的特性类，以将 IronPython 注册为新的 Web 项目的代码隐藏文件语言。

## <a name="websiteprojectattribute"></a>WebSiteProjectAttribute
 此特性置于语言项目。 它将语言添加到 Web 中的编程语言的列表**语言**列表中**新的 Web 站点**对话框。 例如，下面的代码将 IronPython 添加到列表：

```
[WebSiteProject("IronPython", "Iron Python")]
public class PythonProjectPackage : ProjectPackage
```

 此属性还可设置的模板路径以指向模板文件夹。 有关模板文件夹的位置的详细信息，请参阅[网站支持模板](../../extensibility/internals/web-site-support-templates.md)。

## <a name="websiteprojectrelatedfilesattribute"></a>WebSiteProjectRelatedFilesAttribute
 此特性置于语言项目。 允许的网站项目嵌套 （相关） 的一种文件类型在另一种文件类型 （主） 中**解决方案资源管理器**。

 例如，下面的代码指定 IronPython 代码隐藏文件与.aspx 文件关联。 IronPython Web 站点解决方案中创建新的.aspx 网页后，新的.py 源文件生成并显示为.aspx 页的一个子节点。

```
[WebSiteProjectRelatedFiles("aspx", "py")]
public class PythonProjectPackage : ProjectPackage
```

## <a name="provideintellisenseproviderattribute"></a>ProvideIntellisenseProviderAttribute
 此特性置于语言项目包。 它将选择的语言的 IntelliSense 提供程序。

 例如，下面的代码指定 PythonIntellisenseProvider，实现的实例<xref:Microsoft.VisualStudio.Shell.Interop.IVsIntellisenseProject>，应创建按需提供语言服务。

```
[ProvideIntellisenseProvider(typeof(PythonIntellisenseProvider), "IronPythonCodeProvider", "Iron Python", ".py", "IronPython;Python", "IronPython")]
public class PythonPackage : Package, IOleComponent
```

 IVsIntellisenseProject 实现处理引用，并包含代码的网页请求，但未缓存时调用的语言编译器。

## <a name="see-also"></a>请参阅
- [网站支持](../../extensibility/internals/web-site-support.md)