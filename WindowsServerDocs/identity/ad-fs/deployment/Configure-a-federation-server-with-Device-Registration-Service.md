---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: Device Registration Service를 사용하여 페더레이션 서버 구성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 511a039afd47cf7570fffdcaf17842e0eccc5683
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843064"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>Device Registration Service를 사용하여 페더레이션 서버 구성

>적용 대상: Windows Server 2012 R2

Device Registration Service를 사용할 수 있습니다 \(DRS\) 의 절차를 완료 한 후 페더레이션 서버의 [4 단계: Configure a Federation Server](https://technet.microsoft.com/library/dn303424.aspx)합니다. Device Registration Service에 연속 된 두 번째에 대 한 온 보 딩 메커니즘을 제공 authentication, 영구 single\-대 \(SSO\), 및 회사에 대 한 액세스를 필요로 하는 소비자에 게 조건부 액세스 리소스입니다. DRS에 대 한 자세한 내용은 참조 하세요. [SSO 및 원활한 두 번째 단계 인증에서 회사 응용 프로그램에 대 한 모든 장치에서 작업 공간 연결](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>장치를 지원 하도록 Active Directory 포리스트 준비  
  
> [!NOTE]  
> 이 단일\-장치를 지원 하도록 Active Directory 포리스트를 준비 하기 위해 실행 해야 하는 작업 시간입니다. 엔터프라이즈 관리자 권한으로 로그온 해야 하 고 Active Directory 포리스트에이 절차를 완료 하려면 Windows Server 2012 R2 스키마가 필요 합니다.  
>   
> 또한 DRS 포리스트 루트 도메인에서 글로벌 카탈로그 서버를 하나 이상 있다고 필요 합니다. 글로벌 카탈로그 서버는 초기화를 실행 하는 데 필요한\-ADDeviceRegistration 및 AD FS 인증 중입니다. AD FS 초기화는에서\-각 인증 요청에서 DRS 구성의 메모리 내 표현을 개체 및 DRS 개체 기반이 된 GC에 대 한 요청으로 시도 현재 도메인의 DC에서 DRS 구성 개체를 찾을 수 없습니다, 하는 경우 초기화 하는 동안 프로 비전\-ADDeviceRegistration 합니다.  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Active Directory 포리스트를 준비 하려면  
  
1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 형식:  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  ServiceAccountName에 대 한 메시지가 표시 되 면 AD FS에 대 한 서비스 계정으로 선택한 서비스 계정의 이름을 입력 합니다.  GMSA 계정인 경우 계정을 입력 합니다 **도메인\\accountname$** 형식입니다. 도메인 계정에 대 한 형식을 사용 하 여 **도메인\\accountname**합니다.  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>페더레이션 서버 팜 노드에서 Device Registration Service를 사용 하도록 설정  
  
> [!NOTE]  
> 이 절차를 완료 하려면 도메인 관리자 권한으로 로그온 해야 합니다.  
  
#### <a name="to-enable-device-registration-service"></a>Device Registration Service를 사용 하도록 설정 하려면  
  
1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 형식:  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  AD FS 팜의 각 페더레이션 팜 노드에서이 단계를 반복 하는 중...  
  
## <a name="enable-seamless-second-factor-authentication"></a>사용 원활한 2 단계 인증  
원활한 2 단계 인증 액세스 하려는 외부 장치에서 회사 리소스 및 응용 프로그램에 대 한 액세스 보호 수준을 제공 하는 AD FS에서 향상 된 기능입니다. 개인 장치를 작업 공간 연결 하는 경우 '알려진된' 장치 되며 관리자가이 정보를 사용 하 여 리소스에 액세스를 제어 및 조건부 액세스를 수 있습니다.  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>단계 인증을 사용할 수 있도록 원활 하 게 두 번째 영구 단일 로그온\-대 \(SSO\) 및 작업 공간 연결 장치에 대 한 조건부 액세스  
  
1.  AD FS 관리 콘솔에서 인증 정책으로 이동 합니다. 전역 기본 인증을 편집을 선택 합니다. 장치 인증을 사용 하도록 설정 옆의 확인란을 선택 하 고 확인을 클릭 합니다.  
  
## <a name="update-the-web-application-proxy-configuration"></a>구성 업데이트 하 고 웹 응용 프로그램 프록시  
  
> [!IMPORTANT]  
> 웹 응용 프로그램 프록시를 사용 하는 장치 등록 서비스를 게시할 필요가 없습니다.  페더레이션 서버에서 활성화 되 면 장치 등록 서비스 웹 응용 프로그램 프록시를 통해 제공 됩니다.  Device Registration Service를 사용 하기 전에 배포 된 경우 웹 응용 프로그램 프록시 구성을 업데이트 하려면이 절차를 완료 해야 합니다.  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>웹 응용 프로그램 프록시 구성을 업데이트 하려면  
  
1.  웹 응용 프로그램 프록시 서버에서 Windows PowerShell 명령 창을 열고 유형  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  자격 증명을 묻는 메시지가 나타나면 페더레이션 서버에 대 한 관리 권한이 있는 계정의 자격 증명을 입력 합니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

