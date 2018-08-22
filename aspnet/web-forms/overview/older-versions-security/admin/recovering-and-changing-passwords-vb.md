---
uid: web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
title: 복구 암호 및 변경 (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET 지원 암호 복구 및 변경 하기 위한 두 개의 웹 컨트롤을 포함 합니다. PasswordRecovery 컨트롤을 사용 하면 방문자가 손실된 pa를 복구 하는 중...
ms.author: riande
ms.date: 04/01/2008
ms.assetid: f9adcb5d-6d70-4885-a3bf-ed95efb4da1a
msc.legacyurl: /web-forms/overview/older-versions-security/admin/recovering-and-changing-passwords-vb
msc.type: authoredcontent
ms.openlocfilehash: c60433f800ccb2dbaaae49421c6cde1431fef528
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "41828341"
---
<a name="recovering-and-changing-passwords-vb"></a>복구 암호 및 변경 (VB)
====================
[Scott Mitchell](https://twitter.com/ScottOnWriting)

[코드를 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/VB.13.zip) 또는 [PDF 다운로드](http://download.microsoft.com/download/6/0/e/60e1bd94-e5f9-4d5a-a079-f23c98f4f67d/aspnet_tutorial13_ChangingPasswords_vb.pdf)

> ASP.NET 지원 암호 복구 및 변경 하기 위한 두 개의 웹 컨트롤을 포함 합니다. PasswordRecovery 컨트롤 방문자를 분실된 한 암호를 복구할 수 있습니다. ChangePassword 컨트롤을 사용 하면 자신의 암호를 업데이트할 수 있습니다. 이 자습서 시리즈의 PasswordRecovery 전체 살펴본 다른 로그인 관련 웹 컨트롤과 같은 및 ChangePassword를 재설정 하거나 사용자의 암호를 수정할 백그라운드에서 멤버 자격 프레임 워크를 사용 하 여 작업을 제어 합니다.


## <a name="introduction"></a>소개

내 은행, 유틸리티 회사, 전화 회사, 메일 계정 및 개인 설정 된 웹 포털에 대 한 웹 사이트 간의 I, 대부분의 사용자가 기억해 야 할 다른 암호의입니다. 이 요즘 기억 하는 많은 자격 증명을 사용 하 여 사용자가 자신의 암호를 잊어 일반적이 지 않은 아닙니다. 이 위해서 사용자 계정을 제공 하는 웹 사이트 사용자가 자신의 암호를 복구 하는 방법이 포함 해야 합니다. 이 프로세스는 일반적으로 임의의 암호를 생성 하 고 전자 메일로 보내거나 파일에서 사용자의 전자 메일 주소를 포함 합니다. 새 암호를 받은 후에 대부분의 사용자 사이트 돌아가서 기억 하기 쉬운 단일을 임의로 생성 된 것에서 자신의 암호를 변경 합니다.

ASP.NET 지원 암호 복구 및 변경 하기 위한 두 개의 웹 컨트롤을 포함 합니다. PasswordRecovery 컨트롤 방문자를 분실된 한 암호를 복구할 수 있습니다. ChangePassword 컨트롤을 사용 하면 자신의 암호를 업데이트할 수 있습니다. 이 자습서 시리즈의 PasswordRecovery 전체 살펴본 다른 로그인 관련 웹 컨트롤과 같은 및 ChangePassword를 재설정 하거나 사용자의 암호를 수정할 백그라운드에서 멤버 자격 프레임 워크를 사용 하 여 작업을 제어 합니다.

이 자습서에서는이 두 컨트롤을 사용 하 여 살펴보겠습니다. 또한 프로그래밍 방식으로 변경 하 고를 통해 사용자의 암호를 재설정 하는 방법을 살펴보겠습니다 합니다 `MembershipUser` 클래스의 `ChangePassword` 고 `ResetPassword` 메서드.

## <a name="step-1-helping-users-recover-lost-passwords"></a>1 단계: 수 있도록 사용자가 복구 암호 손실

사용자 계정을 지 원하는 모든 웹 사이트 사용자가 잊어버린된 자신의 암호를 복구 하기 위한 메커니즘을 사용 하 여 제공 해야 합니다. 좋은 소식은 ASP.NET에서 이러한 기능을 구현 하는 방법은 PasswordRecovery 웹 컨트롤 덕분입니다. PasswordRecovery 컨트롤 렌더링 자신의 사용자 이름을 묻는 하는 인터페이스 및 필요에 따라 해당 보안 질문에 대답 합니다. 사용자 암호가 다음 이메일입니다.

> [!NOTE]
> 없기 때문에 일반 텍스트로 네트워크를 통해 전자 메일 메시지는 전송 보안 위험 보내는 전자 메일을 통해 사용자의 암호와 관련 된.


PasswordRecovery 컨트롤이 세 가지 뷰가 이루어져 있습니다.

- **사용자 이름** -사용자 이름에 대 한 방문자를 라는 메시지가 표시 됩니다. 초기 보기입니다.
- **질문**-사용자의 사용자 이름 및 보안 질문의 사용자가 보안 질문에 대 한 답을 입력 하는 텍스트 상자가 함께 텍스트를 표시 합니다.
- **성공**-자신의 암호를 전자 메일로 보냈습니다는 사용자에 게 알리는 메시지를 표시 합니다.

뷰를 표시 하 고 다음 멤버 자격 구성 설정에 따라 PasswordRecovery 컨트롤에서 수행 하는 작업에 따라 달라 집니다.

- `RequiresQuestionAndAnswer`
- `EnablePasswordRetrieval`
- `EnablePasswordReset`

멤버 자격 프레임 워크의 `RequiresQuestionAndAnswer` 설정 여부를 사용자 지정 해야 합니다 보안 질문 및 대답을 계정을 등록 하는 경우를 나타냅니다. 설명한 대로 합니다 <a id="_msoanchor_1"> </a> [ *사용자 계정 만들기* ](../membership/creating-user-accounts-vb.md) 자습서, 경우 `RequiresQuestionAndAnswer` CreateUserWizard의 인터페이스에 텍스트를 포함 하는 다음이 True (기본값) 새 사용자의 보안 질문 및 답변에 대 한 제어 경우 `RequiresQuestionAndAnswer` False는 해당 정보가 없으면 수집 됩니다. 마찬가지로, 경우 `RequiresQuestionAndAnswer` True 이면 사용자가 자신의 사용자 이름을 입력 한 후 질문 보기 PasswordRecovery 컨트롤 표시; 사용자가 올바른 보안 대답을 입력 하는 경우에 암호를 복구 합니다. 그러나 경우 `RequiresQuestionAndAnswer` False PasswordRecovery 컨트롤 성공 뷰에 사용자 이름 보기에서 바로 이동 합니다.입니다.

사용자가 제공한 이름을-또는 자신의 사용자 이름 및 보안 대답 하는 경우 후 `RequiresQuestionAndAnswer` 는 PasswordRecovery True-는 사용자가 자신의 암호를 전자 메일입니다. 경우는 `EnablePasswordRetrieval` 옵션이 True로 설정 되어 다음 사용자는 현재 암호를 전자 메일로 전달 합니다. False로 설정 된 경우 및 `EnablePasswordReset` PasswordRecovery 컨트롤 사용자에 대해 임의의 암호를 생성 하 고이 새 암호를 전자 메일을 True로 설정 됩니다. 둘 다 `EnablePasswordRetrieval` 고 `EnablePasswordReset` false, PasswordRecovery 컨트롤 예외를 throw 합니다.

> [!NOTE]
> 이전에 설명한 대로 `SqlMembershipProvider` 세 가지 형식 중 하나에 사용자의 암호를 저장 합니다: Clear, Hashed (기본값) 또는 암호화 합니다. 멤버 자격 구성 설정을;에 사용 되는 저장소 메커니즘에 따라 달라 집니다. 데모 응용 프로그램 Hashed 암호 형식을 사용 합니다. Hashed 암호 형식을 사용 하는 경우는 `EnablePasswordRetrieval` 시스템 데이터베이스에 저장 된 해시 된 버전에서 사용자의 실제 암호를 확인할 수 없으므로 옵션이 False로 설정 되어야 합니다.


그림 1에서는 어떻게 PasswordRecovery의 인터페이스 및 동작의 영향을 받습니다 멤버 자격 구성을 보여 줍니다.


[![RequiresQuestionAndAnswer, EnablePasswordRetrieval, 및 EnablePasswordReset PasswordRecovery 컨트롤의 모양 및 동작에 영향을](recovering-and-changing-passwords-vb/_static/image2.png)](recovering-and-changing-passwords-vb/_static/image1.png)

**그림 1**: 합니다 `RequiresQuestionAndAnswer`를 `EnablePasswordRetrieval`, 및 `EnablePasswordReset` PasswordRecovery 컨트롤의 모양 및 동작에 영향을 줄 ([클릭 하 여 큰 이미지 보기](recovering-and-changing-passwords-vb/_static/image3.png))


> [!NOTE]
> 에 <a id="_msoanchor_2"> </a> [ *SQL Server에서 멤버 자격 스키마 만들기* ](../membership/creating-the-membership-schema-in-sql-server-vb.md) 자습서 설정 하 여 멤버 자격 공급자를 구성 했습니다 `RequiresQuestionAndAnswer` True로 `EnablePasswordRetrieval` 를 False 이면 및 `EnablePasswordReset` True로 합니다.


### <a name="using-the-passwordrecovery-control"></a>PasswordRecovery 컨트롤 사용

PasswordRecovery 컨트롤을 사용 하 여 ASP.NET 페이지에서 살펴보겠습니다. 오픈 `RecoverPassword.aspx` 끌어 및 PasswordRecovery 컨트롤 디자이너 도구 상자에서 삭제 하 고 설정 해당 `ID` 에 `RecoverPwd`입니다. 로그인 및 CreateUserWizard 웹 컨트롤과 같은 PasswordRecovery 컨트롤의 뷰는 레이블, 텍스트 상자, 단추 및 유효성 검사 컨트롤을 포함 하는 풍부한 복합 인터페이스를 렌더링 합니다. 컨트롤의 스타일 속성을 통해 또는 보기 템플릿을 변환 하 여 보기의 모양을 사용자 지정할 수 있습니다. I 관심이 있는 독자를 연습으로 둡니다.

사용자가이 페이지를 방문할 때 그녀가 자신의 사용자 이름을 입력 되며 전송 단추를 클릭 합니다. 설정한 때문에 `RequiresQuestionAndAnswer` 멤버 자격 구성 설정에는 PasswordRecovery에서 True로 속성은 컨트롤을 질문 뷰를 표시 합니다. 사용자가 올바른 보안 대답을 입력 하 고 제출 클릭, PasswordRecovery 컨트롤은 사용자의 암호를 임의로 생성 된 단일 업데이트 후이 암호 파일에서 전자 메일 주소로 전자 메일. 이 모든 된 코드를 전혀 작성할 필요 없이 가능!

마지막 조각이 경향이 구성의는이 페이지를 테스트 하기 전에:의 메일 배달 설정을 지정 해야 `Web.config`합니다. PasswordRecovery 컨트롤 전자 메일을 전송 하는 것에 대 한 이러한 설정을 사용 합니다.

메일 배달 구성 통해 지정 되는 [ `<system.net>` 요소](https://msdn.microsoft.com/library/6484zdc1.aspx)의 [ `<mailSettings>` 요소](https://msdn.microsoft.com/library/w355a94k.aspx)합니다. 사용 합니다 [ `<smtp>` 요소](https://msdn.microsoft.com/library/ms164240.aspx) 배달 방법 및 기본 주소를 나타냅니다. 다음 태그는 명명 된 네트워크 SMTP 서버를 사용 하도록 메일 설정을 구성 `smtp.example.com` 포트 25에 사용자 이름 및 암호의 사용자 이름/암호 자격 증명을 사용 합니다.

> [!NOTE]
> `<system.net>` 루트의 자식 요소인 `<configuration>` 요소와의 형제 `<system.web>`합니다. 따라서에 두지 마십시오 합니다 `<system.net>` 내의 요소는 `<system.web>` 요소 대신 같은 수준에 넣습니다.


[!code-xml[Main](recovering-and-changing-passwords-vb/samples/sample1.xml)]

SMTP 서버에서 네트워크를 사용 하는 것 외에도 보낼 전자 메일 메시지를 보관 해야 여기서 픽업 디렉터리를 지정할 수 있습니다.

SMTP 설정을 구성한 경우, 참조는 `RecoverPassword.aspx` 브라우저를 통해 페이지입니다. 먼저 사용자 저장소에 존재 하지 않는 사용자 이름을 입력 하십시오. 그림 2에서 알 수 있듯이, PasswordRecovery 컨트롤 사용자 정보를 액세스할 수 있는지를 나타내는 메시지를 표시 합니다. 컨트롤을 통해 메시지의 텍스트를 사용자 지정할 수 있습니다 [ `UserNameFailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.usernamefailuretext.aspx)합니다.


[![잘못 된 사용자 이름을 입력 한 경우 오류 메시지가 표시 됩니다.](recovering-and-changing-passwords-vb/_static/image5.png)](recovering-and-changing-passwords-vb/_static/image4.png)

**그림 2**:는 잘못 된 사용자 이름을 입력 하는 경우는 오류 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image6.png))


이제 사용자 이름을 입력 합니다. 액세스할 수 있으며 해당 보안 대답 하는 전자 메일 주소를 사용 하 여 시스템에서 계정의 사용자 이름을 알고 사용 합니다. 사용자 이름을 입력 하 고 제출을 클릭 하면, PasswordRecovery 컨트롤의 질문 뷰를 표시 합니다. 으로 사용자 이름 뷰를 사용 하 여 입력 하는 경우 잘못 된 응답 PasswordRecovery 컨트롤 표시 됩니다 (그림 3 참조)는 오류 메시지. 사용 된 [ `QuestionFailureText` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.questionfailuretext.aspx) 이 오류 메시지를 사용자 지정할 수 있습니다.


[![사용자가 잘못 된 보안 대답을 입력 하는 경우 오류 메시지가 표시 됩니다.](recovering-and-changing-passwords-vb/_static/image8.png)](recovering-and-changing-passwords-vb/_static/image7.png)

**그림 3**: 사용자가 잘못 된 보안 대답을 입력 하는 경우는 오류 메시지가 표시 됩니다 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image9.png))


마지막으로 올바른 보안 대답을 입력 하 고 제출을 클릭 합니다. 내부적으로 PasswordRecovery 컨트롤 임의의 암호를 생성, 사용자 계정에 할당, 새 암호의 사용자에 게 알리는 전자 메일을 보냅니다 (그림 4 참조) 한 후 성공 뷰에 표시 합니다.


[![His 새 암호를 사용 하 여 전자 메일을 사용자에 게 보내기](recovering-and-changing-passwords-vb/_static/image11.png)](recovering-and-changing-passwords-vb/_static/image10.png)

**그림 4**: 사용자는 His 새 암호를 사용 하 여 전자 메일이 전송 됩니다 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image12.png))


### <a name="customizing-the-email"></a>전자 메일을 사용자 지정

PasswordRecovery 컨트롤에서 보낸 기본 전자 메일은 대신 두기 (그림 4 참조). 에 지정 된 계정에서 전송 되는 `<smtp>` 요소의 `from` 주체 암호를 사용 하 여 특성 및 일반 텍스트 본문:

사이트에 반환 하 고 다음 정보를 사용 하 여 로그인 하세요.

사용자 이름: *사용자 이름*

암호: *암호*

이 메시지의 프로그래밍 방식으로 사용자 PasswordRecovery 컨트롤에 대 한 이벤트 처리기를 통해 지정할 수 [ `SendingMail` 이벤트](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.sendingmail.aspx)를 통해 선언적으로 또는 합니다 [ `MailDefinition` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.passwordrecovery.maildefinition.aspx)합니다. 두이 옵션 모두를 살펴보겠습니다.

`SendingMail` 이벤트가 발생 하기 직전의 전자 메일 메시지가 전송 되 고 프로그래밍 방식으로 전자 메일 메시지를 조정 하려면 마지막 기회입니다. 이 이벤트는 이벤트 처리기 형식의 개체로 전달 됩니다 [ `MailMessageEventArgs` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.mailmessageeventargs.aspx)해당 `Message` 속성 전송 될 전자 메일에 대 한 참조를 포함 합니다.

이벤트 처리기를 만듭니다는 `SendingMail` 이벤트 프로그래밍 방식으로 추가 하는 다음 코드를 추가 하 고 `webmaster@example.com` 참조 목록에 있습니다.

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample2.vb)]

선언적 수단을 통해 전자 메일 메시지를 구성할 수도 있습니다. PasswordRecovery `MailDefinition` 속성은 형식의 개체로 [ `MailDefinition` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.aspx)합니다. `MailDefinition` 클래스를 비롯 한 전자 메일 관련 속성을 제공 `From`, `CC`, `Priority`를 `Subject`를 `IsBodyHtml`, `BodyFileName`, 등입니다. 먼저 설정 합니다 [ `Subject` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.subject.aspx) 사용자 암호가 재설정 되었습니다. 같은 (암호)를 기본적으로 사용 되는 것 보다 이해 하기 쉬운...

별도 전자 메일 템플릿 파일을 만들려면 먼저 전자 메일 메시지의 본문을 사용자 지정 하는 본문의 내용을 포함 하는 합니다. 라는 웹 사이트에 새 폴더를 만들어 시작 `EmailTemplates`합니다. 다음으로,이 폴더에 새 텍스트 파일을 추가 `PasswordRecovery.txt` 다음 콘텐츠를 추가 합니다.

[!code-aspx[Main](recovering-and-changing-passwords-vb/samples/sample3.aspx)]

자리 표시자를 사용 하 여 `<%UserName%>` 고 `<%Password%>`입니다. PasswordRecovery 컨트롤이 자동으로 사용자의 사용자 이름 및 전자 메일을 보내기 전에 복구 암호를 사용 하 여 이러한 두 명의 자리 표시자를 바꿉니다.

마지막으로 가리킨 합니다 `MailDefinition`의 [ `BodyFileName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) 방금 만든 메일 템플릿의 (`~/EmailTemplates/PasswordRecovery.txt`).

이러한 변경한 후 다시 방문은 `RecoverPassword.aspx` 페이지 및 사용자 이름 및 보안 대답을 입력 합니다. 받게 그림 5의 것 처럼 보이는 전자 메일을 해야 합니다. `webmaster@example.com` 및 참조 하 고 제목 및 본문 업데이트 되었습니다.


[![제목, 본문 및 참조 목록 업데이트 되었습니다.](recovering-and-changing-passwords-vb/_static/image14.png)](recovering-and-changing-passwords-vb/_static/image13.png)

**그림 5**: The Subject, Body 및 참조 목록 업데이트 되었습니다 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image15.png))


HTML 형식의 전자 메일을 보내도록 설정할 [ `IsBodyHtml` ](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.isbodyhtml.aspx) to True (기본값은 False) 및 업데이트 전자 메일 템플릿 HTML을 포함 합니다.

`MailDefinition` 속성 PasswordRecovery 클래스에 고유 하지 않습니다. 2 단계에서에서 살펴볼 ChangePassword 컨트롤 제공을 `MailDefinition` 속성입니다. CreateUserWizard 컨트롤 이러한 속성을 포함 하는 또한 새 사용자에 게 환영 전자 메일 메시지를 자동으로 보내도록 구성할 수 있습니다.

> [!NOTE]
> 현재는 링크가 없습니다에 도달 하는 것에 대 한 왼쪽 탐색 창에서 `RecoverPassword.aspx` 페이지입니다. 사용자만 이라면 그녀에서 사이트에 성공적으로 로그온 할 수 없는 경우이 페이지를 방문 합니다. 따라서 업데이트를 `Login.aspx` 페이지에 대 한 링크를 포함 하는 `RecoverPassword.aspx` 페이지입니다.


### <a name="programmatically-resetting-a-users-password"></a>프로그래밍 방식으로 사용자의 암호를 다시 설정

사용자의 암호를 PasswordRecovery 재설정 호출을 제어 하는 경우는 `MembershipUser` 개체의 [ `ResetPassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.resetpassword.aspx)합니다. 이 메서드에 두 개의 오버 로드가 있습니다.

- **[`ResetPassword`](https://msdn.microsoft.com/library/d94bdzz2.aspx)** -사용자의 암호를 다시 설정 합니다. 경우에이 오버 로드를 사용 하 여 `RequiresQuestionAndAnswer` 은 False입니다.
- **[`ResetPassword(securityAnswer)`](https://msdn.microsoft.com/library/d90zte4w.aspx)** -사용자의 암호 경우에만 제공 된 다시 설정 *securityAnswer* 정확 합니다. 경우에이 오버 로드를 사용 하 여 `RequiresQuestionAndAnswer` 은 True입니다.

두 오버 로드는 임의로 생성 되 고에 새 암호를 반환합니다.

멤버 자격 프레임 워크의 다른 메서드를 사용 하 여 같은 `ResetPassword` 구성 된 공급자 메서드 대리자입니다. `SqlMembershipProvider` 호출을 `aspnet_Membership_ResetPassword` 의 저장 프로시저에 전달 사용자의 사용자 이름 및 새 암호를 다른 필드 간에 제공 된 암호 대답입니다. 저장된 프로시저의 암호 대답 일치 하 고 사용자의 암호를 업데이트 한 다음 확인 합니다.

몇 가지 하위 수준 구현 참고 사항:

- 잠긴된 사용자는 자신의 암호를 재설정할 수 없습니다. 그러나 승인 되지 않은 사용자는 다음과 같은 작업을 할 수 있습니다. 잠긴를 설명 하 고 승인 상태에서 더 자세히 합니다 <a id="_msoanchor_3"> </a> [ *Unlocking 및 사용자 승인* ](unlocking-and-approving-user-accounts-vb.md) 계정 자습서입니다.
- 암호 대답 올바르지 않으면, 사용자의 실패 한 암호 대답 시도 횟수는 증가 합니다. 지정된 된 수의 잘못 된 보안 대답의 입력 시도가 지정된 된 시간 창 내에서 발생 하는 경우 사용자가 잠겼습니다.

### <a name="a-word-on-how-the-random-passwords-are-generated"></a>단어 하는 방법의 임의 암호 생성

그림 4 및 5에서 전자 메일 메시지에 표시 되는 임의로 생성 된 암호 구성원 클래스에 의해 만들어집니다 [ `GeneratePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)합니다. 이 메서드는 두 개의 정수 입력된 매개 변수- *길이* 하 고 *numberOfNonAlphanumericCharacters* -적어도 문자열을 반환 하 고 *길이* 에서 사용 하 여 긴 문자 최소 *numberOfNonAlphanumericCharacters* 영숫자가 아닌 문자 수입니다. 이러한 두 매개 변수에 대 한 값 멤버 자격 구성에 의해 결정 됩니다 웹 로그인 관련 컨트롤을 멤버 자격 클래스 내에서이 메서드가 호출 되 면 `MinRequiredPasswordLength` 및 `MinRequiredNonalphanumericCharacters` 각각 7과 1로 설정 하는 속성입니다.

`GeneratePassword` 메서드는 암호화 된 강력한 난수 생성기를 사용 하 여 어떤 임의 문자를 선택 하는 데 없는 바이어스 있는지 확인 합니다. 게다가 `GeneratePassword` 는 `Public`를 사용할 수 있는 ASP.NET 응용 프로그램에서 직접 임의 문자열이 나 암호를 생성 하는 경우를 의미 합니다.

> [!NOTE]
> 합니다 `SqlMembershipProvider` 클래스에는 항상 임의 암호를 생성 최소 14 자, 따라서 `MinRequiredPasswordLength` 보다 작거나 14 않으면 해당 값은 무시 됩니다.


## <a name="step-2-changing-passwords"></a>2 단계: 암호 변경

임의로 생성 된 암호는 기억 하기 어렵습니다. 그림 4에 표시 된 암호는 것이 좋습니다: `WWGUZv(f2yM:Bd`합니다. 메모리는 커밋 보세요! 물론 사용자는 이러한 종류의 임의로 생성 된 암호를 보낸 후 그녀 하려고 기억 하기 암호를 변경 합니다.

암호를 변경 하는 사용자 인터페이스를 만들려면 ChangePassword 컨트롤을 사용 합니다. 훨씬 PasswordRecovery 컨트롤과 같은 ChangePassword 컨트롤 구성 보기가: 암호 변경 및 성공 합니다. 암호 변경 뷰를 이전 및 새 암호에 대 한 라는 메시지를 표시 합니다. 올바른 이전 암호와의 최소 길이 및 영숫자가 아닌 문자 요구 사항을 충족 하는 새 암호를 제공한 시 ChangePassword 컨트롤 사용자의 암호를 업데이트 하 고 성공 뷰를 표시 합니다.

> [!NOTE]
> ChangePassword 컨트롤을 호출 하 여 사용자의 암호를 수정 합니다 `MembershipUser` 개체의 [ `ChangePassword` 메서드](https://msdn.microsoft.com/library/system.web.security.membershipuser.changepassword.aspx)합니다. ChangePassword 메서드에 두 개의 `String` 입력 매개 변수- *oldPassword* 하 고 *newPassword*-사용자의 계정을 사용 하 여 업데이트 및를 *newPassword*, 제공 된 것으로 가정 *oldPassword* 정확 합니다.


엽니다는 `ChangePassword.aspx` 페이지 및 페이지 이름을 ChangePassword 컨트롤을 추가 `ChangePwd`합니다. 이 시점에서 디자인 보기 표시 암호 변경 (그림 6 참조)를 확인 합니다. 같은 PasswordRecovery 컨트롤과 컨트롤의 스마트 태그를 통해 뷰 간을 전환할 수 있습니다. 또한 이러한 보기의이 모양을 분류 된 스타일 속성을 통해 또는 서식 파일을 변환 하 여 사용자 지정할 수 있습니다.


[![ChangePassword 컨트롤을 페이지 추가](recovering-and-changing-passwords-vb/_static/image17.png)](recovering-and-changing-passwords-vb/_static/image16.png)

**그림 6**: ChangePassword 컨트롤을 페이지 추가 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image18.png))


ChangePassword 컨트롤에서 현재 로그인된 한 사용자의 암호를 업데이트할 수 있습니다 *또는* 다른, 지정 된 사용자의 암호입니다. 기본 암호 변경 뷰 세 TextBox 컨트롤을 렌더링 그림 6에서 알 수 있듯이: 이전 암호와 새 암호에 대 한 두 가지에 대 한 합니다. 이 기본 인터페이스는 현재 로그온된 한 사용자의 암호를 업데이트 하려면 사용 됩니다.

ChangePassword 컨트롤에 다른 사용자의 암호를 업데이트 하는 데 사용 하려면 컨트롤의 설정 [ `DisplayUserName` 속성](https://msdn.microsoft.com/library/system.web.ui.webcontrols.changepassword.displayusername.aspx) True로 합니다. 이렇게 변경 하려면 해당 암호를 사용자의 사용자 이름을 묻는 페이지에 네 번째 텍스트 상자를 추가 합니다.

설정 `DisplayUserName` 에 True 아웃 로그온 한 사용자 로그인 하지 않고도 암호를 변경 하려는 경우 유용 합니다. 개인적으로 사용 하 여 암호를 변경 하도록 허용 하기 전에 로그인 하도록 요구 하는 잘못 된 생각 합니다. 따라서 둡니다 `DisplayUserName` False (기본값)로 설정 합니다. 그러나이 의사 결정 하는 경우에서는 기본적으로 차단 익명 사용자가이 페이지에 도달 하지 못하도록 합니다. 방문에서 익명 사용자를 거부 하기 위해 사이트의 URL 권한 부여 규칙 업데이트 `ChangePassword.aspx`합니다. URL 권한 부여 규칙 구문에서 메모리를 새로 고침 해야 할 경우를 다시 참조를 <a id="_msoanchor_4"> </a> [ *사용자 기반 권한 부여* ](../membership/user-based-authorization-vb.md) 자습서입니다.

> [!NOTE]
> 하는 것이 보일는 `DisplayUserName` 속성은 관리자가 다른 사용자의 암호를 변경할 수 있도록 하는 데 유용 합니다. 그러나 경우에 `DisplayUserName` 이전 암호가 알려지고 입력 True로 설정 합니다. 관리자가 3 단계에서에서 사용자의 암호를 변경할 수 있도록 하는 방법도 설명 합니다.


방문을 `ChangePassword.aspx` 브라우저를 통해 페이지 및 암호를 변경 합니다. 암호 길이, 멤버 자격 구성에 지정 하는 영숫자가 아닌 문자 요구 사항을 충족 하지 않는 새 암호를 입력 하는 경우 오류 메시지가 표시 됩니다 (그림 7 참조).


[![ChangePassword 컨트롤을 페이지 추가](recovering-and-changing-passwords-vb/_static/image20.png)](recovering-and-changing-passwords-vb/_static/image19.png)

**그림 7**: ChangePassword 컨트롤을 페이지 추가 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image21.png))


사용자의 올바른 이전 암호 및 올바른 새 암호 로그인된을 입력 하면 암호를 변경 하 고 성공 뷰에 표시 합니다.

### <a name="sending-a-confirmation-email"></a>확인 전자 메일 보내기

기본적으로 ChangePassword 컨트롤 암호가 업데이트 된 사용자에 게 전자 메일 메시지를 보내지 않습니다. 전자 메일을 전송 하려는 경우 간단히 컨트롤의 구성 `MailDefinition` 속성입니다. 사용자가 새 암호를 포함 하는 HTML 형식의 전자 메일 전송 되도록 ChangePassword 컨트롤을 구성 하겠습니다.

새 파일을 만들어 시작 합니다 `EmailTemplates` 라는 폴더 `ChangePassword.htm`합니다. 다음 태그를 추가 합니다.

[!code-html[Main](recovering-and-changing-passwords-vb/samples/sample4.html)]

ChangePassword 컨트롤의 다음으로 설정 `MailDefinition` 속성의 `BodyFileName`를 `IsBodyHtml`, 및 `Subject` 속성을 ~ / EmailTemplates/ChangePassword.htm, True 및 암호 변경 되었습니다!, 각각.

다음과 같이 변경한 후 페이지를 다시 방문 하 고 암호를 다시 변경 합니다. 이 이때 ChangePassword 컨트롤 사용자 지정, HTML 형식의 전자 메일을 파일에 대 한 사용자의 전자 메일 주소로 보냅니다 (그림 8 참조).


[![사용자는 해당 암호가 변경 된 알립니다 전자 메일 메시지](recovering-and-changing-passwords-vb/_static/image23.png)](recovering-and-changing-passwords-vb/_static/image22.png)

**그림 8**: 사용자는 해당 암호를 변경에 전자 메일 메시지에 알립니다 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image24.png))


## <a name="step-3-allowing-administrators-to-change-users-passwords"></a>3 단계: 관리자가 사용자의 암호를 변경 하도록 허용

다른 사용자의 암호를 변경 하려면 관리자에 대 한 기능은 사용자를 지 원하는 응용 프로그램의 일반적인 기능입니다. 경우에 따라 시스템에 사용자가 자신의 암호를 변경할 수 없으므로이 기능을 필요 합니다. 이러한 경우 사용자가 잊어버린된 암호를 복구 하는 유일한 방법은 새 암호를 할당 하려면 관리자에 대 한 것입니다. 그러나 PasswordRecovery 및 ChangePassword 컨트롤을 관리자가 필요 하지 사용량이 많은 자체 사용자의 암호를 변경 하 여 사용자는 직접이 수행할 수 없습니다.

하지만 클라이언트의 다른 사용자의 암호를 변경 하려면 관리자에 게 있어야 외계인 될까요? 아쉽게도이 기능을 추가 하면 약간의 작업이 될 수 있습니다. 사용자의 암호를 변경 하려면 이전 및 새 암호를 제공 해야 합니다 `MembershipUser` 개체의 `ChangePassword` 메서드이지만 관리자로 수정 하기 위해 사용자의 암호를 몰라도 없어야 합니다.

한 가지 해결 방법은 다음과 같습니다. 먼저 사용자의 암호를 재설정 하 고 그런 다음 다음과 같은 코드를 사용 하 여 새 암호를 변경 하려면

[!code-vb[Main](recovering-and-changing-passwords-vb/samples/sample5.vb)]

이 코드에 대 한 정보를 검색 하 여 시작 *username*, 암호 관리자를 변경 하려는 사용자는 합니다. 다음으로 `ResetPassword` 메서드가 호출 되는 할당 및 사용자는 새 임의 암호입니다. 이 임의로 생성 된 암호는 메서드에서 반환 되 고 변수에 저장 된 `resetPwd`합니다. 사용자의 암호를 알게 되었으므로 이제 호출을 통해 변경할 수 있습니다 `ChangePassword`합니다.

멤버 자격 시스템 구성이 설정 된 경우이 코드만 작동 한다는 문제는 되도록 `RequiresQuestionAndAnswer` 은 False입니다. 경우 `RequiresQuestionAndAnswer` 샘플 응용 프로그램에서는 그대로 True 인 경우 `ResetPassword` 보안 대답 전달 해야 하는 메서드, 그렇지 않으면 예외가 발생 합니다.

멤버 자격 프레임 워크는 보안 질문 및 대답을 요구 하도록 구성 하는 경우 클라이언트의 관리자 사용자 암호를 변경 하는 일을 할 수는 외계인 아직 세 가지 옵션이 있습니다.

- 공중에서 손이 throw 및 수행할 수 없습니다. 하나만 점은 이것이 클라이언트에 지시 합니다.
- 설정 `RequiresQuestionAndAnswer` 를 False로 합니다. 이 인해 보안 수준이 낮은 응용 프로그램을 합니다. 악의적인 사용자가 다른 사용자의 전자 메일 받은 편지함에 대 한 액세스를 얻은 한다고 가정 합니다. 아마도 손상 된 사용자 들이 책상 앞 점심으로 이동 하 고 해당 워크스테이션 잠금 하지 않은 또는 공용 터미널에서 전자 메일 액세스 및 로그 아웃 하지 않은 있을 수 있습니다. 두 경우 모두 부정한 것인지 사용자가 방문할 수는 `RecoverPassword.aspx` 페이지 및 사용자의 사용자 이름을 입력 합니다. 시스템에서 보안 대답 하지 않고 복구 암호를 전자 메일로 다음입니다.
- 멤버 자격 프레임 워크 및 SQL Server 데이터베이스와 직접 작업에서 만든 추상화 계층을 무시 합니다. 저장된 프로시저를 포함 하는 멤버 자격 스키마 `aspnet_Membership_SetPassword` 사용자의 암호를 설정 하 고 해당 작업을 수행 하기 위해 이전 암호를 보안 대답 필요 하지 않습니다.

이러한 옵션은 특히 매력적인 이지만 개발자의 일상을 따라 이동 합니다.

두었고 했으며 우회 하는 코드를 작성 한 세 번째 방법은 구현 합니다 `Membership` 및 `MembershipUser` 클래스와 직접 작동 합니다 `SecurityTutorials` 데이터베이스.

> [!NOTE]
> 에 데이터베이스와 직접 작업 하는 멤버 자격 프레임 워크에서 제공 하는 간략화가 파괴 됩니다. 이 의사 결정을 연결 하는 `SqlMembershipProvider`,이 코드를 이식 가능 덜 합니다. 또한이 코드 멤버 자격 스키마 변경 되 면 버전의 ASP.NET 나중에 예상 대로 작동 하지 않을 수 있습니다. 이 접근 방식은 해결 방법 이며, 대부분의 해결 방법 등 하지 모범 사례의 예입니다.


코드 보기 좋지 않은 일부 비트 이며 매우 긴 합니다. 따라서 심도 있는 검사를 사용 하 여이 자습서를 어지럽히는 안 함 더 자세히 알고 싶은 경우이 자습서를 방문 하 여 코드를 다운로드 합니다 `~/Administration/ManageUsers.aspx` 페이지입니다. 이 페이지에서 만든 합니다 <a id="_msoanchor_5"> </a> [이전 자습서](building-an-interface-to-select-one-user-account-from-many-vb.md), 각 사용자를 나열 합니다. GridView에 대 한 링크를 포함 하도록 업데이트 된 `UserInformation.aspx` 페이지에서 선택한 사용자의 사용자 이름 문자열을 통해 전달 합니다. `UserInformation.aspx` 자신의 암호를 변경 하는 것에 대 한 선택한 사용자 및 텍스트 상자에 대 한 정보를 표시 하는 페이지 (그림 9 참조).

새 암호를 입력 합니다. 두 번째 텍스트 상자에 확인 하 고 사용자 [업데이트] 단추를 클릭 한 후 다시 게시 근거가 및 `aspnet_Membership_SetPassword` 사용자의 암호 업데이트 저장된 프로시저를 호출 합니다. 코드에 더 익숙해집니다 및 암호를 변경한 사용자에 게 전자 메일 보내기를 포함 하는 기능을 확장 해 보십시오.이 기능에 관심이 있는 독자를 이러한 것이 좋습니다.


[![관리자는 사용자의 암호를 변경할 수 있습니다.](recovering-and-changing-passwords-vb/_static/image26.png)](recovering-and-changing-passwords-vb/_static/image25.png)

**그림 9**: 관리자가 사용자의 암호를 변경 될 수 있습니다 ([큰 이미지를 보려면 클릭](recovering-and-changing-passwords-vb/_static/image27.png))


> [!NOTE]
> `UserInformation.aspx` 멤버 자격 프레임 워크의 선택을 취소 하거나 Hashed 형태로 암호를 저장 하도록 구성 된 경우만 작동 현재 페이지입니다. 이 기능을 추가 하도록 초대 받았다면 있지만 없기에 새 암호를 암호화 하는 코드입니다. 필요한 코드를 추가 하는 방법은 같은 디컴파일러를 사용 하는 것 [Reflector](http://www.aisto.com/roeder/dotnet/) .NET framework; 메서드에 대 한 소스 코드를 검사할 검사를 시작 합니다 `SqlMembershipProvider` 클래스의 `ChangePassword` 메서드. 이 암호의 해시를 만들기 위한 코드 작성을 사용 하는 방법입니다.


## <a name="summary"></a>요약

ASP.NET은 사용자가 자신의 암호를 관리 하는 데 두 가지 컨트롤을 제공 합니다. PasswordRecovery 컨트롤은 해당 암호를 잊어버린 사용자에 게 유용 합니다. 멤버 자격 프레임 워크의 구성에 따라 사용자는 하거나 전자 메일로 임의로 생성 된 새 또는 기존 암호입니다. ChangePassword 컨트롤 사용자를 자신의 암호를 업데이트할 수 있습니다.

로그인 및 CreateUserWizard 컨트롤 처럼 PasswordRecovery 및 ChangePassword 컨트롤 개의치 선언적 태그 또는 코드 줄을 작성 하지 않고도 풍부한 사용자 인터페이스를 렌더링 합니다. 기본 사용자 인터페이스 요구 사항에 부합 하지 않습니다, 다양 한 스타일 속성을 통해 사용자 지정할 수 있습니다. 또는 컨트롤의 인터페이스를 세밀성을 컨트롤에 대 한 템플릿으로 변환 될 수 있습니다. 이러한 컨트롤을 백그라운드에서 멤버 자격 API를 사용 호출을 `MembershipUser` 개체의 `ResetPassword` 고 `ChangePassword` 메서드.

즐거운 프로그래밍!

### <a name="further-reading"></a>추가 정보

이 자습서에서 다루는 항목에 대 한 자세한 내용은 다음 리소스를 참조 하세요.

- [ChangePassword 컨트롤 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/changepassword.aspx)
- [PasswordRecovery 제어 빠른 시작](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/passwordrecovery.aspx)
- [ASP.NET에서 전자 메일 보내기](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`System.Net.Mail` Faq](http://www.systemnetmail.com/)

### <a name="about-the-author"></a>저자 소개

Scott Mitchell, 여러 ASP/ASP.NET 책의 저자 이자 4GuysFromRolla.com의 설립자 이며 1998 Microsoft 웹 기술을 왔습니다. Scott는 독립 컨설턴트, 강사, 그리고 기록기로 작동합니다. 최근 저서는  *[Sams 설명 직접 ASP.NET 2.0 24 시간 동안의](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* 합니다. Scott에 도달할 수 있습니다 [ mitchell@4guysfromrolla.com ](mailto:mitchell@4guysfromrolla.com) 통하거나 저자의 블로그 [ http://ScottOnWriting.NET ](http://scottonwriting.net/)합니다.

### <a name="special-thanks-to"></a>특별히 감사

이 자습서 시리즈는 많은 유용한 검토자가 검토 되었습니다. 이 자습서에 대 한 선행 검토자는 Michael Emmings 및 Suchi Banerjee 포함 됩니다. 내 향후 MSDN 문서를 검토에 관심이 있으십니까? 그렇다면 삭제 나에서 선 [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [이전](building-an-interface-to-select-one-user-account-from-many-vb.md)
> [다음](unlocking-and-approving-user-accounts-vb.md)
