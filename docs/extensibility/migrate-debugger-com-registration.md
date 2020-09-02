---
title: 迁移64位调试器 COM 类注册 |Microsoft Docs
ms.date: 11/10/2016
ms.topic: conceptual
ms.assetid: 45cfcee6-7a68-4d4f-b3f6-e2d8a0fa066a
author: gregg-miskelly
ms.author: greggm
manager: jillfra
ms.workload:
- greggm
ms.openlocfilehash: 74fbb959f8272be001aad8a576724d5eb1ad6157
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62433690"
---
# <a name="migrate-64-bit-debugger-com-class-registration"></a>迁移64位调试器 COM 类注册

对于通过使用 regasm、regsvr32 或直接写入注册表并加载到 *msvsmon.exe* (远程调试器) 来注册 HKEY_CLASSES_ROOT 中的 COM 类的调试器扩展，现在可以向 msvsmon 提供此注册，而无需写入 HKEY_CLASSES_ROOT。 这会影响配置为在 *msvsmon.exe* 进程中加载的旧版 .net 调试器表达式计算器或调试引擎。

## <a name="msvsmon-comclass-def"></a>msvsmon-comclass

若要使用此方法，请 ** 在* msvsmon (InstallDir：* \Common7\IDE\Remote Debugger\x64 * ) 旁边的文件上添加.msvsmon-comclass-def.js。

下面是一个示例 comclass .def 文件，用于注册一个托管和一个本机类：

文件名： *MyCompany.MyExample.msvsmon-comclass-def.js*

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
