---
title: '&lt;value&gt;（C# 编程指南）'
ms.date: 07/20/2015
f1_keywords:
- <value>
helpviewer_keywords:
- <value> C# XML tag
- value C# XML tag
ms.assetid: 08dbadaf-9ab6-43d9-9493-98e43bed199a
ms.openlocfilehash: 24ef4aba13668cd04e20f17ebffac9eb68e796ca
ms.sourcegitcommit: 64f4baed249341e5bf64d1385bf48e3f2e1a0211
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2018
ms.locfileid: "44081851"
---
# <a name="ltvaluegt-c-programming-guide"></a>&lt;value&gt;（C# 编程指南）
## <a name="syntax"></a>语法  
  
```xml  
<value>property-description</value>  
```  
  
#### <a name="parameters"></a>参数  
 `property-description`  
 属性的说明。  
  
## <a name="remarks"></a>备注  
 \<value> 标记可以描述属性表示的值。 请注意，在 Visual Studio .NET 开发环境中通过代码向导添加属性时，将添加新属性的 [\<summary>](../../../csharp/programming-guide/xmldoc/summary.md) 标记。 然后，应手动添加 \<value> 标记，描述属性表示的值。  
  
 使用 [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) 进行编译可以将文档注释处理到文件中。  
  
## <a name="example"></a>示例  
 [!code-csharp[csProgGuideDocComments#14](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/value_1.cs)]  
  
## <a name="see-also"></a>请参阅

- [C# 编程指南](../../../csharp/programming-guide/index.md)  
- [建议的文档注释标记](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
