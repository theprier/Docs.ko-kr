## <a name="register-the-database-context"></a><span data-ttu-id="872a7-101">데이터베이스 컨텍스트 등록</span><span class="sxs-lookup"><span data-stu-id="872a7-101">Register the database context</span></span>

<span data-ttu-id="872a7-102">이 단계에서 데이터베이스 컨텍스트는 [종속성 주입](xref:fundamentals/dependency-injection) 컨테이너에 등록됩니다.</span><span class="sxs-lookup"><span data-stu-id="872a7-102">In this step, the database context is registered with the [dependency injection](xref:fundamentals/dependency-injection) container.</span></span> <span data-ttu-id="872a7-103">DI(종속성 주입) 컨테이너에 등록된 서비스(예: DB 컨텍스트)를 컨트롤러에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="872a7-103">Services (such as the DB context) that are registered with the dependency injection (DI) container are available to the controllers.</span></span>

<span data-ttu-id="872a7-104">[종속성 주입](xref:fundamentals/dependency-injection)에 대한 기본 제공 지원을 사용하여 서비스 컨테이너에 DB 컨텍스트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="872a7-104">Register the DB context with the service container using the built-in support for [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="872a7-105">*Startup.cs* 파일의 내용을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="872a7-105">Replace the contents of the *Startup.cs* file with the following code:</span></span>

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="872a7-106">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Startup.cs?highlight=3,5,13-14)]</span><span class="sxs-lookup"><span data-stu-id="872a7-106">[!code-csharp[](../../tutorials/first-web-api/samples/2.1/TodoApi/Startup.cs?highlight=3,5,13-14)]</span></span>

::: moniker-end

::: moniker range="<= aspnetcore-2.0"

<span data-ttu-id="872a7-107">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup.cs?highlight=2,4,12-13)]</span><span class="sxs-lookup"><span data-stu-id="872a7-107">[!code-csharp[](../../tutorials/first-web-api/samples/2.0/TodoApi/Startup.cs?highlight=2,4,12-13)]</span></span>

::: moniker-end  

<span data-ttu-id="872a7-108">위의 코드:</span><span class="sxs-lookup"><span data-stu-id="872a7-108">The preceding code:</span></span>

* <span data-ttu-id="872a7-109">사용되지 않는 코드를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="872a7-109">Removes the unused code.</span></span>
* <span data-ttu-id="872a7-110">메모리 내 데이터베이스를 서비스 컨테이너에 주입하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="872a7-110">Specifies an in-memory database is injected into the service container.</span></span>
