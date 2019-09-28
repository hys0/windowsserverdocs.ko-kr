---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: 연습-iOS 장치를 사용 하 여 Workplace Join
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5214165c2843461a2da8b574ad28f92b0e0bc64d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407493"
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>연습: iOS 장치를 사용하여 작업 공간 연결


> [!IMPORTANT] 
> 이 메서드는 완전히 온-프레미스 고객만 관련이 있습니다. 하이브리드 또는 클라우드 전용 고객은이 방법을 사용 하 여 iOS 장치를 등록 해서는 안 됩니다. 그리고 온-프레미스 고객이 클라우드로 이동 하기로 결정 한 경우에는이 방법이 호환 되지 않습니다. 장치를 등록 취소 하 고 클라우드에 등록 해야 합니다. 

이 항목에서는 iOS 장치의 작업 공간 연결을 설명합니다. 이 연습을 수행 하려면 먼저 [Windows Server 2012 R2에서 AD FS에 대 한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 섹션의 단계를 완료 해야 합니다. 장치를 사용 하 여 [ 연습에서 액세스 한 것과 동일한 회사 웹 응용 프로그램에 액세스할 수 있습니다. Windows 장치 @ no__t-0으로 Workplace Join 합니다.


## <a name="join-an-ios-device-with-workplace-join"></a>작업 공간 연결을 사용하여 iOS 장치 연결

> [!IMPORTANT]
> 온-프레미스 DRS가 구성 된 경우 iOS 장치는 Active Directory Federation Services (AD FS)를 구성 하는 데 사용 된 SSL (Secure Socket Layer) 인증서를 [Step 단계에서 신뢰 해야 합니다. Workplace Join 성공 하려면 장치 등록 서비스 @ no__t-0을 사용 하 여 페더레이션 서버 (ADFS1)를 구성 합니다.
> 
> -   테스트 CA(인증 기관)에서 AD FS SSL 인증서를 발급한 경우 iOS 장치에 해당 인증 기관 인증서를 설치해야 합니다.
> -   인증 기관 인증서가 웹 사이트에 게시된 경우 iOS 장치에서 해당 웹 사이트로 이동하여 인증서를 설치할 수 있습니다.

이 데모에서는 장치를 작업 공간에 연결합니다.

#### <a name="to-join-an-ios-device-to-a-workplace"></a>iOS 장치를 작업 공간에 연결하려면

1. -   **Azure Active Directory 장치 등록 서비스가 구성된 경우 DRS는 다음을 수행합니다.** Apple Safari를 열고 iOS < 장치에 대 한 Azure Active Directory Device Registration 서비스-공중파 프로필 엔드포인트로 이동 합니다. `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > < @no__t >를 사용 하 여 구성한 도메인 이름은 Azure Active Directory-1입니다. 예를 들어 도메인 이름이 contoso.com인 경우 URL은 `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`입니다.

   -   **온-프레미스 DRS가 구성된 DRS는 다음을 수행합니다.** Apple Safari를 열고 iOS 장치에 대 한 DRS (Device Registration Service)-공중파 프로필 엔드포인트로 이동 합니다. `https://adf1s.contoso.com/enrollmentserver/otaprofile`

   이 URL을 사용자에게 전달하는 방법에는 여러 가지가 있습니다. 한 가지 권장 방법은 AD FS에서 사용자 지정 응용 프로그램 액세스 거부됨 메시지에 이 URL을 게시하는 것입니다. 이 내용은 이후 섹션에서 설명합니다. [응용 프로그램 액세스 정책 및 사용자 지정 액세스 거부됨 메시지 만들기](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2. 회사 도메인 계정을 사용 하 여 웹 페이지에 로그온 합니다. <strong>roberth@contoso.com</strong> 및 암호: <strong>P@ssword</strong>.

3. 프로필을 설치하라는 메시지가 표시됩니다. **프로파일 설치** 화면에서 **설치**를 클릭합니다.

4. 프로필 설치를 확인하라는 메시지가 표시되면 **지금 설치**를 클릭합니다.

5. 장치에 장치의 잠금을 해제하기 위한 PIN이 필요한 경우 PIN을 입력하라는 메시지가 표시됩니다.

6. **프로파일 설치됨** 화면이 표시되면 프로필 설치가 완료된 것입니다. **완료**를 클릭합니다.

   Safari로 돌아갑니다. Safari를 닫거나 그대로 둘 수 있음을 알리는 메시지가 표시됩니다.

> [!TIP]
> 작업 공간 연결 프로필을 보거나 제거하려면 **설정**으로 이동하여 **일반**을 클릭한 다음 iOS 장치에서 **프로파일**을 클릭합니다.

## <a name="see-also"></a>관련 항목


- [회사 애플리케이션 전반에 SSO 및 연속된 두 번째 단계 인증을 위한 모든 디바이스의 작업 공간 연결](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Windows Server 2012 R2의 AD FS에 대한 랩 환경 설정](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [연습: Windows 디바이스를 사용하여 작업 공간 연결](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



