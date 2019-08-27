---
title: Windows 脚本引擎 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows script engines
ms.assetid: e576853d-7252-4eb9-81eb-9d5bb7626ab4
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1acbc364e9ee2a5a4911564eb6d2c7d4c34de458
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63415995"
---
# <a name="windows-script-engines"></a>Windows 脚本引擎
若要实现 Microsoft Windows 脚本引擎，则要创建支持下列接口的 OLE COM 对象。  
  
|||  
|-|-|  
|接口|说明|  
|[IActiveScript](../winscript/reference/iactivescript.md)|提供基本的脚本功能。 需实现此接口。|  
|[IActiveScriptParse](../winscript/reference/iactivescriptparse.md)|提供添加脚本文本、评估表达式等功能。 此接口的实现为可选；但是，若未实现此接口，则脚本引擎必须实现 IPersist* 接口之一才能加载脚本。|  
|IPersist*|提供持久性支持。 若未实现 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md)，则至少需实现下列接口之一。<br /><br /> IPersistStorage：支持 OBJECT 标记中的 DATA={url} 属性。<br /><br /> IPersistStreamInit：同样支持 `IPersistStorage`，还支持 OBJECT 标记中的 DATA="string-encoded byte stream" 属性。<br /><br /> IPersistPropertyBag：支持 OBJECT 标记中的 PARAM= attribute。|  
  
> [!NOTE]
> 可能始终不会调用此脚本引擎来通过 `IPersist*` 保存或还原脚本状态。 相反，会调用 [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) 来使用 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) 创建空白脚本，然后使用 [IActiveScriptParse::AddScriptlet](../winscript/reference/iactivescriptparse-addscriptlet.md) 添加 scriptlet 并将其连接到事件，并使用 [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) 添加常规代码。 但是，脚本引擎应至少完整实现一个 `IPersist*` 接口（最好是 `IPersistStreamInit`），因为其他主机应用程序可能会尝试使用这些接口。  
  
 下面的部分将详细介绍实现 Windows 脚本引擎的过程。  
  
 请参阅 [Windows 脚本接口参考](../winscript/reference/windows-script-interfaces-reference.md)了解详细信息。  
  
## <a name="registry-standard"></a>注册表标准  
 Windows 脚本引擎可以使用类别标识符来标识自己。 Windows 脚本当前定义了两种类别标识符。  
  
|||  
|-|-|  
|类别|说明|  
|CATID_ActiveScript|指示类标识符 (CLSID) 是至少支持 [IActiveScript](../winscript/reference/iactivescript.md) 接口和持久性机制（`IPersistStorage`、`IPersistStreamInit` 或 IPersistPropertyBag 接口）的 Windows 脚本引擎。|  
|CATID_ActiveScriptParse|指示 CLSID 是至少支持 [IActiveScript](../winscript/reference/iactivescript.md) 和 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) 接口的 Windows 脚本引擎。|  
  
 虽然 [IActiveScriptParse](../winscript/reference/iactivescriptparse.md) 不是真正的持久性机制，但是它确实支持功能等效于 `IPersist*::InitNew` 的 [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) 方法。  
  
## <a name="script-engine-states"></a>脚本引擎状态  
 在任意给定时间，Windows 脚本引擎可处于以下几种状态之一。  
  
|||  
|-|-|  
|状态|说明|  
|未初始化|尚未使用 IPersist* 接口初始化或加载脚本，或者脚本尚未设置 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 接口。 通常在这种状态下脚本引擎不可用，直至加载脚本。|  
|已初始化|已使用 `IPersist*` 接口初始化脚本，并且已设置 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 接口，但是脚本未连接到主机对象和接收器事件。 请注意，此状态仅表示已完成 `IPersist*::Load`、`IPersist*::InitNew`、或 [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md) 方法，且已调用 [IActiveScript::SetScriptSite](../winscript/reference/iactivescript-setscriptsite.md) 方法。 在此模式下引擎无法运行代码。 引擎通过 [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) 方法将主机向其传递的代码排入队列，并在转换到启动状态后执行此代码。<br /><br /> 由于语言在语义方面的差异较大，因此无需脚本引擎支持此状态转换。 但是支持 [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) 方法的引擎必须支持此状态转换。 主机必须为此转换做准备并采取适当的操作：释放当前脚本引擎、新建脚本引擎并调用 `IPersist*::Load`、`IPersist*::InitNew` 或 [IActiveScriptParse::InitNew](../winscript/reference/iactivescriptparse-initnew.md)（可能还调用 [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md)）。 应将使用此转换视为对上述步骤的优化。 请注意，脚本引擎已获取的关于已命名项目的名称及描述已命名项目的类型信息的所有信息仍然有效。<br /><br /> 由于语言差异较大，因此难以定义此转换的准确语义。 脚本引擎至少需与所有事件断开连接，并释放通过调用 [IActiveScriptSite::GetItemInfo](../winscript/reference/iactivescriptsite-getiteminfo.md) 方法获取的所有 SCRIPTINFO_IUNKNOWN 指针。 重新运行脚本后，引擎必须重新获取这些指针。 此外，脚本引擎应将脚本重置回适用于当前语言的初始状态。 例如，VBScript 将通过调用已设置 SCRIPTTEXT_ISPERSISTENT 标记的 [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) 重置所有变量并保留动态添加的所有代码。 其他语言可能需要保留当前值（例如 Lisp，因为没有单独的代码/数据）或重置为已知状态（其中包括带有已静态初始化的变量的语言）。<br /><br /> 请注意，转换到启动状态的语义应与调用 `IPersist*::Save` 以保存脚本引擎并调用 `IPersist*::Load` 以加载新的脚本引擎的语义相同（即语义应将脚本引擎保持在同一种状态）；这些操作的语义应与 [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) 的语义相同。 尚不支持 `IActiveScript::Clone` 或 `IPersist*` 的脚本引擎应仔细考虑转换到启动状态的行为方式，以便在将来添加 `IActiveScript::Clone` 或 `IPersist*` 支持后，此转换不会违反上述条件。<br /><br /> 转换到启动状态期间，脚本中执行相应的析构函数等后，脚本引擎将断开与事件接收器的连接。 若要避免执行这些析构函数，主机可以先将脚本转为断开连接状态，然后再转为启动状态。<br /><br /> 可使用 [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) 取消正在运行的脚本线程，而无需等待当前事件等完成运行。|  
|已启动|从初始化状态转换到启动状态后，引擎会执行在初始化状态下排入队列的所有代码。 在启动状态下，引擎可以执行代码，但是引擎未连接到通过 [IActiveScript::AddNamedItem](../winscript/reference/iactivescript-addnameditem.md) 方法添加的任何事件。 引擎可以通过调用从 [IActiveScript::GetScriptDispatch](../winscript/reference/iactivescript-getscriptdispatch.md) 方法获得的 IDispatch 接口或通过调用 [IActiveScriptParse::ParseScriptText](../winscript/reference/iactivescriptparse-parsescripttext.md) 来执行代码。 进一步的后台初始化（渐进式加载）可能仍在继续进行，因此调用已设置 SCRIPTSTATE_CONNECTED 标记的 [IActiveScript::SetScriptState](../winscript/reference/iactivescript-setscriptstate.md) 方法可能会导致脚本受阻，直至初始化完成。|  
|已连接|脚本已加载，并已连接到主机对象的接收器事件。 如果这是从初始化状态进行的转换，则在进入连接状态并连接到事件之前，脚本引擎应先执行必要的操作，来通过启动状态进行转换。|  
|已断开连接|脚本已加载，并且处于运行时状态，但暂时将其与主机对象的接收器事件断开连接。 可以通过逻辑方式（忽略收到的事件）或物理方式（在相应的连接点上调用 IConnectionPoint::Unadvise）来执行此操作。 如果这是从初始化状态进行的转换，则在进入断开连接状态前，脚本引擎应执行必要的操作，来通过启动状态进行转换。 正在运行的事件接收器将在状态更改前完成操作（使用 [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) 取消正在运行的脚本线程）。 此状态与初始化状态的区别在于转换到此状态后，脚本不会重置，脚本的运行时状态不会重置，并且不会执行脚本初始化过程。|  
|已关闭|脚本已关闭。 脚本引擎不再运行，并不再针对多数方法返回错误。|  
  
 下列说明介绍了各种脚本引擎状态之间的关系，并介绍了用于从一种状态转换到另一种状态的方法。  
  
 下列说明介绍了脚本引擎在进行各种状态转换期间所执行的操作。  
  
## <a name="scripting-engine-threading"></a>脚本引擎线程  
 由于 Windows 脚本引擎可用于多种环境，因此尽可能地保留其执行模型的灵活性十分重要。 例如，基于服务器的主机在高效使用 Windows 脚本的同时，可能需要保留多线程设计。 与此同时，不使用线程的主机，例如一个典型的应用程序，应不负责进行线程管理。 Windows 脚本通过限制自由线程脚本引擎回调至主机的方法使主机免于承受此负担，从而实现了这种平衡。  
  
 服务器上使用的脚本引擎通常会实现为自由线程 COM 对象。 这表示可以从进程中的任意一个线程调用 [IActiveScript](../winscript/reference/iactivescript.md) 接口及其关联接口上的方法，而无需进行封送处理。 （遗憾的是，这也意味着脚本引擎必须实现为进程内服务器，因为 OLE 当前不支持自由线程对象进行进程间封送处理。）脚本引擎负责同步。 对于在内部不可重入的脚本引擎或非多线程的语言模型，同步与使用互斥序列化对脚本引擎的访问一样简单。 当然，某些方法，例如 [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md)，不应使用此方法进行序列化，以便可以从其他线程终止卡滞的脚本。  
  
 [IActiveScript](../winscript/reference/iactivescript.md) 通常是自由线程，这一事实通常意味着 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 接口及主机的对象模型也应是自由线程。 这将使主机的实现难以进行，通常情况下主机是其对象模型中包含单一线程或单元模型的 ActiveX 控件的基于 Windows 的单一线程应用程序，而在这种情况下主机实现尤其困难。 鉴于此原因，对脚本引擎使用 [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) 设置了以下限制：  
  
 始终在主机线程的上下文中调用脚本站点。 也就是说，脚本引擎不能在脚本引擎创建的线程的上下文中调用脚本站点，只能从通过 [IActiveScript](../winscript/reference/iactivescript.md) 及其派生项、已公开的脚本引擎的调度对象、Windows 消息从主机调用的脚本引擎方法或主机对象模型中的事件源进行调用。  
  
 不会从简单的线程状态控制方法（例如 [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) 方法）或从 [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) 方法的上下文调用脚本站点。  
  
## <a name="see-also"></a>请参阅  
 [Windows 脚本接口](../winscript/windows-script-interfaces.md)
