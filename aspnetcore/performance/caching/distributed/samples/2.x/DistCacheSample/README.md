# <a name="aspnet-core-distributed-cache-sample"></a>ASP.NET Core 분산된 캐시 샘플

이 샘플의 분산된 된 캐시를 사용을 하는 방법을 보여 줍니다. 이 샘플에 설명 된 시나리오를 보여 줍니다.는 [ASP.NET Core의 분산된 캐시를 사용 하 여 작동](https://docs.microsoft.com/aspnet/core/performance/caching/distributed) 항목입니다.

프로덕션 환경에서 샘플 앱은 분산된 된 SQL Server 캐시를 사용 하도록 구성 됩니다. 분산된 Redis cache를 사용 하도록 앱을 다시 구성 하려면의 맨 위에 있는 전처리기 지시문을 변경 합니다 *Startup.cs* Redis를 사용 하는 파일 (`#define Redis // SQLServer`). 자세한 내용은 [샘플 코드에서 전처리기 지시문](https://docs.microsoft.com/aspnet/core/#preprocessor-directives-in-sample-code)합니다.
