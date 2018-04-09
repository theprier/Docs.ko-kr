---
uid: web-pages/overview/getting-started/11-adding-email-to-your-web-site
title: (Razor) 사이트 페이지는 ASP.NET 웹에서 전자 메일 보내기 | Microsoft Docs
author: tfitzmac
description: 이 장에서 웹 사이트에서 자동화 된 전자 메일 메시지를 전송 하는 방법을 설명 합니다.
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2014
ms.topic: article
ms.assetid: fc49bcb9-f1a9-4048-8c3f-b60951853200
ms.technology: dotnet-webpages
ms.prod: .net-framework
msc.legacyurl: /web-pages/overview/getting-started/11-adding-email-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 9be242d238c627a9557fe7ff7e596974e5b7d1c8
ms.sourcegitcommit: f8852267f463b62d7f975e56bea9aa3f68fbbdeb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
<a name="sending-email-from-an-aspnet-web-pages-razor-site"></a>ASP.NET 웹 페이지 (Razor) 사이트에서 전자 메일 보내기
====================
으로 [Tom FitzMacken](https://github.com/tfitzmac)

> 이 문서에서는 ASP.NET 웹 페이지 (Razor)를 사용 하는 경우 웹 사이트에서 전자 메일 메시지를 전송 하는 방법을 설명 합니다.
> 
> 학습 내용:
> 
> - 웹 사이트에서 전자 메일 메시지를 보내는 방법입니다.
> - 전자 메일 메시지에 파일을 첨부 하는 방법.
> 
> 다음은 문서에 도입 된 ASP.NET 기능입니다.
> 
> - `WebMail` 도우미입니다.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>자습서에서 사용 되는 소프트웨어 버전
> 
> 
> - ASP.NET 웹 페이지 (Razor) 3
>   
> 
> 이 자습서는 ASP.NET 웹 페이지 2 에서도 작동합니다.


<a id="Sending_Email_Messages"></a>
## <a name="sending-email-messages-from-your-website"></a>웹 사이트에서 전자 메일 메시지 보내기

모든 종류의 웹 사이트에서 전자 메일 보내기 해야 이유가 있습니다. 사용자에 게 확인 메시지를 보낼 수 있습니다 (예: 새 사용자를 등록 합니다.) 자신에 게 알림을 보낼 수 있습니다 또는 `WebMail` 도우미를 사용 하면 쉽게 전자 메일을 보낼 수 있습니다.

사용 하 여 `WebMail` 도우미, SMTP 서버에 액세스할 수 있도록 해야 합니다. (SMTP는 *Simple Mail Transfer Protocol*.) SMTP 서버에만 받는 사람의 서버로 메시지를 전달 하는 전자 메일 서버는 &#8212; 전자 메일의 아웃 바운드 측은 합니다. 호스팅 공급자를 사용 하 여 웹 사이트에 대 한 아마도 설정 하면 전자 메일을 가진 및 SMTP server 이름이 무엇 인지 전달할 수 있습니다. 회사 네트워크 내부 작업 관리자 또는 IT 부서 일반적으로 정보를 제공할 수 있습니다는 사용할 수 있는 SMTP 서버에 대 한 합니다. 집에서 작업 하는 경우 해당 SMTP 서버의 이름을 알 수 있는 일반 전자 메일 공급자를 사용 하 여 테스트할 수도 합니다. 일반적으로 필요합니다.

- SMTP 서버의 이름입니다.
- 포트 번호입니다. 이 거의 항상 25입니다. 그러나 ISP 포트 587을 사용 하도록 해야 할 수 있습니다. 전자 메일에 대 한 secure sockets layer (SSL)를 사용 하는 경우에 다른 포트를 할 수 있습니다. 전자 메일 공급자에 문의 하십시오.
- 자격 증명 (사용자 이름, 암호)입니다.

이 절차에서는 두 개의 페이지를 만듭니다. 첫 번째 페이지에는 기술 지원 형식으로 작성 된 하는 경우 설명을 입력 하는 사용자가 수 있는 폼을 있습니다. 첫 번째 페이지는 두 번째 페이지에 해당 정보를 전송합니다. 두 번째 페이지에서 코드는 사용자의 정보를 추출 하 고 전자 메일 메시지를 보냅니다. 또한 문제 보고서를 받았는지 확인 하는 메시지가 표시 됩니다.

![[image]](11-adding-email-to-your-web-site/_static/image1.jpg)

> [!NOTE]
> 이 예제를 단순하게 유지 하기 위해 코드를 초기화는 `WebMail` 도우미 right를 사용 하 여 페이지에 있습니다. 그러나 실제 웹 사이트에 대 한 되는 글로벌 파일에 다음과 같은 초기화 코드를 저장 하는 것이 좋습니다 초기화는 `WebMail` 웹 사이트의 모든 파일에 대 한 도우미입니다. 자세한 내용은 참조 [사이트 전체의 동작을 사용자 지정 ASP.NET 웹 페이지에 대 한](https://go.microsoft.com/fwlink/?LinkId=202906#Setting_Values_For_Helpers)합니다.


1. 새 웹 사이트를 만듭니다.
2. 명명 된 새 페이지 추가 *EmailRequest.cshtml* 다음 태그를 추가 합니다. 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample1.html)]

    에 `action` 는 form 요소의 특성으로 설정 되었습니다 *ProcessRequest.cshtml*합니다. 이 대신 현재 페이지에 다시 해당 페이지에는 양식을 제출할 것을 의미 합니다.
3. 라는 새 페이지를 추가 *ProcessRequest.cshtml* 웹 사이트에 다음 코드와 태그를 추가 합니다.   

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample2.cshtml)]

    코드 페이지에 제출 된 양식 필드 값을 가져옵니다. 다음 호출에서 `WebMail` 도우미의 `Send` 메서드를 만들고 메일 메시지를 보냅니다. 이 경우 사용할 값을 폼에서 전송 된 값으로 연결 하는 텍스트의 구성 됩니다.

    이 페이지에 대 한 코드는 내부에 `try/catch` 블록입니다. 전송 시도가 이유로 모든 전자 메일 작동 하지 않는 경우 (예를 들어 설정 되지 오른쪽)의 코드는 `catch` 블록 실행 하 고 설정 하는 `errorMessage` 변수 발생 한 오류를 합니다. (에 대 한 자세한 내용은 `try/catch` 블록 또는 `<text>` 태그, 참조 [ASP.NET 웹 페이지 프로그래밍 구문을 사용 하 여 Razor 소개](https://go.microsoft.com/fwlink/?LinkID=251587#ID_HandlingErrors).)

    페이지의 본문에는 경우는 `errorMessage` 변수가 비어 (기본값) 이면 사용자에 게 전자 메일 메시지가 전송 된 메시지입니다. 경우는 `errorMessage` 변수는 메시지를 보내는 데 문제가 있었습니다 메시지가 사용자에 게 표시 true로 설정 됩니다.

    오류 메시지를 표시 하는 페이지의 부분에는 추가 테스트: `if(debuggingFlag)`합니다. 이 메일을 보내는 데 문제가 있는 경우 true로 설정할 수 있는 변수입니다. 때 `debuggingFlag` 가 true 이면 추가 오류 메시지가 ASP.NET에서 전자 메일 메시지를 보내려고 시도할 때 보고 무엇이 든 보여 주는 표시 전자 메일을 보내는 데 문제가 있으면 합니다. 그러나 fair 경고,: ASP.NET 전자 메일 메시지를 보낼 수 없는 경우를 보고 하는 오류 메시지는 제네릭일 수 있습니다. 예를 들어 경우 (예를 들어 때문에 서버 이름에는 오류 내용을) ASP.NET SMTP 서버에 연결할 수 없습니다, 오류는 `Failure sending mail`합니다.

    > [!NOTE] 
    > 
    > **중요 한** 예외 개체에서 오류 메시지를 가져올 때 (`ex` 코드에서)를 수행 *하지* 정기적으로 해당 메시지를 통해 사용자에 게 전달 합니다. 예외 개체에 사용자가 보아서는 안 하 고 보안 취약성도 일 수 있는 정보가 포함 되는 경우가 많습니다. 바로 이러한 이유로이 코드에 변수가 포함 되어 `debuggingFlag` 오류 메시지를 표시 하는 스위치로 사용 되는 및 기본적으로 변수를 false로 설정 되어 이유입니다. 변수를 true (및 따라서 오류 메시지 표시)로 설정 해야 *만* 메일을 보내는 문제가 있는 경우를 디버깅 해야 합니다. 문제를 해결 한 후에 설정할 `debuggingFlag` false로 다시 합니다.

    수정 다음 전자 메일의 코드에서 관련된 설정:

   - 설정 `your-SMTP-host` 에 액세스할 수 있는 SMTP 서버의 이름입니다.
   - 설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름에 있습니다.
   - 설정 `your-account-password` 를 SMTP 서버 계정의 암호입니다.
   - 설정 `your-email-address-here` 자신의 전자 메일 주소로 합니다. 메시지에서 보내는 전자 메일 주소입니다. (다른 지정할 수는 일부 전자 메일 공급자 주저 하지 마시기 바랍니다 `From` 주소 및 사용자 이름으로 사용 합니다는 `From` 주소입니다.)

     > [!TIP] 
     > 
     > <a id="configuring_email_settings"></a>
     > ### <a name="configuring-email-settings"></a>전자 메일 설정 구성
     > 
     > SMTP 서버, 포트 번호 및에 대 한 올바른 설정을 있는지 확인 하는 경우에 따라 어려울 수 있습니다. 다음은 이에 대한 몇 가지 팁입니다.
     > 
     > - SMTP 서버 이름을 방식은 다음과 같이 `smtp.provider.com` 또는 `smtp.provider.net`합니다. 그러나 사이트를 호스팅 공급자에 게시 하는 경우 SMTP 서버 이름을 해당 지점에서 않을 `localhost`합니다. 게시 한 후 사이트 공급자의 서버에서 실행 되는 전자 메일 서버 응용 프로그램의 관점에서 로컬 수 있기 때문입니다. 게시 프로세스의 일부로 SMTP 서버 이름을 변경 해야 할 서버 이름에이 변경 될 수도 있습니다.
     > - 포트 번호는 일반적으로 25입니다. 그러나 일부 공급자 사용 해야 할 포트 587 또는 일부 다른 포트입니다.
     > - 올바른 자격 증명을 사용 하 고 있는지 확인 합니다. 사이트를 호스팅 공급자에 게시 한 경우 특별히 설정 된 공급자가 전자 메일에 대 한 자격 증명을 사용 합니다. 이러한 게시에 사용할 자격 증명과 다를 수 있습니다.
     > - 경우에 따라 자격 증명을 전혀 필요 하지 않습니다. 개인 ISP를 사용 하 여 메일을 보내는 전자 메일 공급자 자격 증명 이미 알고 될 수 있습니다. 를 게시 한 후 로컬 컴퓨터에서 테스트 아니라 다른 자격 증명을 사용 하도록 할 수 있습니다.
     > - 전자 메일 공급자가 암호화를 사용 하는 경우 설정 해야 `WebMail.EnableSsl` 를 `true`합니다.
4. 실행 된 *EmailRequest.cshtml* 브라우저에서 페이지입니다. (있는지 확인 페이지에서 선택한는 **파일** 실행 하기 전에 작업 영역입니다.)
5. 사용자 이름 및 문제 설명, 입력 한 다음 클릭는 **전송** 단추입니다. 리디렉션됩니다 하는 *ProcessRequest.cshtml* 페이지에서 메시지를 확인 하는 전자 메일 메시지를 보냅니다입니다. 

    ![[image]](11-adding-email-to-your-web-site/_static/image2.jpg)

<a id="Sending_a_File"></a>
## <a name="sending-a-file-using-email"></a>전자 메일을 사용 하 여 파일 전송

전자 메일 메시지에 첨부 된 파일을 보낼 수도 있습니다. 이 절차에서는 두 개의 HTML 페이지 및 텍스트 파일을 만듭니다. 전자 메일 첨부 파일로 텍스트 파일을 사용 합니다.

1. 웹 사이트에 새 텍스트 파일을 추가 하 고 이름을 *MyFile.txt*합니다.
2. 다음 텍스트를 복사 하는 파일에 붙여넣습니다. 

    `Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`
3. *SendFile.cshtml* 다음 태그를 추가 합니다. 

    [!code-html[Main](11-adding-email-to-your-web-site/samples/sample3.html)]
4. *ProcessFile.cshtml* 다음 태그를 추가 합니다. 

    [!code-cshtml[Main](11-adding-email-to-your-web-site/samples/sample4.cshtml)]
5. 수정 다음 전자 메일의 코드 예제를 관련된 설정:

    - 설정 `your-SMTP-host` 에 액세스할 수 있는 SMTP 서버 이름입니다.
    - 설정 `your-user-name-here` SMTP 서버 계정의 사용자 이름에 있습니다.
    - 설정 `your-email-address-here` 자신의 전자 메일 주소로 합니다. 메시지에서 보내는 전자 메일 주소입니다.
    - 설정 `your-account-password` 를 SMTP 서버 계정의 암호입니다.
    - 설정 `target-email-address-here` 자신의 전자 메일 주소로 합니다. (에 따라 이전에 보내는 것과 일반적으로 전자 메일을 다른 사람에 게 테스트를 위해 있습니다 수 자신에 게 보냅니다.)
6. 실행 된 *SendFile.cshtml* 브라우저에서 페이지입니다.
7. 사용자 이름, 제목 줄 및 연결할 텍스트 파일의 이름 입력 (*MyFile.txt*).
8. `Submit` 단추를 클릭합니다. 이동 하는 이전에 *ProcessFile.cshtml* 페이지에서 메시지를 확인 하 고 하는 메시지를 보냅니다 전자 메일 첨부 파일을 사용 합니다.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>추가 자료


- [ASP.NET 웹 페이지(Razor) 문제 해결 가이드](https://go.microsoft.com/fwlink/?LinkId=253001)
- [Simple Mail Transfer Protocol](https://msdn.microsoft.com/library/aa480435.aspx)
- [ASP.NET 웹 페이지에 대 한 사이트 전체 동작을 사용자 지정](https://go.microsoft.com/fwlink/?LinkId=202906)
