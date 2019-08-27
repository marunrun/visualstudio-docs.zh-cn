---
title: 实现智能主机帮助程序接口 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Smart Host Helper Interfaces, implementing
ms.assetid: b9c44246-4d4d-469e-91be-00c8f5796fa5
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a9a5b94a25a838845acab2ce1c49295b0b28d425
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62976191"
---
# <a name="implementing-smart-host-helper-interfaces"></a>实现智能宿主帮助程序接口
[IDebugDocumentHelper 接口](../winscript/reference/idebugdocumenthelper-interface.md)接口极大简化了为活动调试创建智能主机的任务，因为它提供了智能主机所需的许多接口的实现。  
  
 如果为使用 `IDebugDocumentHelper` 的智能主机，主机应用程序必须执行下列三种操作：  
  
1. `CoCreate` 进程调试管理器，并使用 [IProcessDebugManager 接口](../winscript/reference/iprocessdebugmanager-interface.md) 接口将应用程序添加到可调试的应用程序列表中。  
  
2. 使用 [IProcessDebugManager::CreateDebugDocumentHelper](../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md) 方法创建每个脚本对象的调试文档帮助程序。 确保已定义文档名称、父文档、文本和脚本块。  
  
3. 在实现 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 接口（活动脚本所需的接口）的对象上实现 [IActiveScriptSiteDebug 接口](../winscript/reference/iactivescriptsitedebug-interface.md)接口。 `IActiveScriptSiteDebug` 接口上唯一不常用的方法只需委托给帮助程序。  
  
   如果主机需要进一步控制语法颜色、文档上下文创建和其他扩展功能，则该主机可以实现 [IDebugDocumentHost 接口](../winscript/reference/idebugdocumenthost-interface.md)接口（可选）。  
  
   智能主机帮助程序的主要限制是，它只能处理添加后其内容更改或压缩的文档（尽管文档可以扩展）。 但是，对于许多智能主机来说，它提供的功能正好是所需要的。  
  
   以下部分将更详细介绍每个步骤。  
  
## <a name="create-an-application-object"></a>创建应用程序对象  
 在使用智能主机帮助程序之前，需要创建 [IDebugApplication 接口](../winscript/reference/idebugapplication-interface.md)对象以在调试程序中表示你的应用程序。  
  
#### <a name="to-create-an-application-object"></a>创建应用程序对象  
  
1. 使用 `CoCreateInstance` 创建进程调试管理器的实例。  
  
2. 调用 [IProcessDebugManager::CreateApplication](../winscript/reference/iprocessdebugmanager-createapplication.md)。  
  
3. 使用 [IDebugApplication::SetName](../winscript/reference/idebugapplication-setname.md) 在应用程序上设置名称。  
  
4. 使用 [IProcessDebugManager::AddApplication](../winscript/reference/iprocessdebugmanager-addapplication.md) 将应用程序对象添加到可调试的应用程序的列表中。  
  
     下面的代码概述了此过程，但不包括错误检查或其他可靠的编程技术。  
  
    ```cpp
    CoCreateInstance(CLSID_ProcessDebugManager, NULL,  
          CLSCTX_INPROC_SERVER | CLSCTX_INPROC_HANDLER  
          | CLSCTX_LOCAL_SERVER,  
    IID_IProcessDebugManager, (void **)&g_ppdm);  
    g_ppdm->CreateApplication(&g_pda);  
    g_pda->SetName(L"My cool application");  
    g_ppdm->AddApplication(g_pda, &g_dwAppCookie);  
    ```  
  
## <a name="using-idebugdocumenthelper"></a>使用 IDebugDocumentHelper  
  
#### <a name="to-use-the-helper-minimal-sequence-of-steps"></a>使用帮助程序（最少的步骤顺序）  
  
1. 对于每个主机的文档，使用 [IProcessDebugManager::CreateDebugDocumentHelper](../winscript/reference/iprocessdebugmanager-createdebugdocumenthelper.md) 创建帮助程序。  
  
2. 调用帮助程序上的 [IDebugDocumentHelper::Init](../winscript/reference/idebugdocumenthelper-init.md)，提供名称、文档属性等。  
  
3. 使用文档（或者，如果文档是根，则为 NULL）的父级帮助程序调用 [IDebugDocumentHelper::Attach](../winscript/reference/idebugdocumenthelper-attach.md)，以定义文档在树中的位置并使其对调试程序可见。  
  
4. 调用 [IDebugDocumentHelper::AddDBCSText](../winscript/reference/idebugdocumenthelper-adddbcstext.md) 或 [IDebugDocumentHelper::AddUnicodeText](../winscript/reference/idebugdocumenthelper-addunicodetext.md) 来定义该文档的文本。 （如果像浏览器那样以递增方式下载文档，则可以多次调用。）  
  
5. 调用 [IDebugDocumentHelper::DefineScriptBlock](../winscript/reference/idebugdocumenthelper-definescriptblock.md)定义每个脚本块和关联的脚本引擎的范围。  
  
## <a name="implementing-iactivescriptsitedebug"></a>实现 IActiveScriptSiteDebug  
 若要实现 [IActiveScriptSiteDebug::GetDocumentContextFromPosition](../winscript/reference/iactivescriptsitedebug-getdocumentcontextfromposition.md)，请获取与给定站点相对应的帮助程序，然后获取给定源上下文的起始文档偏移量，如下所示：  
  
```cpp
pddh->GetScriptBlockInfo(dwSourceContext, NULL, &ulStartPos, NULL);  
```  
  
 接下来，使用帮助程序为给定的字符偏移量创建新的文档上下文：  
  
```cpp
pddh->CreateDebugDocumentContext(ulStartPos + uCharacterOffset, cChars, &pddcNew);  
```  
  
 若要实现 [IActiveScriptSiteDebug::GetRootApplicationNode](../winscript/reference/iactivescriptsitedebug-getrootapplicationnode.md)，只需调用 `IDebugApplication::GetRootNode`（继承自 [IRemoteDebugApplication::GetRootNode](../winscript/reference/iremotedebugapplication-getrootnode.md)）。  
  
 若要实现 [IDebugDocumentHelper::GetDebugApplicationNode](../winscript/reference/idebugdocumenthelper-getdebugapplicationnode.md)，只需返回最初使用进程调试管理器创建的 `IDebugApplication`。  
  
## <a name="the-optional-idebugdocumenthost-interface"></a>可选的 IDebugDocumentHost 接口  
 主机可以使用 [IDebugDocumentHelper::SetDebugDocumentHost](../winscript/reference/idebugdocumenthelper-setdebugdocumenthost.md) 提供 [IDebugDocumentHost 接口](../winscript/reference/idebugdocumenthost-interface.md)的实现，以提供它对帮助程序的额外控制。 以下是主机接口允许执行的一些重要事项：  
  
- 使用 [IDebugDocumentHelper::AddDeferredText](../winscript/reference/idebugdocumenthelper-adddeferredtext.md) 添加文本，以便主机不需要立即提供实际字符。 当真正需要字符时，帮助程序将调用主机上的 [IDebugDocumentHost::GetDeferredText](../winscript/reference/idebugdocumenthost-getdeferredtext.md)。  
  
- 替代由帮助程序提供的默认语法着色。 帮助程序调用 [IDebugDocumentHost::GetScriptTextAttribute](../winscript/reference/idebugdocumenthost-getscripttextattributes.md) 来确定一系列字符的着色；如果主机返回 `E_NOTIMPL`，则回退到其默认实现。  
  
- 通过实现 [IDebugDocumentHost::OnCreateDocumentContext](../winscript/reference/idebugdocumenthost-oncreatedocumentcontext.md)，为帮助程序创建的文档上下文提供未知的控制。 从而使主机能够替代默认文档上下文实现的功能。  
  
- 为文档提供文件系统中的路径名称。 某些调试 UI 使用它来允许用户编辑和保存对文档所做的更改。 调用 [IDebugDocumentHost::NotifyChanged](../winscript/reference/idebugdocumenthost-notifychanged.md)，以在文档保存后通知主机。  
  
## <a name="see-also"></a>请参阅  
 [活动脚本调试概述](../winscript/active-script-debugging-overview.md)