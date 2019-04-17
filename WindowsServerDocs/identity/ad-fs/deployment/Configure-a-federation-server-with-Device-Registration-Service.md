---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: "디바이스 등록 서비스에 federation 서버를 구성 합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 511a039afd47cf7570fffdcaf17842e0eccc5683
ms.sourcegitcommit: 9278435cbfa8dbeb30d0557ed0d27832b154edd2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>디바이스 등록 서비스에 federation 서버를 구성 합니다.

>Windows Server 2012 r 2에 적용 됩니다.

절차에 완료 한 후 디바이스 등록 서비스 \(DRS\) 해당 federation 서버에서 사용할 수 있습니다 [4 단계: Federation 서버 구성](https://technet.microsoft.com/library/dn303424.aspx)합니다. 디바이스 등록 서비스를 원활 하 게 초 동안 온 보 딩 메커니즘 인증과 영구 단일 sign\ 켜 짐 \(SSO\), 회사 리소스에 액세스 해야 하는 고객에 게 조건부 액세스를 고려 합니다. DRS에 대 한 자세한 내용은 참조 [SSO 및 원활 하 게 두 번째 요소 인증 간에 회사 응용 프로그램에 모든 디바이스에서 회사에 가입](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>장치를 지원 하기 위해 사용자 Active Directory 숲 준비  
  
> [!NOTE]  
> 장치를 지원 하기 위해 사용자 Active Directory 숲 준비를 실행 해야 하는 one\ 때 작업입니다. 엔터프라이즈 관리자 권한으로 로그온 및 Active Directory 숲이이 절차를 완료 하려면 Windows Server 2012 r 2 스키마 되어 있어야 합니다.  
>   
> 또한 DRS 숲 루트 도메인에 하나 이상의 드 서버가 있어야 합니다. 드 서버 Initialize\ ADDeviceRegistration 실행 하는 데 필요한 ADFS 인증 하는 동안 하 고 있습니다. ADFS 각 인증 요청에 DRS 구성 개체의 in\ 메모리 표현을 초기화 하 고 있는 DRS 개체 Initialize\ ADDeviceRegistration 중 제공한 GC에 대 한 요청을 시도 DRS 구성 개체 없는 경우 dc 현재 도메인을 합니다.  
  
#### <a name="to-prepare-the-active-directory-forest"></a>준비 Active Directory 숲  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창과 입력을 엽니다.  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  ServiceAccountName에 대 한 메시지가 표시 되 면 adfs 선택한 서비스 계정으로 서비스 계정의 이름을 입력 합니다.  GMSA 계정인 경우 계정에 입력 하는 **domain\\accountname$** 형식 있습니다. 도메인 계정에 대 한 형식을 사용 하 여 **domain\\accountname**합니다.  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>Federation 서버 농장 노드에서 디바이스 등록 서비스를 사용 하도록 설정  
  
> [!NOTE]  
> 도메인이이 절차를 수행 하려면 관리자 권한으로 로그온 해야 합니다.  
  
#### <a name="to-enable-device-registration-service"></a>디바이스 등록 서비스를 사용 하도록 설정 하려면  
  
1.  해당 federation 서버를 Windows PowerShell 명령 창과 입력을 엽니다.  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  ADFS 농장의 각 federation 농장 노드에서이 단계를 반복 합니다.  
  
## <a name="enable-seamless-second-factor-authentication"></a>원활 하 게을 사용 하면 두 번째 단계 인증  
원활 하 게는 adfs 수준을 기업 리소스와 응용 프로그램에 액세스 하려고 외부 디바이스에서 액세스 보호를 제공 하는 향상 된 두 번째 요소 인증 합니다. 개인 디바이스를 회사 가입 '알려진된' 디바이스 수 있으며 리소스에 조건부 및 게이트 액세스를 생성 하려면 관리자가이 정보를 사용할 수 있습니다.  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>두 번째 원활 하 게 사용 하도록 설정 하려면 요인 영구 단일 sign\ 켜 짐 \(SSO\) 인증과 회사 가입 디바이스용 조건부 액세스  
  
1.  AD FS Management console에서 인증 정책으로 이동 합니다. 전 세계 주요 인증 편집을 선택 합니다. 디바이스 인증을 옆의 확인란을 선택 하 고 확인을 클릭 합니다.  
  
## <a name="update-the-web-application-proxy-configuration"></a>웹 응용 프로그램 프록시 구성을 업데이트합니다  
  
> [!IMPORTANT]  
> 웹 응용 프로그램 프록시에 게시 디바이스 등록 서비스 필요가 없습니다.  디바이스 등록 서비스 federation 서버에서 활성화 되 면 웹 응용 프로그램 프록시를 통해 제공 됩니다.  이 절차 디바이스 등록 서비스를 사용 하기 전에 배포한 웹 응용 프로그램 프록시 구성을 업데이트를 완료 해야 할 수 있습니다.  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>웹 응용 프로그램 프록시 구성을 업데이트  
  
1.  웹 응용 프로그램 프록시 서버의 명령 창 Windows PowerShell 및 종류를 열으십시오  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  자격 증명을 대화 상자가 나타나면 federation 서버에 관리자 권한이 있는 계정 자격 증명을 입력 합니다.  
  
## <a name="see-also"></a>참조 하십시오 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[지침에 따라 Windows Server 2012 r 2 광고 FS 배포](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Federation 서버 농장 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

