---
title: 旧版语言服务中的注释代码 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ec42d81a2d472cec5f96cbeec416801c22465834
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66342045"
---
# <a name="comment-code-in-a-legacy-language-service"></a>在旧版语言服务中的注释代码
编程语言通常提供一种方法来添加批注或注释的代码。 注释是文本来提供有关代码的其他信息，但在编译或解释过程中忽略的一部分。

 托管的包框架 (MPF) 类的注释和取消注释所选文本提供支持。

## <a name="comment-styles"></a>注释样式
有两种常规样式的注释：

1. 行注释，其中注释是在单个行。

2. 块注释，注释可以包含多个行的位置。

行的注释通常具有起始字符 （或字符），块注释时具有开始和结束字符。 例如，在 C# 中，行注释开头`//`，和块注释开头`/*`结尾`*/`。

当用户选择命令**注释选定内容**从**编辑** > **高级**菜单中，该命令将路由到<xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A>方法<xref:Microsoft.VisualStudio.Package.Source>类。 当用户选择命令**取消注释选定内容**，该命令将路由到<xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A>方法。

## <a name="support-code-comments"></a>支持代码注释
 你可以通过将语言服务支持代码注释`EnableCommenting`名为的参数<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>。 这将设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A>属性的<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。 有关设置语言服务功能的详细信息，请参阅[注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

 您还必须重写<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>方法以返回<xref:Microsoft.VisualStudio.Package.CommentInfo>结构与您的语言的注释字符。 C# 的样式行注释字符是默认值。

### <a name="example"></a>示例
 下面是示例实现的<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>方法。

```csharp
using Microsoft.VisualStudio.Package;

namespace MyLanguagePackage
{
    class MySource : Source
    {
        public override CommentInfo GetCommentFormat() {
            CommentInfo info = new CommentInfo();
            info.LineStart       = "//";
            info.BlockStart      = "/*";
            info.BlockEnd        = "*/";
            info.UseLineComments = true;
            return info;
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)