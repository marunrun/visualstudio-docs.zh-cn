---
title: 迁移 64 位调试器 COM 类注册 |Microsoft Docs
ms.date: 11/10/2016
ms.topic: conceptual
ms.assetid: 45cfcee6-7a68-4d4f-b3f6-e2d8a0fa066a
author: gregg-miskelly
ms.author: greggm
manager: jillfra
ms.workload:
- greggm
ms.openlocfilehash: 74fbb959f8272be001aad8a576724d5eb1ad6157
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62433690"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>迁移 64 位调试器 COM 类注册

注册 COM 的调试器扩展的类在 HKEY_CLASSES_ROOT 中通过使用 regasm，regsvr32，或直接写入注册表和载入*msvsmon.exe* （远程调试器），现可提供此功能注册到 msvsmon 而无需向 HKEY_CLASSES_ROOT 写入。 这会影响旧版.NET 调试器表达式计算器或配置中加载的调试引擎*msvsmon.exe*过程。

## <a name="msvsmon-comclass-def"></a>msvsmon-comclass-def

若要使用此方法，将添加 **.msvsmon comclass def.json* msvsmon 旁边的文件 (InstallDir:* \Common7\IDE\Remote Debugger\x64*)。

下面是注册一个托管的一个示例 msvsmon comclass def 文件和一个本机类：

文件名：*MyCompany.MyExample.msvsmon-comclass-def.json*

```json
{
  "managedCOMClasses": [
    {
      "clsid": "{C9F48B25-36ED-4B22-8210-98BC5BE4D1E7}",
      "assemblyName": "MyCompany.MyAssembly",
      "className": "MyCompany.MyNamespace.MyClass"
    }
  ],
  "nativeCOMClasses": [
    {
      "clsid": "{42A476E9-8FA7-44D5-ADFE-216AD371EEC9}",
      "dllPath": "MyExample.dll"
    }
  ]
}
```
