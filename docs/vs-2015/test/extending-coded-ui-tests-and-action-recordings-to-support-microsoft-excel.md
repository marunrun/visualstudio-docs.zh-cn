---
title: 扩展编码的 UI 测试和操作录制以支持 Microsoft Excel | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 6b0f72a4-70ca-4e55-b236-2ea1034fd8a7
caps.latest.revision: 32
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a48c01203d2e951e917482de3c0d9c2bec29ae01
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660569"
---
# <a name="extending-coded-ui-tests-and-action-recordings-to-support-microsoft-excel"></a>扩展编码的 UI 测试和操作录制以支持 Microsoft Excel
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

编码的 UI 测试和操作录制的测试框架不支持的每个可能的用户界面。 它可能不支持你想要测试的特定 UI。 例如，不能立即创建编码的 UI 测试或 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 电子表格的操作录制。 但是，你可以为编码的 UI 测试框架创建自己的扩展，该扩展将通过利用编码的 UI 测试框架的扩展性支持特定的 UI。 以下主题提供的示例说明如何扩展框架以支持创建编码的 UI 测试和 [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] 的操作录制。 有关支持的平台的详细信息，请参阅[支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)。

 **惠?**

- Visual Studio Enterprise

  本节提供编码的 UI 测试扩展，该扩展可以录制和播放 Excel 工作表的测试。 本节和针对开发人员（该开发人员只想创建一个这样的扩展）的代码注释中对扩展的每个部分进行了介绍。

  ![UI 测试体系结构](../test/media/ui-testarch.png "UI_TestArch")体系结构概述

## <a name="download-the-sample"></a>下载示例
 该示例由 `CodedUIExtensibilitySample.sln` 解决方案中的四个项目组成：

- CodedUIextensibilitySample

- ExcelCodedUIAddInHelper

- ExcelCodedUIAddInHelper

- SampleTestProject

  从此[博客文章](http://go.microsoft.com/fwlink/?LinkID=185592)获取示例。

> [!NOTE]
> 该示例旨在与 Microsoft Excel 2010 配合使用。 该示例可以与其他版本的 Microsoft Excel 一起使用，但目前不支持如此。

## <a name="details-about-the-sample"></a>有关该示例的详细信息
 以下各节提供有关该示例及其结构的信息。

### <a name="microsoft-excel-add-in-excelcodeduiaddinhelper"></a>Microsoft Excel 外接程序：ExcelCodedUIAddinHelper
 此项目包含在 Excel 进程中运行的外接程序。 有关外接程序项目的简要概述，请参阅[编码的 UI 测试的 Excel 外接程序示例](../test/sample-excel-add-in-for-coded-ui-testing.md)。

 有关详细信息，请参阅[演练：创建你的第一个 Excel VSTO 外接程序](https://msdn.microsoft.com/library/a855e2be-3ecf-4112-a7f5-ec0f7fad3b5f)。

### <a name="excel-ui-communication-exceluicommunicationhelper"></a>Excel UI 通信：ExcelUIcommunicationHelper
 此项目包括用于在编码的 UI 测试框架和 Excel 之间传递数据的 `IExcelUICommunication` 接口和信息类。 有关详细信息，请参阅[示例 Excel Communicator 接口](../test/sample-excel-communicator-interface.md)。

### <a name="coded-ui-test-extension-codeduiexentsibilitysample"></a>编码的 UI 测试扩展：CodedUIExentsibilitySample
 此项目包含在 Excel 工作表的测试中使用的自定义类。 每个这些类的代码非常容易理解。 但是，我们提供每个自定义类的简短说明。 有关详细信息，请参阅[用于 Excel 的编码的 UI 测试扩展示例](../test/sample-coded-ui-test-extension-for-excel.md)。

### <a name="deploying-your-add-in-and-extension"></a>部署外接程序和扩展
 创建所有项目和对象后，以管理员的身份运行提供的 `CopyDrop.bat` 文件。 此文件将 `ExcelCodedUIAddinHelper` DLL 和 PDB 文件复制到：

 “`%CommonProgramFiles(x86)%\Microsoft Shared\VSTT\<version number>\UITestExtensionPackages\*.*`”，根据 Visual Studio 版本，其中的版本号可能为 11.0 和 12.0 等。

 `ExcelUICommunicationHelper` DLL 和 PDB 文件复制到 `"%ProgramFiles(x86)%\Microsoft Visual Studio <version number>\Common7\IDE\PrivateAssemblies”`。

 你可能必须调整准确的复制路径，但无需进行其他安装。 在 64 位计算机上，使用 32 位 Visual Studio Enterprise 命令提示符运行 `CopyDrop.bat` 文件。

### <a name="testing-excel-with-the-sampletestproject"></a>使用 SampleTestProject 测试 Excel
 可以在提供的测试项目（使用你可能没有的特定 Excel 版本）中运行测试，或创建你自己的测试项目并记录你自己的测试。 有关详细信息，请参阅[创建编码的 UI 测试](../test/use-ui-automation-to-test-your-code.md#VerifyingCodeUsingCUITCreate)。

## <a name="see-also"></a>请参阅

- <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITechnologyElement>
- [UITestActionFilter](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110))
- <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>
- [使用 UI 自动化来测试代码](../test/use-ui-automation-to-test-your-code.md)
- [编码的 UI 测试的最佳做法](../test/best-practices-for-coded-ui-tests.md)
- [支持编码的 UI 测试和操作录制的配置和平台](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)
