---
title: “类视图”和“对象浏览器”图标 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- icons, in Object Browser
- signal icons
- Class View tool, symbols
- graphic symbols
- IntelliSense, icons
- icons, IntelliSense
- symbols, Object Browser icons
- Object Browser, icons in Class View
ms.assetid: 58cc3f44-c296-4a88-a008-09d28598d9c0
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ef14396e681f77eca469f40b2253c8a64296423d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63422856"
---
# <a name="class-view-and-object-browser-icons"></a>“类视图”和“对象浏览器”图标
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

“类视图”和“对象浏览器”显示表示代码实体的图标，如命名空间、类、函数和变量。 下表展示和描述了图标。  
  
|图标|描述|图标|描述|  
|----------|-----------------|----------|-----------------|  
|![命名空间符号](../ide/media/vxnamespace-icon.gif "vxNamespace_Icon")|命名空间|![声明符号](../ide/media/vxmethod-icon.gif "vxMethod_Icon")|方法或函数|  
|![类图标](../ide/media/vxclass-icon.gif "vxClass_Icon")|类|![运算符符号](../ide/media/vxoperator-icon.gif "vxOperator_Icon")|运算符|  
|![棒糖形接口](../ide/media/vxinterface-icon.gif "vxInterface_Icon")|接口|![属性符号](../ide/media/vxproperty-icon.gif "vxProperty_Icon")|属性|  
|![结构符号](../ide/media/vxstruct-icon.gif "vxStruct_Icon")|结构|![字段图标](../ide/media/vxfield-icon.gif "vxField_Icon")|字段或变量|  
|![联合符号](../ide/media/vxunion-icon.gif "vxUnion_Icon")|联合|![事件符号](../ide/media/vxevent-icon.gif "vxEvent_Icon")|Event|  
|![枚举符号](../ide/media/vxenum-icon.gif "vxEnum_Icon")|Enum|![常量图标](../ide/media/vxconstant-icon.gif "vxConstant_Icon")|返回的常量|  
|![类型定义符号](../ide/media/vxtypedef-icon.gif "vxTypeDef_Icon")|TypeDef|![枚举项符号](../ide/media/vxenumitem-icon.gif "vxEnumItem_Icon")|枚举项|  
|![Visual Studio 模块符号](../ide/media/vxmodule-icon.gif "vxModule_Icon")|模块|![映射项符号](../ide/media/vxmapitem-icon.gif "vxMapItem_Icon")|映射项|  
|![扩展方法符号](../ide/media/extensionmethod.gif "ExtensionMethod")|扩展方法|![声明符号](../ide/media/vxmethod-icon.gif "vxMethod_Icon")|外部声明|  
|![委托符号](../ide/media/vxdelegate-icon.gif "vxDelegate_Icon")|委托|![类视图和对象浏览器的“错误”图标](../ide/media/erroricon.gif "ErrorIcon")|Error|  
|![异常符号](../ide/media/vxexception-icon.gif "vxException_Icon")|例外|![模板符号](../ide/media/vxtemplate-icon.gif "vxTemplate_Icon")|模板|  
|![映射符号](../ide/media/vxmap-icon.gif "vxMap_Icon")|映射|![错误感叹号符号](../ide/media/vxerror-icon.gif "vxError_Icon")|未知|  
|![类型转发符号](../ide/media/ob-type-forward.gif "ob_type_forward")|类型转发|||  
  
## <a name="signal-icons"></a>信号图标  
 以下信号图标应用于所有原有的图标并指示它们的辅助功能。  
  
> [!NOTE]
> 如果项目包含在源代码管理数据库中，则可能会显示更多信号图标来指示源代码管理状态，如签入或签出状态。  
  
|图标|描述|  
|----------|-----------------|  
|\<无信号图标>|Public。 可从此组件中的任何地方访问，也可从任何引用它的组件访问。|  
|![信号 Protected 符号](../ide/media/vxsignal-icon-key.gif "vxSignal_Icon_Key")|Protected。 从包含类或类型访问，或者从由包含类或类型派生的类型访问。|  
|![信号 Private 符号](../ide/media/vxsignal-icon-lock.gif "vxSignal_Icon_Lock")|Private。 只能在包含类或类型中访问。|  
|![信号 Sealed 符号](../ide/media/vxsignal-icon-envelope.gif "vxSignal_Icon_Envelope")|Sealed。|  
|![信号 Friend/Internal 符号](../ide/media/vxsignal-icon-diamond.gif "vxSignal_Icon_Diamond")|Friend/Internal。 仅能从项目访问。|  
|![信号图标箭头](../ide/media/vxsignal-icon-arrow.gif "vxSignal_Icon_Arrow")|快捷方式。 对象的快捷方式。|  
  
## <a name="see-also"></a>请参阅  
 [查看代码的结构](../ide/viewing-the-structure-of-code.md)
