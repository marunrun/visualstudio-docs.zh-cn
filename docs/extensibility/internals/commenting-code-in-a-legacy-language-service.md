---
title: 在旧语言服务中注释代码 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5450199fde29f581dafdf9b2884c88ef26ea4ce7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709441"
---
# <a name="comment-code-in-a-legacy-language-service"></a>旧语言服务中的注释代码
编程语言通常提供注释或注释代码的方法。 注释是文本的一部分，提供有关代码的其他信息，但在编译或解释过程中被忽略。

 托管包框架 （MPF） 类支持注释和取消注释的选定文本。

## <a name="comment-styles"></a>注释样式
有两种一般注释样式：

1. 行注释，其中注释位于单行上。

2. 阻止注释，其中注释可能包含多行。

行注释通常具有起始字符（或字符），而块注释具有开头字符和结束字符。 例如，在 C# 中，行注释以`//`开头，块注释以`/*`开头，以`*/`结尾。

当用户从 **"编辑** > **高级"** 菜单中选择命令 **"注释选择**"时，该命令将路由到<xref:Microsoft.VisualStudio.Package.Source>类<xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A>上的方法。 当用户选择命令 **"取消注释选择"** 时，命令将路由到<xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A>方法。

## <a name="support-code-comments"></a>支持代码注释
 您可以通过 的`EnableCommenting`命名参数来提供语言服务支持代码注释。 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 这将设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A>类的属性<xref:Microsoft.VisualStudio.Package.LanguagePreferences>。 有关设置语言服务功能的详细信息，请参阅[注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)。

 还必须重写 方法<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>以返回具有语言注释<xref:Microsoft.VisualStudio.Package.CommentInfo>字符的结构。 C#样式行注释字符为默认值。

### <a name="example"></a>示例
 下面是<xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A>方法的实现示例。

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
- [传统语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)
- [注册旧语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
