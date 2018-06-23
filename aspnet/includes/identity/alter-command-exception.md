> 일부 명령은 응용 프로그램 Id 데이터 저장소로 SQLite를 사용 하는 경우 지원 되지 않습니다. 데이터베이스 엔진의 제한으로 인해 `Alter` 명령을 다음과 같은 예외를 throw 합니다.
>
> "System.NotSupportedException: SQLite이 마이그레이션 작업을 지원 하지 않습니다." 
>
> 해결 방법으로, 테이블을 변경 하려면 데이터베이스에서 Code First 마이그레이션 실행 합니다.
