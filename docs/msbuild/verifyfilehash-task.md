---
title: VerifyFileHash 任务 | Microsoft Docs
ms.date: 01/28/2019
ms.topic: reference
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- VerifyFileHash task [MSBuild]
- MSBuild, VerifyFileHash task
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9340657704900feb5ebdc188103109872ee39f5d
ms.sourcegitcommit: e3b9cbeea282f1b531c6a3f60515ebfe1688aa0e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2020
ms.locfileid: "77439111"
---
# <a name="verifyfilehash-task"></a>VerifyFileHash 任务

验证文件是否与预期的文件哈希匹配。 如果哈希不匹配，则该任务失败。

此任务已添加到版本 15.8 中，但需要一种用于 16.0 以下 MSBuild 版本的[变通方法](https://github.com/Microsoft/msbuild/pull/3999#issuecomment-458193272)。

## <a name="task-parameters"></a>任务参数

 下表描述了 `VerifyFileHash` 任务的参数。

|参数|描述|
|---------------|-----------------|
|`File`|必选 `String` 参数。<br /><br />要进行哈希处理和验证的文件。|
|`Hash`|必选 `String` 参数。<br /><br />预期的文件哈希。|
|`Algorithm`|可选 `String` 参数。<br /><br />算法。 允许的值：`SHA256`、`SHA384`、`SHA512`。 默认值 = `SHA256`。|
|`HashEncoding`|可选 `String` 参数。<br /><br />用于生成哈希的编码。 默认为 `hex`。 允许的值 = `hex`、`base64`。|

## <a name="example"></a>示例

下例使用 `VerifyFileHash` 任务来验证其自己的校验和。

```xml
<Project>
  <Target Name="VerifyHash">
    <GetFileHash Files="$(MSBuildProjectFullPath)">
      <Output
          TaskParameter="Items"
          ItemName="FilesWithHashes" />
    </GetFileHash>

    <Message Importance="High"
             Text="@(FilesWithHashes->'%(Identity): %(FileHash)')" />

    <VerifyFileHash File="$(MSBuildThisFileFullPath)"
                    Hash="$(ExpectedHash)" />
  </Target>
</Project>
```

在 MSBuild 16.5 和更高版本中，如果不希望在哈希不匹配时生成失败（例如在使用哈希比较作为控制流的条件时），可以使用以下代码将警告降级为消息：

```xml
  <PropertyGroup>
    <MSBuildWarningsAsMessages>$(MSBuildWarningsAsMessages);MSB3952</MSBuildWarningsAsMessages>
  </PropertyGroup>

  <Target Name="DemoVerifyCheck">
    <VerifyFileHash File="$(MSBuildThisFileFullPath)"
                    Hash="1"
                    ContinueOnError="WarnAndContinue" />

    <PropertyGroup>
      <HashMatched>$(MSBuildLastTaskResult)</HashMatched>
    </PropertyGroup>

    <Message Condition=" '$(HashMatched)' != 'true'"
             Text="The hash didn't match" />

    <Message Condition=" '$(HashMatched)' == 'true'"
             Text="The hash did match" />
  </Target>
```

## <a name="see-also"></a>请参阅

- [任务](../msbuild/msbuild-tasks.md)
- [任务参考](../msbuild/msbuild-task-reference.md)
