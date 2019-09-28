---
title: 클러스터에 원격 액세스 배포
description: 이 항목은 Windows Server 2016의 클러스터에 원격 액세스 배포 가이드의 일부입니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5e4108eee0c62ae4d4db31560b31a6f90751c6b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404650"
---
# <a name="deploy-remote-access-in-a-cluster"></a>클러스터에 원격 액세스 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016 및 Windows Server 2012에서는 DirectAccess 및 원격 액세스 서비스 \(RAS @ no__t-1 VPN을 단일 원격 액세스 역할로 결합 합니다. 다양 한 엔터프라이즈 시나리오에서 원격 액세스를 배포할 수 있습니다. 이 개요에서는 Windows 네트워크 부하 분산을 사용 하 여 부하 분산 된 클러스터에 여러 원격 액세스 서버를 배포 하는 엔터프라이즈 시나리오를 소개 합니다. \(NLB @ no__t-1 또는 외부 부하 분산 장치 \(ELB @ no__t-3 (예: F5) Big @ no__t-4IP  

## <a name="BKMK_OVER"></a>시나리오 설명  
클러스터 배포는 여러 원격 액세스 서버를 단일 단위로 수집 하며,이는 외부 가상 IP를 사용 하 여 DirectAccess 또는 VPN을 통해 내부 회사 네트워크에 연결 하는 원격 클라이언트 컴퓨터의 단일 연락 지점 역할을 합니다 @no__ t-0VIP @ no__t-원격 액세스 클러스터의 주소입니다.  클러스터에 대 한 트래픽은 Windows NLB 또는 외부 부하 @no__t 분산 장치 (예: F5 Big @ no__t-1IP @ no__t-2)를 사용 하 여 부하 분산 됩니다.  

## <a name="prerequisites"></a>사전 요구 사항  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  

-   Windows NLB를 통한 기본 부하 분산.  

-   외부 부하 분산 장치가 지원됩니다.  

-   유니캐스트 모드가 NLB에 대한 기본 및 권장 모드입니다.  

-   DirectAccess 관리 콘솔 또는 PowerShell cmdlet 외부에서 정책을 변경하는 것이 지원되지 않습니다.  

-   NLB 또는 외부 부하 분산 장치를 사용 하는 경우에는 IPHTTPS 접두사를 \/59 이외의 값으로 변경할 수 없습니다.  

-   부하 분산된 노드는 동일한 IPv4 서브넷에 있어야 합니다.  

-   ELB 배포에서 관리를 필요로 하는 경우 DirectAccess 클라이언트는 @ no__t-0Teredo를 사용할 수 없습니다. End @ no__t-0to @ no__t-1end 통신에는 IPHTTPS만 사용할 수 있습니다.  

-   알려진 모든 NLB @ no__t-0ELB 핫픽스가 설치 되어 있는지 확인 합니다.  

-   회사 네트워크의 ISATAP는 지원되지 않습니다. ISATAP를 사용 중인 경우 이를 제거하고 기본 IPv6을 사용해야 합니다.  

## <a name="in-this-scenario"></a>이 시나리오의 내용  
클러스터 배포 시나리오는 다음과 같은 단계로 구성됩니다.  

1.  [고급 옵션을 사용 하 여 Always ON VPN 서버를 배포](../../vpn/always-on-vpn/deploy/always-on-vpn-adv-options.md)합니다. 클러스터 배포를 설정 하기 전에 고급 설정이 있는 단일 원격 액세스 서버를 배포 해야 합니다.  

2.  [원격 액세스 클러스터 배포를 계획](plan/Plan-a-Remote-Access-Cluster-Deployment.md)합니다. 단일 서버 배포에서 클러스터를 빌드하려면 클러스터 배포에 대 한 인증서 준비를 포함 하 여 많은 추가 단계가 필요 합니다.  

3.  [원격 액세스 클러스터를 구성](configure/Configure-a-Remote-Access-Cluster.md)합니다. 이는 Windows NLB 또는 외부 부하 분산 장치에 대해 단일 서버 준비, 클러스터에 추가할 추가 서버 준비, 부하 분산 사용 등의 여러 구성 단계로 구성 됩니다.  

## <a name="BKMK_APP"></a>실용적인 응용 프로그램  
여러 서버를 하나의 서버 클러스터로 수집하면 다음과 같은 이점이 있습니다.  

-   확장성입니다. 단일 원격 액세스 서버는 제한 된 수준의 서버 안정성 및 확장 가능한 성능을 제공 합니다. 둘 이상의 서버 리소스를 단일 클러스터로 그룹화함으로써 사용자 수와 처리량을 늘릴 수 있습니다.  

-   고가용성. 클러스터는 액세스 시 always @ no__t-0on 고가용성을 제공 합니다. 클러스터의 한 서버에서 실패할 경우 원격 사용자가 클러스터의 다른 서버를 통해 회사 네트워크에 지속적으로 액세스할 수 있습니다. 클러스터의 모든 서버는 동일한 클러스터 가상 IP \(VIP @ no__t 주소 집합을 포함 하는 동시에 각 서버에 대해 고유한 전용 IP 주소를 계속 유지 관리 합니다.  

-   편리한 @ no__t-0of @ no__t-1management. 클러스터를 통해 여러 서버를 단일 엔터티로 관리할 수 있습니다. 공유 설정은 클러스터 서버 전반에서 쉽게 설정할 수 있습니다. 원격 액세스 설정은 클러스터에 있는 임의의 서버에서 관리 하거나 원격 서버 관리 도구 \(RSAT @ no__t-1을 사용 하 여 원격으로 관리할 수 있습니다. 또한 전체 클러스터는 단일 원격 액세스 관리 콘솔에서 모니터링할 수 있습니다.  

## <a name="BKMK_NEW"></a>이 시나리오에 포함 된 역할 및 기능  
다음 표에는 시나리오에 필요한 역할 및 기능이 나와 있습니다.  

|Role @ no__t-0feature|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 역할|이 역할은 서버 관리자 콘솔을 사용하여 설치 및 제거됩니다. 이전에는 Windows Server 2008 r 2의 기능 이었던 DirectAccess와 라우팅 및 원격 액세스 서비스 \(RRAS @ no__t-1을 모두 포함 합니다 .이는 이전에 네트워크 정책 및 액세스 서비스 \(NPAS @ no__t-3의 역할 서비스 였습니다. 서버 역할. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />-Always On VPN 및 라우팅 및 원격 액세스 서비스 \(RRAS @ no__t VPN-DirectAccess와 VPN은 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />RRAS 라우팅 RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />종속성은 다음과 같습니다.<br /><br />-인터넷 정보 서비스 \(IIS @ no__t-1 웹 서버-이 기능은 네트워크 위치 서버와 기본 웹 프로브를 구성 하는 데 필요 합니다.<br />Windows 로컬 계정에 원격 액세스 서버에 대 한 내부 Database-Used 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치 됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지 원하는 때 기본적으로 원격 액세스 서버에 설치 됩니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 GUI 및 명령줄 도구<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />-RAS 연결 관리자 관리 키트 \(CMAK @ no__t-1<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
|네트워크 부하 분산|이 기능은 Windows NLB을 사용하여 클러스터의 부하를 분산합니다.|  

## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  

-   Windows Server 2012에 대 한 하드웨어 요구 사항을 충족 하는 컴퓨터가 두 대 이상 있어야 합니다.  

-   외부 Load Balancer 시나리오의 경우 전용 하드웨어가 필요 합니다 (\(9.e. F5 이상 Ip @ no__t-1).  

-   시나리오를 테스트 하려면 Windows 10을 실행 하는 하나 이상의 컴퓨터가 Always On VPN 클라이언트로 구성 되어 있어야 합니다.   

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오에 필요한 요구 사항은 다음과 같이 다양합니다.  

-   단일 서버 배포에 필요한 소프트웨어 요구 사항. 자세한 내용은 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포를](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)참조 하세요. 단일 원격 액세스).  

-   단일 서버에 대 한 소프트웨어 요구 사항 외에도 몇 가지 클러스터 @ no__t-0specific 요구 사항이 있습니다.  

    -   각 클러스터 서버에서 IP @ no__t-0HTTPS 인증서 주체 이름은 ConnectTo 주소와 일치 해야 합니다. 클러스터 배포는 클러스터 서버에서 와일드 카드 및 비 @ no__t-0wildcard 카드 인증서를 혼합 하 여 지원 합니다.  

    -   네트워크 위치 서버가 원격 액세스 서버에 설치되어 있는 경우 각 클러스터 서버에서 네트워크 위치 서버 인증서의 주체 이름이 같아야 합니다. 또한 네트워크 위치 서버 인증서의 이름은 DirectAccess 배포의 서버와 동일한 이름을 사용할 수 없습니다.  

    -   단일 서버에 대 한 인증서를 발급 한 것과 동일한 방법을 사용 하 여 IP @ no__t-0HTTPS 및 네트워크 위치 서버 인증서를 발급 해야 합니다. 예를 들어 단일 서버에서 공용 인증 @no__t 기관을 사용 하는 경우-0CA @ no__t-1을 사용 하는 경우 클러스터의 모든 서버에는 공용 CA에서 발급 한 인증서가 있어야 합니다. 또는 단일 서버에서 IP @ no__t-1HTTPS에 대해 자체 @ no__t-0signed 인증서를 사용 하는 경우 클러스터의 모든 서버에서 이와 같은 작업을 수행 해야 합니다.  

    -   서버 클러스터의 DirectAccess 클라이언트 컴퓨터에 할당된 IPv6 접두사는 59비트여야 합니다. VPN이 사용하도록 설정되어 있는 경우 VPN 접두사도 59비트여야 합니다.  

## <a name="KnownIssues"></a>알려진 문제  
클러스터 시나리오를 구성할 때의 알려진 문제는 다음과 같습니다.  

-   단일 네트워크 어댑터를 사용 하 여 IPv4 @ no__t-0only 배포에서 DirectAccess를 구성 하 고, ": 3333:: @no__t"을 포함 하는 기본 DNS64 \(the IPv6 주소가 네트워크 어댑터에서 자동으로 구성 된 후에는를 사용 하도록 설정 하려고 시도 합니다. Remote Access Management console을 통해 load @ no__t-3을 사용 하면 사용자가 IPv6 DIP를 제공 하 라는 메시지가 표시 됩니다. IPv6 DIP가 제공된 경우 **커밋** 클릭 후 다음 오류와 함께 구성에 실패합니다. 매개 변수가 잘못되었습니다.  

    이 문제를 해결하려면  

    1.  [원격 액세스 구성 백업 및 복원](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)에서 백업을 다운로드하고 스크립트를 복원합니다.  

    2.  다운로드 한 스크립트 백업 @ no__t-0RemoteAccess. p s 1을 사용 하 여 원격 액세스 Gpo를 백업 합니다.  

    3.  실패한 단계에서 부하 분산 사용 설정을 시도합니다. 부하 분산 사용 대화 상자에서 세부 정보 영역을 확장 하 고, 세부 정보 영역에서 @ no__t를 마우스 오른쪽 단추로 클릭 한 다음 **스크립트 복사**를 클릭 합니다.  

    4.  메모장을 열고 클립보드의 내용을 붙여넣습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19 /255.255.255.0','fdc4:29bd:abde:3333::2/128') -InternetVirtualIPAddress @('fdc4:29bd:abde:3333::1/128', '10.244.4.21 /255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  

    5.  열려 있는 모든 원격 액세스 대화 상자와 원격 액세스 관리 콘솔을 닫습니다.  

    6.  붙여넣은 텍스트를 편집하고 IPv6 주소를 제거합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19 /255.255.255.0') -InternetVirtualIPAddress @('10.244.4.21 /255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  

    7.  관리자 권한 PowerShell 창에서 이전 단계의 명령을 실행합니다.  

    8.  잘못 된 입력 값 @ no__t를 사용 하 여 cmdlet이 @no__t 실행 되는 동안 오류가 발생 하는 경우 @ no__t-2RemoteAccess 명령을 실행 하 고 지침에 따라 원래 구성의 무결성이 유지 되는지 확인 합니다.  

    9. 이제 원격 액세스 관리 콘솔을 다시 열 수 있습니다.  
