---
title: 向导 （.Vsz） 文件 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0fedf409c0ca320c054ddf1cc16318d08d25463a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703313"
---
# <a name="wizard-vsz-file"></a>向导 (.Vsz) 文件

集成开发环境 （IDE） 使用 .vsz 文件启动向导。 这些 .vsz 文件包含 IDE 用于确定调用哪个向导以及要传递给向导的信息的信息。

.vsz 文件是 .ini 格式的文本文件的版本，该文件没有节。 IDE 已知的信息存储在文件的开头。 这提供了 IDE 调用的向导和要传递给 IDE 的 .vsz 文件中的参数之间的链接。 文件的其余部分提供特定于向导的参数，这些参数将由 IDE 收集并传递给特定向导。

下面的示例显示 .vsz 文件的内容。

```
VSWizard 8.0
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}
Param="WIZARDNAME = Wizard One"
Param="WIZARDUI = FALSE"
```

以下是 .vsz 文件中的部分。

|组成部分|描述|
|----------|-----------------|
|VSWizard|文件中的第一个参数是模板文件格式的版本号。 此版本号必须为 6.0、7.0、7.1 或 8.0。 无法启动其他数字并导致格式无效错误。|
|向导|此字段包含向导的 OLE ProgID，或者包含由 IDE 共同创建的向导 CLSID 的 GUID 字符串表示形式。|
|Param|这些部件是可选的。 您可以根据需要添加尽可能多的。|

这些参数使 .vsz 文件能够将其他自定义参数传递给向导。 每个值都作为字符串元素传递给向导的变体数组中。 有关详细信息，请参阅[自定义参数](../../extensibility/internals/custom-parameters.md)。

要将默认区域设置 ID 添加到 .vsz 文件`FALLBACK_LCID`，请指定 _xxxx，其中 xxx 是区域设置 ID，例如，英语为 1033。 定义`FALLBACK_LCID`参数时，如果未找到当前 ID，向导将使用提供的回退区域设置 ID。

## <a name="see-also"></a>请参阅

- [自定义参数](../../extensibility/internals/custom-parameters.md)
- [向导](../../extensibility/internals/wizards.md)
- [模板目录说明 (.Vsdir) 文件](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)
