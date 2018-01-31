# <a name="cookie-sharing-sample-app"></a>샘플 앱을 공유 하는 쿠키

이 샘플에서는 쿠키 인증을 사용 하는 세 개의 앱 간에 공유 되는 쿠키를 보여 줍니다.

| 프로젝트                             | 설명 |
| ----------------------------------- | ----------- |
| CookieAuth.Core                     | ASP.NET Core Id를 사용 하지 않고 ASP.NET 코어 2.0 Razor 페이지 응용 프로그램 |
| CookieAuthWithIdentity.Core         | ASP.NET Core Id 가진 ASP.NET Core 2.0 MVC 응용 프로그램 |
| CookieAuthWithIdentity.NETFramework | ASP.NET Id를 가진 ASP.NET Framework 4.6.1 MVC 응용 프로그램 |

지침:

1. CookieAuth.Core 응용 프로그램을 실행 합니다. 사용자를 등록 합니다. 응용 프로그램 사용자가 등록 하는 경우 사용자를 인증 합니다. 사용자를 로그 아웃 합니다.
1. 동일한 브라우저 세션의 CookieAuthWithIdentity.Core 앱을 실행 합니다. 핵심 앱과 함께 사용 된 것과 동일한 사용자를 등록 합니다. 응용 프로그램 사용자가 등록 하는 경우 사용자를 인증 합니다. 사용자를 로그 아웃 합니다.
1. 동일한 브라우저 세션의 CookieAuthWithIdentity.NETFramework 앱을 실행 합니다. 다른 앱과 함께 사용 된 것과 동일한 사용자를 등록 합니다. 응용 프로그램 사용자가 등록 하는 경우 사용자를 인증 합니다. 사용자를 로그 아웃 합니다.
1. 세 가지 앱 중 하나에 사용자를 로그인 합니다. 인증 쿠키는 앱 간에 공유 됩니다. 사용자가 다른 두 앱에 자동으로 로그인 하 고 있는지 확인 합니다.
1. 앱에서 사용자를 로그인 합니다. 사용자가 다른 두 응용 프로그램에서 자동으로 서명 note 합니다.

이 샘플에서 설명 하는 기능을 보여 줍니다.는 [쿠키 앱 간에 공유](https://docs.microsoft.com/aspnet/core/security/data-protection/compatibility/cookie-sharing) 항목입니다.
