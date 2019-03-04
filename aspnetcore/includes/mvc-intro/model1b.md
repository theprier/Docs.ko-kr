`Movie` 클래스에 다음 속성을 추가합니다.

[!code-csharp[](~/tutorials/first-mvc-app/start-mvc/sample/MvcMovie22/Models/Movie.cs?name=snippet1)]

`Movie` 클래스에는 다음이 포함됩니다.

* 기본 키에 대해 데이터베이스가 요구하는 `Id` 필드입니다.
* `[DataType(DataType.Date)]`:  [DataType](/dotnet/api/microsoft.aspnetcore.mvc.dataannotations.internal.datatypeattributeadapter) 특성은 데이터 형식(`Date`)을 지정합니다. 이 특성 사용:

  * 사용자는 날짜 필드에 시간 정보를 입력할 필요가 없습니다.
  * 시간 정보가 아니라 날짜만 표시됩니다.

[DataAnnotations](/dotnet/api/system.componentmodel.dataannotations)는 이후 자습서에서 다룹니다.