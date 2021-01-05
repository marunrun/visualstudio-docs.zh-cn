---
title: MSSCCPRJ.SCC.SCC 文件 |Microsoft Docs
description: 了解 MSSCCPRJ.SCC。SCC 文件，该文件是源代码管理插件使用的本地客户端文件，可与 Visual Studio SDK 结合使用。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, MSSCCPRJ.SCC file
- MSSCCPRJ.SCC file
ms.assetid: 6f2e39d6-b79d-407e-976f-b62a3cedd378
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 253482f840350ae1d3cf7ee83e03a88ace15a6cd
ms.sourcegitcommit: dd96a95d87a039525aac86abe689c30e2073ae87
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2021
ms.locfileid: "97863473"
---
# <a name="mssccprjscc-file"></a>MSSCCPRJ.SCC.SCC 文件
使用 IDE 在源代码管理下放置 Visual Studio 解决方案或项目时，IDE 会收到两个关键信息。 信息以字符串的形式来自源代码管理插件。 这些字符串 "AuxPath" 和 "ProjName" 在 IDE 中是不透明的，但它们由插件用于在版本控制中找到解决方案或项目。 IDE 通常通过调用 [SccGetProjPath](../extensibility/sccgetprojpath-function.md)获取这些字符串，然后将它们保存在解决方案或项目文件中，以便以后调用 [SccOpenProject](../extensibility/sccopenproject-function.md)。 在解决方案和项目文件中嵌入时，当用户分支、分叉或复制版本控制中的解决方案和项目文件时，不会自动更新 "AuxPath" 和 "ProjName" 字符串。 为了确保解决方案和项目文件指向其版本控制中的正确位置，用户必须手动更新这些字符串。 因为字符串应是不透明的，所以可能并不总是清楚地说明如何更新它们。

 源代码管理插件可以通过将 "AuxPath" 和 "ProjName" 字符串存储在名为 *mssccprj.scc* 文件的特殊文件中来避免此问题。 它是插件拥有和维护的本地客户端文件。 此文件从不置于源代码管理下，而是由包含受源代码管理的文件的每个目录的插件生成的。 为了确定哪些文件是 Visual Studio 解决方案和项目文件，源代码管理插件可以将文件扩展名与标准或用户提供的列表进行比较。 一旦 IDE 检测到插件支持 *mssccprj.scc* 文件，它就不再将 "AuxPath" 和 "ProjName" 字符串嵌入到解决方案和项目文件中，而是从 *mssccprj.scc* 文件中读取这些字符串。

 支持 *mssccprj.scc* 文件的源代码管理插件必须遵循以下准则：

- 每个目录只能有一个 *mssccprj.scc* 文件。

- 对于位于给定目录中的源代码管理下的多个文件， *mssccprj.scc* 文件可以包含 "AuxPath" 和 "ProjName"。

- "AuxPath" 字符串内不能有引号。 允许使用引号作为分隔符 (例如，一对双引号可用于表示) 的空字符串。 从 *mssccprj.scc* 文件中读取 "AuxPath" 字符串时，IDE 将从该字符串中去除所有引号。

- Mssccprj.scc 中的 "ProjName" 字符串 *。SCC 文件* 必须与从函数返回的字符串完全匹配 `SccGetProjPath` 。 如果函数返回的字符串具有引号，则 *mssccprj.scc* 文件中的字符串必须具有引号，反之亦然。

- 每当文件置于源代码管理下时，就会创建或更新 *mssccprj.scc* 文件。

- 如果删除 *mssccprj.scc* 文件，则提供程序应在下一次执行有关该目录的源代码管理操作时重新生成该文件。

- *Mssccprj.scc* 文件必须严格遵循定义的格式。

## <a name="an-illustration-of-the-mssccprjscc-file-format"></a>MSSCCPRJ.SCC 的插图。SCC 文件格式
 下面是 *mssccprj.scc* 文件格式的示例 (仅将行号作为指南提供，不应将其包含在文件正文中) ：

- [第1行] `SCC = This is a Source Code Control file`

- [第2行]

- [第3行] `[TestApp.sln]`

- [第4行] `SCC_Aux_Path = "\\server\vss\"`

- [第5行] `SCC_Project_Name = "$/TestApp"`

- [第6行]

- [第7行] `[TestApp.csproj]`

- [第8行] `SCC_Aux_Path = "\\server\vss\"`

- [第9行] `SCC_Project_Name = "$/TestApp"`

 第一行指出了文件的用途，并用作此类型的所有文件的签名。 此行应与所有 *mssccprj.scc* 文件中的内容完全一样：

 `SCC = This is a Source Code Control file`

 以下部分详细介绍了每个文件的设置，这些设置以方括号括起来的文件名标记。 此部分对于正在跟踪的每个文件都是重复的。 此行是文件名的示例，即 `[TestApp.csproj]` 。 IDE 需要以下两行。 但是，它不定义定义的值的样式。 变量为 `SCC_Aux_Path` 和 `SCC_Project_Name` 。

 `SCC_Aux_Path = "\\server\vss\"`

 `SCC_Project_Name = "$/TestApp"`

 此部分没有结束分隔符。 文件的名称以及出现在文件中的所有文本都在 scc 标头文件中定义。 有关详细信息，请参阅 [用于查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)。

## <a name="see-also"></a>另请参阅
- [源代码管理插件](../extensibility/source-control-plug-ins.md)
- [用作查找源代码管理插件的键的字符串](../extensibility/strings-used-as-keys-for-finding-a-source-control-plug-in.md)
