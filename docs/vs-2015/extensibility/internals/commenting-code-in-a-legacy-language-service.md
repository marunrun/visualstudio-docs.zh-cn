---
title: 对旧版语言服务中的代码进行注释 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- comments, supporting in language services [managed package framework]
- language services [managed package framework], commenting code
ms.assetid: 9600d6f0-e2b6-4fe0-b935-fb32affb97a4
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cd1405456ca9a6ba00926c82bcc7959ea36d26c2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160908"
---
# <a name="commenting-code-in-a-legacy-language-service"></a>在旧版语言服务中注释代码
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

编程语言通常提供一种批注或注释代码的方法。 注释是提供有关代码的其他信息但在编译或解释过程中被忽略的文本部分。  
  
 管理包框架 (MPF) 类提供对所选文本进行注释和取消注释的支持。  
  
## <a name="comment-styles"></a>注释样式  
 注释有两种常规样式：  
  
1. 行注释，其中注释位于单个行。  
  
2. 阻止注释，其中注释可能包含多行。  
  
   行注释的开头字符 (或字符) ，而块注释则包含开始字符和结束字符。 例如，在 c # 中，行注释以//开头，块注释以/* 开头，以 \* /结尾。  
  
   当用户从 "**编辑**高级" 菜单中选择命令**注释选择**时  ->  **Advanced** ，该命令将路由到 <xref:Microsoft.VisualStudio.Package.Source.CommentSpan%2A> 类的方法 <xref:Microsoft.VisualStudio.Package.Source> 。 当用户选择 " **取消注释选定内容**" 命令时，该命令将路由到 <xref:Microsoft.VisualStudio.Package.Source.UncommentSpan%2A> 方法。  
  
## <a name="supporting-code-comments"></a>支持代码注释  
 你可以通过的命名参数，使你的语言服务支持代码注释 `EnableCommenting` <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 。 这将设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCommenting%2A> 类的属性 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。 有关设置 language servicce 功能的详细信息，请参阅 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)) 。  
  
 还必须重写 <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> 方法以返回 <xref:Microsoft.VisualStudio.Package.CommentInfo> 包含语言注释字符的结构。 C # 样式行注释字符是默认值。  
  
### <a name="example"></a>示例  
 下面是方法的实现示例 <xref:Microsoft.VisualStudio.Package.Source.GetCommentFormat%2A> 。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [旧版语言服务功能](../../extensibility/internals/legacy-language-service-features1.md)   
 [注册旧版语言服务](../../extensibility/internals/registering-a-legacy-language-service1.md)
