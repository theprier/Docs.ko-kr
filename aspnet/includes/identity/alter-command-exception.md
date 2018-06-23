> <span data-ttu-id="b5c01-101">일부 명령은 응용 프로그램 Id 데이터 저장소로 SQLite를 사용 하는 경우 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b5c01-101">Some commands aren't supported if the app uses SQLite as its Identity data store.</span></span> <span data-ttu-id="b5c01-102">데이터베이스 엔진의 제한으로 인해 `Alter` 명령을 다음과 같은 예외를 throw 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c01-102">Due to limitations in the database engine, `Alter` commands throw the following exception:</span></span>
>
> <span data-ttu-id="b5c01-103">"System.NotSupportedException: SQLite이 마이그레이션 작업을 지원 하지 않습니다."</span><span class="sxs-lookup"><span data-stu-id="b5c01-103">"System.NotSupportedException: SQLite does not support this migration operation."</span></span> 
>
> <span data-ttu-id="b5c01-104">해결 방법으로, 테이블을 변경 하려면 데이터베이스에서 Code First 마이그레이션 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b5c01-104">As a work around, run Code First migrations on the database to change the tables.</span></span>
