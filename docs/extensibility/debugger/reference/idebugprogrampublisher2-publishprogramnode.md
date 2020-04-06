---
title: IDebug程序发布者2：:Publish程序节点 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::PublishProgramNode
helpviewer_keywords:
- IDebugProgramPublisher2::PublishProgramNode
ms.assetid: d4b72e04-f726-46cf-8e56-5203ff205b12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: df68e72ee8597805bf02cb9c6e1c3a0bcaf8a449
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721665"
---
# <a name="idebugprogrampublisher2publishprogramnode"></a>IDebugProgramPublisher2::PublishProgramNode
使程序节点可供调试引擎 （DEs） 和会话调试管理器 （SDM） 使用。

## <a name="syntax"></a>语法

```cpp
HRESULT PublishProgramNode(
   IDebugProgramNode2 *pProgramNode
);
```

```csharp
int PublishProgramNode(
   IDebugProgramNode2 pProgramNode
);
```

## <a name="parameters"></a>参数
`pProgramNode`\
[在][IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)对象，表示要提供的程序节点。

## <a name="return-value"></a>返回值
 如果成功，返回`S_OK`;否则，返回错误代码。

## <a name="remarks"></a>备注
 此方法允许在选择和启动程序进行调试之前查询程序以获取信息。

 要从可用性中删除程序节点，请调用["取消发布程序节点"](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)方法。

## <a name="see-also"></a>请参阅
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [UnpublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-unpublishprogramnode.md)
