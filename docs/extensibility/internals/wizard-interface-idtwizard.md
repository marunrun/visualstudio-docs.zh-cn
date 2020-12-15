---
title: 向导界面 (IDTWizard) |Microsoft Docs
description: IDE 使用 IDTWizard 界面与向导进行通信。 向导必须实现此接口，才能安装到 IDE 中。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e87759a979d0c680018d99a1e18a12e645f430c6
ms.sourcegitcommit: 19061b61759ce8e3b083a0e01a858e5435580b3e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/15/2020
ms.locfileid: "97487759"
---
# <a name="wizard-interface-idtwizard"></a>向导界面 (IDTWizard)
集成开发环境 (IDE) 使用接口与 <xref:EnvDTE.IDTWizard> 向导进行通信。 为了在 IDE 中安装，向导必须实现此接口。

 <xref:EnvDTE.IDTWizard.Execute%2A>方法是与接口关联的唯一方法 <xref:EnvDTE.IDTWizard> 。 向导实现此方法，IDE 将在接口上调用方法。 下面的示例演示方法的签名。

```
/* IDTWizard Method */
STDMETHOD(Execute)(THIS_
   /* [in] */ IDispatch *Application,
   /* [in] */ long hwndOwner,
   /* [in] */ SAFEARRAY * *ContextParams,
   /* [in] */ SAFEARRAY * *CustomParams,
   /* [out] [in] */ wizardResult *RetVal
   );
```

 对于 " **新建项目** " 和 " **添加新项** " 向导，启动机制非常相似。 若要启动，请调用 <xref:EnvDTE.IDTWizard> Dteinternal 中定义的接口。 唯一的区别是调用接口时传递到接口的上下文和自定义参数集。

 以下信息描述了 <xref:EnvDTE.IDTWizard> 向导在 IDE 中工作时必须实现的接口 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 。 IDE <xref:EnvDTE.IDTWizard.Execute%2A> 在向导上调用方法，并向其传递以下内容：

- DTE 对象

     DTE 对象是自动化模型的根。

- "窗口" 对话框的句柄，如代码段中所示 `hwndOwner ([in] long)` 。

     向导将其 `hwndOwner` 用作向导对话框的父项。

- 作为 SAFEARRAY 的变量传递到接口的上下文参数，如代码段中所示 `[in] SAFEARRAY (VARIANT)* ContextParams` 。

     上下文参数包含一系列值，这些值特定于正在启动的向导类型和项目的当前状态。 IDE 将上下文参数传递到向导。 有关详细信息，请参阅 [上下文参数](../../extensibility/internals/context-parameters.md)。

- 作为 SAFEARRAY 的变量传递到接口的自定义参数，如代码段中所示 `[in] SAFEARRAY (VARIANT)* CustomParams` 。

     自定义参数包含用户定义参数的数组。 .Vsz 文件将自定义参数传递到 IDE。 这些值由 `Param=` 语句决定。 有关详细信息，请参阅 [自定义参数](../../extensibility/internals/custom-parameters.md)。

- 接口的返回值为

    ```
    wizardResultSuccess = -1,
    wizardResultFailure = 0
    wizardResultCancel = 1
    wizardResultBackout = 2
    ```

## <a name="see-also"></a>请参阅
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
