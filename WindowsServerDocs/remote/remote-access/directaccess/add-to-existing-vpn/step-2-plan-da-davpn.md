---
title: 2 단계 DirectAccess 배포 계획
description: 이 항목은 Windows Server 2016에 대 한 기존 원격 액세스 (VPN) 배포에 DirectAccess 추가 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 72b5b2af-6925-41e0-a3f9-b8809ed711d1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 865f9ffd3eed3ce145364c227845af097194416e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309241"
---
# <a name="step-2-plan-the-directaccess-deployment"></a>2 단계 DirectAccess 배포 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

원격 액세스 인프라를 계획한 후에는 DirectAccess 사용 마법사에 대한 설정을 계획해야 합니다.  
  
|작업|설명|  
|----|--------|  
|클라이언트 배포 계획|클라이언트 컴퓨터에서 DirectAccess를 사용하여 연결하도록 허용할 방법을 계획합니다. DirectAccess 클라이언트로 구성될 관리 컴퓨터를 정합니다.|  
|원격 액세스 서버 배포 계획|원격 액세스 서버를 배포할 방법을 계획합니다.|  
  
## <a name="planning-for-client-deployment"></a><a name="bkmk_2_1_client"></a>클라이언트 배포 계획  
클라이언트 배포를 계획할 때 결정해야 하는 두 가지 사항이 있습니다.  
  
-   DirectAccess를 이동 컴퓨터에서만 사용할 수 있나요, 아니면 모든 컴퓨터에서 사용할 수 있나요?  
  
    DirectAccess 사용 마법사에서 DirectAccess 클라이언트를 구성할 때 지정된 보안 그룹의 이동 컴퓨터에서만 DirectAccess를 사용하여 연결하도록 허용할 수 있습니다. 액세스를 이동 컴퓨터로 제한하면 원격 액세스에서 DirectAccess 클라이언트 GPO가 지정된 보안 그룹의 이동 컴퓨터에만 적용되도록 WMI 필터를 자동으로 구성합니다. 이 설정을 사용하려면 원격 액세스 관리자에게 그룹 정책 WMI 필터를 만들거나 수정할 수 있는 권한이 있어야 합니다.  
  
-   DirectAccess 클라이언트 컴퓨터가 어떤 보안 그룹에 포함되나요?  
  
    DirectAccess 설정은 DirectAccess 클라이언트 GPO에 포함됩니다. 이 GPO는 DirectAccess 사용 마법사에서 지정한 보안 그룹에 속한 컴퓨터에 적용됩니다. 지원되는 모든 도메인에 보안 그룹이 포함되도록 지정할 수 있습니다. 원격 액세스를 구성하기 전에 보안 그룹을 만들어야 합니다. DirectAccess 배포를 완료한 후 보안 그룹에 컴퓨터를 추가할 수 있지만 보안 그룹과 다른 도메인에 상주하는 클라이언트 컴퓨터를 추가한 경우 해당 클라이언트에는 클라이언트 GPO가 적용되지 않습니다. 예를 들어 도메인 A에 DirectAccess 클라이언트에 대한 SG1을 만들고 나중에 도메인 B의 클라이언트를 이 그룹에 추가하는 경우 도메인 B의 클라이언트에는 클라이언트 GPO가 적용되지 않습니다. 이 문제를 방지하려면 클라이언트 컴퓨터가 포함된 각 도메인에 대한 새 클라이언트 보안 그룹을 만들어야 합니다. 또는 새 보안 그룹을 만들지 않으려면 새 도메인의 새 GPO 이름으로 Add-DAClient cmdlet을 실행합니다.  
  
## <a name="planning-for-remote-access-server-deployment"></a><a name="bkmk_2_2_server"></a>원격 액세스 서버 배포 계획  
원격 액세스 서버 배포를 계획할 때 결정할 몇 가지 사항이 있습니다.  
  
-   **네트워크 토폴로지**-원격 액세스 서버를 배포할 때 두 가지 토폴로지를 사용할 수 있습니다.  
  
    -   두 개의 **어댑터**-두 개의 네트워크 어댑터를 사용 하 여 원격 액세스는 인터넷에 직접 연결 된 네트워크 어댑터 하나를 사용 하 여 구성할 수 있으며 다른 네트워크 어댑터는 내부 네트워크에 연결 됩니다. 또는 방화벽이나 라우터와 같은 에지 디바이스 뒤에 서버가 설치됩니다. 이 구성에서는 네트워크 어댑터가 경계 네트워크와 내부 네트워크에 각각 하나씩 연결됩니다.  
  
    -   **단일 네트워크 어댑터**-이 구성에서는 방화벽이 나 라우터와 같은에 지 장치 뒤에 원격 액세스 서버를 설치 합니다. 네트워크 어댑터는 내부 네트워크에 연결됩니다.  
  
-   **네트워크 어댑터**-DirectAccess 사용 마법사는 VPN에서 사용 하는 인터페이스에 따라 원격 액세스 서버에 구성 된 네트워크 어댑터를 자동으로 검색 합니다. 올바른 어댑터를 선택해야 합니다.  
  
-   **ConnectTo 주소**-클라이언트 컴퓨터는 원격 액세스 서버에 연결 하기 위해 ConnectTo 주소를 사용 합니다. 선택한 주소는 IP-HTTPS 연결을 위해 배포할 IP-HTTPS 인증서의 주체 이름과 일치해야 하며 공용 DNS에서 사용할 수 있어야 합니다. IP-HTTPS용 웹 사이트 인증서 계획을 참조하세요.  
  
-   **Ip-https 인증서**-sstp VPN이 구성 된 경우 DirectAccess 사용 마법사가 SSTP에서 ip-https에 사용 하는 인증서를 선택 합니다. SSTP VPN이 구성되어 있지 않은 경우 마법사는 IP-HTTPS용 인증서가 구성되어 있는지 확인합니다. 구성되어 있지 않으면 자체 서명된 IP-HTTPS용 인증서를 자동으로 프로비전하고 Kerberos 인증을 자동으로 사용합니다. 또한 마법사는 IPv4 전용 환경에서의 프로토콜 변환에 NAT64 및 DNS64를 사용하도록 설정합니다.  
  
-   **Ipv6 접두사**-마법사는 네트워크 어댑터에 i p v 6이 배포 된 것을 감지 하면 내부 네트워크에 대 한 ipv6 접두사, DirectAccess 클라이언트 컴퓨터에 할당할 ipv6 접두사 및 VPN 클라이언트 컴퓨터에 할당할 ipv6 접두사를 자동으로 만듭니다. 자동으로 생성된 접두사가 기본 IPv6 또는 ISATAP 인프라에 올바르지 않은 경우 수동으로 변경해야 합니다. 1\.1 네트워크와 서버의 토폴로지 및 설정 구성을 참조하세요.  
  
-   **Windows 7 클라이언트**-기본적으로 windows 7 클라이언트 컴퓨터는 windows Server 2012 원격 액세스 배포에 연결할 수 없습니다. 조직에서 내부 리소스에 원격으로 액세스 해야 하는 Windows 7 클라이언트 컴퓨터를 사용 하는 경우 연결 하도록 허용할 수 있습니다. 내부 리소스에 대한 액세스를 허용할 클라이언트 컴퓨터는 DirectAccess 사용 마법사에서 지정한 보안 그룹의 구성원이어야 합니다.  
  
    > [!NOTE]
    > Windows 7 클라이언트 컴퓨터에서 DirectAccess를 사용 하 여 연결 하도록 허용 하려면 컴퓨터 인증서 인증을 사용 해야 합니다.
  
-   **인증**-DirectAccess 사용 마법사는 Active Directory을 사용 하 여 사용자 자격 증명을 인증 합니다. 2단계 인증을 배포하려면 [OTP 인증을 사용하여 원격 액세스 배포](../../ras/otp/Deploy-RA-OTP.md)를 참조하세요.  
  

  


