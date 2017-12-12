<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="73b46-101">Movie 모델 스캐폴드</span><span class="sxs-lookup"><span data-stu-id="73b46-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="73b46-102">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73b46-102">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>
* <span data-ttu-id="73b46-103">다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="73b46-103">Run the following command:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages/Movies --referenceScriptLibraries
  ```
  
<span data-ttu-id="73b46-104">오류가 표시될 경우:</span><span class="sxs-lookup"><span data-stu-id="73b46-104">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="73b46-105">프로젝트 디렉터리(*Program.cs*, *Startup.cs* 및 *.csproj* 파일이 포함된 디렉터리)에서 명령 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="73b46-105">Open a command window in the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files).</span></span>