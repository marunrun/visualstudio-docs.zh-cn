---
title: IWefDebuggingSupport 接口
ms.date: 02/02/2017
ms.topic: interface
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0a4883d36c1833c66a2539380184521b070f5c2a
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544724"
---
# <a name="iwefdebuggingsupport-interface"></a>IWefDebuggingSupport 接口
  由调试环境（如 Visual Studio）实现，以便为 Office 应用程序进行调试。 Office 应用程序（如 Word 或 Excel）从 Visual Studio 获取此接口，然后在调试会话过程中的特定点调用接口上的方法。

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

|名称|说明|
|----------|-----------------|
|[GetAutoInsertExtensions 方法](../vsto/getautoinsertextensions-method.md)|获取有关在调试过程中将自动插入的 Office 相关应用程序的信息。|
|[SetWefProcessId 方法](../vsto/setwefprocessid-method.md)|提供将运行 Web 扩展框架（WEF）内容的进程标识符。|
