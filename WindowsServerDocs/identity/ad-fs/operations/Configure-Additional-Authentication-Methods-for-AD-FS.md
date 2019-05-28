---
ms.assetid: ddfbbda3-30ca-4537-af12-667efc6f63ff
title: AD FS에 대한 추가 인증 방법 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/04/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 88c4d976b9808d254dc1681ce9eee3ca556824ab
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189794"
---
# <a name="configure-additional-authentication-methods-for-ad-fs"></a>AD FS에 대한 추가 인증 방법 구성

MFA(Multi-Factor Authentication)을 사용하려면 하나 이상의 추가 인증 방법을 선택해야 합니다. 기본적으로 Active Directory Federation Services (AD FS) Windows Server 2012 R2에서의 인증서 인증 (즉, 스마트 카드 기반 인증)을 추가 인증 방법으로 선택할 수 있습니다.

> [!NOTE]
> 인증서 인증을 선택한 경우 스마트 카드 인증서가 안전하게 프로비전되고 PIN 요구 사항이 있는지 확인하세요.

Microsoft Azure를 이용하면 클라우드에서 유사한 기능을 사용할 수 있다는 것을 아시나요? [Microsoft Azure ID 솔루션](http://aka.ms/m2w274)에 대해 자세히 알아보세요.<br /><br />Microsoft Azure에서 하이브리드 ID 솔루션을 만듭니다.<br /> - [Azure Multi-factor Authentication에 알아봅니다.](http://aka.ms/ey6o9r)<br /> - [클라우드 인증을 사용 하 여 단일 포리스트 하이브리드 환경에 대 한 id를 관리 합니다.](http://aka.ms/g1jat8)<br /> - [추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험을 관리 합니다.](http://aka.ms/kt1bbm)

## <a name="microsoft-and-third-party-additional-authentication-methods"></a>Microsoft 및 타사 추가 인증 방법
구성 하 고 Microsoft 및 Windows Server 2012 R2에서 AD FS에서 타사 인증 방법 사용 수도 있습니다. 를 설치 하 고 AD FS를 사용 하 여 등록 한 후에 전역 또는 당 당사자 인증 정책의 일부로 MFA를 적용할 수 있습니다.

다음은 현재 Windows Server 2012 R2에서 AD FS용으로 사용할 수 있는 MFA 제품이 있는 Microsoft 및 타사 공급자의 사전순 목록입니다.

|공급자|제품|세부 정보 링크|
|-|-|-| 
|aPersona|aPersona Microsoft ADFS SSO에 대 한 적응 Multi-factor Authentication|[aPersona ASM ADFS Adapter](https://www.apersona.com/adfs)|
|Duo 보안|AD FS에 대 한 duo MFA 어댑터|[AD FS에 대 한 duo 인증](https://duo.com/docs/adfs)|
|Gemalto|Gemalto Identity & Security Services|[http://www.gemalto.com/identity](http://www.gemalto.com/identity)|
|inWebo Technologies|inWebo Enterprise Authentication 서비스|[inWebo Enterprise Authentication](http://www.inwebo.com)|
|Login People|AD FS 2012 R2용 Login People MFA API 커넥터(공개 베타)|[https://www.loginpeople.com](https://www.loginpeople.com)|
|Microsoft Corp.|Microsoft Azure MFA|[연습 가이드: 중요 한 응용 프로그램에 대 한 추가 다단계 인증을 사용한 위험 관리](https://technet.microsoft.com/library/dn280946.aspx) (3 단계 참조)|
Mideye | ADFS에 대 한 mideye 인증 공급자 | [Microsoft Active Directory 페더레이션 서비스를 사용 하 여 mideye 2 단계 인증](https://www.mideye.com/support/administrators/documentation/integration/microsoft-adfs/)|
|Okta | Active Directory Federation Services에 대 한 Okta MFA | [Okta MFA Active Directory federation Services (ADFS)](https://help.okta.com/en/prod/Content/Topics/integrations/adfs-okta-int.htm)|
|하나의 Id| Starling 2FA AD FS|[Starling 2FA AD FS 어댑터](https://www.oneidentity.com/products/starling-two-factor-authentication/)|
|하나의 Id| Defender AD FS|[Defender AD FS 어댑터](https://www.oneidentity.com/products/defender/)|
|Ping Identity|AD FS에 대 한 PingID MFA 어댑터|[AD FS에 대 한 PingID MFA 어댑터](https://documentation.pingidentity.com/pingid/pingidAdminGuide/index.shtml#pid_c_PingIDforADFSSSO.html)|
|RSA, RSA, EMC의 보안 부서|Microsoft Active Directory Federation Services용 RSA SecurID Authentication Agent|[Microsoft Active Directory Federation Services 용 RSA SecurID Authentication Agent](http://www.emc.com/security/rsa-securid/rsa-authentication-agents/microsoft-ad-fs.htm)|
|SafeNet, Inc.|SafeNet Authentication Service (SAS) Agent for AD FS|[SafeNet Authentication Service: AD FS Agent 구성 가이드](http://www.safenet-inc.com/resources/integration-guide/data-protection/Safenet_Authentication_Service/SafeNet_Authentication_Service__AD_FS_Agent_Configuration_Guide/?langtype=1033)|
|SecureMFA|SecureMFA OTP 공급자| [ADFS 다단계 인증 공급자](https://www.securemfa.com/)|
|Swisscom|모바일 ID 인증 서비스와 서명 서비스|[모바일 ID 인증 서비스](http://swisscom.ch/mid)|
|Symantec|Symantec VIP(Validation and ID Protection Service)|[Symantec 유효성 검사 and ID Protection Service (VIP)](http://www.symantec.com/vip-authentication-service)|
|Trusona|필수 (암호 없는 MFA)와 임원 (필수 + Identity 언어 교정)| [Trusona multi-factor Authentication](https://www.trusona.com/solution-overview/)|


## <a name="custom-authentication-method-for-ad-fs-in-windows-server-2012-r2"></a>Windows Server 2012 R2에서의 AD FS용 사용자 지정 인증 방법
Microsoft에서는 이제 Windows Server 2012 R2에서 AD FS용의 사용자 지정 인증 방법을 구성하기 위한 지침을 제공합니다. 자세한 내용은 [Windows Server 2012 R2에서 AD FS용 사용자 지정 인증 방법 구축](https://go.microsoft.com/fwlink/?LinkID=511980)을 참조하세요.

## <a name="see-also"></a>관련 항목
[추가 Multi-factor Authentication for Sensitive Applications 사용 하 여 위험 관리](Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)


