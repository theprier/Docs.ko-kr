---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
title: 복구 하 고 암호 (C#) 변경 | Microsoft Docs
author: rick-anderson
description: ASP.NET을 복구 하 고 암호 변경 지원에 대 한 두 개의 웹 컨트롤을 포함 합니다. PasswordRecovery 컨트롤을 사용 하면 그의 손실된 pa를 복구 하는 방문자 중...
ms.author: aspnetcontent
manager: wpickett
ms.date: 04/01/2008
ms.topic: article
ms.assetid: 19c4d042-4e34-4b44-9f1d-6bf2253ba366
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-cs
msc.type: authoredcontent
ms.openlocfilehash: 7f8b019631eff4840bf1759f8e2752946abcaf80
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
ms.locfileid: "30891005"
---
<a name="recovering-and-changing-passwords-c"></a>복구 하 고 암호 (C#) 변경
====================
으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/CS.13.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_cs.pdf)

> ASP.NET을 복구 하 고 암호 변경 지원에 대 한 두 개의 웹 컨트롤을 포함 합니다. PasswordRecovery 컨트롤을 사용 하면 자신의 분실된 한 암호를 복구 하는 방문자입니다. ChangePassword 컨트롤 자신의 암호를 업데이트할 수 있습니다. 이 자습서 시리즈의 PasswordRecovery 전체에서 살펴본 다른 로그인 관련 웹 컨트롤 같이 및 ChangePassword를 멤버 자격 프레임 워크를 다시 설정 하거나 사용자의 암호를 수정 하 여 백그라운드 작업을 제어 합니다.


## <a name="introduction"></a>소개

내 은행, 유틸리티 회사, 회사 전화, 전자 메일 계정 및 개인 설정 된 웹 포털에 대 한 웹 사이트, 사이 I, 대부분의 사용자 많을 기억해 야 할 다른 암호입니다. 이 요즘 외우에 너무 많은 자격 증명이 있는 사용자가 암호를 잊어버릴로 드물지 않습니다. 이를 사용자 계정에 제공 하는 웹 사이트 사용자가 암호를 복구 하는 방법도 포함 해야 합니다. 이 프로세스에는 일반적으로 임의의 암호를 생성 하 고 파일에 대 한 사용자의 전자 메일 주소로 전자 메일 포함 됩니다. 새 암호를 받은 후에 대부분의 사용자가 사이트 돌아가서 기억 하기 쉬운 하나를 임의로 생성 된 것과에서 암호를 변경 합니다.

ASP.NET을 복구 하 고 암호 변경 지원에 대 한 두 개의 웹 컨트롤을 포함 합니다. PasswordRecovery 컨트롤을 사용 하면 자신의 분실된 한 암호를 복구 하는 방문자입니다. ChangePassword 컨트롤 자신의 암호를 업데이트할 수 있습니다. 이 자습서 시리즈의 PasswordRecovery 전체에서 살펴본 다른 로그인 관련 웹 컨트롤 같이 및 ChangePassword를 멤버 자격 프레임 워크를 다시 설정 하거나 사용자의 암호를 수정 하 여 백그라운드 작업을 제어 합니다.

이 자습서에서는이 두 컨트롤을 사용 하 여 살펴보겠습니다. 또한 프로그래밍 방식으로 변경 하 고 통해 사용자의 암호를 재설정 하는 방법을 살펴보겠습니다는 `MembershipUser` 클래스의 `ChangePassword` 및 `ResetPassword` 메서드.

## <a name="step-1-helping-users-recover-lost-passwords"></a>1 단계: 수 있도록 지 원하는 사용자가 복구 암호를 손실

사용자 계정을 지 원하는 모든 웹 사이트 사용자 잊어버린된 암호를 복구 하기 위한 몇 가지 메커니즘에 제공 해야 합니다. 다행히도는 ASP.NET에서 이러한 기능을 구현 PasswordRecovery 웹 컨트롤 덕분에 적합 된다는 점입니다. PasswordRecovery 컨트롤은 자신의 사용자 이름에 대 한 사용자 요청 하는 인터페이스를 렌더링 및 필요에 따라 해당 보안 질문에 대답 합니다. 사용자가 암호 다음 메일 합니다.

> [!NOTE]
> 일반 텍스트에서 통신을 통해 전자 메일 메시지를 전송 하기 때문에 보안 위험이 있습니다 보내는 전자 메일을 통해 사용자의 암호와 관련 된.


세 개의 뷰로 PasswordRecovery 컨트롤 구성 됩니다.

- **사용자 이름** -자신의 사용자 이름에 대 한 방문자 라는 메시지를 표시 합니다. 초기 보기입니다.
- **질문**-사용자의 사용자 이름 및 보안 질문의 보안 질문의 답변을 입력 하는 텍스트 상자가 텍스트를 표시 합니다.
- **성공**-암호를 전자 메일로 전송 된 사용자에 게 알리는 메시지가 표시 됩니다.

보기 표시 하 고 PasswordRecovery 컨트롤에서 수행 하는 작업 다음 구성원 구성 설정에 따라 달라 집니다.

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

멤버 자격 프레임 워크의 `RequiresQuestionAndAnswer` 설정 여부를 사용자 지정 해야 보안 질문 및 대답 계정에 등록 하는 경우를 나타냅니다. 설명한 것 처럼는 <a id="_msoanchor_1"> </a> [ *사용자 계정 만들기* ](../membership/creating-user-accounts-cs.md) 자습서, if `RequiresQuestionAndAnswer` CreateUserWizard의 인터페이스에 텍스트 상자에 포함 되어 있으면 True (기본값) 새 사용자의 보안 질문 및 답변에 대 한 제어 경우 `RequiresQuestionAndAnswer` 가 False 이면 이러한 정보를 수집 하지 합니다. 마찬가지로, 경우 `RequiresQuestionAndAnswer` True 이면 사용자가 자신의 사용자 이름을 입력 한 후 질문 볼 PasswordRecovery 컨트롤 표시 이며 사용자가 올바른 보안 대답을 입력 하는 경우에 암호를 복구 합니다. 그러나 경우 `RequiresQuestionAndAnswer` 가 False 이면 PasswordRecovery 컨트롤이 성공 뷰의 사용자 이름 뷰의에서 직접 이동 합니다.

사용자가 제공 된 자신의 사용자 이름-또는 자신의 사용자 이름 및 보안 대답 하는 경우 후 `RequiresQuestionAndAnswer` 가 True-는 PasswordRecovery 사용자가 암호 전자 메일을 보내는 합니다. 경우는 `EnablePasswordRetrieval` 옵션이 True로 설정 되어 다음 사용자는 현재 암호를 메일로 합니다. False로 설정 된 경우 및 `EnablePasswordReset` PasswordRecovery 컨트롤 사용자에 대해 임의의 암호를 생성 하 고이 새 암호를 해당 전자 메일을 True로 설정 합니다. 두 `EnablePasswordRetrieval` 및 `EnablePasswordReset` false, PasswordRecovery 컨트롤에서 예외가 throw 됩니다.

> [!NOTE]
> 이전에 설명한 대로 `SqlMembershipProvider` 세 가지 형식 중 하나에 사용자의 암호를 저장: 지우기, Hashed (기본값), 또는 암호화 합니다. 구성원 구성 설정;에 사용 되는 저장소 메커니즘에 따라 달라 집니다. 데모 응용 프로그램에는 Hashed 암호 형식을 사용합니다. Hashed 암호 형식을 사용 하는 경우는 `EnablePasswordRetrieval` 시스템 데이터베이스에 저장 된 해시 된 버전에서 사용자의 실제 암호를 확인할 수 없으므로 옵션을 False로 설정 해야 합니다.


그림 1 방법을 PasswordRecovery의 인터페이스 및 동작을 받습니다 등록 구성이 나와 있습니다.


[![RequiresQuestionAndAnswer, EnablePasswordRetrieval, 및 EnablePasswordReset PasswordRecovery 컨트롤의 모양 및 동작에 영향을](recovering-and-changing-passwords-cs/_static/image2.png)](recovering-and-changing-passwords-cs/_static/image1.png)

**그림 1**:는 `RequiresQuestionAndAnswer`, `EnablePasswordRetrieval`, 및 `EnablePasswordReset` PasswordRecovery 컨트롤의 모양 및 동작에 영향을 줍니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image3.png))


> [!NOTE]
> 에 <a id="_msoanchor_2"> </a> [ *SQL Server에서 멤버 자격 스키마 만들기* ](../membership/creating-the-membership-schema-in-sql-server-cs.md) 멤버 자격 공급자를 설정 하 여 구성한 자습서 `RequiresQuestionAndAnswer` True로 `EnablePasswordRetrieval` 를 False 이면 및 `EnablePasswordReset` True로 합니다.


### <a name="using-the-passwordrecovery-control"></a>PasswordRecovery 컨트롤 사용

PasswordRecovery 컨트롤을 사용 하 여 ASP.NET 페이지에서 살펴보겠습니다. 열기 `RecoverPassword.aspx` 및 끌어 및 디자이너 도구 상자에서 PasswordRecovery 컨트롤을 끌어 놓으면; 설정의 `ID` 를 `RecoverPwd`합니다. 로그인 및 CreateUserWizard 웹 컨트롤 같이 PasswordRecovery 컨트롤의 뷰는 레이블, 텍스트 상자, 단추 및 유효성 검사 컨트롤을 포함 하는 풍부한 복합 인터페이스를 렌더링 합니다. 컨트롤의 스타일 속성을 통해 또는 뷰를 템플릿으로 변환 하 여 보기의 모양을 사용자 지정할 수 있습니다. I이 그대로 실행으로 관심된 판독기에 대 한 합니다.

사용자가이 페이지를 방문 그녀의 사용자 이름을 입력 그녀가 고 전송 단추를 클릭 합니다. 설정 때문에 `RequiresQuestionAndAnswer` 속성을 true로 PasswordRecovery 우리의 구성원 구성 설정에서 제어는 다음 질문 보기를 표시 합니다. 사용자가 그녀의 올바른 보안 대답을 입력 하 고 전송을 클릭 한 후 PasswordRecovery 컨트롤에서 임의로 생성 된 쿼리와 사용자의 암호를 업데이트 한이 암호를 파일에 대 한 전자 메일 주소로 전자 메일입니다. 이 한 줄의 코드를 작성할 필요 없이 가능한!

이 페이지를 테스트 하기 전에 구성 하는 경향이의 마지막 부분을 하나 있습니다:에 메일 배달 설정을 지정 해야 `Web.config`합니다. PasswordRecovery 제어는 전자 메일을 전송에 대 한 이러한 설정을 사용 합니다.

메일 배달 구성으로 지정 됩니다는 [ `<system.net>` 요소](https://msdn.microsoft.com/library/6484zdc1.aspx)의 [ `<mailSettings>` 요소](https://msdn.microsoft.com/library/w355a94k.aspx)합니다. 사용 하 여는 [ `<smtp>` 요소](https://msdn.microsoft.com/library/ms164240.aspx) 배달 방법 및 주소에서 기본을 나타냅니다. 다음 태그 라는 네트워크 SMTP 서버를 사용 하도록 메일 설정을 구성 `smtp.example.com` 포트 25와 사용자 이름/암호 자격 증명의 사용자 이름 및 암호를 사용 합니다.

> [!NOTE]
> `<system.net>` 루트의 자식 요소인 `<configuration>` 요소와의 형제 `<system.web>`합니다. 따라서에 두지 마십시오는 `<system.net>` 내의 요소는 `<system.web>` 요소로 대신 같은 수준에 넣습니다.


[!code-xml[Main](recovering-and-changing-passwords-cs/samples/sample1.xml)]

SMTP 서버를 사용 하 여 네트워크를 전자 메일 메시지를 보낼 수를 보관 해야 여기서 픽업 디렉터리를 지정할 수 있습니다.

SMTP 설정을 구성한 경우 참조는 `RecoverPassword.aspx` 브라우저를 통해 페이지입니다. 먼저 사용자 저장소에 존재 하지 않는 사용자 이름을 입력 해 보십시오. 그림 2에서 볼 수 있듯이 PasswordRecovery 컨트롤에 사용자 정보를 액세스할 수 없다는 메시지가 표시 됩니다. 컨트롤의를 통해 메시지의 텍스트를 사용자 지정할 수 있는 [ `UserNameFailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)합니다.


[![잘못 된 사용자 이름을 입력 한 경우 오류 메시지가 표시 됩니다.](recovering-and-changing-passwords-cs/_static/image5.png)](recovering-and-changing-passwords-cs/_static/image4.png)

**그림 2**:에서 잘못 된 사용자 이름을 입력 한 경우는 오류 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image6.png))


이제 사용자 이름을 입력 합니다. 에 액세스할 수 있으며 해당 보안 대답 하면 전자 메일 주소를 사용 하 여 시스템에 있는 계정의 사용자 이름 확인을 사용 합니다. 사용자 이름 입력을 하 고 다음 제출을 클릭 하면 PasswordRecovery 컨트롤 질문 보기를 표시 합니다. 으로 사용자 이름 보기를 입력 하는 경우 잘못 된 응답 PasswordRecovery 컨트롤 표시 되는 경우 오류 메시지 (그림 3 참조). 사용 하 여는 [ `QuestionFailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx) 이 오류 메시지를 사용자 지정할 수 있습니다.


[![사용자가 잘못 된 보안 대답을 입력 하는 경우 오류 메시지가 표시 됩니다.](recovering-and-changing-passwords-cs/_static/image8.png)](recovering-and-changing-passwords-cs/_static/image7.png)

**그림 3**: 사용자가 잘못 된 보안 대답을 입력 하는 경우에 오류 메시지가 표시 됩니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image9.png))


마지막으로, 올바른 보안 대답을 입력 한 다음 제출을 클릭 합니다. 내부적으로 PasswordRecovery 컨트롤 임의의 암호를 생성, 사용자 계정에 지정, 새 암호의 사용자에 게 알리는 전자 메일을 보냅니다 (그림 4 참조) 다음 성공 보기를 표시 합니다.


[![사용자 His 새 암호로 전자 메일 전송](recovering-and-changing-passwords-cs/_static/image11.png)](recovering-and-changing-passwords-cs/_static/image10.png)

**그림 4**: 사용자 전자 메일 His 새 암호와 함께 보내집니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image12.png))


### <a name="customizing-the-email"></a>전자 메일을 사용자 지정

PasswordRecovery 컨트롤에서 보냅니다. 기본 전자 메일이 아니라 두기 위해 (그림 4 참조). 메시지에 지정 된 계정에서 보내는 `<smtp>` 요소의 `from` 주체 암호를 사용 하 여 특성 및 일반 텍스트 본문:

사이트로 돌아가 다음 정보를 사용 하 여 로그인 하십시오.

사용자 이름: *사용자 이름*

암호: *암호*

이 메시지의 프로그래밍 방식으로 사용자 PasswordRecovery 컨트롤에 대 한 이벤트 처리기를 통해 지정할 수 [ `SendingMail` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)를 통해 선언적으로 또는 [ `MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)합니다. 두이 옵션 모두를 살펴보겠습니다.

`SendingMail` 이벤트가 발생 하기 바로 전에 전자 메일 메시지 전송 되 고 프로그래밍 방식으로 전자 메일 메시지를 조정 하려면 마지막 기회입니다. 이 이벤트는 이벤트 처리기 형식의 개체로 전달 됩니다 [ `MailMessageEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx), 해당 `Message` 속성을 보내도록 전자 메일에 대 한 참조를 포함 합니다.

에 대 한 이벤트 처리기를 만들고는 `SendingMail` 이벤트 프로그래밍 방식으로 추가 하는 다음 코드를 추가 하 고 `webmaster@example.com` 참조 목록에 있습니다.

[!code-csharp[Main](recovering-and-changing-passwords-cs/samples/sample2.cs)]

선언적 수단을 통해 전자 메일 메시지를 구성할 수도 있습니다. PasswordRecovery `MailDefinition` 속성은 형식의 개체로 [ `MailDefinition` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)합니다. `MailDefinition` 클래스 전자 메일 관련 속성을 포함 하 여 다 수 제공 `From`, `CC`, `Priority`, `Subject`, `IsBodyHtml`, `BodyFileName`, 등입니다. 먼저 설정 된 [ `Subject` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx) 좀 더 구체적인 암호가 재설정과 같은 (암호)로, 기본적으로 사용 된 것 보다...

별도 전자 메일 템플릿 파일을 만들어야 하는 전자 메일 메시지의 본문을 사용자 지정 하는 본문 내용을 들어 있는입니다. 이라는 웹 사이트에서 새 폴더를 만들어 시작 `EmailTemplates`합니다. 다음으로이 폴더에 새 텍스트 파일을 추가 `PasswordRecovery.txt` 다음 내용을 추가 합니다.

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample3.aspx)]

사용 하 여 자리 표시자 `<%UserName%>` 및 `<%Password%>`합니다. 자동으로 PasswordRecovery 제어는 사용자의 사용자 이름 및 전자 메일을 보내기 전에 복구 암호도 이러한 두 자리 표시자를 바꿉니다.

마지막으로 가리킨는 `MailDefinition`의 [ `BodyFileName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) 방금 만든 메일 템플릿으로 (`~/EmailTemplates/PasswordRecovery.txt`).

이러한 변경한 후 조정 된 `RecoverPassword.aspx` 페이지 및 사용자 이름 및 보안 대답을 입력 합니다. 나타나면 그림 5에 있는 것 처럼 보이는 전자 메일을 해야 합니다. `webmaster@example.com` 참조 하 여 제목 및 본문 업데이트 되었습니다.


[![업데이트 된 제목, 본문 및 참조 목록](recovering-and-changing-passwords-cs/_static/image14.png)](recovering-and-changing-passwords-cs/_static/image13.png)

**그림 5**: 제목, 본문 및 참조 목록 업데이트 되었습니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image15.png))


HTML 형식의 전자 메일을 보내려면 설정 [ `IsBodyHtml` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) True (기본값은 False) 및 전자 메일 템플릿 update HTML을 포함 하도록 합니다.

`MailDefinition` 속성 PasswordRecovery 클래스에 고유 하지 않습니다. ChangePassword 컨트롤에서는 2 단계에서에서 알 수 있듯이 한 `MailDefinition` 속성입니다. CreateUserWizard 컨트롤 이러한 속성을 포함 하는 또한 자동으로 새 사용자에 게 환영 전자 메일 메시지를 보낼 구성할 수 있습니다.

> [!NOTE]
> 현재는 링크가 없는 왼쪽 탐색 창에 연결 하기 위한에서 `RecoverPassword.aspx` 페이지. 사용자가만에 관심을 가질 경우 영업 관리자는 사이트에 성공적으로 로그온 할 수 없습니다.이 페이지를 방문 합니다. 따라서 업데이트는 `Login.aspx` 페이지에 링크를 포함 하는 `RecoverPassword.aspx` 페이지.


### <a name="programmatically-resetting-a-users-password"></a>프로그래밍 방식으로 사용자의 암호를 다시 설정

PasswordRecovery 사용자의 암호를 재설정 호출을 제어 하는 경우는 `MembershipUser` 개체의 [ `ResetPassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)합니다. 이 메서드에 두 개의 오버 로드가 있습니다.

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -사용자의 암호를 다시 설정 합니다. 경우에이 오버 로드를 사용 하 여 `RequiresQuestionAndAnswer` 은 False입니다.
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -사용자의 암호 경우에만 제공 된 기본값으로 다시 설정 *securityAnswer* 올바릅니다. 경우에이 오버 로드를 사용 하 여 `RequiresQuestionAndAnswer` 은 True입니다.

두 오버 로드는 새, 임의로 생성 된 암호를 반환 합니다.

멤버 자격 framework의 다른 메서드와 마찬가지로 `ResetPassword` 메서드 대리자에 구성 된 공급자입니다. `SqlMembershipProvider` 호출는 `aspnet_Membership_ResetPassword` 사용자의 사용자 이름 및 새 암호를 제공 된 암호 대답 다른 필드 사이 전달 프로시저를 저장 합니다. 저장된 프로시저를 수행 하면 암호 대답 일치 하는 사용자의 암호를 업데이트 합니다.

몇 가지 하위 수준 구현 참고 사항:

- 잠긴된 사용자가 암호를 재설정할 수 없습니다. 그러나, 승인 되지 않은 사용자 수 있습니다. 아웃는 잠긴 설명 하 고 승인 상태에서 더 자세하게에서는 <a id="_msoanchor_3"> </a> [ *Unlocking 및 사용자 승인* ](unlocking-and-approving-user-accounts-cs.md) 계정 자습서입니다.
- 암호 대답이 올바르지 않을 경우 사용자의 실패 한 암호 대답 시도 횟수 증가 됩니다. 지정된 된 수의 잘못 된 보안 대답의 입력 시도가 지정된 된 시간 창 내에서 발생 한 경우 사용자는 잠깁니다.

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>단어는 임의 암호 어떻게에 생성 됩니다.

그림 4 및 5에서 전자 메일 메시지에 표시 되는 임의로 생성 된 암호는 멤버 자격 클래스에 의해 작성 [ `GeneratePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)합니다. 이 메서드에 두 개의 정수 입력된 매개 변수- *길이* 및 *numberOfNonAlphanumericCharacters* -적어도 문자열을 반환 하 고 *길이* 에서 오래 문자 최소 *numberOfNonAlphanumericCharacters* 영숫자가 아닌 문자 수입니다. 이러한 두 매개 변수의 값을 멤버 자격 구성에 의해 결정 됩니다 구성원 클래스 또는 로그인 관련 웹 컨트롤 내에서이 메서드를 호출 하면 `MinRequiredPasswordLength` 및 `MinRequiredNonalphanumericCharacters` 각각 7과 1로 설정 하는 속성입니다.

`GeneratePassword` 메서드는 강력 하 게 암호화 난수 생성기를 사용 하 여가 없는 바이어스 어떤 임의 문자를 선택 되도록 합니다. 또한 `GeneratePassword` 은 `public`, 사용할 수 있는 것 ASP.NET 응용 프로그램에서 직접 임의의 문자열 또는 암호를 생성 하는 경우를 의미 합니다.

> [!NOTE]
> `SqlMembershipProvider` 클래스에는 항상 임의의 암호를 생성 하므로, 최소 14 자 `MinRequiredPasswordLength` 보다 작거나 14 한 후 해당 값은 무시 됩니다.


## <a name="step-2-changing-passwords"></a>2 단계: 암호를 변경합니다.

임의로 생성 된 암호는 기억 하기 어렵습니다. 그림 4에 표시 된 암호 고려: `WWGUZv(f2yM:Bd`합니다. 메모리에 커밋 해 보십시오. 물론 사용자 이러한 종류의 임의로 생성 된 암호를 보낸 후에 암호 기억 하기 변경 하려고 수 그녀 있습니다.

암호를 변경 하려면 사용자에 대 한 인터페이스를 만들려면 ChangePassword 컨트롤을 사용 합니다. 훨씬 PasswordRecovery 컨트롤 처럼 ChangePassword 컨트롤 구성 두 뷰의: 암호 변경 및 성공 합니다. 이전 구문과 새 암호에 대 한 라는 메시지를 표시 하는 암호 변경 보기입니다. 올바른 이전 암호 최소 길이 및 영숫자가 아닌 문자를 요구 사항을 충족 하는 새 암호를 제공 시 ChangePassword 컨트롤 사용자의 암호를 업데이트 하 고 성공 보기를 표시 합니다.

> [!NOTE]
> 호출 하 여 사용자의 암호를 수정 하는 암호 변경 제어는 `MembershipUser` 개체의 [ `ChangePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)합니다. ChangePassword 메서드에 두 개의 `string` 입력 매개 변수- *oldPassword* 및 *newPassword*-사용자의 계정을 업데이트 하 고는 *newPassword*, 제공 된 것으로 가정 *oldPassword* 올바릅니다.


열기는 `ChangePassword.aspx` 페이지 이름을 지정 하 고 페이지에 ChangePassword 컨트롤을 추가 하 고 `ChangePwd`합니다. 이 시점에서 디자인 보기 표시 암호 변경 (그림 6 참조)를 확인 합니다. 마찬가지로 PasswordRecovery 컨트롤을 컨트롤의 스마트 태그를 통해 뷰 간에 전환할 수 있습니다. 또한 이러한 보기의이 모양을 다양 한 스타일 속성을 통해 또는 서식 파일을 변환 하 여 사용자 지정할 수 있습니다.


[![페이지에 ChangePassword 컨트롤 추가](recovering-and-changing-passwords-cs/_static/image17.png)](recovering-and-changing-passwords-cs/_static/image16.png)

**그림 6**: ChangePassword 컨트롤을 페이지 추가 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image18.png))


ChangePassword 컨트롤에서 현재 로그인된 한 사용자의 암호를 업데이트할 수 *또는* 다른 사용자가 지정 된 사용자의 암호입니다. 기본 암호 변경 보기 3 개의 TextBox 컨트롤을 렌더링 그림 6에서 볼 수 있듯이: 이전 암호와 새 암호를 두 개에 대 한 합니다. 이 기본 인터페이스는 현재 로그온된 한 사용자의 암호를 업데이트할 사용 됩니다.

다른 사용자의 암호를 업데이트 하려면 ChangePassword 컨트롤을 사용 하려면 컨트롤의 설정 [ `DisplayUserName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx) True로 합니다. 그러면 TextBox 네 번째 메시지를 표시 하는 사용자의 사용자 이름에 대 한 암호 변경 하려면 페이지에 추가 됩니다.

설정 `DisplayUserName` 를 True는 로그인 할 필요 없이 암호를 변경 하는 아웃 로그인 한 사용자 수 있도록 하려는 경우에 유용 합니다. 개인적으로 그녀는 암호를 변경 하는 허용 하기 전에 로그인에 사용자 요구에 잘못 된 것이 생각 합니다. 따라서 둡니다 `DisplayUserName` False (기본값)로 설정 합니다. 그러나이 결정에서는 기본적으로 제한 익명 사용자가이 페이지에 도달 하지 못하도록 합니다. 방문에서 익명 사용자의 거부 하기 위해 사이트의 URL 권한 부여 규칙을 업데이트 `ChangePassword.aspx`합니다. URL 권한 부여 규칙 구문에서 메모리를 새로 고치는 경우에 다시 참조는 <a id="_msoanchor_4"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-cs.md) 자습서입니다.

> [!NOTE]
> 하 게 보일 수는 `DisplayUserName` 속성은 다른 사용자의 암호를 변경 하려면 관리자가 허용 하는 데 유용 합니다. 그러나 경우에 `DisplayUserName` 올바른 이전 암호 알려지고 입력 True로 설정 합니다. 3 단계에서에서 사용자의 암호를 변경 하려면 관리자에 대 한 기술에 대 한 설명 하겠습니다.


방문는 `ChangePassword.aspx` 브라우저를 통해 페이지 하 고 암호를 변경 합니다. 암호 길이 및 구성원 구성에 지정 된 영숫자가 아닌 문자 요구 사항에 맞게 실패 하는 새 암호를 입력 하는 경우 오류 메시지가 표시 됩니다 (그림 7 참조).


[![페이지에 ChangePassword 컨트롤 추가](recovering-and-changing-passwords-cs/_static/image20.png)](recovering-and-changing-passwords-cs/_static/image19.png)

**그림 7**: ChangePassword 컨트롤을 페이지 추가 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image21.png))


올바른 이전 암호와 유효한 새 암호를 로그온 한 사용자의 입력 시 암호가 변경 될 하 고 성공 보기가 표시 됩니다.

### <a name="sending-a-confirmation-email"></a>확인 전자 메일 보내기

기본적으로 ChangePassword 컨트롤 암호 방금 업데이트 된 사용자에 게 전자 메일 메시지를 보내지 않습니다. 컨트롤의 구성 하기만 하면 전자 메일을 보내도록 원하면 `MailDefinition` 속성입니다. 사용자가 새 암호를 포함 하는 HTML 형식의 전자 메일을 전송 되도록 ChangePassword 컨트롤을 구성 해 보겠습니다.

새 파일을 만들어 시작는 `EmailTemplates` 라는 폴더 `ChangePassword.htm`합니다. 다음 태그를 추가 합니다.

[!code-html[Main](recovering-and-changing-passwords-cs/samples/sample4.html)]

다음으로 ChangePassword 컨트롤의 설정 `MailDefinition` 속성의 `BodyFileName`, `IsBodyHtml`, 및 `Subject` 속성을 ~ EmailTemplates/ChangePassword.htm, True 및 암호가 변경 된 /! 각각.

다음과 같이 변경한 후 페이지를 다시 확인 하 고 암호를 다시 변경 합니다. 이 이번에 ChangePassword 제어는 파일에 대 한 사용자의 전자 메일 주소로 사용자 지정, HTML 형식의 전자 메일을 보냅니다 (그림 8 참조).


[![사용자는 해당 암호가 변경 알리는 전자 메일 메시지](recovering-and-changing-passwords-cs/_static/image23.png)](recovering-and-changing-passwords-cs/_static/image22.png)

**그림 8**: 사용자는 해당 암호를 변경한는 전자 메일 메시지에 알립니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image24.png))


## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>3 단계: 사용자의 암호를 변경 하려면 관리자 허용

사용자 계정을 지 원하는 응용 프로그램의 공통 기능이 다른 사용자의 암호를 변경 하기 위해 관리 사용자에 대 한 기능입니다. 경우에 따라 시스템에는 기능을 사용자가 자신의 암호를 변경할 수 없으므로이 기능을 필요. 이러한 경우에는 사용자 잊어버린된 암호를 복구할 수는 유일한 방법은 새 암호를 할당 하려면 관리자에 대 한 것입니다. 그러나 PasswordRecovery 및 ChangePassword 컨트롤이 있는 관리자가 필요 하 고 있지 자체 사용자 암호 변경으로 사용자는이 자체를 수행할 수 있습니다.

하지만 클라이언트 원치 관리자가 다른 사용자의 암호를 변경할 수 있어야 하는 경우에 어떻게? 그러나이 기능을 추가 작업의 비트 수 있습니다. 사용자의 암호를 변경 하려면 기존 패턴과 새 암호를 제공 해야는 `MembershipUser` 개체의 `ChangePassword` 메서드이지만 관리자가 수정 하기 위해 사용자의 암호를 알 필요가 없어야 합니다.

한 가지 해결 방법은 먼저 사용자의 암호 다시 설정 하 여 다음 다음과 같은 코드를 사용 하 여 새 암호를 변경 하는 것입니다.

[!code-aspx[Main](recovering-and-changing-passwords-cs/samples/sample5.aspx)]

이 코드에 대 한 정보를 검색 하 여 시작 *username*, 암호 변경 하려면 관리자가 사용자 변수인 합니다. 다음으로 `ResetPassword` 메서드가 호출 되는 할당 및 임의의 암호가 사용자. 이 임의로 생성 된 암호 메서드에 의해 반환 되며 변수에 저장 된 `resetPwd`합니다. 사용자의 암호를 알았으므로 호출을 통해 변경할 수 있습니다 `ChangePassword`합니다.

이 문제는 멤버 자격 시스템 구성이 설정 된 경우이 코드만 작동 한다는 되도록 `RequiresQuestionAndAnswer` 은 False입니다. 경우 `RequiresQuestionAndAnswer` 샘플 응용 프로그램은 True 이면 하면 `ResetPassword` 메서드를 보안 대답 전달 해야 합니다., 그렇지 않으면 예외가 throw 됩니다.

멤버 자격 프레임 워크는 보안 질문 및 대답을 요구 하도록 구성 된 경우 클라이언트 관리자가 사용자의 암호를 변경할 수 원치 아직 세 가지 옵션이 있습니다.

- 손으로 분위기에서 throw 하 고 클라이언트에 하나만 수행할 수 없는 것입니다.
- 설정 `RequiresQuestionAndAnswer` 를 False입니다. 이 인해 덜 안전한 응용 프로그램입니다. 악의적인 사용자가 다른 사용자의 전자 메일 받은 편지함에 대 한 액세스를 통해 얻은 한다고 가정 합니다. 아마도 손상 된 사용자 들이 책상 앞 런치 돌아가려면 없어진 및 자신의 워크스테이션 잠금 하지 않은 또는 공용 터미널에서 자신의 전자 메일에 액세스 및 로그 아웃 하지 않은 있음. 두 경우 모두, 악의적인 사용자가 방문할 수 있는 `RecoverPassword.aspx` 페이지 및 사용자의 사용자 이름을 입력 합니다. 시스템 보안 대답에 대 한 메시지를 표시 하지 않고 복구 암호를 메일로 다음 전송 됩니다.
- 멤버 자격 프레임 워크 및 SQL Server 데이터베이스와 직접 작업에서 만든 추상화 계층을 무시 합니다. 라는 이름의 저장된 프로시저를 포함 하는 멤버 자격 스키마 `aspnet_Membership_SetPassword` 사용자의 암호를 설정 하 고 해당 작업을 수행 하기 위해 보안 대답 나 이전 암호를 필요 하지 않습니다.

이러한 옵션은 특히 매력적인 수 있지만 개발자의 일상 때로는 이동.

했 고 무시 하는 코드를 작성 세 번째 접근 방식을 구현 하려면는 `Membership` 및 `MembershipUser` 에 대해 직접 동작 및 클래스는 `SecurityTutorials` 데이터베이스입니다.

> [!NOTE]
> 데이터베이스와 직접 작업을 하 여 멤버 자격 프레임 워크에서 제공 하는 캡슐화가 파괴 합니다. 이 결정을 연결 하는 `SqlMembershipProvider`, portable 덜 코드 만들기. 또한이 코드 멤버 자격 스키마 변경 되 면 버전의 ASP.NET 나중에 예상 대로 작동 하지 않을 수 있습니다. 이 방법은 문제를 해결 하며, 대부분의 대안 같은 하지 최선의 구현 방법의 예가 합니다.


코드 몇 가지 이상한 비트 고 매우 긴입니다. 따라서 자세하게 살펴보는와이 자습서에서는 공간을 차지 하지 않는 하겠습니다. 더 자세히 알고 싶은 경우 방문 하 고이 자습서에 대 한 코드를 다운로드는 `~/Administration/ManageUsers.aspx` 페이지. 만든이 페이지는 <a id="_msoanchor_5"> </a> [이전 자습서](building-an-interface-to-select-one-user-account-from-many-cs.md), 각 사용자를 나열 합니다. GridView에 대 한 링크를 포함 하도록 업데이트는 `UserInformation.aspx` 페이지에서 선택한 사용자의 사용자는 쿼리 문자열을 통해 전달 합니다. `UserInformation.aspx` 자신의 암호를 변경 하는 데는 선택한 사용자 및 텍스트 상자에 대 한 정보 페이지에 표시 됩니다 (그림 9 참조).

포스트백 계속 후 새 암호를 입력 합니다. 두 번째 텍스트 상자에 확인 하 고 업데이트 사용자 단추를 클릭 하 고 `aspnet_Membership_SetPassword` 저장된 프로시저가 호출 되는 사용자의 암호를 업데이트 합니다. 코드에 대해 암호를 변경한 사용자에 게 전자 메일을 보낼 기능 확장을이 기능에 관심이 알고 싶은 확인해 합니다.


[![관리자는 사용자의 암호를 변경할 수 있습니다.](recovering-and-changing-passwords-cs/_static/image26.png)](recovering-and-changing-passwords-cs/_static/image25.png)

**그림 9**: 관리자가 사용자의 암호를 변경 될 수 있습니다 ([전체 크기 이미지를 보려면 클릭](recovering-and-changing-passwords-cs/_static/image27.png))


> [!NOTE]
> `UserInformation.aspx` 구성원 프레임 워크 일반 또는 Hashed 형식에 암호를 저장 하도록 구성 된 경우에 대해서만 작동 현재 페이지입니다. 이 기능을 추가 하도록 초대 있지만 새 암호를 암호화 하는 코드를 부족 합니다. 같은 디컴파일러를 사용 하는 데 필요한 코드를 추가 하는 방법은 것 [Reflector](http://www.aisto.com/roeder/dotnet/) 않으며.NET Framework의 메서드에 대 한 소스 코드를 검사를 검사 하 여 시작는 `SqlMembershipProvider` 클래스의 `ChangePassword` 메서드. 이 I 암호의 해시를 만들기 위한 코드를 작성 하는 데 사용 하는 방법입니다.


## <a name="summary"></a>요약

ASP.NET은 사용자가 암호를 관리할 수 있도록 두 개의 컨트롤을 제공 합니다. PasswordRecovery 컨트롤은 자신의 암호를 잊은 사용자에 게 유용 합니다. 멤버 자격 프레임 워크의 구성에 따라 사용자는 기존 암호 또는 임의로 생성 된 새 메일로 중 하나입니다. ChangePassword 컨트롤을 사용 하면 사용자가 암호를 업데이트할 수 있습니다.

로그인 및 CreateUserWizard 컨트롤 같이 PasswordRecovery 및 ChangePassword 컨트롤 전혀 선언 태그 또는 줄의 코드를 작성 하지 않고도 다양 한 사용자 인터페이스를 렌더링 합니다. 기본 사용자 인터페이스 요구 사항을 만족 하지 않는 경우에 다양 한 스타일 속성을 통해 사용자 지정할 수 있습니다. 또는 컨트롤의 인터페이스는 훨씬 더 세밀 일정 정도의 제어를 템플릿으로 변환 될 수 있습니다. 원리를 자세히 파악할수록 이러한 컨트롤 사용 하 여 멤버 API를 호출 하는 `MembershipUser` 개체의 `ResetPassword` 및 `ChangePassword` 메서드.

만족도 매우 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에 설명 된 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ChangePassword 제어 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery 제어 퀵 스타트](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [ASP.NET에서 메일을 보내는 중](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` Faq](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>작성자 정보

여러 ASP/ASP.NET 책의 작성자 및 4GuysFromRolla.com의 창립자 Scott Mitchell의 근무 기간이 Microsoft 웹 기술을 1998 이후입니다. Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다. 그의 최신 서적은  *[Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 또는에서 그의 블로그 통해 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈 많은 유용한 검토자가 검토 합니다. 이 자습서에 대 한 선행 검토자 Michael Emmings 및 Suchi Banerjee 포함 됩니다. 향후 내 MSDN 문서를 검토에 관심이 있으십니까? 이 경우 drop me에 한 줄씩 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](building-an-interface-to-select-one-user-account-from-many-cs.md)
> [다음](unlocking-and-approving-user-accounts-cs.md)
