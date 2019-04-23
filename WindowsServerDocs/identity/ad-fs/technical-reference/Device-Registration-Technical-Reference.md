---
ms.assetid: 69ec592a-5499-4249-8ba0-afa356a8ff75
title: 장치 등록 기술 참조
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fac6437e9b6c3893064769a8279c2cf96cbc47d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833784"
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2

# <a name="device-registration-technical-reference"></a>장치 등록 기술 참조
Device Registration Service \(DRS\) 는 Windows Server 2012 R2에서 Active Directory 페더레이션 서비스 역할을 사용 하 여 포함 된 새 Windows 서비스입니다.  DRS는 AD FS 팜의 모든 페더레이션 서버에서 설치 및 구성해야 합니다.  DRS 배포에 대한 자세한 내용은 [Device Registration Service를 사용하여 페더레이션 서버 구성](https://technet.microsoft.com/library/dn486831.aspx)을 참조하세요.  
  
## <a name="active-directory-objects-created-when-a-device-is-registered"></a>장치 등록 시 Active Directory 개체 생성  
Device Registration Service 중 다음 Active Directory 개체가 만들어집니다.  
  
### <a name="device-registration-configuration"></a>장치 등록 구성  
장치 등록 구성은 Active Directory 포리스트의 구성 명명 컨텍스트로 저장됩니다(예: \(예를 들어 **CN\=Device Registration Configuration, CN\=Services < configuration\-명명\-컨텍스트 >**\)합니다. 이 개체는 Active Directory 포리스트가 장치 등록을 위해 초기화될 때 생성됩니다.  
  
장치 등록 구성에는 다음 요소가 포함됩니다.  
  
-   **발급자 키**  
  
    등록된 장치와 연관된 X.509 인증서를 발급하는 데 사용되는 공개 및 개인 키입니다.  개인 키는 DKM으로 보호합니다.  
  
-   **Device Registration Service 구성**  
  
    Device Registration Service와 관련된 정책입니다.  
  
### <a name="registered-devices-container"></a>등록된 장치 컨테이너  
장치 개체 컨테이너는 Active Directory 포리스트에 있는 도메인 중 하나에 만들어집니다.  이 개체 컨테이너에는 Active Directory 포리스트의 모든 장치 개체가 포함됩니다.  
  
기본적으로 컨테이너는 AD FS와 동일한 도메인에 만들어집니다(예:  \(예를 들어 **CN\=RegisteredDevices, DC\=< 기본값\-명명\-컨텍스트 >**\)합니다. 이 개체는 Active Directory 포리스트가 장치 등록을 위해 초기화 될 때 생성 됩니다.  
  
### <a name="registered-devices"></a>등록된 장치  
장치 개체는 Active Directory의 새로운 경량 개체로,  사용자, 장치 및 회사 간의 관계를 나타내는 데 사용됩니다.  장치 개체는 AD FS에서 서명한 인증서를 사용하여 Active Directory의 논리적 장치 개체에 물리적 장치를 고정합니다.  
  
등록된 장치에는 다음 요소가 포함됩니다.  
  
-   **표시 이름**  
  
    장치의 식별 이름입니다.  Windows 장치의 경우 컴퓨터의 호스트 이름입니다.  
  
-   **장치 Id**  
  
    장치 등록 서버에 의해 생성되는 GUID입니다.  
  
-   **인증서 지문**  
  
    등록된 장치에 사용되는 X.509 인증서의 인증서 지문입니다.  
  
-   **OS 유형**  
  
    장치의 운영 체제 유형입니다.  
  
-   **OS 버전**  
  
    장치의 운영 체제 버전입니다.  
  
-   **사용 가능**  
  
    Active Directory에서 장치를 사용할 수 있는지 여부를 나타내는 부울입니다.  사용하도록 설정된 장치만 서비스에 액세스할 수 있습니다.  
  
-   **대략적인 마지막 사용 시간**  
  
    장치가 리소스 액세스에 사용된 대략적인 시간입니다.  복제 트래픽을 제한하기 위해 14일에 한 번씩만 업데이트됩니다.  
  
-   **등록 된 소유자**  
  
    보안 Id \(SID\) 이 장치를 작업 공간 가입 하는 사용자입니다.  
  
## <a name="ad-fsdrs-server-ssl-certificate-revocation-checking"></a>AD FS\/DRS 서버 SSL 인증서 해지 확인  
작업 공간 연결 클라이언트는 AD FS 서버 SSL 인증서의 유효성을 검사합니다.  AD FS 서버 SSL 인증서를 인증서 해지 목록에 포함 된 경우 \(CRL\) 끝점에 클라이언트 인증서 유효성을 검사할 지정 된 끝점에 연결할 수 여야 합니다.  
  
테스트 환경 및 테스트 인증 기관 사용 하는지 \(CA\) CA에서 발급 한 서버 인증서에 CRL 끝점을 포함 하지 않도록 선택할 수 있습니다 서버 SSL 인증서를 발급 하도록 합니다.  이렇게 하면 작업 공간 연결 클라이언트가 CRL 검사를 바이패스할 수 있습니다.  
  
> [!CAUTION]  
> 프로덕션 시스템에서는 이 방법을 사용하지 마세요.  
  

