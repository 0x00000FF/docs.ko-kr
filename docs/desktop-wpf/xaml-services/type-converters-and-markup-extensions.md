---
title: XAML을 위한 형식 변환기 및 태그 확장
ms.date: 03/30/2017
helpviewer_keywords:
- XAML [XAML Services], type converter services
- XAML [XAML Services], value converters
- XAML [XAML Services], markup extension services
- value converters for XAML [XAML Services]
- XAML [XAML Services], service context
ms.assetid: db07a952-05ce-4aa4-b6f9-aac7397d0326
ms.openlocfilehash: bee94b03d4fd6e6f5ef8571e83f554b381dd6582
ms.sourcegitcommit: c2d9718996402993cf31541f11e95531bc68bad0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/27/2020
ms.locfileid: "81432889"
---
# <a name="type-converters-and-markup-extensions-for-xaml"></a><span data-ttu-id="8ecc8-102">XAML을 위한 형식 변환기 및 태그 확장</span><span class="sxs-lookup"><span data-stu-id="8ecc8-102">Type Converters and Markup Extensions for XAML</span></span>

<span data-ttu-id="8ecc8-103">형식 변환기 및 태그 확장은 XAML 형식 시스템과 XAML 작성기가 개체 그래프 구성 요소를 생성하는 데 사용하는 두 가지 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-103">Type converters and markup extensions are two techniques that XAML type systems and XAML writers use to generate object graph components.</span></span> <span data-ttu-id="8ecc8-104">일부 특징을 공유하지만 형식 변환기 및 태그 확장은 XAML 노드 스트림에서 다르게 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-104">Although they share some characteristics, type converters and markup extensions are represented differently in a XAML node stream.</span></span> <span data-ttu-id="8ecc8-105">이 설명서 집합에서는 때때로 형식 변환기, 태그 확장 및 유사한 구문을 총체적으로 값 변환기라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-105">In this documentation set, type converters, markup extensions, and similar constructs are sometimes collectively referred to as value converters.</span></span>

## <a name="value-converters"></a><span data-ttu-id="8ecc8-106">값 변환기</span><span class="sxs-lookup"><span data-stu-id="8ecc8-106">Value Converters</span></span>

<span data-ttu-id="8ecc8-107">XAML에서 값 변환기는 다양한 시나리오에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-107">In XAML, value converters are used for various scenarios.</span></span> <span data-ttu-id="8ecc8-108">다음 목록에서는 XAML의 다양한 값 변환기 유형을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-108">The following list shows the different types of value converters in XAML:</span></span>

- <span data-ttu-id="8ecc8-109">형식 변환기</span><span class="sxs-lookup"><span data-stu-id="8ecc8-109">Type converter</span></span>

- <span data-ttu-id="8ecc8-110">태그 확장</span><span class="sxs-lookup"><span data-stu-id="8ecc8-110">Markup extension</span></span>

- <span data-ttu-id="8ecc8-111">값 직렬 변환기</span><span class="sxs-lookup"><span data-stu-id="8ecc8-111">Value serializer</span></span>

- <span data-ttu-id="8ecc8-112">XAML 텍스트 구문에 대한 논리를 제공하는 관련 클래스 또는 지원 클래스</span><span class="sxs-lookup"><span data-stu-id="8ecc8-112">Related class or support class that provides the logic for a XAML text syntax</span></span>

## <a name="type-converters"></a><span data-ttu-id="8ecc8-113">형식 변환기</span><span class="sxs-lookup"><span data-stu-id="8ecc8-113">Type Converters</span></span>

<span data-ttu-id="8ecc8-114">.NET XAML 서비스 정의에서 형식 변환기는 CLR <xref:System.ComponentModel.TypeConverter> 클래스에서 파생되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-114">In .NET XAML Services definition, type converters are classes that derive from the CLR <xref:System.ComponentModel.TypeConverter> class.</span></span> <span data-ttu-id="8ecc8-115"><xref:System.ComponentModel.TypeConverter>은 XAML이 존재하기 전에 .NET에 있던 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-115"><xref:System.ComponentModel.TypeConverter> is a class that was in the .NET before XAML existed.</span></span> <span data-ttu-id="8ecc8-116">원래 목적은 IDE 속성에 대한 속성 창 및 유사한 텍스트 기반 편집 비유를 지원하는 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-116">Its original purpose was to support property windows and similar text-based editing metaphors for IDE properties.</span></span> <span data-ttu-id="8ecc8-117">.NET에 XAML을 도입하여 텍스트 구문(특성 값 또는 XAML 값 노드에 있는 대로)을 개체로 변환하는 데 사용됩니다. <xref:System.ComponentModel.TypeConverter></span><span class="sxs-lookup"><span data-stu-id="8ecc8-117">The introduction of XAML to .NET uses <xref:System.ComponentModel.TypeConverter> to convert a text syntax (as found in an attribute value or a XAML value node) into an object.</span></span> <span data-ttu-id="8ecc8-118"><xref:System.ComponentModel.TypeConverter> 를 사용하여 개체 값을 텍스트 구문으로 직렬화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-118"><xref:System.ComponentModel.TypeConverter> can also be used to serialize an object value to text syntax.</span></span> <span data-ttu-id="8ecc8-119"><xref:System.ComponentModel.TypeConverter>또한 WPF(Windows 프레젠테이션 파운데이션) 및 Windows 통신 재단(WCF)의 이전 프레임워크별 XAML 구현에서도 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-119"><xref:System.ComponentModel.TypeConverter> was also used in previous framework-specific XAML implementations in Windows Presentation Foundation (WPF) and Windows Communication Foundation (WCF).</span></span> <span data-ttu-id="8ecc8-120">XAML의 <xref:System.ComponentModel.TypeConverter> 에 대한 자세한 내용은 [Type Converters for XAML Overview](type-converters-overview.md)의 이전 프레임워크별 XAML 구현에서도 사용되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-120">For more information about the <xref:System.ComponentModel.TypeConverter> in XAML, see [Type Converters for XAML Overview](type-converters-overview.md).</span></span>

## <a name="markup-extensions"></a><span data-ttu-id="8ecc8-121">태그 확장</span><span class="sxs-lookup"><span data-stu-id="8ecc8-121">Markup Extensions</span></span>

<span data-ttu-id="8ecc8-122">.NET XAML 서비스 구현에서 태그 확장은 <xref:System.Windows.Markup.MarkupExtension> 클래스에서 파생되는 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-122">In .NET XAML Services implementation, markup extensions are classes that derive from the <xref:System.Windows.Markup.MarkupExtension> class.</span></span> <span data-ttu-id="8ecc8-123">태그 확장은 이 폼에서 XAML 언어에 의해 시작되는 개념입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-123">Markup extensions are a concept that in this form is originated by the XAML language.</span></span> <span data-ttu-id="8ecc8-124">태그 확장은 논리 제공을 위해 서비스 클래스를 호출하는 확장 가능한 이스케이프 시퀀스와 같은 것으로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-124">You can think of a markup extension as being something like an extensible escape sequence that calls into a service class to provide its logic.</span></span> <span data-ttu-id="8ecc8-125">태그 측면에서 XAML 프로세서는 텍스트 문자열에서 여는 중괄호({)로 시작하는 텍스트 시퀀스를 통해 태그 확장을 보편적으로 인식합니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-125">In terms of markup, XAML processors universally recognize a markup extension by a text sequence that starts with an opening brace ({) in a text string.</span></span>

<span data-ttu-id="8ecc8-126">태그 확장은 형식 변환기와 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-126">Markup extensions differ from type converters.</span></span> <span data-ttu-id="8ecc8-127">형식 변환기는 일반적으로 형식 또는 멤버와 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-127">Type converters are typically associated with types or members.</span></span> <span data-ttu-id="8ecc8-128">개체 그래프를 만들거나 직렬화 시 해당 엔터티와 연결된 텍스트 구문이 발견될 때 호출됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-128">They are invoked when an object graph creation or a serialization encounters text syntax that is associated with those entities.</span></span>

<span data-ttu-id="8ecc8-129">태그 확장은 단일 지원 서비스 클래스와 연결되지만 모든 멤버 값에 대해 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-129">Markup extensions are associated with a single supporting service class, but can be applied for any member value.</span></span> <span data-ttu-id="8ecc8-130">그러나 태그 확장을 구현하여 서비스 컨텍스트를 사용하여 특정 멤버 또는 대상 유형으로 의도적으로 사용을 제한할 수 있습니다. 태그 확장은 형식 변환기 연결을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-130">(However, you can implement your markup extension to deliberately restrict its use to certain members or destination types, by using service context.) Markup extensions can override a type converter association.</span></span> <span data-ttu-id="8ecc8-131">또는 그렇지 않을 경우 텍스트 구문을 지원하지 않는 멤버에 대한 특성 값을 지정하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-131">Or you can use them to specify an attribute value for members that would not otherwise support a text syntax.</span></span>

<span data-ttu-id="8ecc8-132">XAML에 대한 태그 확장 구현 패턴에 대한 자세한 내용은 [Markup Extensions for XAML Overview](markup-extensions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ecc8-132">For more information about the markup extension implementation pattern for XAML, see [Markup Extensions for XAML Overview](markup-extensions-overview.md).</span></span>

## <a name="value-serializers"></a><span data-ttu-id="8ecc8-133">값 직렬 변환기</span><span class="sxs-lookup"><span data-stu-id="8ecc8-133">Value Serializers</span></span>

<span data-ttu-id="8ecc8-134"><xref:System.Windows.Markup.ValueSerializer> 는 개체를 문자열로 변환하는 작업에 최적화된 특수 형식 변환기입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-134">A <xref:System.Windows.Markup.ValueSerializer> is a specialized type converter that is optimized for converting an object to a string.</span></span> <span data-ttu-id="8ecc8-135">XAML용 <xref:System.Windows.Markup.ValueSerializer> 는 `ConvertFrom` 메서드를 구현하지 않을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-135">A <xref:System.Windows.Markup.ValueSerializer> for XAML might not implement the `ConvertFrom` method at all.</span></span> <span data-ttu-id="8ecc8-136"><xref:System.Windows.Markup.ValueSerializer> 구현은 <xref:System.ComponentModel.TypeConverter> 구현과 유사한 방식으로 서비스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-136">A <xref:System.Windows.Markup.ValueSerializer> implementation obtains services in a manner that is like a <xref:System.ComponentModel.TypeConverter> implementation.</span></span> <span data-ttu-id="8ecc8-137">가상 메서드는 입력 `context` 매개 변수를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-137">The virtual methods provide an input `context` parameter.</span></span> <span data-ttu-id="8ecc8-138">`context` 매개 변수는 <xref:System.Windows.Markup.IValueSerializerContext>인터페이스에서 상속되고 <xref:System.IServiceProvider> 메서드를 포함하는 <xref:System.IServiceProvider.GetService%2A> 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-138">The `context` parameter is of type <xref:System.Windows.Markup.IValueSerializerContext>, which inherits from the <xref:System.IServiceProvider> interface and has a <xref:System.IServiceProvider.GetService%2A> method.</span></span>

<span data-ttu-id="8ecc8-139">XAML 형식 시스템에서 직렬화를 위해 XAML 노드 루프 처리를 사용하는 XAML 작성기 구현의 경우 형식 또는 멤버와 연결된 값 변환기가 자체 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 속성에 의해 보고됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-139">In the XAML type system and for XAML writer implementations that use XAML node loop processing for serialization, a value converter that is associated with a type or member is reported by its own <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> property.</span></span> <span data-ttu-id="8ecc8-140">직렬화를 수행하는 XAML 작성기에 대한 의미는 <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> 및 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 가 있을 경우 부하 경로에 대해 형식 변환기를 사용해야 하고 저장 경로에 대해 값 직렬 변환기를 사용해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-140">The meaning to XAML writers that perform serialization is that if a <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> and <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> exist, the type converter should be used for the load path and the value serializer should be used for the save path.</span></span> <span data-ttu-id="8ecc8-141"><xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> 가 있지만 <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> 가 `null`이면 저장 경로에도 형식 변환기가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-141">If <xref:System.Xaml.XamlType.TypeConverter%2A?displayProperty=nameWithType> exists but <xref:System.Xaml.XamlType.ValueSerializer%2A?displayProperty=nameWithType> is `null`, the type converter is also used for the save path.</span></span>

## <a name="other-value-converters"></a><span data-ttu-id="8ecc8-142">기타 값 변환기</span><span class="sxs-lookup"><span data-stu-id="8ecc8-142">Other Value Converters</span></span>

<span data-ttu-id="8ecc8-143">값 변환기는 형식 변환기 또는 태그 확장의 특정 패턴 이상으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-143">A value converter is extensible beyond the specific patterns of a type converter or a markup extension.</span></span> <span data-ttu-id="8ecc8-144">그러나 이 사용자 지정에는 .NET XAML 서비스에서 제공하는 XAML 형식 시스템의 재정의도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-144">However, this customization would also require the redefinition of the XAML type system as provided by .NET XAML Services.</span></span> <span data-ttu-id="8ecc8-145">기존 XAML 형식 시스템은 형식 변환기, 태그 확장 및 값 직렬 변환기에 대한 표현 및 보고 시스템을 포함하지만 사용자 지정 형식의 값 변환에 대한 표현 및 보고 시스템은 없습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-145">The existing XAML type system has representations and reporting systems for type converters, markup extensions, and value serializers, but not for custom forms of value conversion.</span></span> <span data-ttu-id="8ecc8-146">사용자 지정 값 변환기를 만들려는 경우 <xref:System.Xaml.Schema.XamlValueConverter%601> 형식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-146">If you want to create custom value converters, use the <xref:System.Xaml.Schema.XamlValueConverter%601> type.</span></span>

## <a name="type-converters-and-markup-extensions-in-combination"></a><span data-ttu-id="8ecc8-147">형식 변환기 및 태그 확장 조합</span><span class="sxs-lookup"><span data-stu-id="8ecc8-147">Type Converters and Markup Extensions in Combination</span></span>

<span data-ttu-id="8ecc8-148">태그 확장 및 형식 변환기는 XAML에서 다양한 상황에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-148">Markup extensions and type converters are used for different situations in XAML.</span></span> <span data-ttu-id="8ecc8-149">태그 확장 사용에 컨텍스트를 사용할 수는 있지만 태그 확장에서 값을 제공하는 속성의 형식 변환 동작은 일반적으로 태그 확장 구현에서 확인되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-149">Although context is available for markup extension usages, type conversion behavior of properties where a markup extension provides a value is generally is not checked in the markup extension implementations.</span></span> <span data-ttu-id="8ecc8-150">즉, 태그 확장에서 텍스트 문자열을 해당 `ProvideValue` 출력으로 반환하는 경우에도 특정 속성 또는 속성 값 형식에 적용될 때 해당 문자열의 형식 변환 동작은 호출되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-150">In other words, even if a markup extension returns a text string as its `ProvideValue` output, type conversion behavior on that string as applied to a specific property or property value type is not invoked.</span></span> <span data-ttu-id="8ecc8-151">일반적으로 태그 확장의 목적은 문자열을 처리하고 관련된 형식 변환기 없이 개체를 반환하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-151">Generally, the purpose of a markup extension is to process a string and return an object without any type converter involved.</span></span>

## <a name="service-context-for-a-value-converter"></a><span data-ttu-id="8ecc8-152">값 변환기에 대한 서비스 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="8ecc8-152">Service Context for a Value Converter</span></span>

<span data-ttu-id="8ecc8-153">값 변환기를 구현할 때 값 변환기가 적용되는 컨텍스트에 액세스해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-153">When you implement a value converter, you often need access to a context in which the value converter is applied.</span></span> <span data-ttu-id="8ecc8-154">이 컨텍스트를 서비스 컨텍스트라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-154">This context is known as the service context.</span></span> <span data-ttu-id="8ecc8-155">서비스 컨텍스트에는 활성 XAML 스키마 컨텍스트, XAML 스키마 컨텍스트 및 XAML 개체 작성자가 제공하는 형식 매핑 시스템에 대한 액세스 등과 같은 정보가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-155">The service context might include information such as the active XAML schema context, access to the type-mapping system that the XAML schema context and XAML object writer provide, and so on.</span></span> <span data-ttu-id="8ecc8-156">값 변환기에 사용 가능한 서비스 컨텍스트 및 서비스 컨텍스트에서 제공하는 서비스에 액세스하는 방법에 대한 자세한 내용은 [Service Contexts Available to Type Converters and Markup Extensions](service-contexts-with-type-converters-and-markup-extensions.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8ecc8-156">For more information about the service contexts available for a value converter and how to access the services that a service context might provide, see [Service Contexts Available to Type Converters and Markup Extensions](service-contexts-with-type-converters-and-markup-extensions.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="8ecc8-157">참조</span><span class="sxs-lookup"><span data-stu-id="8ecc8-157">See also</span></span>

- <xref:System.Windows.Markup.MarkupExtension>
- <xref:System.Xaml.XamlObjectWriter>
- [<span data-ttu-id="8ecc8-158">XAML 태그 확장 개요</span><span class="sxs-lookup"><span data-stu-id="8ecc8-158">Markup Extensions for XAML Overview</span></span>](markup-extensions-overview.md)
- [<span data-ttu-id="8ecc8-159">XAML 형식 변환기 개요</span><span class="sxs-lookup"><span data-stu-id="8ecc8-159">Type Converters for XAML Overview</span></span>](type-converters-overview.md)
- [<span data-ttu-id="8ecc8-160">형식 변환기 및 태그 확장에 사용 가능한 서비스 컨텍스트</span><span class="sxs-lookup"><span data-stu-id="8ecc8-160">Service Contexts Available to Type Converters and Markup Extensions</span></span>](service-contexts-with-type-converters-and-markup-extensions.md)