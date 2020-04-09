---
ms.assetid: fdd1c1fd-55aa-4eb8-ae84-53f811de042c
title: Device Registration Service를 사용하여 페더레이션 서버 구성
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c7775801940faeba07ad91aa81434a34c97eb6bc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855516"
---
# <a name="configure-a-federation-server-with-device-registration-service"></a>Device Registration Service를 사용하여 페더레이션 서버 구성

[4 단계: 페더레이션 서버 구성](https://technet.microsoft.com/library/dn303424.aspx)의 절차를 완료 한 후에 페더레이션 서버에서 장치 등록 서비스 \(DRS\)를 사용 하도록 설정할 수 있습니다. 장치 등록 서비스는 원활한 두 번째 단계 인증을 위한 온 보 딩 메커니즘, \(SSO\)의 영구 single sign\-및 회사 리소스에 액세스 해야 하는 소비자에 대 한 조건부 액세스를 제공 합니다. DRS에 대 한 자세한 내용은 [회사 응용 프로그램 전체에서 SSO 및 원활한 두 번째 단계 인증을 위한 모든 장치의 작업 공간 연결](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md) 을 참조 하세요.  
  
## <a name="prepare-your-active-directory-forest-to-support-devices"></a>장치를 지원 하도록 Active Directory 포리스트 준비  
  
> [!NOTE]  
> 장치를 지원 하기 위해 Active Directory 포리스트를 준비 하기 위해 실행 해야 하는 한\-시간 작업입니다. 이 절차를 완료 하려면 엔터프라이즈 관리자 권한으로 로그온 해야 하며 Active Directory 포리스트에 Windows Server 2012 R2 스키마가 있어야 합니다.  
>   
> 또한 DRS를 사용 하려면 포리스트 루트 도메인에 하나 이상의 글로벌 카탈로그 서버가 있어야 합니다. 초기화\-ADDeviceRegistration를 실행 하 고 AD FS 인증 하는 동안에는 글로벌 카탈로그 서버가 필요 합니다. AD FS는 각 인증 요청에 대해 DRS 구성 개체의\-메모리 표시를 초기화 하 고, 현재 도메인의 DC에서 DRS 구성 개체를 찾을 수 없는 경우 초기화\-ADDeviceRegistration 하는 동안 DRS 개체가 프로 비전 된 GC에 대해 요청을 시도 합니다.  
  
#### <a name="to-prepare-the-active-directory-forest"></a>Active Directory 포리스트를 준비 하려면  
  
1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음을 입력 합니다.  
  
    ```  
    Initialize-ADDeviceRegistration  
    ```  
  
2.  ServiceAccountName을 입력하라는 메시지가 표시되면 AD FS용 서비스 계정으로 선택한 서비스 계정의 이름을 입력합니다.  계정이 gMSA 경우 **도메인\\accountname $** format에 계정을 입력 합니다. 도메인 계정의 경우 **도메인\\accountname**형식을 사용 합니다.  
  
## <a name="enable-device-registration-service-on-a-federation-server-farm-node"></a>페더레이션 서버 팜 노드에서 장치 등록 서비스를 사용 하도록 설정  
  
> [!NOTE]  
> 이 절차를 완료 하려면 도메인 관리자 권한으로 로그온 해야 합니다.  
  
#### <a name="to-enable-device-registration-service"></a>장치 등록 서비스를 사용 하도록 설정 하려면  
  
1.  페더레이션 서버에서 Windows PowerShell 명령 창을 열고 다음을 입력 합니다.  
  
    ```  
    Enable-AdfsDeviceRegistration  
    ```  
  
2.  AD FS 팜의 각 페더레이션 팜 노드에서이 단계를 반복 합니다.  
  
## <a name="enable-seamless-second-factor-authentication"></a>원활한 두 번째 단계 인증 사용  
원활한 두 번째 단계 인증은 회사 리소스 및 응용 프로그램에 액세스를 시도 하는 외부 장치의 응용 프로그램에 추가 된 액세스 보호 수준을 제공 하는 AD FS의 향상 된 기능입니다. 개인 장치가 작업 공간에 연결 된 경우이 장치는 ' 알려진 ' 장치가 되며, 관리자는이 정보를 사용 하 여 조건부 액세스를 유도 하 고 리소스에 대 한 게이트를 액세스할 수 있습니다.  
  
#### <a name="to-enable-seamless-second-factor-authentication-persistent-single-sign-on-sso-and-conditional-access-for-workplace-joined-devices"></a>원활한 두 번째 단계 인증을 사용 하도록 설정 하려면 \(SSO\) 및 작업 공간 연결 장치에 대 한 조건부 액세스에 대 한 영구 single sign\-  
  
1.  AD FS 관리 콘솔에서 인증 정책으로 이동 합니다. 전역 기본 인증 편집을 선택합니다. 장치 인증 사용 옆의 확인란을 선택하고 확인을 클릭합니다.  
  
## <a name="update-the-web-application-proxy-configuration"></a>웹 응용 프로그램 프록시 구성 업데이트  
  
> [!IMPORTANT]  
> 웹 응용 프로그램 프록시에는 장치 등록 서비스를 게시할 필요가 없습니다.  장치 등록 서비스는 페더레이션 서버에서 사용 하도록 설정 되 면 웹 응용 프로그램 프록시를 통해 제공 됩니다.  이 절차를 완료 하 여 장치 등록 서비스를 사용 하도록 설정 하기 전에 배포 된 웹 응용 프로그램 프록시 구성을 업데이트 해야 할 수 있습니다.  
  
#### <a name="to-update-the-web-application-proxy-configuration"></a>웹 응용 프로그램 프록시 구성을 업데이트 하려면  
  
1.  웹 응용 프로그램 프록시 서버에서 Windows PowerShell 명령 창을 열고 다음을 입력 합니다.  
  
    ```  
    Update-WebApplicationProxyDeviceRegistration  
    ```  
  
2.  자격 증명을 입력 하 라는 메시지가 표시 되 면 페더레이션 서버에 대 한 관리 권한이 있는 계정의 자격 증명을 입력 합니다.  
  
## <a name="see-also"></a>참고 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

