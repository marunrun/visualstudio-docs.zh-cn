---
title: 向导界面 （IDTWizard） |微软文档
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
ms.openlocfilehash: bb1c8d728a76097321e4e1f16640cab97599d6ba
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703278"
---
# <a name="wizard-interface-idtwizard"></a>向导界面 (IDTWizard)
集成开发环境 （IDE） 使用<xref:EnvDTE.IDTWizard>该接口与向导进行通信。 向导必须实现此接口才能安装在 IDE 中。

 该方法<xref:EnvDTE.IDTWizard.Execute%2A>是与接口关联的唯一<xref:EnvDTE.IDTWizard>方法。 向导实现此方法，IDE 调用接口上的方法。 下面的示例显示了方法的签名。

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

 "**新项目**"和 **"添加新项目**"向导的启动机制类似。 要启动这两个，您<xref:EnvDTE.IDTWizard>调用在 Dtein.h 中定义的接口。 唯一的区别是调用接口时传递给接口的上下文和自定义参数集。

 以下信息描述了向导在<xref:EnvDTE.IDTWizard> [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE 中工作时必须实现的接口。 IDE 调用向导<xref:EnvDTE.IDTWizard.Execute%2A>上的方法，传递如下：

- DTE 对象

     DTE 对象是自动化模型的根。

- 窗口对话框的句柄，如代码段所示`hwndOwner ([in] long)`。

     向导使用此选项`hwndOwner`项作为向导对话框的父级。

- 上下文参数作为 SAFEARRAY 的变体传递给接口，`[in] SAFEARRAY (VARIANT)* ContextParams`如代码段所示。

     上下文参数包含特定于正在启动的向导类型和项目的当前状态的值数组。 IDE 将上下文参数传递给向导。 有关详细信息，请参阅[上下文参数](../../extensibility/internals/context-parameters.md)。

- 自定义参数作为 SAFEARRAY 的变体传递给接口，`[in] SAFEARRAY (VARIANT)* CustomParams`如代码段所示。

     自定义参数包含用户定义的参数数组。 .vsz 文件将自定义参数传递给 IDE。 这些值由`Param=`语句确定。 有关详细信息，请参阅[自定义参数](../../extensibility/internals/custom-parameters.md)。

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
