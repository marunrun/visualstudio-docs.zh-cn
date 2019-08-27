---
title: IManagedAddin 接口
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- IManagedAddin interface
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 320b20fa40250ca47dd414b362059e152eba2c3b
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63420985"
---
# <a name="imanagedaddin-interface"></a>IManagedAddin 接口
  实现 IManagedAddin 接口来创建一个组件，它将加载托管 VSTO 外接程序。此接口在 2007 Microsoft Office system 中添加。

## <a name="syntax"></a>语法

```csharp
[
    object,
    uuid(B9CEAB65-331C-4713-8410-DDDAF8EC191A),
    pointer_default(unique),
    oleautomation
]
interface IManagedAddin : IUnknown
{
    HRESULT Load(
        [in] BSTR bstrManifestURL,
        [in] IDispatch *pdispApplication);
    HRESULT Unload();
};
```

## <a name="methods"></a>方法
 下表列出了由 IManagedAddin 接口定义的方法。

|名称|描述|
|----------|-----------------|
|[IManagedAddin::Load](../vsto/imanagedaddin-load.md)|在 Microsoft Office 应用程序加载托管 VSTO 外接程序时调用。|
|[IManagedAddin::Unload](../vsto/imanagedaddin-unload.md)|在 Microsoft Office 应用程序即将卸载 VSTO 托管外接程序时调用。|

## <a name="remarks"></a>备注
 Microsoft Office 应用程序，从 2007 Microsoft Office system 使用 IManagedAddin 接口来帮助加载 Office VSTO 外接程序。您可以实现 IManagedAddin 接口来创建你自己在 VSTO 外接程序加载程序和适用于运行时托管 VSTO 加载项，而不是使用 VSTO 外接程序加载程序 (*VSTOLoader.dll*) 和[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 有关更多信息，请参见 [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)。

## <a name="how-managed-add-ins-are-loaded"></a>如何加载托管的外接程序
 应用程序启动时，会执行以下步骤：

1. 应用程序通过在以下注册表项下查找项来发现 VSTO 外接程序：

    **HKEY_CURRENT_USER\Software\Microsoft\Office\\ *\<应用程序名称>* \Addins\\**

    此注册表项下的每一项都是 VSTO 外接程序的唯一 ID。 通常情况下，这是 VSTO 外接程序程序集的名称。

2. 应用程序在每个 VSTO 外接程序的注册表项下查找 `Manifest` 项。

    托管的 VSTO 加载项可存储在清单中的完整路径`Manifest`下的项**HKEY_CURRENT_USER\Software\Microsoft\Office\\ _\<应用程序名称 >_ \Addins\\ _\<外接程序 ID>_** 。 清单是一个文件（通常是 XML 文件），提供用于帮助加载 VSTO 外接程序的信息。

3. 如果应用程序找到 `Manifest` 项，便会尝试加载托管 VSTO 外接程序加载程序组件。 应用程序会尝试创建实现 IManagedAddin 接口的 COM 对象。

    [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]包括在 VSTO 外接程序加载程序组件 (*VSTOLoader.dll*)，也可以创建自己的实现 IManagedAddin 接口。

4. 应用程序调用 [IManagedAddin::Load](../vsto/imanagedaddin-load.md) 方法，并传入 `Manifest` 项的值。

5. [IManagedAddin::Load](../vsto/imanagedaddin-load.md) 方法执行加载 VSTO 外接程序所需的任务，例如为正在加载的 VSTO 外接程序配置应用程序域和安全策略。

   有关注册表的详细信息的密钥，Microsoft Office 应用程序用于发现和加载托管 VSTO 外接程序，请参阅[VSTO 外接程序的注册表项](../vsto/registry-entries-for-vsto-add-ins.md)。

## <a name="guidance-to-implement-imanagedaddin"></a>IManagedAddin 实现指南
 如果实现 IManagedAddin，则必须注册包含该实现使用以下 CLSID 的 DLL:

 99D651D7-5F7C-470E-8A3B-774D5D9536AC

 Microsoft Office 应用程序使用此 CLSID 来创建实现 IManagedAddin 的 COM 对象。

> [!CAUTION]
> 此 CLSID 也由*VSTOLoader.dll*中[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。 因此，如果 IManagedAddin 用于创建你自己的 VSTO 外接程序加载程序和运行时组件，将无法部署你的组件运行 VSTO 加载项依赖于的计算机到[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]。

## <a name="see-also"></a>请参阅
- [非托管 API 参考&#40;Visual Studio 中的 Office 开发&#41;](../vsto/unmanaged-api-reference-office-development-in-visual-studio.md)
