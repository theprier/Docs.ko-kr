# <a name="aspnet-core-url-rewriting-sample-aspnet-core-1x"></a>ASP.NET Core URL 다시 작성 샘플(ASP.NET Core 1.x)

이 샘플은 ASP.NET Core 1.x URL 다시 작성 미들웨어의 사용법을 보여 줍니다. 응용 프로그램은 URL 리디렉션 및 URL 다시 작성 옵션을 보여 줍니다. ASP.NET Core 2.x 샘플의 경우 [ASP.NET Core URL 다시 작성 샘플 (ASP.NET Core 2.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/fundamentals/url-rewriting/samples/2.x)을 참조하세요.

샘플을 실행하면, 규칙 중 하나가 요청 URL에 적용될 때 다시 작성되거나 리디렉션된 URL을 보여 주는 응답이 제공됩니다.

## <a name="examples-in-this-sample"></a>이 샘플의 예

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - 성공 상태 코드: 302(Found)
  - 예(리디렉션): **/redirect-rule/{capture_group}**을 **/redirected/{capture_group}**으로
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - 성공 상태 코드: 200(OK)
  - 예(다시 작성): **/rewrite-rule/{capture_group_1}/{capture_group_2}**를 **/rewrtten?var1={capture_group_1}&var2={capture_group_2}**로
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - 성공 상태 코드: 302(Found)
  - 예(리디렉션): **/apache-mod-rules-redirect/ {capture_group}**을 **/redirected?id={capture_group}**으로
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - 성공 상태 코드: 200(OK)
  - 예(다시 작성): **/iis-rules-rewrite/ {capture_group}**을 **/rewritten?id={capture_group}**으로
* `Add(RedirectXMLRequests)`
  - 성공 상태 코드: 301(영구적 이동)
  - 예(리디렉션): **/file.xml**을 **/xmlfiles/file.xml**로
* `Add(new RedirectPNGRequests(".png", "/png-images")))`<br>`Add(new RedirectPNGRequests(".jpg", "/jpg-images")))`
  - 성공 상태 코드: 301(영구적 이동)
  - 예(리디렉션): **/image.png**를 **/png-images/image.png**로
  - 예(리디렉션): **/image.jpg**를 **/jpg-images/image.jpg**로

## <a name="using-a-physicalfileprovider"></a>`PhysicalFileProvider` 사용
또한 `AddApacheModRewrite()` 및 `AddIISUrlRewrite()` 메서드로 전달하도록 `PhysicalFileProvider`를 만들어 `IFileProvider`를 얻을 수 있습니다.
```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```
## <a name="secure-redirection-extensions"></a>보안 리디렉션 확장
이 샘플에는 앱에서 URL을 사용하도록 `WebHostBuilder` 구성(**https://localhost:5001**, **https://localhost**) 및 테스트 인증서(**testCert.pfx**)가 포함되어 있어 이러한 리디렉션 메서드를 탐색하는 데 도움이 됩니다. **Startup.cs**의 `RewriteOptions()`에 그 중 하나를 추가하여 동작을 살펴봅니다.

메서드 | 상태 코드 | 포트
--- | :---: | :---:
`.AddRedirectToHttpsPermanent()` | 301 | NULL(465)
`.AddRedirectToHttps()` | 302 | NULL(465)
`.AddRedirectToHttps(301)` | 301 | NULL(465)
`.AddRedirectToHttps(301, 5001)` | 301 | 5001
