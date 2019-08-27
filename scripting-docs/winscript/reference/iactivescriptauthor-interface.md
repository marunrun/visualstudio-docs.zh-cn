---
title: IActiveScriptAuthor 接口 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptAuthor interface
ms.assetid: df1f454d-01ee-4beb-928b-48513d07365a
caps.latest.revision: 15
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6b3d9725d72f5213aadc3d9400bef87cecb20ba0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63009724"
---
# <a name="iactivescriptauthor-interface"></a>IActiveScriptAuthor 接口
表示创作服务，包括 IntelliSense 和排序规则的信息。  
  
 除了继承的方法之外`IUnknown`，则`IActiveScriptAuthor`接口公开以下方法。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法  
  
|方法|描述|  
|------------|-----------------|  
|[IActiveScriptAuthor::AddNamedItem](../../winscript/reference/iactivescriptauthor-addnameditem.md)|将根级别项的名称添加到引擎的命名空间创作的脚本。 一个*根级别项*是包含属性和方法，并且，还可以包含事件源的对象。|  
|[IActiveScriptAuthor::AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md)|将作为根级别的子级添加的代码 scriptlet`IScriptNode`对象。 在主机，scriptlet 的完全限定的名称可以有只有两个级别。|  
|[IActiveScriptAuthor::AddTypeLib](../../winscript/reference/iactivescriptauthor-addtypelib.md)|将类型库添加到脚本的命名空间。|  
|[IActiveScriptAuthor::GetChars](../../winscript/reference/iactivescriptauthor-getchars.md)|返回请求的完成上下文完成字符组。|  
|[IActiveScriptAuthor::GetEventHandler](../../winscript/reference/iactivescriptauthor-geteventhandler.md)|返回具有指定的特性的 scriptlet。|  
|[IActiveScriptAuthor::GetInfoFromContext](../../winscript/reference/iactivescriptauthor-getinfofromcontext.md)|返回类型的代码块中的信息和给定的字符的定位点位置。 IntelliSense、 全局列表和参数的提示，这提供有关成员的信息。|  
|[IActiveScriptAuthor::GetLanguageFlags](../../winscript/reference/iactivescriptauthor-getlanguageflags.md)|返回语言的信息。|  
|[IActiveScriptAuthor::GetRoot](../../winscript/reference/iactivescriptauthor-getroot.md)|返回`IScriptNode`作者的脚本树的根。|  
|[IActiveScriptAuthor::GetScriptletTextAttributes](../../winscript/reference/iactivescriptauthor-getscriptlettextattributes.md)|返回 scriptlet 文本的属性。|  
|[IActiveScriptAuthor::GetScriptTextAttributes](../../winscript/reference/iactivescriptauthor-getscripttextattributes.md)|返回脚本块的文本属性。|  
|[IActiveScriptAuthor::IsCommitChar](../../winscript/reference/iactivescriptauthor-iscommitchar.md)|返回一个值，指示给定的字符是否应由应用程序提交语句完成。|  
|[IActiveScriptAuthor::ParseScriptText](../../winscript/reference/iactivescriptauthor-parsescripttext.md)|分析脚本文本、 将文本添加到创作脚本创作引擎，并创建`IScriptEntry`对应于脚本块的对象。|  
|[IActiveScriptAuthor::RemoveNamedItem](../../winscript/reference/iactivescriptauthor-removenameditem.md)|删除`NamedItem`脚本创作引擎的命名空间中的对象。|  
|[IActiveScriptAuthor::RemoveTypeLib](../../winscript/reference/iactivescriptauthor-removetypelib.md)|从创作引擎命名空间的脚本中删除类型库。|  
  
## <a name="see-also"></a>请参阅  
 [活动脚本创作接口](../../winscript/reference/active-script-authoring-interfaces.md)