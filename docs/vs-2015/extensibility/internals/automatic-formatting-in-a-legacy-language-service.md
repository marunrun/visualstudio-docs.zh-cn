---
title: 旧版语言服务中的自动格式设置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services, automatic formatting
ms.assetid: c210fc94-77bd-4694-b312-045087d8a549
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e6183fc47138ebb5108e4fbbd2bfa407e5804a72
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157269"
---
# <a name="automatic-formatting-in-a-legacy-language-service"></a>在旧版语言服务中进行自动格式设置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

对于自动格式设置，当用户开始键入已知的代码构造时，语言服务会自动插入代码片段。  
  
## <a name="automatic-formatting-behavior"></a>自动设置格式行为  
 例如，当你键入时 `if` ，语言服务会自动插入匹配的大括号，或者，如果按 enter 键，则语言服务会将新行上的插入点强制为适当的缩进级别，具体取决于上面的行是否打开了新的作用域。  
  
 用于其他语言服务的命令筛选器也可用于自动格式设置。 还可以通过调用突出显示匹配的大括号 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> 。  
  
## <a name="see-also"></a>另请参阅  
 [开发旧版语言服务](../../extensibility/internals/developing-a-legacy-language-service.md)
