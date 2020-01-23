---
title: “类视图”和“对象浏览器”图标
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- icons, in Object Browser
- signal icons
- Class View tool, symbols
- graphic symbols
- IntelliSense, icons
- icons, IntelliSense
- symbols, Object Browser icons
- Object Browser, icons in Class View
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6589d40d8f897eb8df7f108f53973af268d1edc9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588390"
---
# <a name="class-view-and-object-browser-icons"></a>“类视图”和“对象浏览器”图标

“类视图”和“对象浏览器”显示表示代码实体的图标，如命名空间、类、函数和变量   。 下表展示和描述了图标。

|图标|描述|图标|描述|
|----------|-----------------|----------|-----------------|
|![命名空间符号](../ide/media/vxnamespace_icon.gif)|命名空间|![声明符号](../ide/media/vxmethod_icon.gif)|方法或函数|
|![“类”图标](../ide/media/vxclass_icon.gif)|类|![运算符符号](../ide/media/vxoperator_icon.gif)|运算符|
|![棒棒糖形状的接口符号](../ide/media/vxinterface_icon.gif)|接口|![属性符号](../ide/media/vxproperty_icon.gif)|Property|
|![结构符号](../ide/media/vxstruct_icon.gif)|结构|![“字段”图标](../ide/media/vxfield_icon.gif)|字段或变量|
|![联合符号](../ide/media/vxunion_icon.gif)|联合|![事件符号](../ide/media/vxevent_icon.gif)|事件|
|![枚举符号](../ide/media/vxenum_icon.gif)|Enum|![“常量”图标](../ide/media/vxconstant_icon.gif)|返回的常量|
|![类型定义符号](../ide/media/vxtypedef_icon.gif)|TypeDef|![枚举项符号](../ide/media/vxenumitem_icon.gif)|枚举项|
|![Visual Studio 模块符号](../ide/media/vxmodule_icon.gif)|模块|![映射项符号](../ide/media/vxmapitem_icon.gif)|映射项|
|![扩展方法符号](../ide/media/extensionmethod.gif)|扩展方法|![声明符号](../ide/media/vxmethod_icon.gif)|外部声明|
|![委托符号](../ide/media/vxdelegate_icon.gif)|委托|![类视图和对象浏览器的“错误”图标](../ide/media/erroricon.gif)|错误|
|![异常符号](../ide/media/vxexception_icon.gif)|例外|![模板符号](../ide/media/vxtemplate_icon.gif)|模板|
|![映射符号](../ide/media/vxmap_icon.gif)|映射|![错误感叹号符号](../ide/media/vxerror_icon.gif)|未知|
|![“类型转发”符号](../ide/media/ob_type_forward.gif)|类型转发|||

## <a name="signal-icons"></a>信号图标

以下信号图标应用于所有原有的图标并指示它们的辅助功能。

|图标|描述|
|----------|-----------------|
|\<无信号图标>|Public。 可从此组件中的任何地方访问，也可从任何引用它的组件访问。|
|![信号 Protected 符号](../ide/media/vxsignal_icon_key.gif)|Protected。 从包含类或类型访问，或者从由包含类或类型派生的类型访问。|
|![信号 Private 符号](../ide/media/vxsignal_icon_lock.gif)|Private。 只能在包含类或类型中访问。|
|![信号 Sealed 符号](../ide/media/vxsignal_icon_envelope.gif)|Sealed。|
|![信号 Friend&#47;Internal 符号](../ide/media/vxsignal_icon_diamond.gif)|Friend/Internal。 仅能从项目访问。|
|![信号图标箭头](../ide/media/vxsignal_icon_arrow.gif)|快捷方式。 对象的快捷方式。|

> [!NOTE]
> 如果项目包含在源代码管理数据库中，则可能会显示更多信号图标来指示源代码管理状态，如签入或签出状态。

## <a name="see-also"></a>请参阅

- [查看代码结构](../ide/viewing-the-structure-of-code.md)
