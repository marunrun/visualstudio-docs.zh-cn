---
title: Enc不可用原因 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- EncUnavailableReason
helpviewer_keywords:
- EncUnavailableReason enumeration
ms.assetid: c10aa4c0-d7e0-4de1-b8ff-7e050985eb12
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 28863549ab3eac96322530bc85c52697f20448c8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737171"
---
# <a name="encunavailablereason"></a>EncUnavailableReason
`This is for internal use only!`表示 **"编辑"和"继续"** 不可用的原因。

## <a name="syntax"></a>语法

```cpp
enum tagEncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
typedef enum tagEncUnavailableReason EncUnavailableReason;
```

```csharp
public enum EncUnavailableReason {
    ENCUN_NONE,
    ENCUN_INTEROP,
    ENCUN_SQLCLR,
    ENCUN_MINIDUMP,
    ENCUN_EMBEDDED,
    ENCUN_ATTACH,
    ENCUN_WIN64
};
```

## <a name="fields"></a>字段
`ENCUN_NONE`\
没有"编辑并继续"不可用的具体原因。

`ENCUN_INTEROP`\
在互操作呼叫期间，编辑和继续不可用。

`ENCUN_SQLCLR`\
在使用通用语言运行时 （CLR） 的 SQL 过程调用期间，编辑和继续不可用。

`ENCUN_MINIDUMP`\
处理小型转储时，编辑和继续不可用。

`ENCUN_EMBEDDED`\
处理嵌入的代码时，编辑和继续不可用。

`ENCUN_ATTACH`\
编辑和继续不可用，因为会话已附加到调试器，而不是由调试器启动。

`ENCUN_WIN64`\
在处理 64 位 Windows 代码时，编辑和继续不可用。

## <a name="remarks"></a>备注
此枚举仅供[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]内部使用。 自定义端口供应商实现的[GetENC 可用状态](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)和[禁用 ENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)方法应始终返回`E_NOTIMPL`。

## <a name="requirements"></a>要求
标题： msdbg.idl

命名空间：微软.VisualStudio.调试器.互通

程序集：微软.VisualStudio.调试器.Interop.dll

## <a name="see-also"></a>请参阅
- [枚举](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)

- [DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)

- [GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)
