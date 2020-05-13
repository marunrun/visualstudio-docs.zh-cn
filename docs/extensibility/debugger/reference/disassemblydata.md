---
title: 拆解数据 |微软文档
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- DisassemblyData
helpviewer_keywords:
- DisassemblyData structure
ms.assetid: 10e70aa7-9381-40d3-bdd1-d2cad78ef16c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9dcf3316ba57bbb25ee171cba7e4edc4923fa270
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80737285"
---
# <a name="disassemblydata"></a>DisassemblyData
描述要显示的集成开发环境 （IDE） 的一个拆解指令。

## <a name="syntax"></a>语法

```cpp
typedef struct tagDisassemblyData {
    DISASSEMBLY_STREAM_FIELDS dwFields;
    BSTR                      bstrAddress;
    BSTR                      bstrAddressOffset;
    BSTR                      bstrCodeBytes;
    BSTR                      bstrOpcode;
    BSTR                      bstrOperands;
    BSTR                      bstrSymbol;
    UINT64                    uCodeLocationId;
    TEXT_POSITION             posBeg;
    TEXT_POSITION             posEnd;
    BSTR                      bstrDocumentUrl;
    DWORD                     dwByteOffset;
    DISASSEMBLY_FLAGS         dwFlags;
} DisassemblyData;
```

```csharp
public struct DisassemblyData { 
    public uint          dwFields;
    public string        bstrAddress;
    public string        bstrAddressOffset;
    public string        bstrCodeBytes;
    public string        bstrOpcode;
    public string        bstrOperands;
    public string        bstrSymbol;
    public ulong         uCodeLocationId;
    public TEXT_POSITION posBeg;
    public TEXT_POSITION posEnd;
    public string        bstrDocumentUrl;
    public uint          dwByteOffset;
    public uint          dwFlags;
};
```

## <a name="members"></a>成员
`dwFields`\
DISASSEMBLY_STREAM_FIELDS[常](../../../extensibility/debugger/reference/disassembly-stream-fields.md)量，用于指定填写哪些字段。

`bstrAddress`\
地址作为某个起点的偏移量（通常是关联函数的开头）。

`bstrCodeBytes`\
此指令的代码字节。

`bstrOpcode`\
此指令的操作码。

`bstrOperands`\
此指令的操作数。

`bstrSymbol`\
与地址关联的符号名称（如果有）（公共符号、标签等）。

`uCodeLocationId`\
此拆解行的代码位置标识符。 如果一行的代码上下文地址大于另一行的代码上下文地址，则第一行的拆解代码位置标识符也将大于第二行的代码位置标识符。

`posBeg`\
对应于开始拆解数据的文档中的位置的[TEXT_POSITION。](../../../extensibility/debugger/reference/text-position.md)

`posEnd`\
对应于分解数据结束文档中位置的[TEXT_POSITION。](../../../extensibility/debugger/reference/text-position.md)

`bstrDocumentUrl`\
对于可以表示为文件名的文本文档，使用 格式`bstrDocumentUrl``file://file name`填充该字段，其中可以找到源。

对于不能表示为文件名的文本文档，`bstrDocumentUrl`是文档的唯一标识符，调试引擎必须实现[GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)方法。

此字段还可以包含有关校验和的其他信息。 有关详细信息，请参阅备注。

`dwByteOffset`\
指令的字节数是从代码行的开头开始的。

`dwFlags`\
指定哪些标志处于活动状态[的DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)常量。

## <a name="remarks"></a>备注
每个`DisassemblyData`结构描述一个拆解指令。 这些结构的数组从[Read](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)方法返回。

[TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)结构仅用于基于文本的文档。 此指令的源代码范围仅针对从语句或行生成的第一个指令（例如，当时`dwByteOffset == 0`）填写。

对于非文本文档，可以从代码获取文档上下文，`bstrDocumentUrl`并且该字段应为 null 值。 如果`bstrDocumentUrl`字段与前一`bstrDocumentUrl``DisassemblyData`数组元素中的字段相同，则`bstrDocumentUrl`将 设置为 null 值。

如果`dwFlags`字段设置了`DF_DOCUMENT_CHECKSUM`标志，则其他校验和信息将遵循字段指向的`bstrDocumentUrl`字符串。 具体而言，在空字符串终止符之后，后面跟着一个 GUID 标识校验和算法，该算法依次是 4 字节值，指示校验和中的字节数，然后依次为校验和字节。 请参阅本主题中有关如何编码和解码此字段[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]的示例。

## <a name="example"></a>示例
如果`bstrDocumentUrl`设置了标志，`DF_DOCUMENT_CHECKSUM`则该字段可以包含字符串以外的其他信息。 创建和读取此编码字符串的过程在 中[!INCLUDE[vcprvc](../../../code-quality/includes/vcprvc_md.md)]非常简单。 但是，在[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]中，这是另一回事。 对于好奇的人，下面的示例显示了从[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]创建编码字符串的一种方法和在 中[!INCLUDE[csprcs](../../../data-tools/includes/csprcs_md.md)]解码编码字符串的一种方法。

```csharp
using System;
using System.Runtime.InteropServices;

namespace MyNamespace
{
    class MyClass
    {
        string EncodeData(string documentString,
                          Guid checksumGuid,
                          byte[] checksumData)
        {
            string returnString = documentString;

            if (checksumGuid == null || checksumData == null)
            {
                // Nothing more to do. Just return the string.
                return returnString;
            }

            returnString += '\0'; // separating null value

            // Add checksum GUID to string.
            byte[] guidDataArray  = checksumGuid.ToByteArray();
            int    guidDataLength = guidDataArray.Length;
            IntPtr pBuffer        = Marshal.AllocCoTaskMem(guidDataLength);
            for (int i = 0; i < guidDataLength; i++)
            {
                Marshal.WriteByte(pBuffer, i, guidDataArray[i]);
            }
            // Copy guid data bytes to string as wide characters.
            // Assumption: sizeof(char) == 2.
            for (int i = 0; i < guidDataLength / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum count (a 32-bit value).
            Int32 checksumCount = checksumData.Length;
            Marshal.StructureToPtr(checksumCount, pBuffer, true);
            for (int i = 0; i < sizeof(Int32) / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }

            // Add checksum data.
            pBuffer = Marshal.AllocCoTaskMem(checksumCount);
            for (int i = 0; i < checksumCount; i++)
            {
                Marshal.WriteByte(pBuffer, i, checksumData[i]);
            }
            for (int i = 0; i < checksumCount / sizeof(char); i++)
            {
                returnString += (char)Marshal.ReadInt16(pBuffer, i * sizeof(char));
            }
            Marshal.FreeCoTaskMem(pBuffer);

            return returnString;
        }

        void DecodeData(    string encodedString,
                        out string documentString,
                        out Guid   checksumGuid,
                        out byte[] checksumData)
        {
            documentString = String.Empty;
            checksumGuid = Guid.Empty;
            checksumData = null;

            IntPtr pBuffer = Marshal.StringToBSTR(encodedString);
            if (null != pBuffer)
            {
                int bufferOffset = 0;

                // Parse string out. String is assumed to be Unicode.
                documentString = Marshal.PtrToStringUni(pBuffer);
                bufferOffset += (documentString.Length + 1) * sizeof(char);

                // Parse Guid out.
                // Read guid bytes from buffer and store in temporary
                // buffer that contains only the guid bytes. Then the
                // Marshal.PtrToStructure() can work properly.
                byte[] guidDataArray  = checksumGuid.ToByteArray();
                int    guidDataLength = guidDataArray.Length;
                IntPtr pGuidBuffer    = Marshal.AllocCoTaskMem(guidDataLength);
                for (int i = 0; i < guidDataLength; i++)
                {
                    Marshal.WriteByte(pGuidBuffer, i,
                                      Marshal.ReadByte(pBuffer, bufferOffset + i));
                }
                bufferOffset += guidDataLength;
                checksumGuid = (Guid)Marshal.PtrToStructure(pGuidBuffer, typeof(Guid));
                Marshal.FreeCoTaskMem(pGuidBuffer);

                // Parse out the number of checksum data bytes (always 32-bit value).
                int dataCount = Marshal.ReadInt32(pBuffer, bufferOffset);
                bufferOffset += sizeof(Int32);

                // Parse out the checksum data.
                checksumData = new byte[dataCount];
                for (int i = 0; i < dataCount; i++)
                {
                    checksumData[i] = Marshal.ReadByte(pBuffer, bufferOffset + i);
                }
            }
        }
    }
}
```

## <a name="see-also"></a>请参阅
- [结构和联合](../../../extensibility/debugger/reference/structures-and-unions.md)
- [读取](../../../extensibility/debugger/reference/idebugdisassemblystream2-read.md)
- [DISASSEMBLY_STREAM_FIELDS](../../../extensibility/debugger/reference/disassembly-stream-fields.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
- [DISASSEMBLY_FLAGS](../../../extensibility/debugger/reference/disassembly-flags.md)
