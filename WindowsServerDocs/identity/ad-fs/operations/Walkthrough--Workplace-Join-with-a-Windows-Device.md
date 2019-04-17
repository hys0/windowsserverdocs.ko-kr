---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: "연습-Windows 디바이스를 회사 가입"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fd222eb47982591e051594e8a572443b65c0357f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>연습: Workplace Join 사용 하 여 Windows 장치

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

이 항목에서는 회사와 Windows 디바이스를 연결 하려면 회사 참여를 사용 하는 방법을 고 Single Sign-on를 사용 하 여 웹 응용 프로그램에 액세스 하는 방법을 보여 줍니다. 단계를 완료 해야는 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 섹션 전에이 연습 사용해 볼 수 있습니다.

## <a name="access-the-web-application-before-device-registration"></a>장치를 등록 하기 전에 웹 응용 프로그램에 액세스
이 연습 디바이스는 회사에 연결 하기 전에 회사 웹 응용 프로그램을 액세스 합니다. 웹 페이지는 보안 토큰에 포함 되었던 클레임 표시 됩니다. 고 지 클레임 목록 디바이스에 대 한 정보를 포함 되지 않습니다. Single Sign-on 필요가 없습니다 확인할 수 있습니다.

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>디바이스에 회사 참여를 사용 하기 전에 웹 응용 프로그램에 액세스 하려면

1.  Microsoft 계정으로 Client1에 로그온 합니다.

2.  Internet Explorer를 열고 일반 클레임 앱을 검색 **https://webserv1.contoso.com/claimapp**합니다.

3.  회사의 도메인 계정을 사용 하 여 웹 페이지에 로그온: ** roberth@contoso.com **, 암호: ** P@ssword **합니다.

4.  웹 페이지에서 보안 토큰 모든 클레임 보여 줍니다. 사용자 클레임만 보안 토큰에 있습니다.

5.  Internet Explorer를 닫습니다.

6.  Internet Explorer를 열고 동일한 클레임 앱으로 이동 **https://webserv1.contoso.com/claimapp**합니다.

7.  자격 증명을 다시 입력 하 라는 메시지가 표시 됩니다. Single Sign-on 설치 되지 않은 한 회사 계정에 연결 된 디바이스에서 작업 영역에 연결 되지 않은 있습니다.

## <a name="join-your-device-with-workplace-join"></a>회사 계정에 연결 된 디바이스에 참여

> [!IMPORTANT]
> 회사에 성공 참여에 대 한 클라이언트 컴퓨터 (Client1) 해야 SSL 인증서를 신뢰 Active Directory Federation Services ADFS ()를 구성 하는 데 사용 된에서 [2 단계: 장치 등록 서비스 (ADFS1)와 Federation 서버 구성](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)합니다. 인증서에 대 한 정보 해지 유효성을 검사 하기도 수 있어야 합니다. 회사 가입 관련 된 문제를 사용 하는 경우 이벤트 로그 Client1에서 볼 수 있습니다.
> 
> 이벤트 로그를 보려면 이벤트 뷰어를 열고 확장 **응용 프로그램 및 서비스 로그**, 확장 **Microsoft**, 확장 **Windows**을 차례로 클릭 하 고 **회사에 참여**합니다.

#### <a name="to-join-your-device-with-workplace-join"></a>회사 가입와 사용자 디바이스에 참여를

1.  Microsoft 계정으로 Client1에 로그온 합니다.

2.  에 **시작** 화면에서 열려 있는 **참 메뉴** 막대를 선택한 다음는 **설정** 참 메뉴 합니다. 선택 **PC 설정 변경**합니다.

3.  에 **PC 설정** 페이지를 선택 하 고 **네트워크**을 차례로 클릭 하 고 **회사**합니다.

4.  에 **회사 계정에 액세스 하거나 장치 관리 설정 하 여 사용자 Id를 입력** 상자에 입력 ** roberth@contoso.com **을 차례로 클릭 하 고 **참여**합니다.

5.  자격 증명에 대 한 메시지가 표시 되 면 입력 ** roberth@contoso.com **, 암호 및: ** P@ssword **합니다. 클릭 **확인**합니다.

6.  이제 알리는 메시지가 나타납니다. "이이 디바이스가 회사 네트워크에 연결 되었습니다."

### <a name="access-the-web-application-after-joining-the-workplace"></a>웹 응용 프로그램은 회사에 가입한 후 액세스
데모의이 부분을 회사 웹 응용 프로그램 참여 하는 회사와 연결 된 디바이스에서 액세스. 웹 페이지는 보안 토큰에 포함 되었던 클레임 표시 됩니다. 고 지 클레임 목록이 디바이스와 사용자 정보를 포함 합니다. 해야 한다는 Single Sign-on 확인할 수 있습니다.

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>회사에 가입한 후 웹 응용 프로그램에 액세스 하려면

1.  로그온 할 **Client1** Microsoft 계정으로 합니다.

2.  Internet Explorer를 열고 일반 클레임 앱을 검색 **https://webserv1.contoso.com/claimapp**합니다.

3.  회사의 도메인 계정을 사용 하 여 웹 페이지에 로그온: ** roberth@contoso.com **, 암호: ** P@ssword **합니다.

4.  웹 페이지에서 보안 토큰 클레임 보여 줍니다. 사용자 토큰 사용자와 디바이스 클레임 포함 되어 있습니다.

5.  Internet Explorer를 닫습니다.

6.  Internet Explorer를 열고 동일한 클레임 앱으로 이동 **https://webserv1.contoso.com/claimapp**합니다.

7.  사용자는 **하지** 자격 증명을 다시 입력 하 라는 메시지가 표시 됩니다. 회사 계정에 연결 된 디바이스에서 연결 되어 있고 Single Sign-on 따라서 해야 합니다.

## <a name="see-also"></a>참조 하십시오
[회사에 SSO와 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 참여](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
[연습: 회사는 iOS 디바이스와 연결](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



