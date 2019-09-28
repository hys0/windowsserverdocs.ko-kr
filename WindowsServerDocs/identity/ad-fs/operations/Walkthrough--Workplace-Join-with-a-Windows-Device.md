---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: 연습-Windows 장치를 사용 하 여 Workplace Join
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9867e11aa659be9aff9912780e1186a796a7232e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357774"
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>연습: Windows 장치를 사용하여 작업 공간 연결

이 항목에서는 작업 공간 연결을 사용하여 Windows 장치를 작업 공간과 연결하는 방법 및 Single Sign-On을 사용하여 웹 응용 프로그램에 액세스하는 방법을 설명합니다. 이 연습을 수행 하려면 먼저 [Windows Server 2012 R2에서 AD FS에 대 한 랩 환경 설정](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 섹션의 단계를 완료 해야 합니다.

## <a name="access-the-web-application-before-device-registration"></a>장치를 등록하기 전에 웹 응용 프로그램에 액세스
이 연습에서는 장치를 작업 공간에 연결하기 전에 회사 웹 응용 프로그램에 액세스합니다. 웹 페이지에 보안 토큰에 포함된 클레임이 표시됩니다. 클레임 목록에 장치에 대한 정보가 포함되지 않은 것을 볼 수 있습니다. 또한 Single Sign-On이 없는 것을 알 수 있습니다.

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>장치에서 작업 공간 연결을 사용하기 전에 웹 응용 프로그램에 액세스 하려면

1. Microsoft 계정으로 Client1에 로그온합니다.

2. Internet Explorer를 열고 일반 클레임 앱 **https://webserv1.contoso.com/claimapp** 로 이동 합니다.

3. 회사 도메인 계정 ( <strong>roberth@contoso.com</strong>, 암호: <strong>P@ssword)</strong>을 사용 하 여 웹 페이지에 로그온 합니다.

4. 웹 페이지에 보안 토큰의 모든 클레임이 나열됩니다. 사용자 클레임만 보안 토큰에 있습니다.

5. Internet Explorer를 닫습니다.

6. Internet Explorer를 열고 동일한 클레임 앱 ( **https://webserv1.contoso.com/claimapp** 로 이동 합니다.

7. 자격 증명을 다시 입력하라는 메시지가 표시됩니다. 작업 공간 연결을 사용하여 장치에서 작업 공간에 연결하지 않았으므로 Single Sign-On이 없습니다.

## <a name="join-your-device-with-workplace-join"></a>작업 공간 연결을 사용하여 장치를 연결합니다.

> [!IMPORTANT]
> Workplace Join 성공 하려면 클라이언트 컴퓨터 (Client1)가 [Step 2에서 Active Directory Federation Services (AD FS)를 구성 하는 데 사용 된 SSL 인증서를 신뢰 해야 합니다. ADFS1 (Device Registration Service) ](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)을 사용 하 여 페더레이션 서버를 구성 합니다. 또한 인증서 해지 정보의 유효성을 검사할 수 있어야 합니다. 작업 공간 연결에 문제가 있는 경우 Client1에서 이벤트 로그를 볼 수 있습니다.
> 
> 이벤트 로그를 보려면 이벤트 뷰어를 열고 **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**를 차례로 확장하고 **작업 공간 연결**을 클릭합니다.

#### <a name="to-join-your-device-with-workplace-join"></a>작업 공간 연결을 사용하여 장치를 연결하려면

1. Microsoft 계정으로 Client1에 로그온합니다.

2. **시작** 화면에서 **참 메뉴** 모음을 열고 **설정** 참 메뉴를 선택합니다. **PC 설정 변경**을 선택합니다.

3. **PC 설정** 페이지에서 **네트워크**를 클릭한 다음 **작업 공간**을 선택합니다.

4. 회사에 **액세스 하거나 장치 관리를 켜려면 사용자 id를 입력 하세요** . 상자에 <strong>roberth@contoso.com</strong>를 입력 한 다음 **조인**을 클릭 합니다.

5. 자격 증명을 입력 하 라는 메시지가 표시 되 면 <strong>roberth@contoso.com</strong>을 입력 하 고 암호: <strong>P@ssword</strong>을 입력 합니다. **확인**을 클릭합니다.

6. 이제 다음 메시지가 표시됩니다. "이 장치를 회사 네트워크에 연결했습니다."

### <a name="access-the-web-application-after-joining-the-workplace"></a>작업 공간에 연결한 후 웹 응용 프로그램에 액세스
데모의 이 부분에서는 작업 공간 연결을 사용하여 연결된 장치에서 회사 웹 응용 프로그램을 액세스합니다. 웹 페이지에 보안 토큰에 포함된 클레임이 표시됩니다. 클레임 목록에 장치 정보와 사용자 정보가 모두 포함되어 있는 것을 볼 수 있습니다. 또한 이제 Single Sign-On이 있는 것을 알 수 있습니다.

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>작업 공간에 연결한 후 웹 응용 프로그램에 액세스하려면

1. Microsoft 계정으로 **Client1**에 로그온합니다.

2. Internet Explorer를 열고 일반 클레임 앱 **https://webserv1.contoso.com/claimapp** 로 이동 합니다.

3. 회사 도메인 계정 ( <strong>roberth@contoso.com</strong>, 암호: <strong>P@ssword)</strong>을 사용 하 여 웹 페이지에 로그온 합니다.

4. 웹 페이지에 보안 토큰의 클레임이 나열됩니다. 토큰에는 사용자 클레임과 장치 클레임이 모두 포함되어 있습니다.

5. Internet Explorer를 닫습니다.

6. Internet Explorer를 열고 동일한 클레임 앱 ( **https://webserv1.contoso.com/claimapp** 로 이동 합니다.

7. 자격 증명을 다시 입력하라는 메시지가 표시되지 **않습니다** . 장치에서 작업 공간 연결을 사용하여 연결했으므로 Single Sign-On이 있습니다.

## <a name="see-also"></a>관련 항목
[회사 응용 프로그램 전체에서 SSO 및 원활한 두 번째 단계 인증을 위해 모든 장치에서 작업 공간에 연결](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
 Windows Server 2012 R2 
 @ no__t[에서 AD FS에 대 한 랩 환경을 설정 합니다](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md). iOS 디바이스를 사용하여 작업 공간 연결](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



