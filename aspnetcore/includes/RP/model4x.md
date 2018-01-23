<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="f76be-101">Movie 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="f76be-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="f76be-102">명령줄에서 다음을 실행합니다(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 프로젝트 디렉터리에서).</span><span class="sxs-lookup"><span data-stu-id="f76be-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```

<span data-ttu-id="f76be-103">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="f76be-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="f76be-104">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에 대해 명령 셸을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="f76be-104">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
