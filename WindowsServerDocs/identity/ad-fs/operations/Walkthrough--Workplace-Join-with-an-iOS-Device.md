---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: 연습-는 iOS 디바이스와 회사 가입
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a8643bab913dfec07c6bbea0c068e1240f16c5b
ms.sourcegitcommit: a2260c96b0e49519d180c7382b921ce8ddb053fe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>연습: Workplace Join는 iOS 디바이스와

>Windows Server 2012 r 2에 적용 됩니다.

IOS 디바이스에서이 항목에서는 회사에 참여 합니다. 단계를 완료 해야는 [랩 환경 ADFS Windows Server 2012 r 2에서에 대 한 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 섹션 전에이 연습 사용해 볼 수 있습니다. 디바이스를 사용 하 여에 액세스 하는 동일한 회사 웹 응용 프로그램에 액세스 [연습: Windows 디바이스에 회사 참여](Walkthrough--Workplace-Join-with-a-Windows-Device.md)합니다.

## <a name="join-an-ios-device-with-workplace-join"></a>IOS 디바이스와 회사 참여 가입

> [!IMPORTANT]
> IOS 디바이스 Active Directory Federation Services ADFS ()를 구성 하는 데 사용 된 Layer SSL (Secure Socket) 인증서를 신뢰 해야 온-프레미스 DRS 구성 된 경우 [2 단계: 장치 등록 서비스와 federation 서버 (ADFS1) 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4), 성공 가입 회사에 대 한 합니다.
> 
> -   광고 FS ssl (캐나다), 테스트 인증 기관에서 발급, iOS 디바이스에서 인증 기관 인증서를 설치 해야 합니다.
> -   인증 기관 인증서는 웹 사이트에 게시 하는 경우 iOS 디바이스에서 웹 사이트로 이동 하 고 인증서를 설치할 수 있습니다.

이 데모 회사에 디바이스에 가입 하면 합니다.

#### <a name="to-join-an-ios-device-to-a-workplace"></a>회사에 iOS 디바이스를 연결 하려면

1.  -   **Azure Active Directory 디바이스 등록 서비스는 구성 된 DRS 때:** 열기 Apple Safari iOS 디바이스에 대 한 Azure Active Directory 디바이스 등록 서비스 Over-the-Air 프로필 끝점으로 이동 하 고 <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > 위치 <`yourdomainname`> Azure Active Directory로 구성 된 도메인 이름입니다. 예를 들어 도메인 이름 contoso.com 이면 URL 됩니다. `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

    -   **온-프레미스 DRS 구성 된 DRS 되 면**: 열기 Apple Safari iOS 디바이스에 대 한 디바이스 등록 서비스 (DRS) Over-the-Air 프로필 끝점으로 이동 하 고`https://adf1s.contoso.com/enrollmentserver/otaprofile`

    여러 가지 방법으로 사용자에 게이 URL 통신할 수 있습니다. 권장된 방법 중 하나 거부 Adfs의 메시지에 대 한 액세스를 사용자 지정 응용 프로그램이이 URL를 게시 하입니다. 곧 섹션에 대해서는이: [액세스 정책 응용 프로그램 및 사용자 지정 액세스 거부 메시지가 만들기](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2.  회사의 도메인 계정을 사용 하 여 웹 페이지에 로그온: ** roberth@contoso.com ** 및 암호: ** P@ssword **합니다.

3.  프로필을 설치 하 라는 메시지가 표시 됩니다. 에 **프로필 설치** 화면에서 클릭 **설치**합니다.

4.  설치 프로필을 확인 하 라는 메시지가 나타나면 클릭 **지금 설치**합니다.

5.  디바이스에서 디바이스 잠금을 해제 하는 데 PIN 필요, PIN을 입력 하 라는 메시지가 표시 됩니다.

6.  표시 되 면 프로필 설치가 완료 되 고 **프로필이 설치** 화면 합니다. 클릭 **완료**합니다.

    Safari로 돌아갑니다. 닫을 수 있는 또는 Safari 두고을 알리는 메시지가 표시 됩니다.

> [!TIP]
> 찾아보기 보거나 회사 가입 프로필을 제거 하려면 **설정**, 클릭 **일반**을 차례로 클릭 하 고 **프로필** iOS 디바이스에서 합니다.

## <a name="see-also"></a>참조 하십시오


- [SSO 및 원활 하 게 초에 대 한 모든 디바이스에서 회사에 가입 인증 회사 응용 프로그램에서 요인](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Windows Server 2012 r 2에서 adfs 랩 환경을 설정합니다](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [연습: Workplace Join 사용 하 여 Windows 장치](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



