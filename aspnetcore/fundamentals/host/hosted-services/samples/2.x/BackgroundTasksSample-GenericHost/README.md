# <a name="aspnet-core-background-tasks-sample-generic-host"></a>ASP.NET Core 백그라운드 작업 샘플(일반 호스트)

이 샘플은 [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice)의 사용법을 보여줍니다. 이 샘플에서는 [ASP.NET Core에서 호스팅되는 서비스를 사용하는 백그라운드 작업](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) 토픽에서 설명된 기능을 보여 줍니다.

[Visual Studio Code](https://code.visualstudio.com/)에서 샘플을 실행할 때 *.vscode/launch.json*에서 콘솔 구성의 **콘솔** 값을 `externalTerminal` 또는 `integratedTerminal`로 설정합니다. `internalConsole` 사용은 앱이 백그라운드 작업 항목을 큐에 넣는 데 사용하는 콘솔 키 입력과 호환되지 않습니다.
