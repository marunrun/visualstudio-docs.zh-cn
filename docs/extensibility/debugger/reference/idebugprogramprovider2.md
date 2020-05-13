---
title: IDebug程序提供程序2 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2
helpviewer_keywords:
- IDebugProgramProvider2 interface
ms.assetid: a9ec7b3e-a59c-4069-b2ee-6f45916eeb78
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 43557e5d81e5140967a1189e57a350595d0f7220
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721694"
---
# <a name="idebugprogramprovider2"></a>IDebugProgramProvider2
此已注册的接口允许会话调试管理器 （SDM） 获取有关通过[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)接口"发布"的程序的信息。

## <a name="syntax"></a>语法

```
IDebugProgramProvider2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者说明
调试引擎 （DE） 实现此接口，以提供有关正在调试的程序的信息。 此接口使用指标`metricProgramProvider`在注册表的 DE 部分注册，如[用于调试的 SDK 帮助器](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)中所述。

## <a name="notes-for-callers"></a>呼叫者备注
使用`CLSID`从注册表获取`CoCreateInstance`的程序提供程序调用 COM 的功能。 请参阅示例。

## <a name="methods-in-vtable-order"></a>按 Vtable 顺序排列的方法

|方法|描述|
|------------|-----------------|
|[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)|获取有关以各种方式运行、筛选的程序的信息。|
|[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)|获取程序节点，给定特定的进程 ID。|
|[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)|建立回调以监视与特定类型的进程关联的提供程序事件。|
|[设置区域设置](../../../extensibility/debugger/reference/idebugprogramprovider2-setlocale.md)|为 DE 所需的任何特定于语言的资源建立区域设置。|

## <a name="remarks"></a>备注
通常，进程使用此接口来了解该进程中运行的程序。

## <a name="requirements"></a>要求
标题： msdbg.h

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="example"></a>示例

```cpp
IDebugProgramProvider2 *GetProgramProvider(GUID *pDebugEngineGuid)
{
    // This is typically defined globally. For this example, it is
    // defined here.
    static const WCHAR strRegistrationRoot[] = L"Software\\Microsoft\\VisualStudio\\8.0Exp";
    IDebugProgramProvider2 *pProvider = NULL;
    if (pDebugEngineGuid != NULL) {
        CLSID clsidProvider = { 0 };
        ::GetMetric(NULL,
                    metrictypeEngine,
                    *pDebugEngineGuid,
                    metricProgramProvider,
                    &clsidProvider,
                    strRegistrationRoot);
        if (!IsEqualGUID(clsidProvider,GUID_NULL)) {
            CComPtr<IDebugProgramProvider2> spProgramProvider;
            spProgramProvider.CoCreateInstance(clsidProvider);
            if (spProgramProvider != NULL) {
                pProvider = spProgramProvider.Detach();
            }
        }
    }
    return(pProvider);
}
```

## <a name="see-also"></a>请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
