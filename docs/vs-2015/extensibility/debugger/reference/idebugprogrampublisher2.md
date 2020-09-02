---
title: IDebugProgramPublisher2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2
helpviewer_keywords:
- IDebugProgramPublisher2 interface
ms.assetid: b1d17f63-7146-4076-a588-034cfc6858b9
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d49173a4c1f10be1544cf07b0b01640321d6d181
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697300"
---
# <a name="idebugprogrampublisher2"></a>IDebugProgramPublisher2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

此接口允许调试引擎 (DE) 或自定义端口供应商注册程序以进行调试。  
  
## <a name="syntax"></a>语法  
  
```  
IDebugProgramPublisher2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>实施者注意事项  
 Visual Studio 将实现此接口，以注册要调试的程序，使其在多个进程中可见进行调试。  
  
## <a name="notes-for-callers"></a>调用方说明  
 调用 COM 的 `CoCreateInstance` 函数 `CLSID_ProgramPublisher` 以获取此接口 (参见示例) 。 一个 DE 或自定义端口提供程序使用此接口来注册表示正在调试的程序的程序节点。  
  
## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法  
 此接口实现以下方法：  
  
|方法|说明|  
|------------|-----------------|  
|[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)|使程序节点可用于 DEs 和会话调试管理器 (SDM) 。|  
|[UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)|删除程序节点，使其不再可用。|  
|[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)|使程序对 DEs 和 SDM 可用。|  
|[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)|删除程序，使其不再可用。|  
|[SetDebuggerPresent](../../../extensibility/debugger/reference/idebugprogrampublisher2-setdebuggerpresent.md)|设置指示存在调试器的标志。|  
  
## <a name="remarks"></a>备注  
 此接口使程序和程序节点可用 (即 "发布" 它们) 供 DEs 和会话调试管理器 (SDM) 使用。 若要访问发布的程序和程序节点，请使用 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md) 接口。 这是 Visual Studio 可识别正在调试的程序的唯一方法。  
  
## <a name="requirements"></a>要求  
 标头： msdbg  
  
 命名空间： VisualStudio  
  
 程序集： Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="example"></a>示例  
 此示例演示如何实例化程序发行者并注册程序节点。 这是从教程中的 " [发布程序" 节点](https://msdn.microsoft.com/d0100e02-4e2b-4e72-9e90-f7bc11777bae)中获取的。  
  
```cpp#  
// This is how m_srpProgramPublisher is defined in the class definition:  
// CComPtr<IDebugProgramPublisher2> m_srpProgramPublisher.  
  
void CProgram::Start(IDebugEngine2 * pEngine)  
{  
    m_spEngine = pEngine;  
  
    HRESULT hr = m_srpProgramPublisher.CoCreateInstance(CLSID_ProgramPublisher);  
    if ( FAILED(hr) )  
    {  
        ATLTRACE("Failed to create the program publisher: 0x%x.", hr);  
        return;  
    }  
  
    // Register ourselves with the program publisher. Note that  
    // CProgram implements the IDebgProgramNode2 interface, hence  
    // the static cast on "this".  
    hr = m_srpProgramPublisher->PublishProgramNode(  
        static_cast<IDebugProgramNode2*>(this));  
    if ( FAILED(hr) )  
    {  
        ATLTRACE("Failed to publish the program node: 0x%x.", hr);  
        m_srpProgramPublisher.Release();  
        return;  
    }  
  
    ATLTRACE("Added program node.\n");  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)   
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
