---
title: 向导界面 (IDTWizard) |Microsoft Docs
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
ms.openlocfilehash: 7bd4e9a650bee4f5f13f1aeab39a59a1c04a253c
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66330903"
---
# <a name="wizard-interface-idtwizard"></a>向导界面 (IDTWizard)
集成的开发环境 (IDE) 使用<xref:EnvDTE.IDTWizard>接口与向导进行通信。 向导必须实现此接口，以便在 IDE 中安装。

 <xref:EnvDTE.IDTWizard.Execute%2A>方法是与相关联的唯一方法<xref:EnvDTE.IDTWizard>接口。 向导实现此方法，并在 IDE 的接口上调用方法。 下面的示例演示了该方法的签名。

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

 启动机制是两个类似**新的项目**并**添加新项**向导。 若要启动任一，请调用<xref:EnvDTE.IDTWizard>Dteinternal.h 中定义的接口。 唯一区别是一组的上下文和接口调用时传递给该接口的自定义参数。

 以下信息介绍<xref:EnvDTE.IDTWizard>向导为在工作而必须实现的接口[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]IDE。 IDE 调用<xref:EnvDTE.IDTWizard.Execute%2A>在向导中，并向其传递以下方法：

- DTE 对象

     DTE 对象是自动化模型的根。

- 窗口对话框中，代码段中所示的图柄`hwndOwner ([in] long)`。

     该向导将使用此`hwndOwner`作为向导对话框中的父级。

- 上下文参数传递给的接口作为变体为 SAFEARRAY 代码段中所示`[in] SAFEARRAY (VARIANT)* ContextParams`。

     上下文参数包含特定于正在启动的向导类型的值的数组和项目的当前状态。 IDE 将上下文参数传递给该向导。 有关详细信息，请参阅[上下文参数](../../extensibility/internals/context-parameters.md)。

- 自定义参数传递给的接口为 variant 类型的 SAFEARRAY 的代码段中所示`[in] SAFEARRAY (VARIANT)* CustomParams`。

     自定义参数包含用户定义的参数的数组。 .Vsz 文件传递到 IDE 的自定义参数。 值由`Param=`语句。 有关详细信息，请参阅[自定义参数](../../extensibility/internals/custom-parameters.md)。

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