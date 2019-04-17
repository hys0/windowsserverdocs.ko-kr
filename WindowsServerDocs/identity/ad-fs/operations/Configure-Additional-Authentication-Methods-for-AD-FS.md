---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: "추가 인증 방법을 adfs 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 65baa6f94e1efa1fa337eab477b18f947cf0bb2d
ms.sourcegitcommit: 36d7b1dfd7da8e9f303d007a628e76149de000f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/21/2018
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>추가 인증 방법을 adfs 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

다중 요소 인증 MFA ()을 사용 하기 위해 하나 이상의 추가 인증 방법을 선택 해야 합니다. 기본적으로 Windows Server 2012 r 2에 AD FS(Active Directory Federation Services)에서 인증서 인증 (즉, 스마트 카드 기반 인증)을 추가 인증 방법으로 선택할 수 있습니다.

> [!NOTE]
> 인증서 인증을 선택 하는 경우 스마트 카드 인증서 안전 하 게 제공 되었고 및는 pin 요구 사항이 있는지 확인 합니다.

Microsoft Azure 클라우드에서 비슷한 기능을 제공 한다는 알고 계 셨나요? 자세한 내용은 [Microsoft Azure id 솔루션](http://aka.ms/m2w274)합니다.<br /><br />Microsoft Azure에 하이브리드 id 솔루션을 만듭니다.<br /> - [Azure 다단계 인증에 알아보세요.](http://aka.ms/ey6o9r)<br /> - [클라우드 인증을 사용 하 여 단일 숲 하이브리드 환경에 대 한 id를 관리 합니다.](http://aka.ms/g1jat8)<br /> - [추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리 합니다.](http://aka.ms/kt1bbm)|

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Microsoft 및 제 3 자 인증 방법
구성 하 고 Microsoft 및 제 3 자 인증 방법을 adfs Windows Server 2012 r 2에서를 사용 하도록 설정 수 있습니다. 설치 하 고 등록 된 ADFS, 전체 또는 당 3를 사용 하지 않고-자 인증 정책의 일부로 MFA 적용할 수 있습니다.

아래에 Microsoft 및 제 3 자 공급자에 게 MFA 제품 사전순 현재 사용할 수 있는 ADFS Windows Server 2012 r 2에서에 대 한 합니다.

||||
|-|-|-|
|**공급자**|**제공**|**자세히 알아보려면 연결**|
|Gemalto|Gemalto Id 및 보안 서비스|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo 기술|inWebo 인증 엔터프라이즈 서비스|[엔터프라이즈 인증 inWebo](http://www.inwebo.com)|
|로그인 피플|광고 FS 2012 r 2 (공개 베타)에 대 한 로그인 피플 MFA API 커넥터|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft Corp.|Microsoft Azure MFA|[연습 가이드: 관리 민감한 응용 프로그램에 대 한 추가 다단계 인증 위험](https://technet.microsoft.com/library/dn280946.aspx) (3 단계 참조)|
|보안 부서의 EMC RSA|Microsoft의 Active Directory Federation Services RSA SecurID 인증 에이전트|[Microsoft의 Active Directory Federation Services RSA SecurID 인증 에이전트](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet i n c.|Adfs SafeNet 인증 서비스 (SAS) 에이전트|[SafeNet 인증 서비스: 광고 FS 에이전트 구성 지침에 따라](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|Swisscom|모바일 ID 인증 서비스와 서명 서비스|[모바일 ID 인증 서비스](http://swisscom.ch/mid)|
|Symantec|ID 보호 서비스 (VIP)를 Symantec 유효성 검사|[ID 보호 서비스 (VIP)를 Symantec 유효성 검사](http://www.symantec.com/vip-authentication-service)|

## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 r 2에서 adfs 사용자 지정 인증 방법
이제 ADFS Windows Server 2012 r 2에서에 대 한 직접 사용자 지정 인증 방법을 구축 하기 위한 지침을 제공 했습니다. 자세한 내용은 참조 [ADFS Windows Server 2012 r 2에서에 대 한 사용자 지정 인증 방법을 빌드](https://go.microsoft.com/fwlink/?LinkID=511980)합니다.

## <a name="see-also"></a>참조 하십시오
[추가 다단계 인증 민감한 응용 프로그램에 대 한 위험을 관리](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


