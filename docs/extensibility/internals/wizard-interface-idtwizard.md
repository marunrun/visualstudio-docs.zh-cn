---
title: 向导接口（IDTWizard） |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IDTWizard interface
- wizards, interface
ms.assetid: 09618d9d-d115-45b6-bccc-de328994b39c
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f571fbd0a68ddbf56b637071ac250159461f61d1
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72721534"
---
# <a name="wizard-interface-idtwizard"></a>向导界面 (IDTWizard)
集成开发环境（IDE）使用 <xref:EnvDTE.IDTWizard> 接口来与向导进行通信。 为了在 IDE 中安装，向导必须实现此接口。

 @No__t_0 方法是与 <xref:EnvDTE.IDTWizard> 接口相关联的唯一方法。 向导实现此方法，IDE 将在接口上调用方法。 下面的示例演示方法的签名。

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

 对于 "**新建项目**" 和 "**添加新项**" 向导，启动机制非常相似。 若要启动，请调用 Dteinternal 中定义的 <xref:EnvDTE.IDTWizard> 接口。 唯一的区别是调用接口时传递到接口的上下文和自定义参数集。

 以下信息描述了向导为在 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 中工作而必须实现的 <xref:EnvDTE.IDTWizard> 接口。 IDE 在向导上调用 <xref:EnvDTE.IDTWizard.Execute%2A> 方法，并向其传递以下内容：

- DTE 对象

     DTE 对象是自动化模型的根。

- "窗口" 对话框的句柄，如代码段中所示，`hwndOwner ([in] long)` "。

     向导使用此 `hwndOwner` 作为向导对话框的父项。

- 作为 SAFEARRAY 的变量传递到接口的上下文参数，如代码段中所示，`[in] SAFEARRAY (VARIANT)* ContextParams`。

     上下文参数包含一系列值，这些值特定于正在启动的向导类型和项目的当前状态。 IDE 将上下文参数传递到向导。 有关详细信息，请参阅[上下文参数](../../extensibility/internals/context-parameters.md)。

- 作为 SAFEARRAY 的变量传递到接口的自定义参数，如代码段中所示，`[in] SAFEARRAY (VARIANT)* CustomParams`。

     自定义参数包含用户定义参数的数组。 .Vsz 文件将自定义参数传递到 IDE。 这些值由 `Param=` 语句确定。 有关详细信息，请参阅[自定义参数](../../extensibility/internals/custom-parameters.md)。

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