---
title: IDebugProgramProvider2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2
helpviewer_keywords:
- IDebugProgramProvider2 interface
ms.assetid: a9ec7b3e-a59c-4069-b2ee-6f45916eeb78
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a6f392e823d28440a73a1aaa606351c28c6e9c70
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66343359"
---
# <a name="idebugprogramprovider2"></a>IDebugProgramProvider2
此注册的接口允许会话调试管理器 (SDM) 以获取有关已"发布"通过的程序的信息[IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)接口。

## <a name="syntax"></a>语法

```
IDebugProgramProvider2 : IUnknown
```

## <a name="notes-for-implementers"></a>实施者的说明
调试引擎 (DE) 实现此接口以提供有关正在调试的程序的信息。 在注册表使用该度量值的 DE 部分中注册此接口`metricProgramProvider`，如中所述[以便进行调试的 SDK 帮助程序](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)。

## <a name="notes-for-callers"></a>调用方的说明
调用 COM 的`CoCreateInstance`函数和`CLSID`从注册表获取的程序提供程序。 请参阅示例。

## <a name="methods-in-vtable-order"></a>Vtable 顺序中的方法

|方法|描述|
|------------|-----------------|
|[GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)|获取程序运行，以通过多种方式筛选的相关信息。|
|[GetProviderProgramNode](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprogramnode.md)|获取的程序节点中，给定一个特定的进程 id。|
|[WatchForProviderEvents](../../../extensibility/debugger/reference/idebugprogramprovider2-watchforproviderevents.md)|建立一个回调，以监视与特定类型的进程相关联的提供程序事件。|
|[SetLocale](../../../extensibility/debugger/reference/idebugprogramprovider2-setlocale.md)|建立所需的 DE 任何特定于语言的资源的区域设置。|

## <a name="remarks"></a>备注
通常情况下，一个进程使用此接口来找出有关该进程中运行的程序。

## <a name="requirements"></a>要求
标头： msdbg.h

命名空间:Microsoft.VisualStudio.Debugger.Interop

程序集：Microsoft.VisualStudio.Debugger.Interop.dll

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
