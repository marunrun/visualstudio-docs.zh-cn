---
title: IWefDebuggingSupport 接口
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a71adf5371275fbbdc19cdf09be96ef900ec073d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62583758"
---
# <a name="iwefdebuggingsupport-interface"></a>IWefDebuggingSupport 接口
  实现的调试环境，如 Visual Studio 中，为了便于调试 office 的应用。 Office 应用程序，如 Word 或 Excel，将从 Visual Studio 中获取此接口，然后在特定时间点的接口上调试会话期间调用的方法。

## <a name="syntax"></a>语法

```csharp
[
    uuid(ccaf1a90-ce1c-4199-9cd6-b40c5c57a671),
    oleautomation
]
interface IWefDebuggingSupport : IUnknown
{
    HRESULT SetWefProcessId(
        [in] DWORD dwProcessId);
    HRESULT GetAutoInsertExtensions(
        [out, retval] SAFEARRAY(BSTR)* psaExtensionNames);
}
```

## <a name="methods"></a>方法
 下表列出了 IWefDebuggingSupport 接口定义的方法。

|名称|描述|
|----------|-----------------|
|[GetAutoInsertExtensions 方法](../vsto/getautoinsertextensions-method.md)|获取要在调试期间自动插入的 Office 应用的相关信息。|
|[SetWefProcessId 方法](../vsto/setwefprocessid-method.md)|提供将运行 Web 扩展框架 (WEF) 内容的进程标识符。|
