---
title: IDebug程序发布者2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2
helpviewer_keywords:
- IDebugProgramPublisher2 interface
ms.assetid: b1d17f63-7146-4076-a588-034cfc6858b9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b17f5bab02e49951eb1647af95641af807c44863
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721521"
---
# <a name="idebugprogrampublisher2"></a>IDebugProgramPublisher2
此接口允许调试引擎 （DE） 或自定义端口供应商注册程序进行调试。

## <a name="syntax"></a>语法

```
IDebugProgramPublisher2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
Visual Studio 实现此接口来注册正在调试的程序，以便使其可见以跨多个进程进行调试。

## <a name="notes-for-callers"></a>呼叫者备注
使用 调用`CoCreateInstance`COM`CLSID_ProgramPublisher`的函数以获取此接口（请参阅示例）。 DE 或自定义端口供应商使用此接口注册表示正在调试的程序的程序节点。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法
此接口实现以下方法：

|方法|描述|
|------------|-----------------|
|[PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)|使程序节点可供 D 和会话调试管理器 （SDM）。|
|[UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)|删除程序节点，使其不再可用。|
|[PublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogram.md)|使程序可供 D 和 SDM 使用。|
|[UnpublishProgram](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogram.md)|删除程序，使其不再可用。|
|[SetDebuggerPresent](../../../extensibility/debugger/reference/idebugprogrampublisher2-setdebuggerpresent.md)|设置指示存在调试器的标志。|

## <a name="remarks"></a>备注
此接口使程序和程序节点可用（即"发布"它们），供 D 和会话调试管理器 （SDM） 使用。 要访问已发布的程序和程序节点，请使用[IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)接口。 这是 Visual Studio 能够识别正在调试程序的唯一方法。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="example"></a>示例
此示例演示如何实例化程序发布者和注册程序节点。 这是从教程，[发布程序节点](https://msdn.microsoft.com/library/d0100e02-4e2b-4e72-9e90-f7bc11777bae)。

```cpp
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

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)
