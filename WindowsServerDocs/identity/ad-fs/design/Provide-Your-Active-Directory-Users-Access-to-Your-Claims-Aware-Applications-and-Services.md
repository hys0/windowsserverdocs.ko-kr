---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: "인식 클레임 응용 프로그램 및 서비스에 사용자 Active Directory 사용자가 액세스할 수 있도록"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f6fb37c16c20915c0051e3a24cdb0c147ae92d9c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>인식 클레임 응용 프로그램 및 서비스에 사용자 Active Directory 사용자가 액세스할 수 있도록

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Federation Services \(AD FS\) 배포에서 계정 파트너 조직에는 관리자 시간과 여 호스팅된 리소스에 회사 네트워크에는 직원 single\ sign\-켜 짐 \(SSO\) 액세스를 제공 하는 배포 목표는 다음과 같습니다.  
  
-   회사 네트워크에서 Active Directory 숲에 로그인 되어 있는 직원 SSO 사용 여러 응용 프로그램 또는 조직에서 주변 네트워크의 서비스에 액세스할 수 있습니다. 이러한 응용 프로그램과 서비스 Adfs로 보호 됩니다.  
  
    예를 들어, Fabrikam 회사 네트워크 직원 Fabrikam에 대 한 주변 네트워크에서 호스트 되는 Web\ 기반 응용 프로그램에 대 한 액세스를 연방 있는 하 않도록 할 수 있습니다.  
  
-   원격 직원에 게 Active Directory 도메인 로그온 ADFS 토큰 federation 서버 광고 FS\ 보안 Web\ 기반 응용 프로그램이 나 조직에도 있는 서비스에 연결 된 액세스할 조직에서 얻을 수 있습니다.  
  
-   에 직원 ADFS 토큰 Active Directory 특성 스토어에 대 한 정보를 채울 수 있습니다.  
  
다음과 같은 구성 요소는이 배포 목표에 대해 필요 합니다.  
  
-   **Active Directory Domain Services \ (AD DS \):** AD DS ADFS 토큰 생성 하는 데 사용 하는 직원의 사용자 계정에 포함 되어 있습니다. 그룹 구성원 및 특성 같은 정보 그룹 청구 및 사용자 지정 클레임 ADFS 토큰으로 채워집니다.  
  
    > [!NOTE]  
    > ADFS 토큰 생성 하기 위해 id 포함 LDAP(Lightweight Directory Access Protocol) \(LDAP\) 또는 구조적 쿼리 언어 \(SQL\) 사용할 수 있습니다.  
  
-   **기업 DNS:** Domain Name System \(DNS\)이 구현 인트라넷 클라이언트 계정 federation 서버를 찾을 수 있도록 간단한 호스트 \(A\) 리소스 기록에 포함 되어 있습니다. Dns이 구현 하는 회사 네트워크에 필요한 다른 DNS 레코드 호스팅할도 수 있습니다. 자세한 내용은 참조 [이름을 확인 요구 사항을 Federation 서버에 대 한](Name-Resolution-Requirements-for-Federation-Servers.md)합니다.  
  
-   **계정 파트너 federation 서버:** 이 federation 서버 계정 파트너 숲 속의 도메인에 가입입니다. 인증 직원 사용자 계정 및 ADFS 토큰 생성 합니다. 직원에 대 한 클라이언트 컴퓨터 ADFS 토큰을 얻기 위해이 federation 서버에 대 한 Windows 통합 인증을 수행 합니다. 자세한 내용은 참조 [계정 파트너에 해당 Federation 서버의 역할 검토](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)합니다.  
  
    계정 파트너 federation 서버 다음 사용자에 게 인증할 수 있습니다.  
  
    -   사용자이 도메인 계정에이 직원  
  
    -   이 숲 속의 아무 곳 이나 사용자 계정으로 직원  
  
    -   이 숲에서 사용자가 있는 포리스트 어디서 나 사용자 계정으로 직원 신뢰 하 \ (통해 two\ 방법은 Windows trust\)  
  
-   **직원:** 직원 Web\ 기반 서비스에 액세스 \(through an application\) Web\ 기반 응용 프로그램이 나 \ (지원 되는 웹 browser\)를 통해 사용자가 로그온 회사 네트워크에 있습니다. 회사 네트워크에는 직원 클라이언트 컴퓨터 통신 federation 서버 인증을 위한와 직접 합니다.  
  
연결 된 항목에 대 한 정보를 검토 한 후 하기에 나와 있는 단계에 따라이 목표를 배포 [검사: 웹 SSO 연방 디자인을 구현](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)합니다.  
  
다음은 각각의이 ADFS 배포 목표에 필요한 구성 요소입니다.  
  
![사용자 청구에 대 한 액세스](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
