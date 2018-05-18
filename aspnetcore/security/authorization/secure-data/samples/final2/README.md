# <a name="how-to-buildrun-secure-user-data-sample"></a><span data-ttu-id="8b7f0-101">보안 사용자 데이터 샘플을 빌드/실행 하는 방법</span><span class="sxs-lookup"><span data-stu-id="8b7f0-101">How to build/run Secure user data sample</span></span>

* <span data-ttu-id="8b7f0-102">암호 관리자 도구와 함께 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f0-102">Set password with the Secret Manager tool:</span></span>

  `dotnet user-secrets set SeedUserPW <pw>`

* <span data-ttu-id="8b7f0-103">데이터베이스를 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="8b7f0-103">Update the database:</span></span>

    `dotnet ef database update`

* <span data-ttu-id="8b7f0-104">프로젝트에서 SSL을 사용 하도록 설정</span><span class="sxs-lookup"><span data-stu-id="8b7f0-104">Enable SSL in the project</span></span>