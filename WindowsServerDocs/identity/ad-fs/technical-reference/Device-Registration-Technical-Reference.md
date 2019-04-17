---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: "디바이스 등록 기술 참조"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fac6437e9b6c3893064769a8279c2cf96cbc47d6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 r 2

# <a name="device-registration-technical-reference"></a>디바이스 등록 기술 참조
디바이스 등록 서비스 \(DRS\) Active Directory Federation 서비스 역할 Windows Server 2012 r 2와 함께 제공 되는 새로운 Windows 서비스입니다.  DRS 설치 하 고 모든 ADFS 농장의 federation 서버 구성 해야 합니다.  에 대 한 내용은 DRS 배포, [federation 서버 등록 서비스 디바이스를 구성](https://technet.microsoft.com/library/dn486831.aspx)합니다.  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>장치를 등록 시 생성 active Directory 개체  
다음 Active Directory 개체 디바이스 등록 서비스의 일환으로 만들어집니다.  
  
### <a name="device-registration-configuration"></a>디바이스 등록 구성  
장치 등록 구성 Active Directory 숲 속의 구성 명명 컨텍스트에 저장 됩니다. \ (예를 들어, **CN\ = 디바이스 등록 구성 CN\ 서비스 = < configuration\ naming\ 직접 >**\). 장치를 등록에 대 한 Active Directory 숲은 initialed 때이 개체가 만들어집니다.  
  
장치 등록 구성 요소 포함 됩니다.  
  
-   **발행인이 키**  
  
    등록 된 디바이스와 연결 된 X.509 인증서를 실행 하는 데 사용 공개 하 게 비밀로 키.  개인 키는 DKM 보호 합니다.  
  
-   **디바이스 등록 서비스 구성**  
  
    디바이스 등록 서비스에는 정책입니다.  
  
### <a name="registered-devices-container"></a>등록 된 디바이스 컨테이너  
장치 개체 컨테이너 Active Directory 숲 속의 도메인 중 하나를 생성 됩니다.  이 개체 컨테이너의 모든 디바이스에 대 한 Active Directory 숲 개체 포함 됩니다.  
  
기본적으로 컨테이너 Adfs와 같은 도메인에 만들어집니다.  \ (예를 들어, **CN\ DC\ RegisteredDevices = = < default\ naming\ 직접 >**\). 장치를 등록에 대 한 Active Directory 숲은 initialed 때이 개체가 만들어집니다.  
  
### <a name="registered-devices"></a>등록 된 디바이스  
디바이스 개체 Active directory에서 개체 새, 밝은 무게는입니다.  관계를 나타내는 데 사용 됩니다: 사용자, 장치와 회사입니다.  장치 개체 논리 장치 Active Directory 개체 실제 장치를 고정 하려면 Adfs에 의해 서명 인증서를 사용 합니다.  
  
등록 된 디바이스에 다음과 같은 요소 포함 됩니다.  
  
-   **표시 이름**  
  
    디바이스의 이름입니다.  Windows 디바이스에 대 한 컴퓨터의 호스트 이름입니다.  
  
-   **디바이스 Id**  
  
    장치를 등록 server에서 생성 되는 GUID.  
  
-   **인증서 지문**  
  
    등록 된 디바이스와 함께 사용 되는 X.509 인증서의 인증서 지문입니다.  
  
-   **운영 체제 유형**  
  
    디바이스의 운영 체제 종류 합니다.  
  
-   **OS 버전**  
  
    디바이스의 운영 체제의 버전입니다.  
  
-   **사용 하도록 설정**  
  
    디바이스가 Active Directory에 사용 가능 여부를 나타내는 Boolean 합니다.  활성화 된 장치만 서비스에 액세스할 수 있습니다.  
  
-   **마지막 사용 시간 (대략적 크기)**  
  
    장치 리소스에 액세스 하는 데 사용 된 시간 (대략적 크기).  복제 교통량을 제한 하려면만 14 일 마다 업데이트 되 합니다.  
  
-   **등록된 소유자**  
  
    이 장치는 회사에 가입 하는 사용자의 보안 Id \(SID\) 합니다.  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>광고 FS\/DRS 서버 SSL 인증서 해지 확인  
Workplace Join 클라이언트 FS 서버 SSL AD 인증서의 유효성을 검사 합니다.  광고 FS 서버 ssl 포함 인증서 해지 목록 \(CRL\) 끝점, 클라이언트는 인증서를 확인 하는 지정 된 끝점 연결할 수 있어야 합니다.  
  
테스트 환경과 테스트 인증 기관 사용 중인 경우 \(CA\) 인증서를 발급 서버 SSL 서버 인증서 기관에서 발급 한에 CRL 끝점 포함 하지 않도록 선택할 수 있습니다.  이렇게 하면 Workplace Join 클라이언트 CRL 확인을 건너뛸 수 있습니다.  
  
> [!CAUTION]  
> 프로덕션 시스템에 대 한 권장 하지 않습니다.  
  

