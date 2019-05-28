---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: 연습-iOS 장치를 사용 하 여 작업 공간 연결
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 42b71667758f392d641c5262e34322f8b21cfad9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188907"
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>연습: iOS 장치를 사용하여 작업 공간 연결


> [!IMPORTANT] 
> 이 메서드는만 완벽 하 게 온-프레미스 고객에 게 적합 합니다. 하이브리드 또는 클라우드 전용 고객에 게 iOS 장치를 등록 하려면이 메서드를 사용 하지 해야 합니다. 및 온-프레미스 고객은 클라우드로 이동 하려는 경우이 메서드 호환 되지 않습니다. 장치 등록을 취소 하 고 클라우드를 사용 하 여 등록 해야 합니다. 

이 항목에서는 iOS 장치의 작업 공간 연결을 설명합니다. 단계를 완료 해야 합니다 [Windows Server 2012 R2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 섹션 전에이 연습을 시도해 볼 수 있습니다. 장치를 사용 하 여에서 나 액세스할 수 있는 동일한 회사 웹 응용 프로그램에 액세스할 [연습: Windows 장치를 사용 하 여 작업 공간 연결](Walkthrough--Workplace-Join-with-a-Windows-Device.md)합니다.


## <a name="join-an-ios-device-with-workplace-join"></a>작업 공간 연결을 사용하여 iOS 장치 연결

> [!IMPORTANT]
> 온-프레미스 DRS가 구성 되 면 iOS 장치에는 Active Directory Federation Services (AD FS)를 구성 하는 데 사용 된 보안 소켓 레이어 (SSL) 인증서를 신뢰 해야 [2 단계: 페더레이션 서버 (ADFS1) with Device Registration Service 구성](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4), 작업 공간 연결에 성공 하려면에 대 한 합니다.
> 
> -   테스트 CA(인증 기관)에서 AD FS SSL 인증서를 발급한 경우 iOS 장치에 해당 인증 기관 인증서를 설치해야 합니다.
> -   인증 기관 인증서가 웹 사이트에 게시된 경우 iOS 장치에서 해당 웹 사이트로 이동하여 인증서를 설치할 수 있습니다.

이 데모에서는 장치를 작업 공간에 연결합니다.

#### <a name="to-join-an-ios-device-to-a-workplace"></a>iOS 장치를 작업 공간에 연결하려면

1.  -   **Azure Active Directory 장치 등록 서비스가 구성된 경우 DRS는 다음을 수행합니다.** Apple Safari를 열고 iOS 장치의 Azure Active Directory Device Registration service (over-the-air) 프로필 끝점으로 이동 <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > 여기서 <`yourdomainname`> Azure Active Directory를 사용 하 여 구성한 도메인 이름입니다. 예를 들어 도메인 이름이 contoso.com인 경우 URL은 `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`입니다.

    -   **온-프레미스 DRS가 구성된 DRS는 다음을 수행합니다.** Apple Safari를 열고 iOS 장치의 DRS Device Registration Service () (over-the-air) 프로필 끝점으로 이동 `https://adf1s.contoso.com/enrollmentserver/otaprofile`

    이 URL을 사용자에게 전달하는 방법에는 여러 가지가 있습니다. 한 가지 권장 방법은 AD FS에서 사용자 지정 응용 프로그램 액세스 거부됨 메시지에 이 URL을 게시하는 것입니다. 이 내용은 이후 섹션에서 설명합니다. [응용 프로그램 액세스 정책 및 사용자 지정 액세스 거부됨 메시지 만들기](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2.  회사 도메인 계정을 사용 하 여 웹 페이지에 로그온 합니다. **roberth@contoso.com** 및 암호: **P@ssword**합니다.

3.  프로필을 설치하라는 메시지가 표시됩니다. **프로파일 설치** 화면에서 **설치**를 클릭합니다.

4.  프로필 설치를 확인하라는 메시지가 표시되면 **지금 설치**를 클릭합니다.

5.  장치에 장치의 잠금을 해제하기 위한 PIN이 필요한 경우 PIN을 입력하라는 메시지가 표시됩니다.

6.  **프로파일 설치됨** 화면이 표시되면 프로필 설치가 완료된 것입니다. **완료**를 클릭합니다.

    Safari로 돌아갑니다. Safari를 닫거나 그대로 둘 수 있음을 알리는 메시지가 표시됩니다.

> [!TIP]
> 작업 공간 연결 프로필을 보거나 제거하려면 **설정**으로 이동하여 **일반**을 클릭한 다음 iOS 장치에서 **프로파일**을 클릭합니다.

## <a name="see-also"></a>관련 항목


- [SSO 및 원활한 두 번째 위한 모든 장치의 작업 공간 연결 단계 회사 응용 프로그램에서 인증](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Windows Server 2012 R2의 AD FS에 대한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [연습: Windows 디바이스를 사용하여 작업 공간 연결](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



