---
title: IDebugProgramProvider2 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80721694"
---
# <a name="idebugprogramprovider2"></a>IDebugProgramProvider2
此注册接口允许会话调试管理器 (SDM) 获取有关通过 [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md) 接口 "已发布" 的程序的信息。

## <a name="syntax"></a>语法

```
IDebugProgramProvider2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者注意事项
调试引擎 (DE) 实现此接口，以便提供有关正在调试的程序的信息。 此接口使用度量值在注册表的 "DE" 部分中注册 `metricProgramProvider` ，如 [SDK 帮助程序进行调试](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)中所述。

## <a name="notes-for-callers"></a>调用方说明
`CoCreateInstance`通过 `CLSID` 从注册表获取的程序提供程序调用 COM 的函数。 请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序的方法

|方法|说明|
|------------|-----------------|
|[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)|获取有关运行的程序的信息，以多种方式进行筛选。|
|[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)|获取给定特定进程 ID 的程序节点。|
|[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)|建立一个回调，以监视与特定类型的进程关联的提供程序事件。|
|[SetLocale](../../../extensibility/debugger/reference/idebugprogramprovider2-setlocale.md)|为 DE 所需的任何特定于语言的资源建立区域设置。|

## <a name="remarks"></a>备注
通常，进程使用此接口来找出在该进程中运行的程序。

## <a name="requirements"></a>要求
标头： msdbg

命名空间： VisualStudio

程序集： Microsoft.VisualStudio.Debugger.Interop.dll

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

## <a name="see-also"></a>另请参阅
- [核心接口](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [用于调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
