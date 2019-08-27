---
title: 向导 (。在 Vsz) 文件 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b4bbd69bc92ee96fcf93749aa6f700ad76ff72c8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309723"
---
# <a name="wizard-vsz-file"></a>向导 (.Vsz) 文件

集成的开发环境 (IDE) 使用.vsz 文件来启动向导。 这些.vsz 文件包含 IDE 使用以确定要调用哪个向导的信息和要传递给该向导的信息。

.Vsz 文件是具有不包括任何部分的.ini 格式的文本文件的版本。 知道对 IDE 的信息存储在文件开头。 这提供了 IDE 调用向导.vsz 文件传递到 IDE 中的参数之间的链接。 文件的其余部分提供了的参数特定于该向导并且，是要收集的 IDE，并传递到特定的向导。

下面的示例显示了.vsz 文件的内容。

```
VSWizard 8.0
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}
Param="WIZARDNAME = Wizard One"
Param="WIZARDUI = FALSE"
```

以下是.vsz 文件中的部分。

|部件|描述|
|----------|-----------------|
|VSWizard|在文件中的第一个参数是模板文件格式的版本号。 此版本号必须 6.0、 7.0、 7.1 或 8.0。 其他数字不能启动，并且会导致无效的格式错误。|
|向导|此字段包含 OLE ProgID 的向导中，或者由 IDE 共同创建向导的 CLSID 的 GUID 字符串表示形式。|
|参数|这些部分是可选的。 您可以添加多达所需。|

参数，要将附加的自定义参数传递到向导的.vsz 文件。 每个值作为数组中的变体的字符串元素传递给该向导。 有关详细信息，请参阅[自定义参数](../../extensibility/internals/custom-parameters.md)。

若要将默认区域设置 ID 添加到你的.vsz 文件中，指定`FALLBACK_LCID`= 的 xxxx，其中 xxxx 是区域设置 ID，例如，1033 为英语。 当`FALLBACK_LCID`定义参数，该向导使用提供的回退区域设置 ID，如果找不到当前的 ID。

## <a name="see-also"></a>请参阅

- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)