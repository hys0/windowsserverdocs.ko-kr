---
title: 클러스터에 원격 액세스 배포
description: 이 항목은 Windows Server 2016에서 클러스터에 원격 액세스 배포 가이드의 일부입니다.
manager: dougkim
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab2b0731a5673e14fb130d539324701a336f30ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863634"
---
# <a name="deploy-remote-access-in-a-cluster"></a>클러스터에 원격 액세스 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

Windows Server 2016 및 Windows Server 2012 DirectAccess 및 원격 액세스 서비스를 결합 \(RAS\) VPN 단일 원격 액세스 역할을 합니다. 다양 한 엔터프라이즈 시나리오에서에서 원격 액세스를 배포할 수 있습니다. Windows 네트워크 부하 분산 사용 하 여 분산 된 부하를 클러스터에 여러 원격 액세스 서버 배포에 대 한이 개요에서는 엔터프라이즈 시나리오를 소개 \(NLB\) 또는 외부 부하 분산 장치를 사용 하 여 \(ELB \), F5 큰 같은\-IP입니다.  

## <a name="BKMK_OVER"></a>시나리오 설명  
클러스터 배포 외부가상IP를사용하여내부회사네트워크에DirectAccess또는VPN을통해연결하는원격클라이언트컴퓨터에대한연락처의단일지점으로사용하는단일단위로여러원격액세스서버수집\(VIP\) 원격 액세스 클러스터의 주소입니다.  클러스터에 트래픽은 Windows NLB를 사용 하 여 부하가 되거나 외부 부하 분산 장치가 \(같은 F5 빅\-IP\)입니다.  

## <a name="prerequisites"></a>사전 요구 사항  
이 시나리오의 배포를 시작하기 전에 다음 목록에서 중요한 요구 사항을 검토하세요.  

-   Windows NLB를 통한 기본 부하 분산.  

-   외부 부하 분산 장치가 지원됩니다.  

-   유니캐스트 모드가 NLB에 대한 기본 및 권장 모드입니다.  

-   DirectAccess 관리 콘솔 또는 PowerShell cmdlet 외부에서 정책을 변경하는 것이 지원되지 않습니다.  

-   NLB 또는 외부 부하 분산 장치를 사용 하는 경우 IPHTTPS 접두사를 변경할 수 없습니다 어디에 이외의 \/59입니다.  

-   부하 분산된 노드는 동일한 IPv4 서브넷에 있어야 합니다.  

-   ELB 배포의 경우 관리 관리가 필요한 다음 DirectAccess 클라이언트가 사용할 수 없는&nbsp;Teredo입니다. IPHTTPS만 끝에 사용할 수 있습니다\-에\-통신을 종료 합니다.  

-   알려진된 모든 NLB 확인\/ELB 핫픽스가 설치 되어 있습니다.  

-   회사 네트워크의 ISATAP는 지원되지 않습니다. ISATAP를 사용 중인 경우 이를 제거하고 기본 IPv6을 사용해야 합니다.  

## <a name="in-this-scenario"></a>이 시나리오의 내용  
클러스터 배포 시나리오는 다음과 같은 단계로 구성됩니다.  

1.  [고급 옵션을 사용 하 여 VPN 서버에는 항상 배포](../../vpn/always-on-vpn/deploy/always-on-vpn-adv-options.md)합니다. 고급 설정 사용 하 여 단일 원격 액세스 서버 클러스터 배포를 설정 하기 전에 배포 되어야 합니다.  

2.  [원격 액세스 클러스터 배포 계획](plan/Plan-a-Remote-Access-Cluster-Deployment.md)합니다. 단일 서버 배포에서 클러스터의 추가 빌드 단계가 필요를 클러스터 배포에 대 한 인증서를 준비 합니다.  

3.  [원격 액세스 클러스터를 구성](configure/Configure-a-Remote-Access-Cluster.md)합니다. 구성 단계를 Windows NLB 또는 외부 부하 분산 장치에 대 한 단일 서버를 준비, 클러스터에 연결할 추가 서버 준비, 부하 분산 사용 등의 숫자로 구성 됩니다.  

## <a name="BKMK_APP"></a>실제 응용 프로그램  
여러 서버를 하나의 서버 클러스터로 수집하면 다음과 같은 이점이 있습니다.  

-   확장성입니다. 단일 원격 액세스 서버는 제한 된 수준의 서버 안정성 및 확장성이 뛰어난 성능을 제공합니다. 둘 이상의 서버 리소스를 단일 클러스터로 그룹화함으로써 사용자 수와 처리량을 늘릴 수 있습니다.  

-   고가용성입니다. 항상에 대 한 고가용성을 제공 하는 클러스터\-액세스 합니다. 클러스터의 한 서버에서 실패할 경우 원격 사용자가 클러스터의 다른 서버를 통해 회사 네트워크에 지속적으로 액세스할 수 있습니다. 클러스터의 모든 서버 집합이 동일한 클러스터 가상 IP \(VIP\) 주소를 유지 하면서도 고유한 전용 서버 마다 IP 주소입니다.  

-   간편한\-의\-관리 합니다. 클러스터에는 여러 서버를 단일 엔터티로 관리할 수 있습니다. 공유 설정은 클러스터 서버 전반에서 쉽게 설정할 수 있습니다. 원격 액세스 설정은 클러스터 또는 원격 서버 관리 도구를 사용 하 여 원격 서버에서 관리할 수 있습니다 \(RSAT\)합니다. 또한 전체 클러스터는 단일 원격 액세스 관리 콘솔에서 모니터링할 수 있습니다.  

## <a name="BKMK_NEW"></a>역할과이 시나리오에 포함 된 기능  
다음 표에는 시나리오에 필요한 역할 및 기능이 나와 있습니다.  

|역할\/기능|이 시나리오를 지원하는 방법|  
|---------|-----------------|  
|원격 액세스 역할|이 역할은 서버 관리자 콘솔을 사용하여 설치 및 제거됩니다. 해당 DirectAccess 모두 포함 된 이전에 Windows Server 2008 R2와 라우팅 및 원격 액세스 서비스의 기능 \(RRAS\), 역할 서비스는 네트워크 정책 및 액세스 서비스 이전된\(NPAS\) 서버 역할입니다. 원격 액세스 역할은 다음의 두 가지 구성 요소로 구성됩니다.<br /><br />-Always On VPN 및 라우팅 및 원격 액세스 서비스 \(RRAS\) VPN-DirectAccess 및 VPN 원격 액세스 관리 콘솔에서 함께 관리 됩니다.<br />RRAS 라우팅 RRAS 라우팅 기능은 레거시 라우팅 및 원격 액세스 콘솔에서 관리 됩니다.<br /><br />종속성은 다음과 같습니다.<br /><br />인터넷 정보 서비스 \(IIS\) 웹 서버-이 기능은 네트워크 위치 서버와 기본 웹 프로브를 구성 해야 합니다.<br />Windows 로컬 계정에 원격 액세스 서버에 대 한 내부 Database-Used 합니다.|  
|원격 액세스 관리 도구 기능|이 기능은 다음과 같이 설치 됩니다.<br /><br />-이 값은 원격 액세스 역할이 설치 되어 있고 원격 관리 콘솔 사용자 인터페이스를 지 원하는 때 기본적으로 원격 액세스 서버에 설치 됩니다.<br />-앱는 하지 원격 액세스 서버 역할을 실행 하는 서버에 필요에 따라 설치 수 있습니다. 이 경우 이 기능은 DirectAccess 및 VPN을 실행하는 원격 액세스 컴퓨터를 원격으로 관리하는 데 사용됩니다.<br /><br />원격 액세스 관리 도구 기능의 구성 요소는 다음과 같습니다.<br /><br />-원격 액세스 GUI 및 명령줄 도구<br />-Windows PowerShell 용 원격 액세스 모듈<br /><br />이 기능은 다음 요소에 종속됩니다.<br /><br />그룹 정책 관리 콘솔<br />RAS 연결 관리자 관리 키트 \(CMAK\)<br />Windows PowerShell 3.0<br />-그래픽 관리 도구 및 인프라|  
|네트워크 부하 분산|이 기능은 Windows NLB을 사용하여 클러스터의 부하를 분산합니다.|  

## <a name="BKMK_HARD"></a>하드웨어 요구 사항  
이 시나리오의 하드웨어 요구 사항은 다음과 같습니다.  

-   Windows Server 2012에 대 한 하드웨어 요구 사항을 충족 하는 두 개 이상의 컴퓨터.  

-   외부 부하 분산 장치 시나리오의 경우 전용된 하드웨어가 필요 \(즉, F5 BigIP\)합니다.  

-   시나리오를 테스트 하기 위해 Always On VPN 클라이언트를 구성 하는 Windows 10을 실행 하는 컴퓨터가 하나 이상 있어야 합니다.   

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항  
이 시나리오에 필요한 요구 사항은 다음과 같이 다양합니다.  

-   단일 서버 배포에 필요한 소프트웨어 요구 사항. 자세한 내용은 참조 [고급 설정을 사용 하 여 단일 DirectAccess 서버 배포](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)합니다. 단일 원격 액세스)입니다.  

-   단일 서버에 대 한 소프트웨어 요구 사항 외에 여러 가지 클러스터\-특정 요구 사항:  

    -   각 클러스터 된 서버의 IP\-HTTPS 인증서 주체 이름이 ConnectTo 주소와 일치 해야 합니다. 클러스터 배포 지원 와일드 카드 및 비 혼합\-클러스터 서버에서 와일드 카드 인증서입니다.  

    -   네트워크 위치 서버가 원격 액세스 서버에 설치되어 있는 경우 각 클러스터 서버에서 네트워크 위치 서버 인증서의 주체 이름이 같아야 합니다. 또한 네트워크 위치 서버 인증서의 이름은 DirectAccess 배포의 서버와 동일한 이름을 사용할 수 없습니다.  

    -   IP\-단일 서버에 인증서가 발급 된 동일한 방법을 사용 하 여 HTTPS 및 네트워크 위치 서버 인증서를 발급 되어야 합니다. 예를 들어 단일 서버에서는 공용 인증 기관일 \(CA\) 클러스터의 모든 서버 공용 CA에서 발급 한 인증서가 있어야 합니다. 단일 서버 자체를 사용 하는 경우 또는\-IP에 대 한 서명 된 인증서\-HTTPS 다음 클러스터의 모든 서버 마찬가지로 수행 해야 합니다.  

    -   서버 클러스터의 DirectAccess 클라이언트 컴퓨터에 할당된 IPv6 접두사는 59비트여야 합니다. VPN이 사용하도록 설정되어 있는 경우 VPN 접두사도 59비트여야 합니다.  

## <a name="KnownIssues"></a>알려진된 문제  
클러스터 시나리오를 구성할 때의 알려진 문제는 다음과 같습니다.  

-   IPv4에서 DirectAccess를 구성한 후\-만 배포는 단일 네트워크 어댑터를 사용 하 여 DNS64 기본 이후에 \(포함 하는 IPv6 주소 ": 3333::"\) 네트워크 어댑터에서 자동으로 구성 됩니다 로드를 사용 하는 동안\-IPv6 DIP를 제공 하는 사용자에 대 한 프롬프트를 사용 하면 원격 액세스 관리 콘솔을 통해 분산 합니다. IPv6 DIP가 제공된 경우 **커밋** 클릭 후 다음 오류와 함께 구성에 실패합니다. 매개 변수가 잘못되었습니다.  

    이 문제를 해결하려면  

    1.  [원격 액세스 구성 백업 및 복원](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)에서 백업을 다운로드하고 스크립트를 복원합니다.  

    2.  다운로드 한를 사용 하 여 원격 액세스 Gpo를 백업 스크립트 백업\-RemoteAccess.ps1  

    3.  실패한 단계에서 부하 분산 사용 설정을 시도합니다. 부하 분산 사용 대화 상자에서 오른쪽 세부 정보 영역을 확장\-세부 정보 영역에서 클릭 한 다음 클릭 **스크립트 복사**합니다.  

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

    8.  Cmdlet이 실패 하면 실행 중인 경우 \(잘못 된 입력된 값 때문이 아니라\)을 명령을 실행 하 여 복원\-원래 구성의 무결성이 유지 됩니다 있도록 RemoteAccess.ps1 및 다음 지침 .  

    9. 이제 원격 액세스 관리 콘솔을 다시 열 수 있습니다.  
