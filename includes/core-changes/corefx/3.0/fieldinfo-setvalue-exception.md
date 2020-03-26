---
ms.openlocfilehash: dc733ee32184db5af59bb06e294cd73765977581
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2020
ms.locfileid: "77449563"
---
### <a name="fieldinfosetvalue-throws-exception-for-static-init-only-fields"></a><span data-ttu-id="9083d-101">FieldInfo.SetValue가 초기화 전용 정적 필드에 대해 예외를 throw</span><span class="sxs-lookup"><span data-stu-id="9083d-101">FieldInfo.SetValue throws exception for static, init-only fields</span></span>

<span data-ttu-id="9083d-102">.NET Core 3.0부터 <xref:System.Reflection.FieldAttributes.InitOnly>를 호출하여 정적 <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=fullName> 필드에 값을 설정하려고 하면 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-102">Starting in .NET Core 3.0, an exception is thrown when you attempt to set a value on a static, <xref:System.Reflection.FieldAttributes.InitOnly> field by calling <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=fullName>.</span></span>

#### <a name="change-description"></a><span data-ttu-id="9083d-103">변경 내용 설명</span><span class="sxs-lookup"><span data-stu-id="9083d-103">Change description</span></span>

<span data-ttu-id="9083d-104">.NET Framework 및 3.0 이전 버전의 .NET Core에서는 [을 호출하여 초기화 후 상수인 정적 필드의 값을 설정할 수 있습니다(](~/docs/csharp/language-reference/keywords/readonly.md)C#의 readonly<xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=fullName>).</span><span class="sxs-lookup"><span data-stu-id="9083d-104">In .NET Framework and versions of .NET Core prior to 3.0, you could set the value of a static field that's constant after it is initialized ([readonly in C#](~/docs/csharp/language-reference/keywords/readonly.md)) by calling <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=fullName>.</span></span> <span data-ttu-id="9083d-105">그러나 이러한 필드를 이 방식으로 설정하면 대상 프레임워크 및 최적화 설정에 따라 예기치 않은 동작이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-105">However, setting such a field in this way resulted in unpredictable behavior based on the target framework and optimization settings.</span></span>

<span data-ttu-id="9083d-106">.NET Core 3.0 이상 버전에서 정적 <xref:System.Reflection.FieldInfo.SetValue%2A> 필드에 <xref:System.Reflection.FieldAttributes.InitOnly>를 호출하면 <xref:System.FieldAccessException?displayProperty=nameWithType> 예외가 throw됩니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-106">In .NET Core 3.0 and later versions, when you call <xref:System.Reflection.FieldInfo.SetValue%2A> on a static, <xref:System.Reflection.FieldAttributes.InitOnly> field, a <xref:System.FieldAccessException?displayProperty=nameWithType> exception is thrown.</span></span>

> [!TIP]
> <span data-ttu-id="9083d-107"><xref:System.Reflection.FieldAttributes.InitOnly> 필드는 선언되는 시점에 또는 포함하는 클래스의 생성자에서만 설정할 수 있는 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-107">An <xref:System.Reflection.FieldAttributes.InitOnly> field is one that can only be set at the time it's declared or in the constructor for the containing class.</span></span> <span data-ttu-id="9083d-108">즉, 초기화 후에는 상수입니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-108">In other words, it's constant after it is initialized.</span></span>

#### <a name="version-introduced"></a><span data-ttu-id="9083d-109">도입된 버전</span><span class="sxs-lookup"><span data-stu-id="9083d-109">Version introduced</span></span>

<span data-ttu-id="9083d-110">3.0</span><span class="sxs-lookup"><span data-stu-id="9083d-110">3.0</span></span>

#### <a name="recommended-action"></a><span data-ttu-id="9083d-111">권장 조치</span><span class="sxs-lookup"><span data-stu-id="9083d-111">Recommended action</span></span>

<span data-ttu-id="9083d-112">정적 생성자에서 정적 <xref:System.Reflection.FieldAttributes.InitOnly> 필드를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-112">Initialize static, <xref:System.Reflection.FieldAttributes.InitOnly> fields in a static constructor.</span></span> <span data-ttu-id="9083d-113">이는 동적 형식과 비동적 형식 모두에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-113">This applies to both dynamic and non-dynamic types.</span></span>

<span data-ttu-id="9083d-114">또는 필드에서 <xref:System.Reflection.FieldAttributes.InitOnly?displayProperty=nameWithType> 특성을 제거한 다음 <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=nameWithType>를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9083d-114">Alternatively, you can remove the <xref:System.Reflection.FieldAttributes.InitOnly?displayProperty=nameWithType> attribute from the field, and then call <xref:System.Reflection.FieldInfo.SetValue%2A?displayProperty=nameWithType>.</span></span>

#### <a name="category"></a><span data-ttu-id="9083d-115">범주</span><span class="sxs-lookup"><span data-stu-id="9083d-115">Category</span></span>

<span data-ttu-id="9083d-116">CoreFx</span><span class="sxs-lookup"><span data-stu-id="9083d-116">CoreFx</span></span>

#### <a name="affected-apis"></a><span data-ttu-id="9083d-117">영향을 받는 API</span><span class="sxs-lookup"><span data-stu-id="9083d-117">Affected APIs</span></span>

- <xref:System.Reflection.FieldInfo.SetValue(System.Object,System.Object)?displayProperty=nameWithType>
- <xref:System.Reflection.FieldInfo.SetValue(System.Object,System.Object,System.Reflection.BindingFlags,System.Reflection.Binder,System.Globalization.CultureInfo)?displayProperty=nameWithType>

<!--

### Affected APIs

- `M:System.Reflection.FieldInfo.SetValue(System.Object,System.Object)`
- `M:System.Reflection.FieldInfo.SetValue(System.Object,System.Object,System.Reflection.BindingFlags,System.Reflection.Binder,System.Globalization.CultureInfo)`

-->