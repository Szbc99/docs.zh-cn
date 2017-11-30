---
title: "unit 类型 (F#)"
description: "了解如何的 F # 单位类型通常用来保存其中一个值时所需的语言语法需要或所需的任何值的位置。"
keywords: "visual f#, f#, 函数编程"
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: eabbb6d7-80f3-4fa5-80b4-0f48982466a7
ms.openlocfilehash: 60ac08c0e3f8380a8f9dec7a083ede93c68bb0e8
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="unit-type"></a><span data-ttu-id="ed76a-104">unit 类型</span><span class="sxs-lookup"><span data-stu-id="ed76a-104">Unit Type</span></span>

<span data-ttu-id="ed76a-105">`unit`类型是类型，该值指示一个特定值; 如果没有`unit`类型具有只能是单个值，当没有其他值存在，或者需要时充当占位符。</span><span class="sxs-lookup"><span data-stu-id="ed76a-105">The `unit` type is a type that indicates the absence of a specific value; the `unit` type has only a single value, which acts as a placeholder when no other value exists or is needed.</span></span>


## <a name="syntax"></a><span data-ttu-id="ed76a-106">语法</span><span class="sxs-lookup"><span data-stu-id="ed76a-106">Syntax</span></span>

```fsharp
// The value of the unit type.
()
```

## <a name="remarks"></a><span data-ttu-id="ed76a-107">备注</span><span class="sxs-lookup"><span data-stu-id="ed76a-107">Remarks</span></span>
<span data-ttu-id="ed76a-108">每个 F # 表达式的计算结果必须为一个值。</span><span class="sxs-lookup"><span data-stu-id="ed76a-108">Every F# expression must evaluate to a value.</span></span> <span data-ttu-id="ed76a-109">不会生成有意义，类型的值的表达式`unit`使用。</span><span class="sxs-lookup"><span data-stu-id="ed76a-109">For expressions that do not generate a value that is of interest, the value of type `unit` is used.</span></span> <span data-ttu-id="ed76a-110">`unit`类型类似于`void`C# 和 c + + 等语言的类型。</span><span class="sxs-lookup"><span data-stu-id="ed76a-110">The `unit` type resembles the `void` type in languages such as C# and C++.</span></span>

<span data-ttu-id="ed76a-111">`unit`类型具有单个值，该值指定标记`()`。</span><span class="sxs-lookup"><span data-stu-id="ed76a-111">The `unit` type has a single value, and that value is indicated by the token `()`.</span></span>

<span data-ttu-id="ed76a-112">值`unit`类型通常使用 F # 编程来保留位置，而值所需的语言语法，但需要或所需的任何值中。</span><span class="sxs-lookup"><span data-stu-id="ed76a-112">The value of the `unit` type is often used in F# programming to hold the place where a value is required by the language syntax, but when no value is needed or desired.</span></span> <span data-ttu-id="ed76a-113">一个示例可能是的返回值`printf`函数。</span><span class="sxs-lookup"><span data-stu-id="ed76a-113">An example might be the return value of a `printf` function.</span></span> <span data-ttu-id="ed76a-114">因为的重要操作`printf`操作发生在函数中，该函数不需要返回实际值。</span><span class="sxs-lookup"><span data-stu-id="ed76a-114">Because the important actions of the `printf` operation occur in the function, the function does not have to return an actual value.</span></span> <span data-ttu-id="ed76a-115">因此，返回值的类型是`unit`。</span><span class="sxs-lookup"><span data-stu-id="ed76a-115">Therefore, the return value is of type `unit`.</span></span>

<span data-ttu-id="ed76a-116">某些构造应`unit`值。</span><span class="sxs-lookup"><span data-stu-id="ed76a-116">Some constructs expect a `unit` value.</span></span> <span data-ttu-id="ed76a-117">例如，`do`绑定或所有代码模块的顶层是计算结果应为`unit`值。</span><span class="sxs-lookup"><span data-stu-id="ed76a-117">For example, a `do` binding or any code at the top level of a module is expected to evaluate to a `unit` value.</span></span> <span data-ttu-id="ed76a-118">编译器将报告警告时`do`绑定或模块的顶层的代码生成的结果以外`unit`未使用，如下面的示例中所示的值。</span><span class="sxs-lookup"><span data-stu-id="ed76a-118">The compiler reports a warning when a `do` binding or code at the top level of a module produces a result other than the `unit` value that is not used, as shown in the following example.</span></span>

[!code-fsharp[Main](../../../samples/snippets/fsharp/lang-ref-1/snippet901.fs)]

<span data-ttu-id="ed76a-119">此警告是函数编程; 的特征它不会显示在其他.NET 编程语言。</span><span class="sxs-lookup"><span data-stu-id="ed76a-119">This warning is a characteristic of functional programming; it does not appear in other .NET programming languages.</span></span> <span data-ttu-id="ed76a-120">在纯粹的函数的程序中，函数不具有任何方面的副作用，最终的返回值是函数调用的唯一结果。</span><span class="sxs-lookup"><span data-stu-id="ed76a-120">In a purely functional program, in which functions do not have any side effects, the final return value is the only result of a function call.</span></span> <span data-ttu-id="ed76a-121">因此，当结果将被忽略，它是可能的编程错误。</span><span class="sxs-lookup"><span data-stu-id="ed76a-121">Therefore, when the result is ignored, it is a possible programming error.</span></span> <span data-ttu-id="ed76a-122">虽然 F # 不是纯粹的函数编程语言，所以最好遵循函数编程的方式，只要有可能。</span><span class="sxs-lookup"><span data-stu-id="ed76a-122">Although F# is not a purely functional programming language, it is a good practice to follow functional programming style whenever possible.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed76a-123">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ed76a-123">See Also</span></span>
[<span data-ttu-id="ed76a-124">基元</span><span class="sxs-lookup"><span data-stu-id="ed76a-124">Primitive</span></span>](primitive-types.md)

[<span data-ttu-id="ed76a-125">F# 语言参考</span><span class="sxs-lookup"><span data-stu-id="ed76a-125">F# Language Reference</span></span>](index.md)