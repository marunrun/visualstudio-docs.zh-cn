---
title: Windows 脚本接口 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 4c750627-6797-4857-9f5e-e5f54371f83c
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 141f3f0e60e797a4104c3e276775631f6e9196c5
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835402"
---
# <a name="windows-script-interfaces"></a>Windows 脚本接口

Microsoft Windows 脚本接口为应用程序提供一种方法，以添加脚本和 OLE 自动化。 依赖于 Windows 脚本的脚本宿主可以使用来自多个源和供应商的脚本引擎来管理组件之间的脚本。 脚本本身的实现（语言、语法、持久格式、执行模型等）留给脚本供应商。

Windows 脚本文档分为以下几个部分：

[Windows 脚本宿主](../winscript/windows-script-hosts.md)

[Windows 脚本引擎](../winscript/windows-script-engines.md)

[活动脚本调试概述](../winscript/active-script-debugging-overview.md)

[活动脚本分析概述](../winscript/active-script-profiling-overview.md)

[Windows 脚本接口参考](../winscript/reference/windows-script-interfaces-reference.md)

## <a name="windows-script-background"></a>Windows 脚本背景

Windows 脚本接口分为两类：Windows 脚本宿主和 Windows 脚本引擎。 主机创建脚本引擎并调用引擎来运行脚本。 Windows 脚本宿主的示例包括：

- Microsoft Internet Explorer

- Internet 创作工具

- shell

可以为任何语言或运行时环境开发 Windows 脚本引擎，包括：

- Microsoft Visual Basic Scripting Edition (VBScript)

- Perl

- Lisp

为使主机的实现尽可能灵活，提供适用于 Windows 脚本的 OLE 自动化包装器。 但是，使用此包装器对象来实例化脚本引擎的主机对运行时命名空间、持久性模型等没有一定程度的控制权，但如果直接使用 Windows 脚本，则拥有控制权。

Windows 脚本设计隔离了仅在创作环境中所需的界面元素，以便非创作主机（如浏览器和查看器）和脚本引擎（如 VBScript）能够保持轻量。

## <a name="windows-script-basic-architecture"></a>Windows 脚本基本体系结构

下图显示 Windows 脚本宿主和 Windows 脚本引擎之间的交互。

以下列表提供主机和引擎之间进行交互的步骤。

1. 创建项目。 主机加载项目或文档。 （此步骤并不特定于 Windows 脚本，但是为了完整起见，这里也包含了此步骤。）

2. 创建 Windows 脚本引擎。 主机调用 `CoCreateInstance` 创建新的 Windows 脚本引擎，以便指定特定于要使用的脚本引擎的类标识符 (CLSID)。 例如，Internet Explorer 的 HTML 浏览器通过 HTML 标记的 CLSID = 属性接收到脚本引擎的类标识符 \<OBJECT> 。

3. 加载脚本。 如果已保存脚本内容，则主机可以调用脚本引擎的 `IPersist*::Load` 方法来为它提供脚本存储、流或属性包。 否则，主机使用 `IPersist*::InitNew` 或 [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) 方法来创建 null 脚本。 以文本形式维护脚本的主机可以在调用 `IActiveScriptParse::InitNew` 之后，使用 [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) 向脚本引擎提供脚本的文本。

4. 添加命名项。 对于导入到脚本引擎命名空间中的每个顶级命名项（例如，页和表单），主机调用 [IActiveScript::AddNamedItem](../winscript/reference/iactivescript-addnameditem.md) 方法在引擎的命名空间中创建条目。 如果顶级命名项已是步骤 3 中加载的脚本的部分持久状态，那么此步骤就不需要。 主机不使用 `IActiveScript::AddNamedItem` 添加子级命名项（例如 HTML 页上的控件）；相反，引擎使用主机的 `ITypeInfo` 和 `IDispatch` 接口间接获得顶级项的子项。

5. 运行该脚本。 主机通过设置 [IActiveScript::SetScriptState](../winscript/reference/iactivescript-setscriptstate.md) 方法中的 SCRIPTSTATE_CONNECTED 标志来使引擎运行脚本。 此调用可能会以类似于脚本 `main()` 函数的方式执行任何脚本引擎构造工作，包括静态绑定、挂接事件（参阅下文）和执行代码。

6. 获取项信息。 每当脚本引擎需要将符号与顶级项关联时，都会调用返回给定项信息的 [IActiveScriptSite::GetItemInfo](../winscript/reference/iactivescriptsite-getiteminfo.md) 方法。

7. 挂接事件。 启动实际脚本之前，脚本引擎通过 `IConnectionPoint` 接口连接到所有相关对象的事件。

8. 调用属性和方法。 脚本运行时，脚本引擎通过 `IDispatch::Invoke` 或其他标准 OLE 绑定机制实现对命名对象方法和属性的引用。

## <a name="windows-script-terms"></a>Windows 脚本术语

此列表包含本文档中使用的与脚本相关的术语定义。

|术语|定义|
|----------|----------------|
|代码对象|由脚本引擎创建的实例，它与命名项（例如 Visual Basic 中窗体对应的模块）或者与命名项关联的 C++ 类关联。 最好它是支持 OLE 自动化的 OLE 组件对象模型 (COM) 对象，以便主机或其他非脚本实体能够操作代码对象。|
|命名项|主机认为对脚本感兴趣的 OLE COM 对象（最好是支持 OLE 自动化的对象）。 示例包括 Web 浏览器中的 HTML 页和浏览器，以及 Microsoft Word 中的文档和对话框。|
|脚本|构成脚本引擎运行的程序的数据。 脚本可以是任何可执行的连续数据，包括文本片段、`pcode` 块，甚至是特定于计算机的可执行字节代码。 主机通过任一 `IPersist*` 接口或 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) 接口将脚本加载到脚本引擎中。|
|脚本引擎|用于处理脚本的 OLE 对象。 脚本引擎实现 [IActiveScript](../winscript/reference/iactivescript.md) 和 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) 接口（可选）。|
|脚本宿主|拥有 Windows 脚本引擎的应用程序或程序。 主机实现 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 和 [IActiveScriptSiteWindow](../winscript/reference/iactivescriptsitewindow.md) 接口（可选）。|
|Scriptlet|通过 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) 接口附加到对象的部分脚本。 scriptlet 的聚合集合是脚本。|
|脚本语言|编写脚本的语言（例如 VBScript）和该语言的语义。|