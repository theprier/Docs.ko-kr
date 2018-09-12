---
title: 권한 부여로 보호 되는 사용자 데이터를 사용 하 여 ASP.NET Core 앱 만들기
author: rick-anderson
description: 권한 부여로 보호 되는 사용자 데이터를 사용 하 여 Razor 페이지 앱을 만드는 방법에 알아봅니다. HTTPS, 인증, 보안, ASP.NET Core Id를 포함합니다.
ms.author: riande
ms.date: 7/24/2018
uid: security/authorization/secure-data
ms.openlocfilehash: a263b092194763ae4ff3360fc0d76e8ee494b5a6
ms.sourcegitcommit: e7e1e531b80b3f4117ff119caadbebf4dcf5dcb7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2018
ms.locfileid: "44510365"
---
::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="95443-104">참조 [이 PDF](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core MVC 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-104">See [this PDF](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core MVC version.</span></span> <span data-ttu-id="95443-105">이 자습서에서는 ASP.NET Core 1.1 버전은 [이](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-105">The ASP.NET Core 1.1 version of this tutorial is in [this](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) folder.</span></span> <span data-ttu-id="95443-106">ASP.NET Core 샘플에는 1.1 합니다 [샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-106">The 1.1 ASP.NET Core sample is in the [samples](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).</span></span>
::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="95443-107">참조 [이 pdf](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_July16_18.pdf)</span><span class="sxs-lookup"><span data-stu-id="95443-107">See [this pdf](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_July16_18.pdf)</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a><span data-ttu-id="95443-108">권한 부여로 보호 되는 사용자 데이터를 사용 하 여 ASP.NET Core 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-108">Create an ASP.NET Core app with user data protected by authorization</span></span>

<span data-ttu-id="95443-109">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="95443-109">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="95443-110">이 자습서에는 권한 부여로 보호 되는 사용자 데이터를 사용 하 여 ASP.NET Core 웹 앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95443-110">This tutorial shows how to create an ASP.NET Core web app with user data protected by authorization.</span></span> <span data-ttu-id="95443-111">인증 된 (등록 된) 사용자는 연락처 목록에 표시를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-111">It displays a list of contacts that authenticated (registered) users have created.</span></span> <span data-ttu-id="95443-112">세 가지 보안 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-112">There are three security groups:</span></span>

* <span data-ttu-id="95443-113">**등록 된 사용자** 편집/삭제할 수 있습니다 자신의 데이터 및 승인 된 모든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-113">**Registered users** can view all the approved data and can edit/delete their own data.</span></span>
* <span data-ttu-id="95443-114">**관리자** 승인 하거나 연락처 데이터를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-114">**Managers** can approve or reject contact data.</span></span> <span data-ttu-id="95443-115">승인 된 연락처만 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-115">Only approved contacts are visible to users.</span></span>
* <span data-ttu-id="95443-116">**관리자** 승인/거부를 편집/삭제할 모든 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-116">**Administrators** can approve/reject and edit/delete any data.</span></span>

<span data-ttu-id="95443-117">다음 이미지에서는 Rick 사용자 (`rick@example.com`)에 로그인 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-117">In the following image, user Rick (`rick@example.com`) is signed in.</span></span> <span data-ttu-id="95443-118">Rick 승인 된 연락처를 보기만 할 수 있습니다 하 고 **편집할**/**삭제**/**새로 만들기** 자신의 연락처에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-118">Rick can only view approved contacts and **Edit**/**Delete**/**Create New** links for his contacts.</span></span> <span data-ttu-id="95443-119">Rick을 표시 하 여 만든 마지막 레코드만 **편집** 하 고 **삭제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-119">Only the last record, created by Rick, displays **Edit** and **Delete** links.</span></span> <span data-ttu-id="95443-120">다른 사용자에 게는 관리자가 "승인 됨" 상태 변경 될 때까지 마지막 레코드를 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-120">Other users won't see the last record until a manager or administrator changes the status to "Approved".</span></span>

![이전 이미지 설명](secure-data/_static/rick.png)

<span data-ttu-id="95443-122">다음 이미지에서는 `manager@contoso.com` managers 역할에 서명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-122">In the following image, `manager@contoso.com` is signed in and in the managers role:</span></span>

![이전 이미지 설명](secure-data/_static/manager1.png)

<span data-ttu-id="95443-124">다음 이미지는 관리자의 연락처 세부 정보 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="95443-124">The following image shows the managers details view of a contact:</span></span>

![이전 이미지 설명](secure-data/_static/manager.png)

<span data-ttu-id="95443-126">합니다 **승인** 하 고 **거부** 단추가 관리자와 관리자만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-126">The **Approve** and **Reject** buttons are only displayed for managers and administrators.</span></span>

<span data-ttu-id="95443-127">다음 이미지에서는 `admin@contoso.com` 로그인 하 여 관리자 역할에:</span><span class="sxs-lookup"><span data-stu-id="95443-127">In the following image, `admin@contoso.com` is signed in and in the administrators role:</span></span>

![이전 이미지 설명](secure-data/_static/admin.png)

<span data-ttu-id="95443-129">관리자는 모든 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-129">The administrator has all privileges.</span></span> <span data-ttu-id="95443-130">그녀는 연락처 읽기/편집/삭제할 수 및 연락처의 상태를 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-130">She can read/edit/delete any contact and change the status of contacts.</span></span>

<span data-ttu-id="95443-131">앱에서 만든 [스 캐 폴딩](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) 다음 `Contact` 모델:</span><span class="sxs-lookup"><span data-stu-id="95443-131">The app was created by [scaffolding](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) the following `Contact` model:</span></span>

[!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet)]

<span data-ttu-id="95443-132">다음 인증 처리기를 포함 하는 샘플:</span><span class="sxs-lookup"><span data-stu-id="95443-132">The sample contains the following authorization handlers:</span></span>

* <span data-ttu-id="95443-133">`ContactIsOwnerAuthorizationHandler`: 사용자 데이터 편집할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-133">`ContactIsOwnerAuthorizationHandler`: Ensures that a user can only edit their data.</span></span>
* <span data-ttu-id="95443-134">`ContactManagerAuthorizationHandler`: 관리자 승인 또는 거부 연락처를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-134">`ContactManagerAuthorizationHandler`: Allows managers to approve or reject contacts.</span></span>
* <span data-ttu-id="95443-135">`ContactAdministratorsAuthorizationHandler`: 관리자를 승인 하거나 거부할 연락처 및 연락처 편집/삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-135">`ContactAdministratorsAuthorizationHandler`: Allows administrators to approve or reject contacts and to edit/delete contacts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95443-136">전제 조건</span><span class="sxs-lookup"><span data-stu-id="95443-136">Prerequisites</span></span>

<span data-ttu-id="95443-137">이 자습서 고급 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-137">This tutorial is advanced.</span></span> <span data-ttu-id="95443-138">에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-138">You should be familiar with:</span></span>

* [<span data-ttu-id="95443-139">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="95443-139">ASP.NET Core</span></span>](xref:tutorials/first-mvc-app/start-mvc)
* [<span data-ttu-id="95443-140">인증</span><span class="sxs-lookup"><span data-stu-id="95443-140">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="95443-141">계정 확인 및 비밀번호 복구</span><span class="sxs-lookup"><span data-stu-id="95443-141">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="95443-142">권한 부여</span><span class="sxs-lookup"><span data-stu-id="95443-142">Authorization</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="95443-143">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="95443-143">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

::: moniker-end
::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="95443-144">ASP.NET Core 2.1에서 `User.IsInRole` 사용 하는 경우 실패 `AddDefaultIdentity`합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-144">In ASP.NET Core 2.1, `User.IsInRole` fails when using `AddDefaultIdentity`.</span></span> <span data-ttu-id="95443-145">이 자습서에서는 `AddDefaultIdentity` ASP.NET Core 2.2 미리 보기 1 이상이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-145">This tutorial uses `AddDefaultIdentity` and therefore requires ASP.NET Core 2.2 preview 1 or later.</span></span> <span data-ttu-id="95443-146">참조 [이 GitHub 문제](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909) 해결에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-146">See [this GitHub issue](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909) for a work-around.</span></span>

::: moniker-end
::: moniker range=">= aspnetcore-2.1"

## <a name="the-starter-and-completed-app"></a><span data-ttu-id="95443-147">시작 및 완료 된 앱</span><span class="sxs-lookup"><span data-stu-id="95443-147">The starter and completed app</span></span>

<span data-ttu-id="95443-148">[다운로드](xref:tutorials/index#how-to-download-a-sample) 는 [완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) 앱.</span><span class="sxs-lookup"><span data-stu-id="95443-148">[Download](xref:tutorials/index#how-to-download-a-sample) the [completed](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) app.</span></span> <span data-ttu-id="95443-149">[테스트](#test-the-completed-app) 완성된 된 앱의 보안 기능에 익숙해질 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-149">[Test](#test-the-completed-app) the completed app so you become familiar with its security features.</span></span>

### <a name="the-starter-app"></a><span data-ttu-id="95443-150">시작 앱</span><span class="sxs-lookup"><span data-stu-id="95443-150">The starter app</span></span>

<span data-ttu-id="95443-151">[다운로드](xref:tutorials/index#how-to-download-a-sample) 는 [스타터](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) 앱.</span><span class="sxs-lookup"><span data-stu-id="95443-151">[Download](xref:tutorials/index#how-to-download-a-sample) the [starter](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) app.</span></span>

<span data-ttu-id="95443-152">앱 실행을 탭 합니다 **ContactManager** 에 연결 하 고 만들기, 편집 및 연락처를 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-152">Run the app, tap the **ContactManager** link, and verify you can create, edit, and delete a contact.</span></span>

## <a name="secure-user-data"></a><span data-ttu-id="95443-153">사용자 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="95443-153">Secure user data</span></span>

<span data-ttu-id="95443-154">다음 섹션에서는 모든 주요 단계가 보안 사용자 데이터 앱 만들기 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-154">The following sections have all the major steps to create the secure user data app.</span></span> <span data-ttu-id="95443-155">완료 된 프로젝트 참조 하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-155">You may find it helpful to refer to the completed project.</span></span>

### <a name="tie-the-contact-data-to-the-user"></a><span data-ttu-id="95443-156">사용자에 게 연락 데이터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-156">Tie the contact data to the user</span></span>

<span data-ttu-id="95443-157">ASP.NET을 사용 하 여 [Identity](xref:security/authentication/identity) 데이터에 있지만 다른 사용자 데이터가 아닌 사용자 ID 사용자를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-157">Use the ASP.NET [Identity](xref:security/authentication/identity) user ID to ensure users can edit their data, but not other users data.</span></span> <span data-ttu-id="95443-158">추가 `OwnerID` 하 고 `ContactStatus` 에 `Contact` 모델:</span><span class="sxs-lookup"><span data-stu-id="95443-158">Add `OwnerID` and `ContactStatus` to the `Contact` model:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

<span data-ttu-id="95443-159">`OwnerID` 사용자의 id를 `AspNetUser` 테이블에 [Identity](xref:security/authentication/identity) 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-159">`OwnerID` is the user's ID from the `AspNetUser` table in the [Identity](xref:security/authentication/identity) database.</span></span> <span data-ttu-id="95443-160">`Status` 필드 연락처를 일반 사용자가 볼 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-160">The `Status` field determines if a contact is viewable by general users.</span></span>

<span data-ttu-id="95443-161">새 마이그레이션을 만들고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-161">Create a new migration and update the database:</span></span>

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="add-role-services-to-identity"></a><span data-ttu-id="95443-162">Id에 역할 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="95443-162">Add Role services to Identity</span></span>

<span data-ttu-id="95443-163">추가 [역할](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) 역할 서비스를 추가 하려면:</span><span class="sxs-lookup"><span data-stu-id="95443-163">Append [AddRoles](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) to add Role services:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet2&highlight=12)]

### <a name="require-authenticated-users"></a><span data-ttu-id="95443-164">인증 된 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-164">Require authenticated users</span></span>

<span data-ttu-id="95443-165">사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-165">Set the default authentication policy to require users to be authenticated:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet&highlight=17-99)] 

 <span data-ttu-id="95443-166">사용 하 여 Razor 페이지, 컨트롤러 또는 작업 메서드 수준에서 인증을 옵트아웃할 수 있습니다는 `[AllowAnonymous]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-166">You can opt out of authentication at the Razor Page, controller, or action method level with the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="95443-167">새로 추가 된 Razor 페이지 및 컨트롤러를 보호 사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-167">Setting the default authentication policy to require users to be authenticated protects newly added Razor Pages and controllers.</span></span> <span data-ttu-id="95443-168">기본적으로 필요한 인증은 새 컨트롤러 및 포함할 Razor 페이지에 의존 하는 것 보다 안전 하지는 `[Authorize]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-168">Having authentication required by default is more secure than relying on new controllers and Razor Pages to include the `[Authorize]` attribute.</span></span>

<span data-ttu-id="95443-169">추가 [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) 인덱스에, 정보 및 연락처 페이지 익명 사용자가 등록 하기 전에 사이트에 대 한 정보를 얻을 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-169">Add [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) to the Index, About, and Contact pages so anonymous users can get information about the site before they register.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Index.cshtml.cs?highlight=1,6)]

### <a name="configure-the-test-account"></a><span data-ttu-id="95443-170">테스트 계정 구성</span><span class="sxs-lookup"><span data-stu-id="95443-170">Configure the test account</span></span>

<span data-ttu-id="95443-171">`SeedData` 클래스에는 두 개의 계정을 만듭니다: 관리자 및 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-171">The `SeedData` class creates two accounts: administrator and manager.</span></span> <span data-ttu-id="95443-172">사용 된 [암호 관리자 도구](xref:security/app-secrets) 이러한 계정에 대 한 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-172">Use the [Secret Manager tool](xref:security/app-secrets) to set a password for these accounts.</span></span> <span data-ttu-id="95443-173">프로젝트 디렉터리에서 암호를 설정 (포함 하는 디렉터리 *Program.cs*):</span><span class="sxs-lookup"><span data-stu-id="95443-173">Set the password from the project directory (the directory containing *Program.cs*):</span></span>

```console
dotnet user-secrets set SeedUserPW <PW>
```

<span data-ttu-id="95443-174">강력한 암호를 지정 하지 않으면 예외가 발생 될 때 `SeedData.Initialize` 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-174">If a strong password is not specified, an exception is thrown when `SeedData.Initialize` is called.</span></span>

<span data-ttu-id="95443-175">업데이트 `Main` 테스트 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-175">Update `Main` to use the test password:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a><span data-ttu-id="95443-176">테스트 계정을 만들고 연락처를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-176">Create the test accounts and update the contacts</span></span>

<span data-ttu-id="95443-177">업데이트를 `Initialize` 의 메서드는 `SeedData` 클래스 테스트 계정을 만들려면:</span><span class="sxs-lookup"><span data-stu-id="95443-177">Update the `Initialize` method in the `SeedData` class to create the test accounts:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet_Initialize)]

<span data-ttu-id="95443-178">관리자 사용자 ID를 추가 하 고 `ContactStatus` 연락처를 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-178">Add the administrator user ID and `ContactStatus` to the contacts.</span></span> <span data-ttu-id="95443-179">"제출" 및 "Rejected" 하나의 연락처 중 하나를 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-179">Make one of the contacts "Submitted" and one "Rejected".</span></span> <span data-ttu-id="95443-180">사용자 ID 및 상태를 모든 연락처를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-180">Add the user ID and status to all the contacts.</span></span> <span data-ttu-id="95443-181">하나만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-181">Only one contact is shown:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a><span data-ttu-id="95443-182">소유자, 관리자 및 관리자 권한 부여 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-182">Create owner, manager, and administrator authorization handlers</span></span>

<span data-ttu-id="95443-183">만들기는 `ContactIsOwnerAuthorizationHandler` 클래스를 *권한 부여* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-183">Create a `ContactIsOwnerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="95443-184">`ContactIsOwnerAuthorizationHandler` 리소스에 역할을 하는 사용자 리소스를 소유 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-184">The `ContactIsOwnerAuthorizationHandler` verifies that the user acting on a resource owns the resource.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

<span data-ttu-id="95443-185">합니다 `ContactIsOwnerAuthorizationHandler` 호출 [컨텍스트. 성공](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) 현재 인증 된 사용자가 연락처 소유자입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-185">The `ContactIsOwnerAuthorizationHandler` calls [context.Succeed](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) if the current authenticated user is the contact owner.</span></span> <span data-ttu-id="95443-186">권한 부여 처리기 일반적으로:</span><span class="sxs-lookup"><span data-stu-id="95443-186">Authorization handlers generally:</span></span>

* <span data-ttu-id="95443-187">반환 `context.Succeed` 요구 사항이 충족 되는 경우.</span><span class="sxs-lookup"><span data-stu-id="95443-187">Return `context.Succeed` when the requirements are met.</span></span>
* <span data-ttu-id="95443-188">반환 `Task.CompletedTask` 요구 사항이 충족 되지 않는 경우.</span><span class="sxs-lookup"><span data-stu-id="95443-188">Return `Task.CompletedTask` when requirements aren't met.</span></span> <span data-ttu-id="95443-189">`Task.CompletedTask` 성공 또는 실패를 모두&mdash;다른 권한 부여 처리기 실행을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-189">`Task.CompletedTask` is neither success or failure&mdash;it allows other authorization handlers to run.</span></span>

<span data-ttu-id="95443-190">명시적으로 실패 하는 경우 반환 [컨텍스트. 실패](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail)합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-190">If you need to explicitly fail, return [context.Fail](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).</span></span>

<span data-ttu-id="95443-191">앱 편집/삭제/만들려면 연락처 소유자가 자신의 데이터를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-191">The app allows contact owners to edit/delete/create their own data.</span></span> <span data-ttu-id="95443-192">`ContactIsOwnerAuthorizationHandler` 요구 사항 매개 변수에 전달 된 작업을 확인 하려면 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-192">`ContactIsOwnerAuthorizationHandler` doesn't need to check the operation passed in the requirement parameter.</span></span>

### <a name="create-a-manager-authorization-handler"></a><span data-ttu-id="95443-193">관리자 권한 부여 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-193">Create a manager authorization handler</span></span>

<span data-ttu-id="95443-194">만들기는 `ContactManagerAuthorizationHandler` 클래스를 *권한 부여* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-194">Create a `ContactManagerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="95443-195">`ContactManagerAuthorizationHandler` 리소스에 대해 작동 하는 사용자가 관리자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-195">The `ContactManagerAuthorizationHandler` verifies the user acting on the resource is a manager.</span></span> <span data-ttu-id="95443-196">관리자만 승인 하거나 (새롭거나 변경 된) 콘텐츠 변경 내용을 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-196">Only managers can approve or reject content changes (new or changed).</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a><span data-ttu-id="95443-197">관리자 권한 부여 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-197">Create an administrator authorization handler</span></span>

<span data-ttu-id="95443-198">만들기는 `ContactAdministratorsAuthorizationHandler` 클래스를 *권한 부여* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-198">Create a `ContactAdministratorsAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="95443-199">`ContactAdministratorsAuthorizationHandler` 리소스에 대해 작동 하는 사용자가 관리자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-199">The `ContactAdministratorsAuthorizationHandler` verifies the user acting on the resource is an administrator.</span></span> <span data-ttu-id="95443-200">관리자는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-200">Administrator can do all operations.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a><span data-ttu-id="95443-201">인증 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-201">Register the authorization handlers</span></span>

<span data-ttu-id="95443-202">Entity Framework Core를 사용 하 여 서비스에 등록 해야 합니다 [종속성 주입](xref:fundamentals/dependency-injection) 사용 하 여 [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions)합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-202">Services using Entity Framework Core must be registered for [dependency injection](xref:fundamentals/dependency-injection) using [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions).</span></span> <span data-ttu-id="95443-203">합니다 `ContactIsOwnerAuthorizationHandler` ASP.NET Core를 사용 하 여 [Identity](xref:security/authentication/identity), Entity Framework Core에서 빌드되는 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-203">The `ContactIsOwnerAuthorizationHandler` uses ASP.NET Core [Identity](xref:security/authentication/identity), which is built on Entity Framework Core.</span></span> <span data-ttu-id="95443-204">사용할 수 있도록 서비스 컬렉션을 사용 하 여 처리기를 등록 합니다 `ContactsController` 를 통해 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-204">Register the handlers with the service collection so they're available to the `ContactsController` through [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="95443-205">끝에 다음 코드를 추가 `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="95443-205">Add the following code to the end of `ConfigureServices`:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet_defaultPolicy&highlight=27-99)]

<span data-ttu-id="95443-206">`ContactAdministratorsAuthorizationHandler` 및 `ContactManagerAuthorizationHandler` 단일 항목으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-206">`ContactAdministratorsAuthorizationHandler` and `ContactManagerAuthorizationHandler` are added as singletons.</span></span> <span data-ttu-id="95443-207">EF를 사용 하지 않는 서 필요한 모든 정보는 단일 항목 들은 합니다 `Context` 의 매개 변수는 `HandleRequirementAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="95443-207">They're singletons because they don't use EF and all the information needed is in the `Context` parameter of the `HandleRequirementAsync` method.</span></span>

## <a name="support-authorization"></a><span data-ttu-id="95443-208">권한 부여를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-208">Support authorization</span></span>

<span data-ttu-id="95443-209">이 섹션에서는 Razor 페이지를 업데이트 하 고 작업 요구 사항 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-209">In this section, you update the Razor Pages and add an operations requirements class.</span></span>

### <a name="review-the-contact-operations-requirements-class"></a><span data-ttu-id="95443-210">연락처 작업 요구 사항 클래스를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-210">Review the contact operations requirements class</span></span>

<span data-ttu-id="95443-211">검토를 `ContactOperations` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-211">Review the `ContactOperations` class.</span></span> <span data-ttu-id="95443-212">이 클래스는 포함 요구 사항을 지 원하는:</span><span class="sxs-lookup"><span data-stu-id="95443-212">This class contains the requirements the app supports:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-contacts-razor-pages"></a><span data-ttu-id="95443-213">연락처 Razor 페이지에 대 한 기본 클래스 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-213">Create a base class for the Contacts Razor Pages</span></span>

<span data-ttu-id="95443-214">연락처 Razor 페이지에에서 사용 된 서비스를 포함 하는 기본 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95443-214">Create a base class that contains the services used in the contacts Razor Pages.</span></span> <span data-ttu-id="95443-215">초기화 코드를 한 위치에 배치 하는 기본 클래스:</span><span class="sxs-lookup"><span data-stu-id="95443-215">The base class puts the initialization code in one location:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/DI_BasePageModel.cs)]

<span data-ttu-id="95443-216">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="95443-216">The preceding code:</span></span>

* <span data-ttu-id="95443-217">추가 된 `IAuthorizationService` 권한 부여 처리기에 액세스 하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-217">Adds the `IAuthorizationService` service to access to the authorization handlers.</span></span>
* <span data-ttu-id="95443-218">Id 추가 `UserManager` 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-218">Adds the Identity `UserManager` service.</span></span>
* <span data-ttu-id="95443-219">`ApplicationDbContext`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-219">Add the `ApplicationDbContext`.</span></span>

### <a name="update-the-createmodel"></a><span data-ttu-id="95443-220">업데이트 된 CreateModel</span><span class="sxs-lookup"><span data-stu-id="95443-220">Update the CreateModel</span></span>

<span data-ttu-id="95443-221">만들기 페이지 모델 생성자를 사용 하 여 업데이트를 `DI_BasePageModel` 기본 클래스:</span><span class="sxs-lookup"><span data-stu-id="95443-221">Update the create page model constructor to use the `DI_BasePageModel` base class:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

<span data-ttu-id="95443-222">업데이트 된 `CreateModel.OnPostAsync` 방법:</span><span class="sxs-lookup"><span data-stu-id="95443-222">Update the `CreateModel.OnPostAsync` method to:</span></span>

* <span data-ttu-id="95443-223">사용자 ID를 추가 합니다 `Contact` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-223">Add the user ID to the `Contact` model.</span></span>
* <span data-ttu-id="95443-224">사용자에 게 연락처를 만들 수 있는 권한을 확인 하는 권한 부여 처리기를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-224">Call the authorization handler to verify the user has permission to create contacts.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a><span data-ttu-id="95443-225">업데이트 된 IndexModel</span><span class="sxs-lookup"><span data-stu-id="95443-225">Update the IndexModel</span></span>

<span data-ttu-id="95443-226">업데이트 된 `OnGetAsync` 메서드 승인 된 연락처만 일반 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-226">Update the `OnGetAsync` method so only approved contacts are shown to general users:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a><span data-ttu-id="95443-227">업데이트 된 EditModel</span><span class="sxs-lookup"><span data-stu-id="95443-227">Update the EditModel</span></span>

<span data-ttu-id="95443-228">사용자가 연락처를 소유를 확인 하는 권한 부여 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-228">Add an authorization handler to verify the user owns the contact.</span></span> <span data-ttu-id="95443-229">리소스 권한 부여가 유효성을 검사 하기 때문에 `[Authorize]` 특성 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-229">Because resource authorization is being validated, the `[Authorize]` attribute is not enough.</span></span> <span data-ttu-id="95443-230">특성을 평가 하는 경우 앱 리소스에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-230">The app doesn't have access to the resource when attributes are evaluated.</span></span> <span data-ttu-id="95443-231">명령적 리소스 기반 권한 부여를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-231">Resource-based authorization must be imperative.</span></span> <span data-ttu-id="95443-232">페이지 모델에 로드 하 여 또는 자체 처리기 내에서 로드 하 여 앱에 리소스에 대 한 액세스 검사를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-232">Checks must be performed once the app has access to the resource, either by loading it in the page model or by loading it within the handler itself.</span></span> <span data-ttu-id="95443-233">자주 리소스 키를 전달 하 여 리소스에 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-233">You frequently access the resource by passing in the resource key.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a><span data-ttu-id="95443-234">업데이트 된 DeleteModel</span><span class="sxs-lookup"><span data-stu-id="95443-234">Update the DeleteModel</span></span>

<span data-ttu-id="95443-235">인증 처리기를 사용 하 여 사용자 연락처에 대 한 삭제 권한을 확인 하려면 삭제 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-235">Update the delete page model to use the authorization handler to verify the user has delete permission on the contact.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a><span data-ttu-id="95443-236">권한 부여 서비스 보기 삽입</span><span class="sxs-lookup"><span data-stu-id="95443-236">Inject the authorization service into the views</span></span>

<span data-ttu-id="95443-237">현재 UI은 편집 및 사용자가 수정할 수 없습니다. 연락처에 대 한 링크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-237">Currently, the UI shows edit and delete links for contacts the user can't modify.</span></span>

<span data-ttu-id="95443-238">권한 부여 서비스를 주입 합니다 *views/_viewimports.cshtml* 모든 보기에 사용할 수 있도록 파일:</span><span class="sxs-lookup"><span data-stu-id="95443-238">Inject the authorization service in the *Views/_ViewImports.cshtml* file so it's available to all views:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/_ViewImports.cshtml?highlight=6-99)]

<span data-ttu-id="95443-239">위의 태그는 몇 개 추가 `using` 문입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-239">The preceding markup adds several `using` statements.</span></span>

<span data-ttu-id="95443-240">업데이트를 **편집** 및 **삭제** 에 연결 *Pages/Contacts/Index.cshtml* 하므로 적절 한 권한 가진 사용자만 렌더링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-240">Update the **Edit** and **Delete** links in *Pages/Contacts/Index.cshtml* so they're only rendered for users with the appropriate permissions:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml?highlight=34-36,62-999)]

> [!WARNING]
> <span data-ttu-id="95443-241">데이터를 변경할 수 있는 권한이 없는 사용자에 게 링크를 숨기기는 앱을 보호 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-241">Hiding links from users that don't have permission to change data doesn't secure the app.</span></span> <span data-ttu-id="95443-242">링크 숨기기는 올바른 링크를 표시 하 여 앱 보다 친숙 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-242">Hiding links makes the app more user-friendly by displaying only valid links.</span></span> <span data-ttu-id="95443-243">사용자가 편집을 호출 하 고 자신이 소유 하지 않는 데이터에 대 한 작업을 삭제 하도록 생성 된 Url hack 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-243">Users can hack the generated URLs to invoke edit and delete operations on data they don't own.</span></span> <span data-ttu-id="95443-244">Razor 페이지 또는 컨트롤러에 데이터를 보호 하는 액세스 검사를 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-244">The Razor Page or controller must enforce access checks to secure the data.</span></span>

### <a name="update-details"></a><span data-ttu-id="95443-245">세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="95443-245">Update Details</span></span>

<span data-ttu-id="95443-246">관리자 승인 또는 연락처를 거부할 수 있도록 세부 정보 보기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-246">Update the details view so managers can approve or reject contacts:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml?name=snippet)]

<span data-ttu-id="95443-247">업데이트 세부 정보 페이지 모델:</span><span class="sxs-lookup"><span data-stu-id="95443-247">Update the details page model:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="add-a-user-to-a-role"></a><span data-ttu-id="95443-248">역할에 사용자 추가</span><span class="sxs-lookup"><span data-stu-id="95443-248">Add a user to a role</span></span>

<span data-ttu-id="95443-249">역할 Id 쿠키에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95443-249">Roles are stored in the Identity cookie.</span></span> <span data-ttu-id="95443-250">쿠키를 다시 생성 될 때까지 역할 쿠키에 유지 되지 않습니다 사용자 또는 사용자로 변경 아웃 하 고 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-250">Changes made to user roles are not persisted to the cookie until the cookie is regenerated or the user signs out and signs in.</span></span> <span data-ttu-id="95443-251">사용자 역할에 추가 응용 프로그램을 호출 해야 `SignInManager.RefreshSignInAsync(user)` 쿠키를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-251">Applications that add users to a role should call `SignInManager.RefreshSignInAsync(user)` to update the cookie.</span></span>

## <a name="test-the-completed-app"></a><span data-ttu-id="95443-252">완성된 된 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="95443-252">Test the completed app</span></span>

<span data-ttu-id="95443-253">앱에 있는 경우 연락처:</span><span class="sxs-lookup"><span data-stu-id="95443-253">If the app has contacts:</span></span>

* <span data-ttu-id="95443-254">모든 레코드를 삭제 합니다 `Contact` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-254">Delete all the records in the `Contact` table.</span></span>
* <span data-ttu-id="95443-255">데이터베이스를 시드하려면 앱을 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-255">Restart the app to seed the database.</span></span>

<span data-ttu-id="95443-256">연락처를 검색 하는 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-256">Register a user for browsing the contacts.</span></span>

<span data-ttu-id="95443-257">완성된 된 앱을 테스트 하는 간편한 방법은 3 개의 서로 다른 브라우저 (또는 incognito/InPrivate 버전)를 시작 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-257">An easy way to test the completed app is to launch three different browsers (or incognito/InPrivate versions).</span></span> <span data-ttu-id="95443-258">하나의 브라우저에서 새 사용자를 등록 합니다 (예를 들어 `test@example.com`).</span><span class="sxs-lookup"><span data-stu-id="95443-258">In one browser, register a new user (for example, `test@example.com`).</span></span> <span data-ttu-id="95443-259">다른 사용자와 각 브라우저에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-259">Sign in to each browser with a different user.</span></span> <span data-ttu-id="95443-260">다음 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-260">Verify the following operations:</span></span>

* <span data-ttu-id="95443-261">등록 된 사용자의 승인 된 모든 연락처 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-261">Registered users can view all the approved contact data.</span></span>
* <span data-ttu-id="95443-262">등록 된 사용자 편집/삭제할 수 있습니다 자신의 고유 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-262">Registered users can edit/delete their own data.</span></span>
* <span data-ttu-id="95443-263">관리자 승인 하거나 연락처 데이터를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-263">Managers can approve or reject contact data.</span></span> <span data-ttu-id="95443-264">합니다 `Details` 표시를 볼 **승인** 하 고 **거부** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-264">The `Details` view shows **Approve** and **Reject** buttons.</span></span>
* <span data-ttu-id="95443-265">관리자 승인/거부를 편집/삭제할 모든 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-265">Administrators can approve/reject and edit/delete any data.</span></span>

| <span data-ttu-id="95443-266">사용자</span><span class="sxs-lookup"><span data-stu-id="95443-266">User</span></span>| <span data-ttu-id="95443-267">옵션</span><span class="sxs-lookup"><span data-stu-id="95443-267">Options</span></span> |
| ------------ | ---------|
| test@example.com | <span data-ttu-id="95443-268">편집/삭제할 수 있습니다 자체 데이터</span><span class="sxs-lookup"><span data-stu-id="95443-268">Can edit/delete own data</span></span> |
| manager@contoso.com | <span data-ttu-id="95443-269">승인/거부 하 고 편집/삭제할 데이터 소유할 수 있습니다</span><span class="sxs-lookup"><span data-stu-id="95443-269">Can approve/reject and edit/delete own data</span></span> |
| admin@contoso.com | <span data-ttu-id="95443-270">수 편집/삭제 및 모든 데이터를 승인/거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-270">Can edit/delete and approve/reject all data</span></span>|

<span data-ttu-id="95443-271">관리자의 브라우저에서 연락처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="95443-271">Create a contact in the administrator's browser.</span></span> <span data-ttu-id="95443-272">삭제에 대 한 URL을 복사 하 고 관리자 연락처에서 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-272">Copy the URL for delete and edit from the administrator contact.</span></span> <span data-ttu-id="95443-273">테스트 사용자를 이러한 작업을 수행할 수 없습니다 확인 하려면 테스트 사용자의 브라우저에 이러한 링크를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-273">Paste these links into the test user's browser to verify the test user can't perform these operations.</span></span>

## <a name="create-the-starter-app"></a><span data-ttu-id="95443-274">시작 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-274">Create the starter app</span></span>

* <span data-ttu-id="95443-275">"ContactManager" 라는 Razor 페이지 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="95443-275">Create a Razor Pages app named "ContactManager"</span></span>
   * <span data-ttu-id="95443-276">응용 프로그램을 만들 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-276">Create the app with **Individual User Accounts**.</span></span>
   * <span data-ttu-id="95443-277">네임 스페이스에는 샘플에 사용 된 네임 스페이스와 일치 하므로 "ContactManager" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-277">Name it "ContactManager" so the namespace matches the namespace used in the sample.</span></span>
   * <span data-ttu-id="95443-278">`-uld` SQLite 대신 LocalDB를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-278">`-uld` specifies LocalDB instead of SQLite</span></span>

  ```console
  dotnet new webapp -o ContactManager -au Individual -uld
  ```

* <span data-ttu-id="95443-279">추가 *Models\Contact.cs*:</span><span class="sxs-lookup"><span data-stu-id="95443-279">Add *Models\Contact.cs*:</span></span>

  [!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet1)]

* <span data-ttu-id="95443-280">스 캐 폴드는 `Contact` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-280">Scaffold the `Contact` model.</span></span>
* <span data-ttu-id="95443-281">초기 마이그레이션을 만들고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-281">Create initial migration and update the database:</span></span>

```console
dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
dotnet ef database drop -f
dotnet ef migrations add initial
dotnet ef database update
```

* <span data-ttu-id="95443-282">업데이트를 **ContactManager** 에 고정 합니다 *pages/_layout.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="95443-282">Update the **ContactManager** anchor in the *Pages/_Layout.cshtml* file:</span></span>

```cshtml
<a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
```

* <span data-ttu-id="95443-283">만들기, 편집 및 연락처를 삭제 하 여 앱 테스트</span><span class="sxs-lookup"><span data-stu-id="95443-283">Test the app by creating, editing, and deleting a contact</span></span>

### <a name="seed-the-database"></a><span data-ttu-id="95443-284">데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="95443-284">Seed the database</span></span>

<span data-ttu-id="95443-285">추가 된 [SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs) 클래스는 *데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="95443-285">Add the [SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs) class to the *Data* folder.</span></span>

<span data-ttu-id="95443-286">호출 `SeedData.Initialize` 에서 `Main`:</span><span class="sxs-lookup"><span data-stu-id="95443-286">Call `SeedData.Initialize` from `Main`:</span></span>

[!code-csharp[](secure-data/samples/starter2.1/Program.cs?name=snippet)]

<span data-ttu-id="95443-287">응용 프로그램 데이터베이스를 시드를 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-287">Test that the app seeded the database.</span></span> <span data-ttu-id="95443-288">DB 연락처의 모든 행이 없으면 시드 메서드가 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95443-288">If there are any rows in the contact DB, the seed method doesn't run.</span></span>

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a><span data-ttu-id="95443-289">추가 자료</span><span class="sxs-lookup"><span data-stu-id="95443-289">Additional resources</span></span>

* <span data-ttu-id="95443-290">[ASP.NET Core 권한 부여 랩](https://github.com/blowdart/AspNetAuthorizationWorkshop)합니다.</span><span class="sxs-lookup"><span data-stu-id="95443-290">[ASP.NET Core Authorization Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop).</span></span> <span data-ttu-id="95443-291">이 랩에서이 자습서에 도입 된 보안 기능에 자세한 내용으로 이어집니다.</span><span class="sxs-lookup"><span data-stu-id="95443-291">This lab goes into more detail on the security features introduced in this tutorial.</span></span>
* [<span data-ttu-id="95443-292">ASP.NET Core에서 권한 부여: 단순, 역할, 클레임 기반 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="95443-292">Authorization in ASP.NET Core: Simple, role, claims-based, and custom</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="95443-293">사용자 지정 정책 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="95443-293">Custom policy-based authorization</span></span>](xref:security/authorization/policies)

::: moniker-end
