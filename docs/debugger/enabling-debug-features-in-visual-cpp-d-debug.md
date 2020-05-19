---
title: 在 C++ 项目中启用调试功能 (-D_DEBUG) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- /D_DEBUG compiler option [C++]
- debugging [C++], enabling debug features
- debugging [MFC], enabling debug features
- assertions, enabling debug features
- D_DEBUG compiler option
- MFC libraries, debug version
- debug builds, MFC
- _DEBUG macro
ms.assetid: 276e2254-7274-435e-ba4d-67fcef4f33bc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 19d341cba47e0a3d2259cc57d239c63420095347
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737960"
---
# <a name="enabling-debug-features-in-c-projects-d_debug"></a>在 C++ 项目中启用调试功能 (/D_DEBUG)
在 [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] 中，如果在编译程序时定义了 _DEBUG 符号，则将启用某些调试功能（如断言）。 可以用下列两种方法之一定义 _DEBUG：

- 在源代码中指定 #define _DEBUG，或

- 指定 /D_DEBUG 编译器选项。 （如果是在 Visual Studio 中使用向导创建项目，则 /D_DEBUG 将在“调试”配置中自动定义。）

  在定义了 _DEBUG 后，编译器将编译包围在 #ifdef _DEBUG 和 `#endif` 内的代码段 。

  MFC 程序的调试配置必须与 MFC 库的调试版本链接。 MFC 头文件根据所定义的符号（如 _DEBUG 和 _UNICODE）确定要链接的 MFC 库的正确版本 。 有关详细信息，请参阅 [MFC 库版本](/cpp/mfc/mfc-library-versions)。

## <a name="see-also"></a>请参阅
- [调试本机代码](../debugger/debugging-native-code.md)
- [C++ 调试配置的项目设置](../debugger/project-settings-for-a-cpp-debug-configuration.md)