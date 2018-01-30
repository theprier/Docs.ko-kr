---
title: "EF 코어-8의 5-데이터 모델을 사용 하 여 razor 페이지"
author: rick-anderson
description: "이 자습서에서는 더 많은 엔터티 및 관계를 추가 및 서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델을 사용자 지정 합니다."
manager: wpickett
ms.author: riande
ms.date: 10/25/2017
ms.prod: asp.net-core
ms.technology: aspnet
ms.topic: get-started-article
uid: data/ef-rp/complex-data-model
ms.openlocfilehash: 58bb773ba16314827da84909def05a8ef370479b
ms.sourcegitcommit: a510f38930abc84c4b302029d019a34dfe76823b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/30/2018
---
# <a name="creating-a-complex-data-model---ef-core-with-razor-pages-tutorial-5-of-8"></a><span data-ttu-id="15722-103">복잡 한 데이터 모델-EF 코어 Razor 페이지 자습서 (8 5)와 함께 만들기</span><span class="sxs-lookup"><span data-stu-id="15722-103">Creating a complex data model - EF Core with Razor Pages tutorial (5 of 8)</span></span>

<span data-ttu-id="15722-104">여 [Tom Dykstra](https://github.com/tdykstra) 및 [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="15722-104">By [Tom Dykstra](https://github.com/tdykstra) and [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

[!INCLUDE[about the series](../../includes/RP-EF/intro.md)]

<span data-ttu-id="15722-105">이전 자습서의 세 가지 엔터티 작성 된 기본 데이터 모델이 들어 있는 작업.</span><span class="sxs-lookup"><span data-stu-id="15722-105">The previous tutorials worked with a basic data model that was composed of three entities.</span></span> <span data-ttu-id="15722-106">이 자습서:</span><span class="sxs-lookup"><span data-stu-id="15722-106">In this tutorial:</span></span>

* <span data-ttu-id="15722-107">더 많은 엔터티 및 관계 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-107">More entities and relationships are added.</span></span>
* <span data-ttu-id="15722-108">서식 지정, 유효성 검사 및 데이터베이스 매핑 규칙을 지정 하 여 데이터 모델 사용자 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-108">The data model is customized by specifying formatting, validation, and database mapping rules.</span></span>

<span data-ttu-id="15722-109">완성 된 데이터 모델에 대 한 엔터티 클래스는 다음 그림에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-109">The entity classes for the completed data model is shown in the following illustration:</span></span>

![엔터티 다이어그램](complex-data-model/_static/diagram.png)

<span data-ttu-id="15722-111">문제를 해결할 수 없는를 실행 하는 경우 다운로드는 [이 단계에 대 한 완성 된 앱](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-111">If you run into problems you can't solve, download the [completed app for this stage](https://github.com/aspnet/Docs/tree/master/aspnetcore/data/ef-rp/intro/samples/StageSnapShots/cu-part5-complex).</span></span>

## <a name="customize-the-data-model-with-attributes"></a><span data-ttu-id="15722-112">특성을 가진 데이터 모델 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="15722-112">Customize the data model with attributes</span></span>

<span data-ttu-id="15722-113">이 섹션에서는 데이터 모델 사용자 특성을 사용 하 여 지정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-113">In this section, the data model is customized using attributes.</span></span>

### <a name="the-datatype-attribute"></a><span data-ttu-id="15722-114">데이터 형식 특성</span><span class="sxs-lookup"><span data-stu-id="15722-114">The DataType attribute</span></span>

<span data-ttu-id="15722-115">학생 페이지는 현재 등록 날짜의 시간을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-115">The student pages currently displays the time of the enrollment date.</span></span> <span data-ttu-id="15722-116">일반적으로 날짜 필드에 날짜 및 시간이 아닌 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="15722-116">Typically, date fields show only the date and not the time.</span></span>

<span data-ttu-id="15722-117">업데이트 *Models/Student.cs* 를 다음으로 코드를 강조 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-117">Update *Models/Student.cs* with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_DataType&highlight=3,12-13)]

<span data-ttu-id="15722-118">[DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) 특성 데이터베이스 내장 형식 보다 구체적인 데이터 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-118">The [DataType](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatypeattribute?view=netframework-4.7.1) attribute specifies a data type that's more specific than the database intrinsic type.</span></span> <span data-ttu-id="15722-119">이 경우에는 날짜를 표시할지 날짜 및 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-119">In this case only the date should be displayed, not the date and time.</span></span> <span data-ttu-id="15722-120">[DataType 열거형](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) 날짜, 시간, 전화 번호, 통화, EmailAddress 등과 같은 많은 데이터 형식에 대 한 제공 합니다. `DataType` 특성 응용 프로그램에서 특정 형식의 기능을 제공 하는 자동으로 활성화할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-120">The [DataType Enumeration](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.datatype?view=netframework-4.7.1) provides for many data types, such as Date, Time, PhoneNumber, Currency, EmailAddress, etc. The `DataType` attribute can also enable the app to automatically provide type-specific features.</span></span> <span data-ttu-id="15722-121">예:</span><span class="sxs-lookup"><span data-stu-id="15722-121">For example:</span></span>

* <span data-ttu-id="15722-122">`mailto:` 에 대 한 링크가 자동으로 만들어집니다 `DataType.EmailAddress`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-122">The `mailto:` link is automatically created for `DataType.EmailAddress`.</span></span>
* <span data-ttu-id="15722-123">날짜 선택 ´ ë ç `DataType.Date` 대부분의 브라우저에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-123">The date selector is provided for `DataType.Date` in most browsers.</span></span>

<span data-ttu-id="15722-124">`DataType` 특성 내보냅니다 HTML 5 `data-` HTML 5 브라우저를 사용 하는 (커맨드 데이터 대시) 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-124">The `DataType` attribute emits HTML 5 `data-` (pronounced data dash) attributes that HTML 5 browsers consume.</span></span> <span data-ttu-id="15722-125">`DataType` 특성 유효성 검사를 제공 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-125">The `DataType` attributes don't provide validation.</span></span>

<span data-ttu-id="15722-126">`DataType.Date`표시 되는 날짜의 형식을 지정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-126">`DataType.Date` doesn't specify the format of the date that's displayed.</span></span> <span data-ttu-id="15722-127">기본적으로 날짜 필드는 서버에 따라 기본 형식에 따라 표시 [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-127">By default, the date field is displayed according to the default formats based on the server's [CultureInfo](https://docs.microsoft.com/aspnet/core/fundamentals/localization#provide-localized-resources-for-the-languages-and-cultures-you-support).</span></span>

<span data-ttu-id="15722-128">`DisplayFormat` 특성은 날짜 형식을 명시적으로 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-128">The `DisplayFormat` attribute is used to explicitly specify the date format:</span></span>

```csharp
[DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

<span data-ttu-id="15722-129">`ApplyFormatInEditMode` 설정은 서식을 적용 해야 하는지도 편집 UI에 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-129">The `ApplyFormatInEditMode` setting specifies that the formatting should also be applied to the edit UI.</span></span> <span data-ttu-id="15722-130">일부 필드를 사용 하면 안 `ApplyFormatInEditMode`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-130">Some fields shouldn't use `ApplyFormatInEditMode`.</span></span> <span data-ttu-id="15722-131">예를 들어, 통화 기호는 일반적으로 나타나지 편집 텍스트 상자에.</span><span class="sxs-lookup"><span data-stu-id="15722-131">For example, the currency symbol should generally not be displayed in an edit text box.</span></span>

<span data-ttu-id="15722-132">`DisplayFormat` 특성 단독으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-132">The `DisplayFormat` attribute can be used by itself.</span></span> <span data-ttu-id="15722-133">일반적으로 사용 하는 `DataType` 특성이 `DisplayFormat` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-133">It's generally a good idea to use the `DataType` attribute with the `DisplayFormat` attribute.</span></span> <span data-ttu-id="15722-134">`DataType` 특성의 데이터를 화면에 렌더링 하는 방법 전송할 의미 체계를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-134">The `DataType` attribute conveys the semantics of the data as opposed to how to render it on a screen.</span></span> <span data-ttu-id="15722-135">`DataType` 특성에서 사용할 수 있는 다음과 같은 이점을 제공 `DisplayFormat`:</span><span class="sxs-lookup"><span data-stu-id="15722-135">The `DataType` attribute provides the following benefits that are not available in `DisplayFormat`:</span></span>

* <span data-ttu-id="15722-136">브라우저는 HTML5 기능을 활성화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-136">The browser can enable HTML5 features.</span></span> <span data-ttu-id="15722-137">예를 들어 calendar 컨트롤, 로캘에 적합 한 통화 기호, 전자 메일 링크, 클라이언트 쪽 입력된 유효성 검사, 등을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-137">For example, show a calendar control, the locale-appropriate currency symbol, email links, client-side input validation, etc.</span></span>
* <span data-ttu-id="15722-138">기본적으로 브라우저는 로캘을 기반으로 올바른 형식을 사용 하 여 데이터를 렌더링 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-138">By default, the browser renders data using the correct format based on the locale.</span></span>

<span data-ttu-id="15722-139">자세한 내용은 참조는 [ \<입력 > 태그 도우미 설명서](xref:mvc/views/working-with-forms#the-input-tag-helper)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-139">For more information, see the [\<input> Tag Helper documentation](xref:mvc/views/working-with-forms#the-input-tag-helper).</span></span>

<span data-ttu-id="15722-140">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-140">Run the app.</span></span> <span data-ttu-id="15722-141">학생 인덱스 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-141">Navigate to the Students Index page.</span></span> <span data-ttu-id="15722-142">시간이 더 이상 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-142">Times are no longer displayed.</span></span> <span data-ttu-id="15722-143">사용 하는 모든 보기는 `Student` 모델에는 시간을 제외한 날짜가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-143">Every view that uses the `Student` model displays the date without time.</span></span>

![학생 인덱스 페이지 시간 없이 날짜를 표시 합니다.](complex-data-model/_static/dates-no-times.png)

### <a name="the-stringlength-attribute"></a><span data-ttu-id="15722-145">StringLength 특성</span><span class="sxs-lookup"><span data-stu-id="15722-145">The StringLength attribute</span></span>

<span data-ttu-id="15722-146">데이터 유효성 검사 규칙 및 유효성 검사 오류 메시지를 특성으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-146">Data validation rules and validation error messages can be specified with attributes.</span></span> <span data-ttu-id="15722-147">[StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) 특성 문자 데이터 필드에는 사용할 수 있는 최소 및 최대 길이 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-147">The [StringLength](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.stringlengthattribute?view=netframework-4.7.1) attribute specifies the minimum and maximum length of characters that are allowed in a data field.</span></span> <span data-ttu-id="15722-148">`StringLength` 특성은 또한 클라이언트 쪽 및 서버 쪽 유효성 검사를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-148">The `StringLength` attribute also provides client-side and server-side validation.</span></span> <span data-ttu-id="15722-149">최소 값은 데이터베이스 스키마에 대해 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-149">The minimum value has no impact on the database schema.</span></span>

<span data-ttu-id="15722-150">업데이트는 `Student` 를 다음 코드로 모델:</span><span class="sxs-lookup"><span data-stu-id="15722-150">Update the `Student` model with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_StringLength&highlight=10,12)]

<span data-ttu-id="15722-151">위의 코드 이름을 최대 50 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-151">The preceding code limits names to no more than 50 characters.</span></span> <span data-ttu-id="15722-152">`StringLength` 특성 이름에 공백을 입력에서 사용자를 방지 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-152">The `StringLength` attribute doesn't prevent a user from entering white space for a name.</span></span> <span data-ttu-id="15722-153">[정규식으로](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) 특성 입력에 제한을 적용 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-153">The [RegularExpression](https://docs.microsoft.com/dotnet/api/system.componentmodel.dataannotations.regularexpressionattribute?view=netframework-4.7.1) attribute is used to apply restrictions to the input.</span></span> <span data-ttu-id="15722-154">예를 들어 다음 코드는 첫 번째 문자를 대문자로 변환 하 고 나머지 문자를 사전순으로 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-154">For example, the following code requires the first character to be upper case and the remaining characters to be alphabetical:</span></span>

```csharp
[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]
```

<span data-ttu-id="15722-155">응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-155">Run the app:</span></span>

* <span data-ttu-id="15722-156">학생 페이지로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-156">Navigate to the Students page.</span></span>
* <span data-ttu-id="15722-157">선택 **새로 만들기**, 50 자 보다 긴 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-157">Select **Create New**, and enter a name longer than 50 characters.</span></span>
* <span data-ttu-id="15722-158">선택 **만들기**, 클라이언트 쪽 유효성 검사 오류 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-158">Select **Create**, client-side validation shows an error message.</span></span>

![학생 인덱스 문자열 길이 오류를 보여주는 페이지](complex-data-model/_static/string-length-errors.png)

<span data-ttu-id="15722-160">**SQL Server 개체 탐색기** (SSOX) 두 번 클릭 하 여 학생 테이블 디자이너를 열고는 **학생** 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-160">In **SQL Server Object Explorer** (SSOX), open the Student table designer by double-clicking the **Student** table.</span></span>

![마이그레이션 전에 SSOX에 students 테이블](complex-data-model/_static/ssox-before-migration.png)

<span data-ttu-id="15722-162">위 그림에 대 한 스키마를 보여 줍니다.는 `Student` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-162">The preceding image shows the schema for the `Student` table.</span></span> <span data-ttu-id="15722-163">이름 필드 형식이 있어야 `nvarchar(MAX)` 마이그레이션 DB에서 실행 되지 않은 때문에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-163">The name fields have type `nvarchar(MAX)` because migrations has not been run on the DB.</span></span> <span data-ttu-id="15722-164">이름 필드 됩니다 마이그레이션이 시작 되 면이 자습서의 뒷부분에 나오는, `nvarchar(50)`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-164">When migrations are run later in this tutorial, the name fields become `nvarchar(50)`.</span></span>

### <a name="the-column-attribute"></a><span data-ttu-id="15722-165">Column 특성</span><span class="sxs-lookup"><span data-stu-id="15722-165">The Column attribute</span></span>

<span data-ttu-id="15722-166">특성은 클래스 및 속성을 데이터베이스에 매핑되는 방식을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-166">Attributes can control how classes and properties are mapped to the database.</span></span> <span data-ttu-id="15722-167">이 섹션에서는 `Column` 특성의 이름에 매핑할 때 사용 되는 `FirstMidName` 속성을 "FirstName" DB에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-167">In this section, the `Column` attribute is used to map the name of the `FirstMidName` property to "FirstName" in the DB.</span></span>

<span data-ttu-id="15722-168">모델에 속성 이름이 열 이름에 사용 됩니다 DB를 만들면 (경우는 제외의 `Column` 특성은 사용).</span><span class="sxs-lookup"><span data-stu-id="15722-168">When the DB is created, property names on the model are used for column names (except when the `Column` attribute is used).</span></span>

<span data-ttu-id="15722-169">`Student` 사용 하 여 모델 `FirstMidName` 첫 번째 이름에 대 한 필드 중간 이름 포함도 될 수 있으므로 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-169">The `Student` model uses `FirstMidName` for the first-name field because the field might also contain a middle name.</span></span>

<span data-ttu-id="15722-170">업데이트는 *Student.cs* 다음 강조 표시 된 코드로 파일:</span><span class="sxs-lookup"><span data-stu-id="15722-170">Update the *Student.cs* file with the following highlighted code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_Column&highlight=4,14)]

<span data-ttu-id="15722-171">이전 변경으로 인해 `Student.FirstMidName` 응용 프로그램에 매핑되는 `FirstName` 의 열은 `Student` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-171">With the preceding change, `Student.FirstMidName` in the app maps to the `FirstName` column of the `Student` table.</span></span>

<span data-ttu-id="15722-172">추가 `Column` 특성이 변경 모델이 고 `SchoolContext`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-172">The addition of the `Column` attribute changes the model backing the `SchoolContext`.</span></span> <span data-ttu-id="15722-173">모델이 고 `SchoolContext` 데이터베이스와 일치 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-173">The model backing the `SchoolContext` no longer matches the database.</span></span> <span data-ttu-id="15722-174">마이그레이션 적용 하기 전에 앱이 실행 되는 경우 다음과 같은 예외가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-174">If the app is run before applying migrations, the following exception is generated:</span></span>

```SQL
SqlException: Invalid column name 'FirstName'.
```
<span data-ttu-id="15722-175">DB 업데이트:</span><span class="sxs-lookup"><span data-stu-id="15722-175">To update the DB:</span></span>

* <span data-ttu-id="15722-176">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-176">Build the project.</span></span>
* <span data-ttu-id="15722-177">프로젝트 폴더에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15722-177">Open a command window in the project folder.</span></span> <span data-ttu-id="15722-178">새 마이그레이션 만들고 DB 업데이트 하려면 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-178">Enter the following commands to create a new migration and update the DB:</span></span>

    ```console
    dotnet ef migrations add ColumnFirstName
    dotnet ef database update
    ```

<span data-ttu-id="15722-179">`dotnet ef migrations add ColumnFirstName` 명령은 다음과 같은 경고 메시지를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-179">The `dotnet ef migrations add ColumnFirstName` command generates the following warning message:</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
```

<span data-ttu-id="15722-180">경고가 실제로 생성 되는 이름 필드는 이제 때문에 50 자로 제한 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-180">The warning is generated because the name fields are now limited to 50 characters.</span></span> <span data-ttu-id="15722-181">Db에서 이름 50 개 이상의 문자가 있으면 마지막 문자까지 51 손실 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-181">If a name in the DB had more than 50 characters, the 51 to last character would be lost.</span></span>

* <span data-ttu-id="15722-182">응용 프로그램을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-182">Test the app.</span></span>

<span data-ttu-id="15722-183">학생 테이블을 SSOX을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15722-183">Open the Student table in SSOX:</span></span>

![마이그레이션 후에 SSOX 학생 테이블](complex-data-model/_static/ssox-after-migration.png)

<span data-ttu-id="15722-185">이름 열 형식의 된 마이그레이션을 적용 하기 전에 [nvarchar (max)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-185">Before migration was applied, the name columns were of type [nvarchar(MAX)](https://docs.microsoft.com/sql/t-sql/data-types/nchar-and-nvarchar-transact-sql).</span></span> <span data-ttu-id="15722-186">이름 열은 이제 `nvarchar(50)`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-186">The name columns are now `nvarchar(50)`.</span></span> <span data-ttu-id="15722-187">열 이름이 바뀐 `FirstMidName` 를 `FirstName`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-187">The column name has changed from `FirstMidName` to `FirstName`.</span></span>

> [!Note]
> <span data-ttu-id="15722-188">다음 섹션의 일부 단계에는 응용 프로그램 작성과 컴파일러 오류를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-188">In the following section, building the app at some stages generates compiler errors.</span></span> <span data-ttu-id="15722-189">지침에는 응용 프로그램을 빌드하려면 시기를 지정 하십시오.</span><span class="sxs-lookup"><span data-stu-id="15722-189">The instructions specify when to build the app.</span></span>

## <a name="student-entity-update"></a><span data-ttu-id="15722-190">학생의 엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="15722-190">Student entity update</span></span>

![학생 엔터티](complex-data-model/_static/student-entity.png)

<span data-ttu-id="15722-192">업데이트 *Models/Student.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-192">Update *Models/Student.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Student.cs?name=snippet_BeforeInheritance&highlight=11,13,15,18,22,24-31)]

### <a name="the-required-attribute"></a><span data-ttu-id="15722-193">필수 특성</span><span class="sxs-lookup"><span data-stu-id="15722-193">The Required attribute</span></span>

<span data-ttu-id="15722-194">`Required` 특성 필드에 필수 이름 속성을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-194">The `Required` attribute makes the name properties required fields.</span></span> <span data-ttu-id="15722-195">`Required` nullable이 아닌 형식 예: 값 형식에 대 한 특성이 필요 하지 않습니다 (`DateTime`, `int`, `double`등.).</span><span class="sxs-lookup"><span data-stu-id="15722-195">The `Required` attribute isn't needed for non-nullable types such as value types (`DateTime`, `int`, `double`, etc.).</span></span> <span data-ttu-id="15722-196">Null 일 수 없는 형식 필수 필드로 자동으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-196">Types that can't be null are automatically treated as required fields.</span></span>

<span data-ttu-id="15722-197">`Required` 특성의 최소 길이 매개 변수를 대체할 수 있습니다는 `StringLength` 특성:</span><span class="sxs-lookup"><span data-stu-id="15722-197">The `Required` attribute could be replaced with a minimum length parameter in the `StringLength` attribute:</span></span>

```csharp
[Display(Name = "Last Name")]
[StringLength(50, MinimumLength=1)]
public string LastName { get; set; }
```

### <a name="the-display-attribute"></a><span data-ttu-id="15722-198">표시 특성</span><span class="sxs-lookup"><span data-stu-id="15722-198">The Display attribute</span></span>

<span data-ttu-id="15722-199">`Display` 특성 캡션 텍스트 상자에 대 한 "이름", "Last Name", "전체 Name" 및 "등록 날짜입니다." 해야 함을 지정</span><span class="sxs-lookup"><span data-stu-id="15722-199">The `Display` attribute specifies that the caption for the text boxes should be "First Name", "Last Name", "Full Name", and "Enrollment Date."</span></span> <span data-ttu-id="15722-200">기본 캡션을 예를 들어 "Lastname. 가" 단어를 분할 하지 공간이</span><span class="sxs-lookup"><span data-stu-id="15722-200">The default captions had no space dividing the words, for example "Lastname."</span></span>

### <a name="the-fullname-calculated-property"></a><span data-ttu-id="15722-201">계산 FullName 속성</span><span class="sxs-lookup"><span data-stu-id="15722-201">The FullName calculated property</span></span>

<span data-ttu-id="15722-202">`FullName`다른 두 개의 속성을 연결 하 여 생성 하는 값을 반환 하는 계산 된 속성이입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-202">`FullName` is a calculated property that returns a value that's created by concatenating two other properties.</span></span> <span data-ttu-id="15722-203">`FullName`get 접근자만에 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-203">`FullName` cannot be set, it has only a get accessor.</span></span> <span data-ttu-id="15722-204">더 `FullName` 열이 데이터베이스에 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-204">No `FullName` column is created in the database.</span></span>

## <a name="create-the-instructor-entity"></a><span data-ttu-id="15722-205">Instructor 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="15722-205">Create the Instructor Entity</span></span>

![Instructor 엔터티](complex-data-model/_static/instructor-entity.png)

<span data-ttu-id="15722-207">만들 *Models/Instructor.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-207">Create *Models/Instructor.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Instructor.cs?name=snippet_BeforeInheritance)]

<span data-ttu-id="15722-208">여러 속성을 가지에서 동일는 `Student` 및 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-208">Notice that several properties are the same in the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="15722-209">이 시리즈의 뒷부분에 나오는 상속 구현 자습서에서는이 코드는 중복 제거를 리팩터링 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-209">In the Implementing Inheritance tutorial later in this series, this code is refactored to eliminate the redundancy.</span></span>

<span data-ttu-id="15722-210">한 줄에 특성이 여러 개 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-210">Multiple attributes can be on one line.</span></span> <span data-ttu-id="15722-211">`HireDate` 특성을 다음과 같이 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-211">The `HireDate` attributes could be written as follows:</span></span>

```csharp
[DataType(DataType.Date),Display(Name = "Hire Date"),DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
```

### <a name="the-courseassignments-and-officeassignment-navigation-properties"></a><span data-ttu-id="15722-212">CourseAssignments 및 OfficeAssignment 탐색 속성</span><span class="sxs-lookup"><span data-stu-id="15722-212">The CourseAssignments and OfficeAssignment navigation properties</span></span>

<span data-ttu-id="15722-213">`CourseAssignments` 및 `OfficeAssignment` 속성은 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-213">The `CourseAssignments` and `OfficeAssignment` properties are navigation properties.</span></span>

<span data-ttu-id="15722-214">강사 courses 개수에 관계 없이 배울 수 하므로 `CourseAssignments` 컬렉션으로 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-214">An instructor can teach any number of courses, so `CourseAssignments` is defined as a collection.</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="15722-215">여러 엔터티를 보유 하는 탐색 속성 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="15722-215">If a navigation property holds multiple entities:</span></span>

* <span data-ttu-id="15722-216">에 항목 추가, 삭제 하 고 업데이트할 수는 목록 형식 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-216">It must be a list type where the entries can be added, deleted, and updated.</span></span>

<span data-ttu-id="15722-217">탐색 속성 유형은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-217">Navigation property types include:</span></span>

* `ICollection<T>`
*  `List<T>`
*  `HashSet<T>`

<span data-ttu-id="15722-218">경우 `ICollection<T>` 지정, EF 코어 만듭니다는 `HashSet<T>` 기본적으로 컬렉션입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-218">If `ICollection<T>` is specified, EF Core creates a `HashSet<T>` collection by default.</span></span>

<span data-ttu-id="15722-219">`CourseAssignment` 엔터티는 다 대 다 관계에 섹션에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-219">The `CourseAssignment` entity is explained in the section on many-to-many relationships.</span></span>

<span data-ttu-id="15722-220">Contoso 대학 비즈니스 규칙 강사 최대 하나의 office 포함 될 수 있는 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-220">Contoso University business rules state that an instructor can have at most one office.</span></span> <span data-ttu-id="15722-221">`OfficeAssignment` 속성에는 단일 저장 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-221">The `OfficeAssignment` property holds a single `OfficeAssignment` entity.</span></span> <span data-ttu-id="15722-222">`OfficeAssignment`없는 사무실 할당 된 경우 null입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-222">`OfficeAssignment` is null if no office is assigned.</span></span>

```csharp
public OfficeAssignment OfficeAssignment { get; set; }
```

## <a name="create-the-officeassignment-entity"></a><span data-ttu-id="15722-223">OfficeAssignment 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="15722-223">Create the OfficeAssignment entity</span></span>

![OfficeAssignment 엔터티](complex-data-model/_static/officeassignment-entity.png)

<span data-ttu-id="15722-225">만들 *Models/OfficeAssignment.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-225">Create *Models/OfficeAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/OfficeAssignment.cs)]

### <a name="the-key-attribute"></a><span data-ttu-id="15722-226">키 특성</span><span class="sxs-lookup"><span data-stu-id="15722-226">The Key attribute</span></span>

<span data-ttu-id="15722-227">`[Key]` 식별 하는 속성의 기본 키 (PK)로 속성 이름을 어질 때 classnameID 또는 ID가 아닌 다른 특성은 사용</span><span class="sxs-lookup"><span data-stu-id="15722-227">The `[Key]` attribute is used to identify a property as the primary key (PK) when the property name is something other than classnameID or ID.</span></span>

<span data-ttu-id="15722-228">사이 관계가 0 또는 1을 하나는 `Instructor` 및 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-228">There's a one-to-zero-or-one relationship between the `Instructor` and `OfficeAssignment` entities.</span></span> <span data-ttu-id="15722-229">에 할당 된 강사 관련 하 여 사무실 할당만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-229">An office assignment only exists in relation to the instructor it's assigned to.</span></span> <span data-ttu-id="15722-230">`OfficeAssignment` PK 이기도 해당 외래 키 (FK)에 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-230">The `OfficeAssignment` PK is also its foreign key (FK) to the `Instructor` entity.</span></span> <span data-ttu-id="15722-231">EF 코어 자동으로 인식할 수 없습니다 `InstructorID` 의 PK로 `OfficeAssignment` 때문에:</span><span class="sxs-lookup"><span data-stu-id="15722-231">EF Core can't automatically recognize `InstructorID` as the PK of `OfficeAssignment` because:</span></span>

* <span data-ttu-id="15722-232">`InstructorID`ID 또는 classnameID 명명 규칙을 따르지 않는 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-232">`InstructorID` doesn't follow the ID or classnameID naming convention.</span></span>

<span data-ttu-id="15722-233">따라서는 `Key` 특성을 식별 하는 데 사용 됩니다 `InstructorID` 는 PK로:</span><span class="sxs-lookup"><span data-stu-id="15722-233">Therefore, the `Key` attribute is used to identify `InstructorID` as the PK:</span></span>

```csharp
[Key]
public int InstructorID { get; set; }
```

<span data-ttu-id="15722-234">기본적으로 EF 코어 확인 관계에 대 한 열이 때문에 데이터베이스 생성 된으로 키를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-234">By default, EF Core treats the key as non-database-generated because the column is for an identifying relationship.</span></span>

### <a name="the-instructor-navigation-property"></a><span data-ttu-id="15722-235">강사 탐색 속성</span><span class="sxs-lookup"><span data-stu-id="15722-235">The Instructor navigation property</span></span>

<span data-ttu-id="15722-236">`OfficeAssignment` 탐색 속성에는 `Instructor` 엔터티는 null을 허용 하기 때문에:</span><span class="sxs-lookup"><span data-stu-id="15722-236">The `OfficeAssignment` navigation property for the `Instructor` entity is nullable because:</span></span>

* <span data-ttu-id="15722-237">참조 형식 (예: 클래스는 null을 허용)</span><span class="sxs-lookup"><span data-stu-id="15722-237">Reference types (such as classes are nullable).</span></span>
* <span data-ttu-id="15722-238">강사는 사무실 할당이 없을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-238">An instructor might not have an office assignment.</span></span>


<span data-ttu-id="15722-239">`OfficeAssignment` 엔터티에 비 nullable `Instructor` 탐색 속성 이므로:</span><span class="sxs-lookup"><span data-stu-id="15722-239">The `OfficeAssignment` entity has a non-nullable `Instructor` navigation property because:</span></span>

* <span data-ttu-id="15722-240">`InstructorID`null을 허용 하지입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-240">`InstructorID` is non-nullable.</span></span>
* <span data-ttu-id="15722-241">사무실 할당 강사 없이 존재할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-241">An office assignment can't exist without an instructor.</span></span>

<span data-ttu-id="15722-242">경우는 `Instructor` 엔터티에 포함 된 관련 `OfficeAssignment` 엔터티에, 각 엔터티에 탐색 속성에 다른 하나에 대 한 참조입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-242">When an `Instructor` entity has a related `OfficeAssignment` entity, each entity has a reference to the other one in its navigation property.</span></span>

<span data-ttu-id="15722-243">`[Required]` 특성에 적용할 수는 `Instructor` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="15722-243">The `[Required]` attribute could be applied to the `Instructor` navigation property:</span></span>

```csharp
[Required]
public Instructor Instructor { get; set; }
```

<span data-ttu-id="15722-244">위의 코드 관련된 강사 같아야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-244">The preceding code specifies that there must be a related instructor.</span></span> <span data-ttu-id="15722-245">위의 코드 필요 하지 않습니다. 때문에 `InstructorID` 외래 키 (PK는 이기도 함)은 nullable이 아닌 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-245">The preceding code is unnecessary because the `InstructorID` foreign key (which is also the PK) is non-nullable.</span></span>

## <a name="modify-the-course-entity"></a><span data-ttu-id="15722-246">과정 엔터티 수정</span><span class="sxs-lookup"><span data-stu-id="15722-246">Modify the Course Entity</span></span>

![과정 엔터티](complex-data-model/_static/course-entity.png)

<span data-ttu-id="15722-248">업데이트 *Models/Course.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-248">Update *Models/Course.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Course.cs?name=snippet_Final&highlight=2,10,13,16,19,21,23)]

<span data-ttu-id="15722-249">`Course` 엔터티에 포함 된 외래 키 (FK) 속성 `DepartmentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-249">The `Course` entity has a foreign key (FK) property `DepartmentID`.</span></span> <span data-ttu-id="15722-250">`DepartmentID`관련 가리키는 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-250">`DepartmentID` points to the related `Department` entity.</span></span> <span data-ttu-id="15722-251">`Course` 엔터티에 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-251">The `Course` entity has a `Department` navigation property.</span></span>

<span data-ttu-id="15722-252">EF 코어는 모델에 관련된 엔터티에 대 한 탐색 속성을 포함 하는 경우 데이터 모델에 대 한 외래 키 속성이 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-252">EF Core doesn't require a FK property for a data model when the model has a navigation property for a related entity.</span></span>

<span data-ttu-id="15722-253">EF 코어 자동으로 만듭니다 FKs 데이터베이스에 필요한 곳 마다.</span><span class="sxs-lookup"><span data-stu-id="15722-253">EF Core automatically creates FKs in the database wherever they're needed.</span></span> <span data-ttu-id="15722-254">EF 코어 만듭니다 [숨기](https://docs.microsoft.com/ef/core/modeling/shadow-properties) 자동으로 만들어진된 FKs에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-254">EF Core creates [shadow properties](https://docs.microsoft.com/ef/core/modeling/shadow-properties) for automatically created FKs.</span></span> <span data-ttu-id="15722-255">쉽고 효율적으로 데이터 모델에는 외래 키를 포함 합니다. 업데이트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-255">Having the FK in the data model can make updates simpler and more efficient.</span></span> <span data-ttu-id="15722-256">예를 들어 모델에 외래 키 속성 `DepartmentID` 은 *하지* 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-256">For example, consider a model where the FK property `DepartmentID` is *not* included.</span></span> <span data-ttu-id="15722-257">때 과정 엔터티는 편집 하려면 인출 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-257">When a course entity is fetched to edit:</span></span>

* <span data-ttu-id="15722-258">`Department` 엔터티는 명시적으로 로드 된 경우 null입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-258">The `Department` entity is null if it's not explicitly loaded.</span></span>
* <span data-ttu-id="15722-259">과정 엔터티를 업데이트 하려면는 `Department` 엔터티 먼저 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-259">To update the course entity, the `Department` entity must first be fetched.</span></span>

<span data-ttu-id="15722-260">때 외래 키 속성 `DepartmentID` 포함 된 데이터 모델에는 가져올 필요가 없습니다는 `Department` 업데이트 하기 전에 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-260">When the FK property `DepartmentID` is included in the data model, there's no need to fetch the `Department` entity before an update.</span></span>

### <a name="the-databasegenerated-attribute"></a><span data-ttu-id="15722-261">DatabaseGenerated 특성</span><span class="sxs-lookup"><span data-stu-id="15722-261">The DatabaseGenerated attribute</span></span>

<span data-ttu-id="15722-262">`[DatabaseGenerated(DatabaseGeneratedOption.None)]` 는 PK는 응용 프로그램에서 제공 하지 않고 하는 데이터베이스에서 생성 된 특성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-262">The `[DatabaseGenerated(DatabaseGeneratedOption.None)]` attribute specifies that the PK is provided by the application rather than generated by the database.</span></span>

```csharp
[DatabaseGenerated(DatabaseGeneratedOption.None)]
[Display(Name = "Number")]
public int CourseID { get; set; }
```

<span data-ttu-id="15722-263">기본적으로 EF 코어 PK 값 DB에 의해 생성 되어 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-263">By default, EF Core assumes that PK values are generated by the DB.</span></span> <span data-ttu-id="15722-264">DB PK 생성 된 값은 일반적으로 가장 좋은 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-264">DB generated PK values is generally the best approach.</span></span> <span data-ttu-id="15722-265">에 대 한 `Course` 사용자 엔터티는 PK. 지정</span><span class="sxs-lookup"><span data-stu-id="15722-265">For `Course` entities, the user specifies the PK.</span></span> <span data-ttu-id="15722-266">예를 들어 수학 부서에 대 한 1000 시리즈, 영어 부서에 대 한 2000 시리즈와 같은 과정 번호입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-266">For example, a course number such as a 1000 series for the math department, a 2000 series for the English department.</span></span>

<span data-ttu-id="15722-267">`DatabaseGenerated` 특성 기본 값을 생성 하려면 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-267">The `DatabaseGenerated` attribute can also be used to generate default values.</span></span> <span data-ttu-id="15722-268">예를 들어 DB 날짜 필드는 행이 만들어지거나 업데이트 날짜를 기록 하려면 자동으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-268">For example, the DB can automatically generate a date field to record the date a row was created or updated.</span></span> <span data-ttu-id="15722-269">자세한 내용은 참조 [속성 생성](https://docs.microsoft.com/ef/core/modeling/generated-properties)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-269">For more information, see [Generated Properties](https://docs.microsoft.com/ef/core/modeling/generated-properties).</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="15722-270">외래 키와 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-270">Foreign key and navigation properties</span></span>

<span data-ttu-id="15722-271">외래 키 (FK) 속성 및 탐색 속성을는 `Course` 엔터티는 다음과 같은 관계를 반영 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-271">The foreign key (FK) properties and navigation properties in the `Course` entity reflect the following relationships:</span></span>

<span data-ttu-id="15722-272">이므로 과정 한 부서에 할당 된는 `DepartmentID` FK 및 `Department` 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-272">A course is assigned to one department, so there's a `DepartmentID` FK and a `Department` navigation property.</span></span>

```csharp
public int DepartmentID { get; set; }
public Department Department { get; set; }
```

<span data-ttu-id="15722-273">과정을 학생을 등록 여러 개가 있을 수 있으므로 `Enrollments` 탐색 속성은 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="15722-273">A course can have any number of students enrolled in it, so the `Enrollments` navigation property is a collection:</span></span>

```csharp
public ICollection<Enrollment> Enrollments { get; set; }
```

<span data-ttu-id="15722-274">여러 강사 하 여 과정을 배울 수 있습니다 하므로 `CourseAssignments` 탐색 속성은 컬렉션:</span><span class="sxs-lookup"><span data-stu-id="15722-274">A course may be taught by multiple instructors, so the `CourseAssignments` navigation property is a collection:</span></span>

```csharp
public ICollection<CourseAssignment> CourseAssignments { get; set; }
```

<span data-ttu-id="15722-275">`CourseAssignment`설명 [나중](#many-to-many-relationships)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-275">`CourseAssignment` is explained [later](#many-to-many-relationships).</span></span>

## <a name="create-the-department-entity"></a><span data-ttu-id="15722-276">부서 엔터티 만들기</span><span class="sxs-lookup"><span data-stu-id="15722-276">Create the Department entity</span></span>

![Department 엔터티](complex-data-model/_static/department-entity.png)

<span data-ttu-id="15722-278">만들 *Models/Department.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-278">Create *Models/Department.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Department.cs?name=snippet_Begin)]

### <a name="the-column-attribute"></a><span data-ttu-id="15722-279">Column 특성</span><span class="sxs-lookup"><span data-stu-id="15722-279">The Column attribute</span></span>

<span data-ttu-id="15722-280">이전에 `Column` 특성은 열 이름 매핑을 변경 하는 데 사용 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-280">Previously the `Column` attribute was used to change column name mapping.</span></span> <span data-ttu-id="15722-281">에 대 한 코드에는 `Department` 엔터티에 `Column` 특성 SQL 데이터 형식 매핑을 변경 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-281">In the code for the `Department` entity, the `Column` attribute is used to change SQL data type mapping.</span></span> <span data-ttu-id="15722-282">`Budget` 열은 SQL Server money 형식을 사용 하 여 DB에 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-282">The `Budget` column is defined using the SQL Server money type in the DB:</span></span>

```csharp
[Column(TypeName="money")]
public decimal Budget { get; set; }
```

<span data-ttu-id="15722-283">열 매핑은 일반적으로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-283">Column mapping is generally not required.</span></span> <span data-ttu-id="15722-284">EF 코어에는 일반적으로 속성에 대 한 CLR 형식에 따라 적절 한 SQL Server 데이터 형식을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-284">EF Core generally chooses the appropriate SQL Server data type based on the CLR type for the property.</span></span> <span data-ttu-id="15722-285">CLR `decimal` SQL Server에 매핑됩니다 `decimal` 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-285">The CLR `decimal` type maps to a SQL Server `decimal` type.</span></span> <span data-ttu-id="15722-286">`Budget`통화에 대 한이 고 money 데이터 형식이 통화에 대 한 더 적합 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-286">`Budget` is for currency, and the money data type is more appropriate for currency.</span></span>

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="15722-287">외래 키와 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-287">Foreign key and navigation properties</span></span>

<span data-ttu-id="15722-288">외래 키 및 탐색 속성은 다음과 같은 관계 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-288">The FK and navigation properties reflect the following relationships:</span></span>

* <span data-ttu-id="15722-289">부서 수도 있습니다 관리자를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-289">A department may or may not have an administrator.</span></span>
* <span data-ttu-id="15722-290">관리자는 항상 강사입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-290">An administrator is always an instructor.</span></span> <span data-ttu-id="15722-291">따라서는 `InstructorID` 속성에 외래 키로 포함 되어는 `Instructor` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-291">Therefore the `InstructorID` property is included as the FK to the `Instructor` entity.</span></span>

<span data-ttu-id="15722-292">탐색 속성이 명명 `Administrator` 보유 하지만 `Instructor` 엔터티:</span><span class="sxs-lookup"><span data-stu-id="15722-292">The navigation property is named `Administrator` but holds an `Instructor` entity:</span></span>

```csharp
public int? InstructorID { get; set; }
public Instructor Administrator { get; set; }
```

<span data-ttu-id="15722-293">위의 코드에서 물음표 (?) 속성은 null을 허용을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-293">The question mark (?) in the preceding code specifies the property is nullable.</span></span>

<span data-ttu-id="15722-294">부서는 Courses 탐색 속성 이므로 많은 과목을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-294">A department may have many courses, so there's a Courses navigation property:</span></span>

```csharp
public ICollection<Course> Courses { get; set; }
```

<span data-ttu-id="15722-295">참고: 일반적으로 EF 코어 모두 삭제를 하 고 다 대 다 관계에 대 한 nullable이 아닌 FKs에 대 한 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-295">Note: By convention, EF Core enables cascade delete for non-nullable FKs and for many-to-many relationships.</span></span> <span data-ttu-id="15722-296">연계 delete 순환 cascade 규칙 삭제 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-296">Cascading delete can result in circular cascade delete rules.</span></span> <span data-ttu-id="15722-297">순환 모두 마이그레이션하는 추가 될 때 예외가 규칙 원인을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-297">Circular cascade delete rules causes an exception when a migration is added.</span></span>

<span data-ttu-id="15722-298">예를 들어 경우는 `Department.InstructorID` 속성이 nullable로 정의 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-298">For example, if the `Department.InstructorID` property wasn't defined as nullable:</span></span>

* <span data-ttu-id="15722-299">EF 코어 부서 삭제 될 때 강의 삭제 하는 cascade delete 규칙을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-299">EF Core configures a cascade delete rule to delete the instructor when the department is deleted.</span></span>
* <span data-ttu-id="15722-300">강사 부서 삭제 될 때 삭제는 의도 된 동작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-300">Deleting the instructor when the department is deleted isn't the intended behavior.</span></span>

<span data-ttu-id="15722-301">비즈니스 규칙이 요구 하는 경우는 `InstructorID` 속성을 허용 하지 않는 수 다음 fluent API 문을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-301">If business rules required the `InstructorID` property be non-nullable, use the following fluent API statement:</span></span>

 ```csharp
 modelBuilder.Entity<Department>()
    .HasOne(d => d.Administrator)
    .WithMany()
    .OnDelete(DeleteBehavior.Restrict)
 ```

<span data-ttu-id="15722-302">위의 코드는 부서 강사 관계에 cascade delete를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-302">The preceding code disables cascade delete on the department-instructor relationship.</span></span>

## <a name="update-the-enrollment-entity"></a><span data-ttu-id="15722-303">등록 엔터티 업데이트</span><span class="sxs-lookup"><span data-stu-id="15722-303">Update the Enrollment entity</span></span>

<span data-ttu-id="15722-304">등록 레코드가 한 과정을 학생 별로 수행 한 과정입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-304">An enrollment record is for a one course taken by one student.</span></span>

![등록 엔터티](complex-data-model/_static/enrollment-entity.png)

<span data-ttu-id="15722-306">업데이트 *Models/Enrollment.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-306">Update *Models/Enrollment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/Enrollment.cs?name=snippet_Final&highlight=1-2,16)]

### <a name="foreign-key-and-navigation-properties"></a><span data-ttu-id="15722-307">외래 키와 탐색 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-307">Foreign key and navigation properties</span></span>

<span data-ttu-id="15722-308">외래 키 속성 및 탐색 속성은 다음과 같은 관계 반영 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-308">The FK properties and navigation properties reflect the following relationships:</span></span>

<span data-ttu-id="15722-309">이므로 한 과정에 대 한 등록 레코드는 한 `CourseID` 외래 키 속성 및 `Course` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="15722-309">An enrollment record is for one course, so there's a `CourseID` FK property and a `Course` navigation property:</span></span>

```csharp
public int CourseID { get; set; }
public Course Course { get; set; }
```

<span data-ttu-id="15722-310">등록 레코드는 한 학생 있기 때문에 `StudentID` 외래 키 속성 및 `Student` 탐색 속성:</span><span class="sxs-lookup"><span data-stu-id="15722-310">An enrollment record is for one student, so there's a `StudentID` FK property and a `Student` navigation property:</span></span>

```csharp
public int StudentID { get; set; }
public Student Student { get; set; }
```

## <a name="many-to-many-relationships"></a><span data-ttu-id="15722-311">다 대 다 관계</span><span class="sxs-lookup"><span data-stu-id="15722-311">Many-to-Many Relationships</span></span>

<span data-ttu-id="15722-312">사이 다 대 다 관계가 있는 `Student` 및 `Course` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-312">There's a many-to-many relationship between the `Student` and `Course` entities.</span></span> <span data-ttu-id="15722-313">`Enrollment` 엔터티 역할 다 대 다 조인 테이블을 *페이로드를 사용한* 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-313">The `Enrollment` entity functions as a many-to-many join table *with payload* in the database.</span></span> <span data-ttu-id="15722-314">"페이로드" 의미 하는 `Enrollment` 조인 된 테이블에 대 한 FKs 외에도 추가 데이터를 포함 하는 테이블 (이 경우는 PK 및 `Grade`).</span><span class="sxs-lookup"><span data-stu-id="15722-314">"With payload" means that the `Enrollment` table contains additional data besides FKs for the joined tables (in this case, the PK and `Grade`).</span></span>

<span data-ttu-id="15722-315">다음 그림은 엔터티 다이어그램에서 이러한 관계 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15722-315">The following illustration shows what these relationships look like in an entity diagram.</span></span> <span data-ttu-id="15722-316">(이 다이어그램 EF에 대 한 EF 파워 도구를 사용 하 여 생성 된 6.x 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-316">(This diagram was generated using EF Power Tools for EF 6.x.</span></span> <span data-ttu-id="15722-317">다이어그램 만들기의 일부가 아닌 자습서입니다.)</span><span class="sxs-lookup"><span data-stu-id="15722-317">Creating the diagram isn't part of the tutorial.)</span></span>

![학생 과정 다 대 다 관계](complex-data-model/_static/student-course.png)

<span data-ttu-id="15722-319">각 관계 한쪽 끝에 별표 (\*)부터 1에서 형식이 다른 경우 일 대 다 관계를 나타내는입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-319">Each relationship line has a 1 at one end and an asterisk (\*) at the other, indicating a one-to-many relationship.</span></span>

<span data-ttu-id="15722-320">경우는 `Enrollment` 테이블 등급 정보를 포함 하지 않은, 두 개의 FKs 포함 시키기만 하면 (`CourseID` 및 `StudentID`).</span><span class="sxs-lookup"><span data-stu-id="15722-320">If the `Enrollment` table didn't include grade information, it would only need to contain the two FKs (`CourseID` and `StudentID`).</span></span> <span data-ttu-id="15722-321">페이로드 없는 다 대 다 조인 테이블에는 순수 조인 테이블 (pjt가) 라고도 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-321">A many-to-many join table without payload is sometimes called a pure join table (PJT).</span></span>

<span data-ttu-id="15722-322">`Instructor` 및 `Course` 엔터티 순수 조인 테이블을 사용 하 여 다 대 다 관계가 설정 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-322">The `Instructor` and `Course` entities have a many-to-many relationship using a pure join table.</span></span>

<span data-ttu-id="15722-323">참고: EF 6.x 지원 다 대 다 관계가 되지만 EF 코어에 대 한 테이블 암시적 조인 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-323">Note: EF 6.x supports implicit join tables for many-to-many relationships, but EF Core doesn't.</span></span> <span data-ttu-id="15722-324">자세한 내용은 참조 [다 대 다 관계 EF 코어 2.0에서](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-324">For more information, see [Many-to-many relationships in EF Core 2.0](https://blog.oneunicorn.com/2017/09/25/many-to-many-relationships-in-ef-core-2-0-part-1-the-basics/).</span></span>

## <a name="the-courseassignment-entity"></a><span data-ttu-id="15722-325">CourseAssignment 엔터티</span><span class="sxs-lookup"><span data-stu-id="15722-325">The CourseAssignment entity</span></span>

![CourseAssignment 엔터티](complex-data-model/_static/courseassignment-entity.png)

<span data-ttu-id="15722-327">만들 *Models/CourseAssignment.cs* 를 다음 코드로:</span><span class="sxs-lookup"><span data-stu-id="15722-327">Create *Models/CourseAssignment.cs* with the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Models/CourseAssignment.cs)]

### <a name="instructor-to-courses"></a><span data-ttu-id="15722-328">강사 교육 과정-</span><span class="sxs-lookup"><span data-stu-id="15722-328">Instructor-to-Courses</span></span>

![강사-Courses m:M](complex-data-model/_static/courseassignment.png)

<span data-ttu-id="15722-330">강사 교육 과정 다 대 다 관계:</span><span class="sxs-lookup"><span data-stu-id="15722-330">The Instructor-to-Courses many-to-many relationship:</span></span>

* <span data-ttu-id="15722-331">엔터티 집합으로 표현 되어야 하는 조인 테이블이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-331">Requires a join table that must be represented by an entity set.</span></span>
* <span data-ttu-id="15722-332">순수 조인 테이블 (페이로드 없는 테이블)입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-332">Is a pure join table (table without payload).</span></span>

<span data-ttu-id="15722-333">일반적으로 조인 엔터티 이름을 `EntityName1EntityName2`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-333">It's common to name a join entity `EntityName1EntityName2`.</span></span> <span data-ttu-id="15722-334">예를 들어이 패턴을 사용 하 여 강사-Courses 조인 테이블은 `CourseInstructor`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-334">For example, the Instructor-to-Courses join table using this pattern is `CourseInstructor`.</span></span> <span data-ttu-id="15722-335">그러나 관계를 설명 하는 이름을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-335">However, we recommend using a name that describes the relationship.</span></span>

<span data-ttu-id="15722-336">데이터 모델은 단순 시작 및 증가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-336">Data models start out simple and grow.</span></span> <span data-ttu-id="15722-337">No 페이로드 조인 (PJTs) 자주 페이로드를 포함 하도록 개선 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-337">No-payload joins (PJTs) frequently evolve to include payload.</span></span> <span data-ttu-id="15722-338">설명이 포함 된 엔터티 이름을 사용 하 여 이름을 조인 테이블에 변경 될 때 변경 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-338">By starting with a descriptive entity name, the name doesn't need to change when the join table changes.</span></span> <span data-ttu-id="15722-339">것이 가장 좋습니다, 조인 엔터티 자체 자연 (가능한 한 단어) 이름을 비즈니스 도메인에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-339">Ideally, the join entity would have its own natural (possibly single word) name in the business domain.</span></span> <span data-ttu-id="15722-340">예를 들어 설명서 및 고객 등급을 호출 하는 조인 엔터티와 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-340">For example, Books and Customers could be linked with a join entity called Ratings.</span></span> <span data-ttu-id="15722-341">강사 교육 과정 다 대 다 관계에 대 한 `CourseAssignment` 보다 선호 `CourseInstructor`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-341">For the Instructor-to-Courses many-to-many relationship, `CourseAssignment` is preferred over `CourseInstructor`.</span></span>

### <a name="composite-key"></a><span data-ttu-id="15722-342">복합 키</span><span class="sxs-lookup"><span data-stu-id="15722-342">Composite key</span></span>

<span data-ttu-id="15722-343">FKs는 null을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-343">FKs are not nullable.</span></span> <span data-ttu-id="15722-344">두 개의 FKs `CourseAssignment` (`InstructorID` 및 `CourseID`) 함께의 각 행을 고유 하 게 식별 된 `CourseAssignment` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-344">The two FKs in `CourseAssignment` (`InstructorID` and `CourseID`) together uniquely identify each row of the `CourseAssignment` table.</span></span> <span data-ttu-id="15722-345">`CourseAssignment`전용된 PK. 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-345">`CourseAssignment` doesn't require a dedicated PK.</span></span> <span data-ttu-id="15722-346">`InstructorID` 및 `CourseID` 복합 PK.로 기능 속성</span><span class="sxs-lookup"><span data-stu-id="15722-346">The `InstructorID` and `CourseID` properties function as a composite PK.</span></span> <span data-ttu-id="15722-347">복합 PKs EF 코어로 지정 하는 유일한 방법은 *fluent API*합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-347">The only way to specify composite PKs to EF Core is with the *fluent API*.</span></span> <span data-ttu-id="15722-348">다음 섹션에서는 복합 PK.를 구성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15722-348">The next section shows how to configure the composite PK.</span></span>

<span data-ttu-id="15722-349">복합 키를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-349">The composite key ensures:</span></span>

* <span data-ttu-id="15722-350">여러 행을 하나의 과정에 대 한 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-350">Multiple rows are allowed for one course.</span></span>
* <span data-ttu-id="15722-351">여러 행은 하나의 강사에 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-351">Multiple rows are allowed for one instructor.</span></span>
* <span data-ttu-id="15722-352">동일한 강사 및 과정에 대 한 여러 행이 허용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-352">Multiple rows for the same instructor and course isn't allowed.</span></span>

<span data-ttu-id="15722-353">`Enrollment` 이러한 종류의 중복이 가능 하므로 조인 엔터티 자체 PK을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-353">The `Enrollment` join entity defines its own PK, so duplicates of this sort are possible.</span></span> <span data-ttu-id="15722-354">방지 하려면 이러한 중복 항목:</span><span class="sxs-lookup"><span data-stu-id="15722-354">To prevent such duplicates:</span></span>

* <span data-ttu-id="15722-355">외래 키 필드에 고유 인덱스를 추가 하거나</span><span class="sxs-lookup"><span data-stu-id="15722-355">Add a unique index on the FK fields, or</span></span>
* <span data-ttu-id="15722-356">구성 `Enrollment` 비슷합니다 복합 기본 키가 있는 `CourseAssignment`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-356">Configure `Enrollment` with a primary composite key similar to `CourseAssignment`.</span></span> <span data-ttu-id="15722-357">자세한 내용은 참조 [인덱스](https://docs.microsoft.com/ef/core/modeling/indexes)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-357">For more information, see [Indexes](https://docs.microsoft.com/ef/core/modeling/indexes).</span></span>

## <a name="update-the-db-context"></a><span data-ttu-id="15722-358">DB 컨텍스트를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-358">Update the DB context</span></span>

<span data-ttu-id="15722-359">다음 강조 표시 된 코드를 추가 *Data/SchoolContext.cs*:</span><span class="sxs-lookup"><span data-stu-id="15722-359">Add the following highlighted code to *Data/SchoolContext.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/SchoolContext.cs?name=snippet_BeforeInheritance&highlight=15-18,25-31)]

<span data-ttu-id="15722-360">새 엔터티를 추가 하 고 구성 하는 위의 코드는 `CourseAssignment` 엔터티의 복합 PK.</span><span class="sxs-lookup"><span data-stu-id="15722-360">The preceding code adds the new entities and configures the `CourseAssignment` entity's composite PK.</span></span>

## <a name="fluent-api-alternative-to-attributes"></a><span data-ttu-id="15722-361">특성에 대 한 fluent API 대안</span><span class="sxs-lookup"><span data-stu-id="15722-361">Fluent API alternative to attributes</span></span>

<span data-ttu-id="15722-362">`OnModelCreating` 코드에서는 앞의 메서드는 *fluent API* EF 핵심 동작을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-362">The `OnModelCreating` method in the preceding code uses the *fluent API* to configure EF Core behavior.</span></span> <span data-ttu-id="15722-363">API는 일련의 단일 문으로 함께 메서드 호출을 가설에서 많이 사용 하기 때문에 "fluent" 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-363">The API is called "fluent" because it's often used by stringing a series of method calls together into a single statement.</span></span> <span data-ttu-id="15722-364">[코드 다음](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) 은 fluent API의 예:</span><span class="sxs-lookup"><span data-stu-id="15722-364">The [following code](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration) is an example of the fluent API:</span></span>

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Blog>()
        .Property(b => b.Url)
        .IsRequired();
}
```

<span data-ttu-id="15722-365">이 자습서에서는 fluent API는 특성으로 수행할 수 없는 DB 매핑을 위해서만 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-365">In this tutorial, the fluent API is used only for DB mapping that can't be done with attributes.</span></span> <span data-ttu-id="15722-366">그러나 fluent API 서식, 유효성 검사 및 매핑 규칙 특성으로 수행할 수 있는 대부분을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-366">However, the fluent API can specify most of the formatting, validation, and mapping rules that can be done with attributes.</span></span>

<span data-ttu-id="15722-367">와 같은 일부 특성 `MinimumLength` fluent API를 통해 적용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-367">Some attributes such as `MinimumLength` can't be applied with the fluent API.</span></span> <span data-ttu-id="15722-368">`MinimumLength`스키마를 변경 하지 않는 최소 길이 유효성 검사 규칙에만 적용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-368">`MinimumLength` doesn't change the schema, it only applies a minimum length validation rule.</span></span>

<span data-ttu-id="15722-369">일부 개발자가 단독으로 보관할 수 있는 엔터티 클래스 "정리 합니다." fluent API를 사용 하는 것을 선호합니다</span><span class="sxs-lookup"><span data-stu-id="15722-369">Some developers prefer to use the fluent API exclusively so that they can keep their entity classes "clean."</span></span> <span data-ttu-id="15722-370">특성 및 fluent API를 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-370">Attributes and the fluent API can be mixed.</span></span> <span data-ttu-id="15722-371">일부 구성만 수행할 수 있는 fluent api (복합 PK 지정) 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-371">There are some configurations that can only be done with the fluent API (specifying a composite PK).</span></span> <span data-ttu-id="15722-372">특성에 수행할 수 있는 몇 가지 구성이 (`MinimumLength`).</span><span class="sxs-lookup"><span data-stu-id="15722-372">There are some configurations that can only be done with attributes (`MinimumLength`).</span></span> <span data-ttu-id="15722-373">Fluent API 또는 특성을 사용 하기 위한 권장된 방식:</span><span class="sxs-lookup"><span data-stu-id="15722-373">The recommended practice for using fluent API or attributes:</span></span>

* <span data-ttu-id="15722-374">이 두 가지 방법 중 하나를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-374">Choose one of these two approaches.</span></span>
* <span data-ttu-id="15722-375">가능한 한 계속 선택한 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-375">Use the chosen approach consistently as much as possible.</span></span>

<span data-ttu-id="15722-376">이 사용 되는 특성 중 일부 자습서에 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-376">Some of the attributes used in the this tutorial are used for:</span></span>

* <span data-ttu-id="15722-377">유효성 검사에만 (예를 들어 `MinimumLength`).</span><span class="sxs-lookup"><span data-stu-id="15722-377">Validation only (for example, `MinimumLength`).</span></span>
* <span data-ttu-id="15722-378">EF 핵심 구성만 (예를 들어 `HasKey`).</span><span class="sxs-lookup"><span data-stu-id="15722-378">EF Core configuration only (for example, `HasKey`).</span></span>
* <span data-ttu-id="15722-379">유효성 검사 및 EF 핵심 구성 (예를 들어 `[StringLength(50)]`).</span><span class="sxs-lookup"><span data-stu-id="15722-379">Validation and EF Core configuration (for example, `[StringLength(50)]`).</span></span>

<span data-ttu-id="15722-380">Fluent API와 비교 하는 특성에 대 한 자세한 내용은 참조 [구성 방법이](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-380">For more information about attributes vs. fluent API, see [Methods of configuration](https://docs.microsoft.com/ef/core/modeling/#methods-of-configuration).</span></span>

## <a name="entity-diagram-showing-relationships"></a><span data-ttu-id="15722-381">관계를 보여 주는 엔터티 다이어그램</span><span class="sxs-lookup"><span data-stu-id="15722-381">Entity Diagram Showing Relationships</span></span>

<span data-ttu-id="15722-382">다음 그림 EF 파워 도구 만드는 완성 School 모델 다이어그램을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="15722-382">The following illustration shows the diagram that EF Power Tools create for the completed School model.</span></span>

![엔터티 다이어그램](complex-data-model/_static/diagram.png)

<span data-ttu-id="15722-384">위 다이어그램을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="15722-384">The preceding diagram shows:</span></span>

* <span data-ttu-id="15722-385">일 대 다 관계의 여러 줄 (1 ~ \*).</span><span class="sxs-lookup"><span data-stu-id="15722-385">Several one-to-many relationship lines (1 to \*).</span></span>
* <span data-ttu-id="15722-386">사이 0 또는 1을 한 관계 선을 (1 0..1)에 `Instructor` 및 `OfficeAssignment` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-386">The one-to-zero-or-one relationship line (1 to 0..1) between the `Instructor` and `OfficeAssignment` entities.</span></span>
* <span data-ttu-id="15722-387">0-또는---일대다 관계 선을 (0..1 대 \*) 사이 `Instructor` 및 `Department` 엔터티.</span><span class="sxs-lookup"><span data-stu-id="15722-387">The zero-or-one-to-many relationship line (0..1 to \*) between the `Instructor` and `Department` entities.</span></span>

## <a name="seed-the-db-with-test-data"></a><span data-ttu-id="15722-388">테스트 데이터로 DB 초기값</span><span class="sxs-lookup"><span data-stu-id="15722-388">Seed the DB with Test Data</span></span>

<span data-ttu-id="15722-389">코드를 업데이트 *Data/DbInitializer.cs*:</span><span class="sxs-lookup"><span data-stu-id="15722-389">Update the code in *Data/DbInitializer.cs*:</span></span>

[!code-csharp[Main](intro/samples/cu/Data/DbInitializer.cs?name=snippet_Final)]

<span data-ttu-id="15722-390">위의 코드는 새 엔터티에 대 한 데이터를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-390">The preceding code provides seed data for the new entities.</span></span> <span data-ttu-id="15722-391">이 코드의 대부분을 새 엔터티 개체를 만들고 예제 데이터를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-391">Most of this code creates new entity objects and loads sample data.</span></span> <span data-ttu-id="15722-392">샘플 데이터는 테스트를 위해 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-392">The sample data is used for testing.</span></span> <span data-ttu-id="15722-393">위의 코드는 다음과 같은 다 대 다 관계를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15722-393">The preceding code creates the following many-to-many relationships:</span></span>

* `Enrollments`
* `CourseAssignment`

<span data-ttu-id="15722-394">참고: [EF 코어 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) 지원할 [데이터 시드는](https://github.com/aspnet/EntityFrameworkCore/issues/629)합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-394">Note: [EF Core 2.1](https://github.com/aspnet/EntityFrameworkCore/wiki/Roadmap) will support [data seeding](https://github.com/aspnet/EntityFrameworkCore/issues/629).</span></span>

## <a name="add-a-migration"></a><span data-ttu-id="15722-395">추가 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="15722-395">Add a migration</span></span>

<span data-ttu-id="15722-396">프로젝트를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-396">Build the project.</span></span> <span data-ttu-id="15722-397">프로젝트 폴더에 명령 창을 열고 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-397">Open a command window in the project folder and enter the following command:</span></span>

```console
dotnet ef migrations add ComplexDataModel
```

<span data-ttu-id="15722-398">위의 명령은 가능한 데이터 손실에 대 한 경고를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-398">The preceding command displays a warning about possible data loss.</span></span>

```text
An operation was scaffolded that may result in the loss of data.
Please review the migration for accuracy.
Done. To undo this action, use 'ef migrations remove'
```

<span data-ttu-id="15722-399">경우는 `database update` 명령이 실행, 다음과 같은 오류가 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-399">If the `database update` command is run, the following error is produced:</span></span>

```text
The ALTER TABLE statement conflicted with the FOREIGN KEY constraint "FK_dbo.Course_dbo.Department_DepartmentID". The conflict occurred in
database "ContosoUniversity", table "dbo.Department", column 'DepartmentID'.
```

<span data-ttu-id="15722-400">마이그레이션이 시작 되 면 기존 데이터와, 기존 데이터와 충족 되지 않은 외래 키 제약 조건이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-400">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="15722-401">이 자습서에서는 새 DB 만들어지면 외래 키 제약 조건을 위반 하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-401">For this tutorial, a new DB is created, so there are no FK constraint violations.</span></span> <span data-ttu-id="15722-402">참조 [레거시 데이터와 foreign key 제약 조건을 수정](#fk) 현재 데이터베이스에서 외래 키 위반을 해결 하는 방법에 대 한 지침은 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-402">See [Fixing foreign key constraints with legacy data](#fk) for instructions on how to fix the FK violations on the current DB.</span></span>

## <a name="change-the-connection-string-and-update-the-db"></a><span data-ttu-id="15722-403">연결 문자열을 변경 하 고 DB 업데이트</span><span class="sxs-lookup"><span data-stu-id="15722-403">Change the connection string and update the DB</span></span>

<span data-ttu-id="15722-404">업데이트 된 코드 `DbInitializer` 새 엔터티에 대 한 데이터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-404">The code in the updated `DbInitializer` adds seed data for the new entities.</span></span> <span data-ttu-id="15722-405">새 빈 DB를 만들려면 EF 코어를 강제로:</span><span class="sxs-lookup"><span data-stu-id="15722-405">To force EF Core to create a new empty DB:</span></span>

* <span data-ttu-id="15722-406">DB 연결 문자열 이름을 변경 *appsettings.json* ContosoUniversity3를 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-406">Change the DB connection string name in *appsettings.json* to ContosoUniversity3.</span></span> <span data-ttu-id="15722-407">새 이름에는 컴퓨터에서 사용 되지 않을 수 있는 이름 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-407">The new name must be a name that hasn't been used on the computer.</span></span>

    ```json
    {
      "ConnectionStrings": {
        "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=ContosoUniversity3;Trusted_Connection=True;MultipleActiveResultSets=true"
      },
    ```

* <span data-ttu-id="15722-408">또는 사용 하 여 DB 삭제:</span><span class="sxs-lookup"><span data-stu-id="15722-408">Alternatively, delete the DB using:</span></span>

    * <span data-ttu-id="15722-409">**SQL Server 개체 탐색기** (SSOX).</span><span class="sxs-lookup"><span data-stu-id="15722-409">**SQL Server Object Explorer** (SSOX).</span></span>
    * <span data-ttu-id="15722-410">`database drop` CLI 명령을:</span><span class="sxs-lookup"><span data-stu-id="15722-410">The `database drop` CLI command:</span></span>

   ```console
   dotnet ef database drop
   ```

<span data-ttu-id="15722-411">실행 `database update` 명령 창에서:</span><span class="sxs-lookup"><span data-stu-id="15722-411">Run `database update` in the command window:</span></span>

```console
dotnet ef database update
```

<span data-ttu-id="15722-412">위의 명령은 모든 마이그레이션 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-412">The preceding command runs all the migrations.</span></span>

<span data-ttu-id="15722-413">앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-413">Run the app.</span></span> <span data-ttu-id="15722-414">실행 응용 프로그램 실행은 `DbInitializer.Initialize` 메서드.</span><span class="sxs-lookup"><span data-stu-id="15722-414">Running the app runs the `DbInitializer.Initialize` method.</span></span> <span data-ttu-id="15722-415">`DbInitializer.Initialize` 새 DB 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="15722-415">The `DbInitializer.Initialize` populates the new DB.</span></span>

<span data-ttu-id="15722-416">SSOX DB를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="15722-416">Open the DB in SSOX:</span></span>

* <span data-ttu-id="15722-417">확장 된 **테이블** 노드.</span><span class="sxs-lookup"><span data-stu-id="15722-417">Expand the **Tables** node.</span></span> <span data-ttu-id="15722-418">생성된 된 테이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="15722-418">The created tables are displayed.</span></span>
* <span data-ttu-id="15722-419">SSOX 이전에 열려 있으면 클릭는 **새로 고침** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-419">If SSOX was opened previously, click the **Refresh** button.</span></span>

![SSOX의 테이블](complex-data-model/_static/ssox-tables.png)

<span data-ttu-id="15722-421">검사는 **CourseAssignment** 테이블:</span><span class="sxs-lookup"><span data-stu-id="15722-421">Examine the **CourseAssignment** table:</span></span>

* <span data-ttu-id="15722-422">마우스 오른쪽 단추로 클릭는 **CourseAssignment** 테이블을 선택한 **데이터 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-422">Right-click the **CourseAssignment** table and select **View Data**.</span></span>
* <span data-ttu-id="15722-423">확인 된 **CourseAssignment** 테이블 데이터가 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-423">Verify the **CourseAssignment** table contains data.</span></span>

![SSOX의 CourseAssignment 데이터](complex-data-model/_static/ssox-ci-data.png)

<a name="fk"></a>

## <a name="fixing-foreign-key-constraints-with-legacy-data"></a><span data-ttu-id="15722-425">레거시 데이터와 foreign key 제약 조건 수정</span><span class="sxs-lookup"><span data-stu-id="15722-425">Fixing foreign key constraints with legacy data</span></span>

<span data-ttu-id="15722-426">이 섹션은 선택 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-426">This section is optional.</span></span>

<span data-ttu-id="15722-427">마이그레이션이 시작 되 면 기존 데이터와, 기존 데이터와 충족 되지 않은 외래 키 제약 조건이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-427">When migrations are run with existing data, there may be FK constraints that are not satisfied with the exiting data.</span></span> <span data-ttu-id="15722-428">프로덕션 데이터와 함께 기존 데이터를 마이그레이션하기에 단계를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-428">With production data, steps must be taken to migrate the existing data.</span></span> <span data-ttu-id="15722-429">이 섹션에서는 외래 키 제약 조건 위반을 해결 하는 예제를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-429">This section provides an example of fixing FK constraint violations.</span></span> <span data-ttu-id="15722-430">이러한 코드 변경 내용 백업 없이 만들지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-430">Don't make these code changes without a backup.</span></span> <span data-ttu-id="15722-431">항목도 변경 하지 않습니다 이러한 코드는 이전 단원을 완료 하 고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-431">Don't make these code changes if you completed the previous section and updated the database.</span></span>

<span data-ttu-id="15722-432">*{timestamp}_ComplexDataModel.cs* 파일 다음 코드를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-432">The *{timestamp}_ComplexDataModel.cs* file contains the following code:</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_DepartmentID)]

<span data-ttu-id="15722-433">위의 코드는 nullable이 아닌 추가 `DepartmentID` 외래 키에는 `Course` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-433">The preceding code adds a non-nullable `DepartmentID` FK to the `Course` table.</span></span> <span data-ttu-id="15722-434">행을 포함 하는 이전 자습서에서 DB `Course`, 마이그레이션 하 여 해당 테이블을 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="15722-434">The DB from the previous tutorial contains rows in `Course`, so that table cannot be updated by migrations.</span></span>

<span data-ttu-id="15722-435">확인 하 고 `ComplexDataModel` 기존 데이터와 마이그레이션 작업:</span><span class="sxs-lookup"><span data-stu-id="15722-435">To make the `ComplexDataModel` migration work with existing data:</span></span>

* <span data-ttu-id="15722-436">새 열을 지정 하는 코드를 변경 (`DepartmentID`) 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-436">Change the code to give the new column (`DepartmentID`) a default value.</span></span>
* <span data-ttu-id="15722-437">기본 부서 프록시로 "Temp" 라는 가짜 부서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="15722-437">Create a fake department named "Temp" to act as the default department.</span></span>

### <a name="fix-the-foreign-key-constraints"></a><span data-ttu-id="15722-438">Foreign key 제약 조건 수정</span><span class="sxs-lookup"><span data-stu-id="15722-438">Fix the foreign key constraints</span></span>

<span data-ttu-id="15722-439">업데이트는 `ComplexDataModel` 클래스 `Up` 메서드:</span><span class="sxs-lookup"><span data-stu-id="15722-439">Update the `ComplexDataModel` classes `Up` method:</span></span>

* <span data-ttu-id="15722-440">열기는 *{timestamp}_ComplexDataModel.cs* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-440">Open the *{timestamp}_ComplexDataModel.cs* file.</span></span>
* <span data-ttu-id="15722-441">주석 줄을 추가 하는 코드는 `DepartmentID` 열을는 `Course` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="15722-441">Comment out the line of code that adds the `DepartmentID` column to the `Course` table.</span></span>

[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CommentOut&highlight=9-13)]

<span data-ttu-id="15722-442">다음 강조 표시 된 코드를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-442">Add the following highlighted code.</span></span> <span data-ttu-id="15722-443">새 코드 후로 이동 된 `.CreateTable( name: "Department"` 블록:[!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span><span class="sxs-lookup"><span data-stu-id="15722-443">The new code goes after the `.CreateTable( name: "Department"` block: [!code-csharp[Main](intro/samples/cu/Migrations/20171027005808_ComplexDataModel.cs?name=snippet_CreateDefaultValue&highlight=22-32)]</span></span>

<span data-ttu-id="15722-444">이전 변경 내용이 기존와 `Course` 행 후 "Temp" 부서에 관련 되도록는 `ComplexDataModel` `Up` 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-444">With the preceding changes, existing `Course` rows will be related to the "Temp" department after the `ComplexDataModel` `Up` method runs.</span></span>

<span data-ttu-id="15722-445">프로덕션 응용 프로그램은:</span><span class="sxs-lookup"><span data-stu-id="15722-445">A production app would:</span></span>

* <span data-ttu-id="15722-446">코드 또는 추가 하는 스크립트가 포함 `Department` 행 및 관련 `Course` 행을 새 `Department` 행.</span><span class="sxs-lookup"><span data-stu-id="15722-446">Include code or scripts to add `Department` rows and related `Course` rows to the new `Department` rows.</span></span>
* <span data-ttu-id="15722-447">"Temp" 부서 또는 대 한 기본값을 사용 하지 `Course.DepartmentID`합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-447">Not use the "Temp" department or the default value for `Course.DepartmentID`.</span></span>

<span data-ttu-id="15722-448">다음 자습서에서는 관련된 데이터에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="15722-448">The next tutorial covers related data.</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="15722-449">[이전](xref:data/ef-rp/migrations)
[다음](xref:data/ef-rp/read-related-data)</span><span class="sxs-lookup"><span data-stu-id="15722-449">[Previous](xref:data/ef-rp/migrations)
[Next](xref:data/ef-rp/read-related-data)</span></span>
