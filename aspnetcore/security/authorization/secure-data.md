---
title: "권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기"
author: rick-anderson
description: "권한 부여에 의해 보호 되는 사용자 데이터와 함께 Razor 페이지 앱을 만드는 방법에 알아봅니다. SSL, 인증, 보안, ASP.NET Core Id를 포함합니다."
manager: wpickett
ms.author: riande
ms.date: 01/24/2018
ms.prod: aspnet-core
ms.technology: aspnet
ms.topic: article
uid: security/authorization/secure-data
ms.openlocfilehash: 6333082a2b2b4f6d3f1ce2afc600b4203a0f5dca
ms.sourcegitcommit: 7a87d66cf1d01febe6635c7306f2f679434901d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a><span data-ttu-id="817dd-104">권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="817dd-104">Create an ASP.NET Core app with user data protected by authorization</span></span>

<span data-ttu-id="817dd-105">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT) 및 [Joe Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="817dd-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

<span data-ttu-id="817dd-106">이 자습서에는 권한 부여에 의해 보호 되는 사용자 데이터와 ASP.NET Core 웹 앱을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-106">This tutorial shows how to create an ASP.NET Core web app with user data protected by authorization.</span></span> <span data-ttu-id="817dd-107">인증 된 (등록 된) 사용자 연락처 목록을 표시를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-107">It displays a list of contacts that authenticated (registered) users have created.</span></span> <span data-ttu-id="817dd-108">세 가지 보안 그룹이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-108">There are three security groups:</span></span>

* <span data-ttu-id="817dd-109">**사용자가 등록** 수 편집/삭제 자신의 데이터 및 승인 된 모든 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-109">**Registered users** can view all the approved data and can edit/delete their own data.</span></span>
* <span data-ttu-id="817dd-110">**관리자** 승인 또는 연락처 데이터를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-110">**Managers** can approve or reject contact data.</span></span> <span data-ttu-id="817dd-111">승인 된 연락처에만 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-111">Only approved contacts are visible to users.</span></span>
* <span data-ttu-id="817dd-112">**관리자** 수 승인/거부 및 모든 데이터를 편집/삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-112">**Administrators** can approve/reject and edit/delete any data.</span></span>

<span data-ttu-id="817dd-113">다음 이미지에서는 Rick 사용자 (`rick@example.com`)에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-113">In the following image, user Rick (`rick@example.com`) is signed in.</span></span> <span data-ttu-id="817dd-114">Rick 승인 된 연락처를 보기만 할 수 있습니다 및 **편집**/**삭제**/**새로 만들기** 그의 연락처에 대 한 링크입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-114">Rick can only view approved contacts and **Edit**/**Delete**/**Create New** links for his contacts.</span></span> <span data-ttu-id="817dd-115">마지막 레코드만 Rick를 표시 하 여 만든 **편집** 및 **삭제** 링크 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-115">Only the last record, created by Rick, displays **Edit** and **Delete** links.</span></span> <span data-ttu-id="817dd-116">다른 사용자에 게는 관리자 또는 관리자가 상태를 "승인 됨"으로 변경 될 때까지 마지막 레코드를 표시 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-116">Other users won't see the last record until a manager or administrator changes the status to "Approved".</span></span>

![이전 이미지 설명](secure-data/_static/rick.png)

<span data-ttu-id="817dd-118">다음 그림에 `manager@contoso.com` 관리자 역할에서 서명:</span><span class="sxs-lookup"><span data-stu-id="817dd-118">In the following image, `manager@contoso.com` is signed in and in the managers role:</span></span>

![이전 이미지 설명](secure-data/_static/manager1.png)

<span data-ttu-id="817dd-120">다음 이미지는 관리자의 연락처 세부 정보 보기를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-120">The following image shows the managers details view of a contact:</span></span>

![이전 이미지 설명](secure-data/_static/manager.png)

<span data-ttu-id="817dd-122">**승인** 및 **거부** 단추가 관리자와 관리자만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-122">The **Approve** and **Reject** buttons are only displayed for managers and administrators.</span></span>

<span data-ttu-id="817dd-123">다음 그림에 `admin@contoso.com` 관리자 역할에서 서명:</span><span class="sxs-lookup"><span data-stu-id="817dd-123">In the following image, `admin@contoso.com` is signed in and in the administrators role:</span></span>

![이전 이미지 설명](secure-data/_static/admin.png)

<span data-ttu-id="817dd-125">관리자는 모든 권한을 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-125">The administrator has all privileges.</span></span> <span data-ttu-id="817dd-126">그녀는 모든 연락처 읽기/편집/삭제 수 한 연락처의 상태를 변경 했습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-126">She can read/edit/delete any contact and change the status of contacts.</span></span>

<span data-ttu-id="817dd-127">응용 프로그램에서 만들어진 [스 캐 폴딩](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) 다음 `Contact` 모델:</span><span class="sxs-lookup"><span data-stu-id="817dd-127">The app was created by [scaffolding](xref:tutorials/first-mvc-app-xplat/adding-model#scaffold-the-moviecontroller) the following `Contact` model:</span></span>

[!code-csharp[Main](secure-data/samples/starter2/Models/Contact.cs?name=snippet1)]

<span data-ttu-id="817dd-128">이 샘플에 다음 권한 부여 처리기를 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-128">The sample contains the following authorization handlers:</span></span>

* <span data-ttu-id="817dd-129">`ContactIsOwnerAuthorizationHandler`: 사용자가 데이터를 편집할 수만 보장 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-129">`ContactIsOwnerAuthorizationHandler`: Ensures that a user can only edit their data.</span></span>
* <span data-ttu-id="817dd-130">`ContactManagerAuthorizationHandler`: 관리자가 승인 또는 거부 연락처 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-130">`ContactManagerAuthorizationHandler`: Allows managers to approve or reject contacts.</span></span>
* <span data-ttu-id="817dd-131">`ContactAdministratorsAuthorizationHandler`: 관리자가 승인 또는 연락처를 거부 하 고 연락처 편집 하거나 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-131">`ContactAdministratorsAuthorizationHandler`: Allows administrators to approve or reject contacts and to edit/delete contacts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="817dd-132">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="817dd-132">Prerequisites</span></span>

<span data-ttu-id="817dd-133">이 자습서를 진행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-133">This tutorial is advanced.</span></span> <span data-ttu-id="817dd-134">에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-134">You should be familiar with:</span></span>

* [<span data-ttu-id="817dd-135">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="817dd-135">ASP.NET Core</span></span>](xref:tutorials/first-mvc-app/start-mvc)
* [<span data-ttu-id="817dd-136">인증</span><span class="sxs-lookup"><span data-stu-id="817dd-136">Authentication</span></span>](xref:security/authentication/index)
* [<span data-ttu-id="817dd-137">계정 확인 및 암호 복구</span><span class="sxs-lookup"><span data-stu-id="817dd-137">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="817dd-138">권한 부여</span><span class="sxs-lookup"><span data-stu-id="817dd-138">Authorization</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="817dd-139">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="817dd-139">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

<span data-ttu-id="817dd-140">참조 [이 PDF 파일](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core MVC 버전에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-140">See [this PDF file](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core MVC version.</span></span> <span data-ttu-id="817dd-141">이 자습서의 ASP.NET Core 1.1 버전은에 [이](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-141">The ASP.NET Core 1.1 version of this tutorial is in [this](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) folder.</span></span> <span data-ttu-id="817dd-142">ASP.NET Core 예제에는 1.1는 [샘플](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-142">The 1.1 ASP.NET Core sample is in the [samples](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).</span></span>

## <a name="the-starter-and-completed-app"></a><span data-ttu-id="817dd-143">시작 및 완료 된 앱</span><span class="sxs-lookup"><span data-stu-id="817dd-143">The starter and completed app</span></span>

<span data-ttu-id="817dd-144">[다운로드](xref:tutorials/index#how-to-download-a-sample) 는 [완료](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-144">[Download](xref:tutorials/index#how-to-download-a-sample) the [completed](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) app.</span></span> <span data-ttu-id="817dd-145">[테스트](#test-the-completed-app) 해당 보안 기능에 잘 알고 있으므로 완료 된 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-145">[Test](#test-the-completed-app) the completed app so you become familiar with its security features.</span></span>

### <a name="the-starter-app"></a><span data-ttu-id="817dd-146">시작 응용 프로그램</span><span class="sxs-lookup"><span data-stu-id="817dd-146">The starter app</span></span>

<span data-ttu-id="817dd-147">[다운로드](xref:tutorials/index#how-to-download-a-sample) 는 [스타터](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-147">[Download](xref:tutorials/index#how-to-download-a-sample) the [starter](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) app.</span></span>

<span data-ttu-id="817dd-148">응용 프로그램 실행을 탭의 **ContactManager** 링크를 선택한 만들기, 편집 및 연락처를 삭제를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-148">Run the app, tap the **ContactManager** link, and verify you can create, edit, and delete a contact.</span></span>

## <a name="secure-user-data"></a><span data-ttu-id="817dd-149">사용자 데이터 보호</span><span class="sxs-lookup"><span data-stu-id="817dd-149">Secure user data</span></span>

<span data-ttu-id="817dd-150">다음 섹션에서는 보안 사용자 데이터 응용 프로그램을 만드는 모든 주요 단계 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-150">The following sections have all the major steps to create the secure user data app.</span></span> <span data-ttu-id="817dd-151">완료 된 프로젝트를 참조 하는 것이 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-151">You may find it helpful to refer to the completed project.</span></span>

### <a name="tie-the-contact-data-to-the-user"></a><span data-ttu-id="817dd-152">사용자에 게 연락 데이터를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-152">Tie the contact data to the user</span></span>

<span data-ttu-id="817dd-153">ASP.NET을 사용 하 여 [Identity](xref:security/authentication/identity) 가 데이터를 하지만 다른 사용자가 데이터가 아닌 사용자 ID 사용자를 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-153">Use the ASP.NET [Identity](xref:security/authentication/identity) user ID to ensure users can edit their data, but not other users data.</span></span> <span data-ttu-id="817dd-154">추가 `OwnerID` 및 `ContactStatus` 에 `Contact` 모델:</span><span class="sxs-lookup"><span data-stu-id="817dd-154">Add `OwnerID` and `ContactStatus` to the `Contact` model:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

<span data-ttu-id="817dd-155">`OwnerID`사용자의 id는 `AspNetUser` 테이블에 [Identity](xref:security/authentication/identity) 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-155">`OwnerID` is the user's ID from the `AspNetUser` table in the [Identity](xref:security/authentication/identity) database.</span></span> <span data-ttu-id="817dd-156">`Status` 필드 연락처 일반 사용자가 볼 수 있는지 여부를 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-156">The `Status` field determines if a contact is viewable by general users.</span></span>

<span data-ttu-id="817dd-157">새 마이그레이션 만들고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-157">Create a new migration and update the database:</span></span>

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="require-ssl-and-authenticated-users"></a><span data-ttu-id="817dd-158">SSL 및 인증 된 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-158">Require SSL and authenticated users</span></span>

<span data-ttu-id="817dd-159">추가 [IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) 를 `Startup`:</span><span class="sxs-lookup"><span data-stu-id="817dd-159">Add [IHostingEnvironment](/dotnet/api/microsoft.aspnetcore.hosting.ihostingenvironment) to `Startup`:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=snippet_env)]

<span data-ttu-id="817dd-160">에 `ConfigureServices` 의 메서드는 *Startup.cs* 파일에서 추가 된 [RequireHttpsAttribute](/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute) 권한 부여 필터:</span><span class="sxs-lookup"><span data-stu-id="817dd-160">In the `ConfigureServices` method of the *Startup.cs* file, add the [RequireHttpsAttribute](/aspnet/core/api/microsoft.aspnetcore.mvc.requirehttpsattribute) authorization filter:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=snippet_SSL&highlight=19-999)]

<span data-ttu-id="817dd-161">Visual Studio를 사용 하는 경우에 SSL을 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-161">If you're using Visual Studio, enable SSL.</span></span>

<span data-ttu-id="817dd-162">참조를 HTTPS로 HTTP 요청을 리디렉션할 [URL 다시 쓰기 미들웨어](xref:fundamentals/url-rewriting)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-162">To redirect HTTP requests to HTTPS, see [URL Rewriting Middleware](xref:fundamentals/url-rewriting).</span></span> <span data-ttu-id="817dd-163">Visual Studio 코드를 사용 하 여 이거나 로컬 테스트 인증서를 SSL에 대 한 포함 되지 않은 플랫폼에 대 한 테스트:</span><span class="sxs-lookup"><span data-stu-id="817dd-163">If you're using Visual Studio Code or testing on a local platform that doesn't include a test certificate for SSL:</span></span>

  <span data-ttu-id="817dd-164">설정 `"LocalTest:skipSSL": true` 에 *appsettings 합니다. Developement.json* 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-164">Set `"LocalTest:skipSSL": true` in the *appsettings.Developement.json* file.</span></span>

### <a name="require-authenticated-users"></a><span data-ttu-id="817dd-165">인증 된 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-165">Require authenticated users</span></span>

<span data-ttu-id="817dd-166">사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-166">Set the default authentication policy to require users to be authenticated.</span></span> <span data-ttu-id="817dd-167">인증을 통해 Razor 페이지, 컨트롤러 또는 동작 메서드 수준에서 옵트아웃을 선택할 수 있습니다는 `[AllowAnonymous]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-167">You can opt out of authentication at the Razor Page, controller, or action method level with the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="817dd-168">새로 추가 된 Razor 페이지와 컨트롤러 보호 사용자를 인증 하도록 요구 하는 기본 인증 정책을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-168">Setting the default authentication policy to require users to be authenticated protects newly added Razor Pages and controllers.</span></span> <span data-ttu-id="817dd-169">기본적으로 필요한 인증은 새로운 컨트롤러와 Razor 페이지를 포함 하도록 이용 보다 더 안전한 것은 `[Authorize]` 특성입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-169">Having authentication required by default is safer than relying on new controllers and Razor Pages to include the `[Authorize]` attribute.</span></span> <span data-ttu-id="817dd-170">다음을 추가 `ConfigureServices` 의 메서드는 *Startup.cs* 파일:</span><span class="sxs-lookup"><span data-stu-id="817dd-170">Add the following to the `ConfigureServices` method of the *Startup.cs* file:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=snippet_defaultPolicy&highlight=31-999)]

<span data-ttu-id="817dd-171">추가 [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) 인덱스 및 연락처 정보, 페이지 익명 사용자가 등록 하기 전에 사이트에 대 한 정보를 가져올 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-171">Add [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) to the Index, About, and Contact pages so anonymous users can get information about the site before they register.</span></span> 

[!code-csharp[Main](secure-data/samples/final2/Pages/Index.cshtml.cs?name=snippet&highlight=2)]

<span data-ttu-id="817dd-172">추가 `[AllowAnonymous]` 에 [LoginModel 및 RegisterModel](https://github.com/aspnet/templating/issues/238)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-172">Add `[AllowAnonymous]` to the [LoginModel and RegisterModel](https://github.com/aspnet/templating/issues/238).</span></span>

### <a name="configure-the-test-account"></a><span data-ttu-id="817dd-173">테스트 계정 구성</span><span class="sxs-lookup"><span data-stu-id="817dd-173">Configure the test account</span></span>

<span data-ttu-id="817dd-174">`SeedData` 클래스에는 두 개의 계정을 만듭니다: 관리자 및 관리자입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-174">The `SeedData` class creates two accounts: administrator and manager.</span></span> <span data-ttu-id="817dd-175">사용 하 여는 [암호 관리자 도구](xref:security/app-secrets) 이러한 계정에 대 한 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-175">Use the [Secret Manager tool](xref:security/app-secrets) to set a password for these accounts.</span></span> <span data-ttu-id="817dd-176">프로젝트 디렉터리에서 암호를 설정 (포함 된 디렉터리 *Program.cs*):</span><span class="sxs-lookup"><span data-stu-id="817dd-176">Set the password from the project directory (the directory containing *Program.cs*):</span></span>

```console
dotnet user-secrets set SeedUserPW <PW>
```

<span data-ttu-id="817dd-177">업데이트 `Main` 테스트 암호를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-177">Update `Main` to use the test password:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a><span data-ttu-id="817dd-178">테스트 계정을 만들고 연락처를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-178">Create the test accounts and update the contacts</span></span>

<span data-ttu-id="817dd-179">업데이트는 `Initialize` 에서 메서드는 `SeedData` 테스트 계정을 만들 클래스:</span><span class="sxs-lookup"><span data-stu-id="817dd-179">Update the `Initialize` method in the `SeedData` class to create the test accounts:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Data/SeedData.cs?name=snippet_Initialize)]

<span data-ttu-id="817dd-180">관리자 사용자 ID를 추가 하 고 `ContactStatus` 연락처에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-180">Add the administrator user ID and `ContactStatus` to the contacts.</span></span> <span data-ttu-id="817dd-181">"제출 됨" 및 "Rejected" 하나의 연락처 중 하나를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-181">Make one of the contacts "Submitted" and one "Rejected".</span></span> <span data-ttu-id="817dd-182">사용자 ID 및 상태에 있는 모든 연락처를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-182">Add the user ID and status to all the contacts.</span></span> <span data-ttu-id="817dd-183">하나만 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-183">Only one contact is shown:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a><span data-ttu-id="817dd-184">소유자, 관리자 및 관리자 권한 부여 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="817dd-184">Create owner, manager, and administrator authorization handlers</span></span>

<span data-ttu-id="817dd-185">만들기는 `ContactIsOwnerAuthorizationHandler` 클래스에 *권한 부여* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-185">Create a `ContactIsOwnerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="817dd-186">`ContactIsOwnerAuthorizationHandler` 리소스에 대해 작동 하는 사용자 리소스를 소유 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-186">The `ContactIsOwnerAuthorizationHandler` verifies that the user acting on a resource owns the resource.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

<span data-ttu-id="817dd-187">`ContactIsOwnerAuthorizationHandler` 호출 [컨텍스트. 성공](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) 현재 인증 된 사용자가 연락처 소유자 인 경우.</span><span class="sxs-lookup"><span data-stu-id="817dd-187">The `ContactIsOwnerAuthorizationHandler` calls [context.Succeed](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) if the current authenticated user is the contact owner.</span></span> <span data-ttu-id="817dd-188">권한 부여 처리기 일반적으로:</span><span class="sxs-lookup"><span data-stu-id="817dd-188">Authorization handlers generally:</span></span>

* <span data-ttu-id="817dd-189">반환할 `context.Succeed` 에서 요구 사항이 충족 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-189">Return `context.Succeed` when the requirements are met.</span></span>
* <span data-ttu-id="817dd-190">반환할 `Task.CompletedTask` 요구 사항이 충족 되지 않으면 경우.</span><span class="sxs-lookup"><span data-stu-id="817dd-190">Return `Task.CompletedTask` when requirements aren't met.</span></span> <span data-ttu-id="817dd-191">`Task.CompletedTask`모두 성공 또는 실패는&mdash;다른 권한 부여 처리기 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-191">`Task.CompletedTask` is neither success or failure&mdash;it allows other authorization handlers to run.</span></span>

<span data-ttu-id="817dd-192">명시적으로 실패 해야 할 경우 반환 [컨텍스트. 실패](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-192">If you need to explicitly fail, return [context.Fail](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).</span></span>

<span data-ttu-id="817dd-193">응용 프로그램 자체 데이터 연락처 소유자가 데이터를 편집/삭제/만들기를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-193">The app allows contact owners to edit/delete/create their own data.</span></span> <span data-ttu-id="817dd-194">`ContactIsOwnerAuthorizationHandler`요구 사항 매개 변수에서 전달 하 고 작업을 확인 하려면 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-194">`ContactIsOwnerAuthorizationHandler` doesn't need to check the operation passed in the requirement parameter.</span></span>

### <a name="create-a-manager-authorization-handler"></a><span data-ttu-id="817dd-195">관리자 권한 부여 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="817dd-195">Create a manager authorization handler</span></span>

<span data-ttu-id="817dd-196">만들기는 `ContactManagerAuthorizationHandler` 클래스에 *권한 부여* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-196">Create a `ContactManagerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="817dd-197">`ContactManagerAuthorizationHandler` 리소스에 대해 작동 하는 사용자는 관리자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-197">The `ContactManagerAuthorizationHandler` verifies the user acting on the resource is a manager.</span></span> <span data-ttu-id="817dd-198">관리자만 승인 하거나 (새롭거나 변경 된) 콘텐츠 변경 내용을 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-198">Only managers can approve or reject content changes (new or changed).</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a><span data-ttu-id="817dd-199">관리자 권한 부여 처리기 만들기</span><span class="sxs-lookup"><span data-stu-id="817dd-199">Create an administrator authorization handler</span></span>

<span data-ttu-id="817dd-200">만들기는 `ContactAdministratorsAuthorizationHandler` 클래스에 *권한 부여* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-200">Create a `ContactAdministratorsAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="817dd-201">`ContactAdministratorsAuthorizationHandler` 리소스에 대해 작동 하는 사용자가 관리자를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-201">The `ContactAdministratorsAuthorizationHandler` verifies the user acting on the resource is an administrator.</span></span> <span data-ttu-id="817dd-202">관리자는 모든 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-202">Administrator can do all operations.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a><span data-ttu-id="817dd-203">인증 처리기를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-203">Register the authorization handlers</span></span>

<span data-ttu-id="817dd-204">Entity Framework Core를 사용 하 여 서비스를 위해 등록 되어야 [종속성 주입](xref:fundamentals/dependency-injection) 를 사용 하 여 [AddScoped](/aspnet/core/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-204">Services using Entity Framework Core must be registered for [dependency injection](xref:fundamentals/dependency-injection) using [AddScoped](/aspnet/core/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions).</span></span> <span data-ttu-id="817dd-205">`ContactIsOwnerAuthorizationHandler` ASP.NET Core를 사용 하 여 [Identity](xref:security/authentication/identity), Entity Framework Core 기반입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-205">The `ContactIsOwnerAuthorizationHandler` uses ASP.NET Core [Identity](xref:security/authentication/identity), which is built on Entity Framework Core.</span></span> <span data-ttu-id="817dd-206">가 사용할 수 있도록 서비스 컬렉션에 처리기를 등록 된 `ContactsController` 통해 [종속성 주입](xref:fundamentals/dependency-injection)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-206">Register the handlers with the service collection so they're available to the `ContactsController` through [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="817dd-207">다음 코드의 끝에 추가 `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="817dd-207">Add the following code to the end of `ConfigureServices`:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Startup.cs?name=ConfigureServices&highlight=41-999)]

<span data-ttu-id="817dd-208">`ContactAdministratorsAuthorizationHandler`및 `ContactManagerAuthorizationHandler` 단일 항목으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-208">`ContactAdministratorsAuthorizationHandler` and `ContactManagerAuthorizationHandler` are added as singletons.</span></span> <span data-ttu-id="817dd-209">EF를 사용 하지 않는 하 고 필요한 모든 정보는 되므로 singleton 하기가 `Context` 의 매개 변수는 `HandleRequirementAsync` 메서드.</span><span class="sxs-lookup"><span data-stu-id="817dd-209">They're singletons because they don't use EF and all the information needed is in the `Context` parameter of the `HandleRequirementAsync` method.</span></span>

## <a name="support-authorization"></a><span data-ttu-id="817dd-210">권한 부여를 지원 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-210">Support authorization</span></span>

<span data-ttu-id="817dd-211">이 섹션에서는 Razor 페이지를 업데이트 및 운영 요구 사항 클래스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-211">In this section, you update the Razor Pages and add an operations requirements class.</span></span>

### <a name="review-the-contact-operations-requirements-class"></a><span data-ttu-id="817dd-212">연락처 작업 요구 사항 클래스를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-212">Review the contact operations requirements class</span></span>

<span data-ttu-id="817dd-213">검토는 `ContactOperations` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-213">Review the `ContactOperations` class.</span></span> <span data-ttu-id="817dd-214">이 클래스는 요구 사항이 포함 되어 응용 프로그램이 지 원하는:</span><span class="sxs-lookup"><span data-stu-id="817dd-214">This class contains the requirements the app supports:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-razor-pages"></a><span data-ttu-id="817dd-215">Razor 페이지에 대 한 기본 클래스를 만들으십시오</span><span class="sxs-lookup"><span data-stu-id="817dd-215">Create a base class for the Razor Pages</span></span>

<span data-ttu-id="817dd-216">Razor 페이지에 있는 연락처에 사용 되는 서비스를 포함 하는 기본 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-216">Create a base class that contains the services used in the contacts Razor Pages.</span></span> <span data-ttu-id="817dd-217">해당 초기화 코드가 한 위치에 배치 하는 기본 클래스:</span><span class="sxs-lookup"><span data-stu-id="817dd-217">The base class puts that initialization code in one location:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/DI_BasePageModel.cs)]

<span data-ttu-id="817dd-218">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="817dd-218">The preceding code:</span></span>

* <span data-ttu-id="817dd-219">추가 `IAuthorizationService` 서비스가 권한 부여 처리기에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-219">Adds the `IAuthorizationService` service to access to the authorization handlers.</span></span>
* <span data-ttu-id="817dd-220">Id를 추가 `UserManager` 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-220">Adds the Identity `UserManager` service.</span></span>
* <span data-ttu-id="817dd-221">`ApplicationDbContext`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-221">Add the `ApplicationDbContext`.</span></span>

### <a name="update-the-createmodel"></a><span data-ttu-id="817dd-222">업데이트는 CreateModel</span><span class="sxs-lookup"><span data-stu-id="817dd-222">Update the CreateModel</span></span>

<span data-ttu-id="817dd-223">사용 하도록 만들기 페이지 모델 생성자를 업데이트는 `DI_BasePageModel` 기본 클래스:</span><span class="sxs-lookup"><span data-stu-id="817dd-223">Update the create page model constructor to use the `DI_BasePageModel` base class:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

<span data-ttu-id="817dd-224">업데이트는 `CreateModel.OnPostAsync` 메서드:</span><span class="sxs-lookup"><span data-stu-id="817dd-224">Update the `CreateModel.OnPostAsync` method to:</span></span>

* <span data-ttu-id="817dd-225">사용자 ID를 추가 `Contact` 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-225">Add the user ID to the `Contact` model.</span></span>
* <span data-ttu-id="817dd-226">사용자에 게 연락처를 만들 수 있는 권한을 확인 하는 권한 부여 처리기를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-226">Call the authorization handler to verify the user has permission to create contacts.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a><span data-ttu-id="817dd-227">업데이트는 IndexModel</span><span class="sxs-lookup"><span data-stu-id="817dd-227">Update the IndexModel</span></span>

<span data-ttu-id="817dd-228">업데이트는 `OnGetAsync` 메서드 연락처만 승인 된 일반 사용자에 게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-228">Update the `OnGetAsync` method so only approved contacts are shown to general users:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a><span data-ttu-id="817dd-229">업데이트는 EditModel</span><span class="sxs-lookup"><span data-stu-id="817dd-229">Update the EditModel</span></span>

<span data-ttu-id="817dd-230">연락처를 소유 하 고 확인 하기 위해 인증 처리기를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-230">Add an authorization handler to verify the user owns the contact.</span></span> <span data-ttu-id="817dd-231">리소스 권한 부여가 유효성을 검사 하기 때문에 `[Authorize]` 특성 충분 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-231">Because resource authorization is being validated, the `[Authorize]` attribute is not enough.</span></span> <span data-ttu-id="817dd-232">앱에 특성 평가 되는 경우 리소스에 액세스할 수 없는 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-232">The app doesn't have access to the resource when attributes are evaluated.</span></span> <span data-ttu-id="817dd-233">리소스 기반 권한 부여는 명령적 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-233">Resource-based authorization must be imperative.</span></span> <span data-ttu-id="817dd-234">페이지 모델에 로드 하 여 또는 자체 처리기 내에서 로드 하 여 응용 프로그램에는 리소스에 대 한 액세스 검사를 수행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-234">Checks must be performed once the app has access to the resource, either by loading it in the page model or by loading it within the handler itself.</span></span> <span data-ttu-id="817dd-235">리소스 키를 전달 하 여 리소스에 액세스할 자주 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-235">You frequently access the resource by passing in the resource key.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a><span data-ttu-id="817dd-236">업데이트는 DeleteModel</span><span class="sxs-lookup"><span data-stu-id="817dd-236">Update the DeleteModel</span></span>

<span data-ttu-id="817dd-237">Delete 페이지 모델 사용자에 게 연락처에 delete 권한을 확인 하려면 권한 부여 처리기를 사용 하도록 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-237">Update the delete page model to use the authorization handler to verify the user has delete permission on the contact.</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a><span data-ttu-id="817dd-238">인증 서비스는 뷰에 삽입</span><span class="sxs-lookup"><span data-stu-id="817dd-238">Inject the authorization service into the views</span></span>

<span data-ttu-id="817dd-239">현재 UI에 표시 된 편집한 사용자가을 수정할 수 없는 데이터에 대 한 링크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-239">Currently, the UI shows edit and delete links for data the user can't modify.</span></span> <span data-ttu-id="817dd-240">UI는 권한 부여 처리기 보기에 적용 하 여 고정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-240">The UI is fixed by applying the authorization handler to the views.</span></span>

<span data-ttu-id="817dd-241">권한 부여 서비스를 주입는 *Views/_ViewImports.cshtml* 모든 보기에 사용할 수 있도록 파일:</span><span class="sxs-lookup"><span data-stu-id="817dd-241">Inject the authorization service in the *Views/_ViewImports.cshtml* file so it's available to all views:</span></span>

[!code-cshtml[Main](secure-data/samples/final2/Pages/_ViewImports.cshtml?highlight=6-9)]

<span data-ttu-id="817dd-242">위의 태그 몇 개 추가 `using` 문.</span><span class="sxs-lookup"><span data-stu-id="817dd-242">The preceding markup adds several `using` statements.</span></span>

<span data-ttu-id="817dd-243">업데이트는 **편집** 및 **삭제** 에서는 정적으로 연결 *Pages/Contacts/Index.cshtml* 적절 한 사용 권한 가진 사용자만 렌더링 될 있도록:</span><span class="sxs-lookup"><span data-stu-id="817dd-243">Update the **Edit** and **Delete** links in *Pages/Contacts/Index.cshtml* so they're only rendered for users with the appropriate permissions:</span></span>

[!code-cshtml[Main](secure-data/samples/final2/Pages/Contacts/Index.cshtml?highlight=34-36,64-999)]

> [!WARNING]
> <span data-ttu-id="817dd-244">데이터를 변경할 수 있는 권한이 없는 사용자 로부터 링크 숨기기 응용 프로그램 보안을 설정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-244">Hiding links from users that don't have permission to change data doesn't secure the app.</span></span> <span data-ttu-id="817dd-245">링크 숨기기 하면 유효한 링크를 표시 하 여 응용 프로그램 보다 사용자 친화적인 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-245">Hiding links makes the app more user-friendly by displaying only valid links.</span></span> <span data-ttu-id="817dd-246">사용자가 편집을 호출 하 고 자신이 소유 하지 않는 데이터에 대 한 작업을 삭제 하도록 생성 된 Url 해킹 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-246">Users can hack the generated URLs to invoke edit and delete operations on data they don't own.</span></span> <span data-ttu-id="817dd-247">Razor 페이지 또는 컨트롤러는 데이터 보호를 위해 액세스 검사를 적용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-247">The Razor Page or controller must enforce access checks to secure the data.</span></span>

### <a name="update-details"></a><span data-ttu-id="817dd-248">세부 정보 업데이트</span><span class="sxs-lookup"><span data-stu-id="817dd-248">Update Details</span></span>

<span data-ttu-id="817dd-249">관리자 승인 또는 연락처를 거부할 수 있도록 자세히 보기를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-249">Update the details view so managers can approve or reject contacts:</span></span>

[!code-cshtml[Main](secure-data/samples/final2/Pages/Contacts/Details.cshtml?range=48-999)]

<span data-ttu-id="817dd-250">세부 정보 페이지 모델을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-250">Update the details page model:</span></span>

[!code-csharp[Main](secure-data/samples/final2/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="test-the-completed-app"></a><span data-ttu-id="817dd-251">완성 된 응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="817dd-251">Test the completed app</span></span>

<span data-ttu-id="817dd-252">Visual Studio 코드를 사용 하 여 이거나 로컬 테스트 인증서를 SSL에 대 한 포함 되지 않은 플랫폼에 대 한 테스트:</span><span class="sxs-lookup"><span data-stu-id="817dd-252">If you're using Visual Studio Code or testing on a local platform that doesn't include a test certificate for SSL:</span></span>

* <span data-ttu-id="817dd-253">설정 `"LocalTest:skipSSL": true` 에 *appsettings 합니다. Developement.json* SSL 요구 사항을 건너뛸 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-253">Set `"LocalTest:skipSSL": true` in the *appsettings.Developement.json* file to skip the SSL requirement.</span></span> <span data-ttu-id="817dd-254">개발 컴퓨터에만 SSL을 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-254">Skip SSL only on a development machine.</span></span>

<span data-ttu-id="817dd-255">응용 프로그램에 연락처 하는 경우:</span><span class="sxs-lookup"><span data-stu-id="817dd-255">If the app has contacts:</span></span>

* <span data-ttu-id="817dd-256">모든 레코드를 삭제는 `Contact` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-256">Delete all the records in the `Contact` table.</span></span>
* <span data-ttu-id="817dd-257">응용 프로그램에서 데이터베이스를 시드하고 다시 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-257">Restart the app to seed the database.</span></span>

<span data-ttu-id="817dd-258">연락처 검색에 대 한 사용자를 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-258">Register a user for browsing the contacts.</span></span>

<span data-ttu-id="817dd-259">완성 된 앱을 테스트 하는 쉬운 방법은 세 가지 서로 다른 브라우저 (또는 incognito/InPrivate 버전)를 시작 하려면입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-259">An easy way to test the completed app is to launch three different browsers (or incognito/InPrivate versions).</span></span> <span data-ttu-id="817dd-260">하나의 브라우저에서 새 사용자를 등록 합니다 (예를 들어 `test@example.com`).</span><span class="sxs-lookup"><span data-stu-id="817dd-260">In one browser, register a new user (for example, `test@example.com`).</span></span> <span data-ttu-id="817dd-261">각 브라우저에 다른 사용자로 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-261">Sign in to each browser with a different user.</span></span> <span data-ttu-id="817dd-262">다음 작업을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-262">Verify the following operations:</span></span>

* <span data-ttu-id="817dd-263">등록 된 사용자의 승인 된 모든 연락처 데이터를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-263">Registered users can view all the approved contact data.</span></span>
* <span data-ttu-id="817dd-264">등록 된 사용자 수 편집/삭제 자신의 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-264">Registered users can edit/delete their own data.</span></span>
* <span data-ttu-id="817dd-265">관리자 승인 하거나 연락 데이터를 거부할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-265">Managers can approve or reject contact data.</span></span> <span data-ttu-id="817dd-266">`Details` 보기 보여줍니다 **승인** 및 **거부** 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-266">The `Details` view shows **Approve** and **Reject** buttons.</span></span>
* <span data-ttu-id="817dd-267">관리자 승인/거부 있으며 편집/삭제 된 데이터.</span><span class="sxs-lookup"><span data-stu-id="817dd-267">Administrators can approve/reject and edit/delete any data.</span></span>

| <span data-ttu-id="817dd-268">사용자</span><span class="sxs-lookup"><span data-stu-id="817dd-268">User</span></span>| <span data-ttu-id="817dd-269">옵션</span><span class="sxs-lookup"><span data-stu-id="817dd-269">Options</span></span> |
| ------------ | ---------|
| test@example.com | <span data-ttu-id="817dd-270">수 편집/삭제 자체 데이터</span><span class="sxs-lookup"><span data-stu-id="817dd-270">Can edit/delete own data</span></span> |
| manager@contoso.com | <span data-ttu-id="817dd-271">승인/거부 및 편집/삭제를 데이터 소유할 수 있습니까</span><span class="sxs-lookup"><span data-stu-id="817dd-271">Can approve/reject and edit/delete own data</span></span> |
| admin@contoso.com | <span data-ttu-id="817dd-272">편집/삭제 있고 모든 데이터를 승인/거부 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-272">Can edit/delete and approve/reject all data</span></span>|

<span data-ttu-id="817dd-273">관리자의 브라우저에서 연락처를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-273">Create a contact in the administrator's browser.</span></span> <span data-ttu-id="817dd-274">Delete에 대 한 URL을 복사 하 고 관리자 연락처에서 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-274">Copy the URL for delete and edit from the administrator contact.</span></span> <span data-ttu-id="817dd-275">테스트 사용자는 이러한 작업을 수행할 수를 확인 하려면 테스트 사용자의 브라우저에 다음이 링크를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-275">Paste these links into the test user's browser to verify the test user can't perform these operations.</span></span>

## <a name="create-the-starter-app"></a><span data-ttu-id="817dd-276">시작 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="817dd-276">Create the starter app</span></span>

* <span data-ttu-id="817dd-277">"ContactManager" 라는 Razor 페이지 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="817dd-277">Create a Razor Pages app named "ContactManager"</span></span>

  * <span data-ttu-id="817dd-278">응용 프로그램을 만들 **개별 사용자 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-278">Create the app with **Individual User Accounts**.</span></span>
  * <span data-ttu-id="817dd-279">네임 스페이스에는 샘플에 사용 된 네임 스페이스와 일치 하므로 "ContactManager" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-279">Name it "ContactManager" so your namespace matches the namespace used in the sample.</span></span>

  ```console
  dotnet new razor -o ContactManager -au Individual -uld
  ```

  * <span data-ttu-id="817dd-280">`-uld`SQLite는 대신 LocalDB를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-280">`-uld` specifies LocalDB instead of SQLite</span></span>

* <span data-ttu-id="817dd-281">다음 추가 `Contact` 모델:</span><span class="sxs-lookup"><span data-stu-id="817dd-281">Add the following `Contact` model:</span></span>

  [!code-csharp[Main](secure-data/samples/starter2/Models/Contact.cs?name=snippet1)]

* <span data-ttu-id="817dd-282">스 캐 폴드 된 `Contact` 모델:</span><span class="sxs-lookup"><span data-stu-id="817dd-282">Scaffold the `Contact` model:</span></span>

```console
dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
```

* <span data-ttu-id="817dd-283">업데이트는 **ContactManager** 고정는 *Pages/_Layout.cshtml* 파일:</span><span class="sxs-lookup"><span data-stu-id="817dd-283">Update the **ContactManager** anchor in the *Pages/_Layout.cshtml* file:</span></span>

```cshtml
<a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
```

* <span data-ttu-id="817dd-284">초기 마이그레이션을 스 캐 폴드 하 고 데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-284">Scaffold the initial migration and update the database:</span></span>

```console
dotnet ef migrations add initial
dotnet ef database update
```

* <span data-ttu-id="817dd-285">만들고, 편집 및 연락처를 삭제 하 여 앱을 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-285">Test the app by creating, editing, and deleting a contact</span></span>

### <a name="seed-the-database"></a><span data-ttu-id="817dd-286">데이터베이스 시드</span><span class="sxs-lookup"><span data-stu-id="817dd-286">Seed the database</span></span>

<span data-ttu-id="817dd-287">추가 `SeedData` 클래스는 *데이터* 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-287">Add the `SeedData` class to the *Data* folder.</span></span> <span data-ttu-id="817dd-288">샘플을 다운로드 하는 경우 복사할 수 있습니다는 *SeedData.cs* 파일을 여 *데이터* 시작 프로젝트의 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-288">If you've downloaded the sample, you can copy the *SeedData.cs* file to the *Data* folder of the starter project.</span></span>

<span data-ttu-id="817dd-289">호출 `SeedData.Initialize` 에서 `Main`:</span><span class="sxs-lookup"><span data-stu-id="817dd-289">Call `SeedData.Initialize` from `Main`:</span></span>

[!code-csharp[Main](secure-data/samples/starter2/Program.cs?name=snippet)]

<span data-ttu-id="817dd-290">응용 프로그램 데이터베이스 시드 있는지 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-290">Test that the app seeded the database.</span></span> <span data-ttu-id="817dd-291">DB 연락처의 모든 행이 있는 경우에 초기값 메서드 실행 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-291">If there are any rows in the contact DB, the seed method doesn't run.</span></span>

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a><span data-ttu-id="817dd-292">추가 리소스</span><span class="sxs-lookup"><span data-stu-id="817dd-292">Additional resources</span></span>

* <span data-ttu-id="817dd-293">[ASP.NET Core 권한 부여 랩](https://github.com/blowdart/AspNetAuthorizationWorkshop)합니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-293">[ASP.NET Core Authorization Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop).</span></span> <span data-ttu-id="817dd-294">이 자습서에 도입 된 보안 기능에이 랩 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="817dd-294">This lab goes into more detail on the security features introduced in this tutorial.</span></span>
* [<span data-ttu-id="817dd-295">ASP.NET Core에서 권한 부여: 단순, 역할, 클레임 기반 및 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="817dd-295">Authorization in ASP.NET Core: Simple, role, claims-based, and custom</span></span>](xref:security/authorization/index)
* [<span data-ttu-id="817dd-296">사용자 지정 정책 기반 권한 부여</span><span class="sxs-lookup"><span data-stu-id="817dd-296">Custom policy-based authorization</span></span>](xref:security/authorization/policies)
