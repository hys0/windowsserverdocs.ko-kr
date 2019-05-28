---
title: Windows Server 2016의 새로운 기능
description: 계산, ID, 관리, 자동화, 네트워킹, 보안, 저장소의 새로운 기능입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 05/21/2019
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2827f332-44d4-4785-8b13-98429087dcc7
author: jasongerend
ms.author: jgerend
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 8d36961558066197a54f42d27a3560d653bd81f2
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976629"
---
# <a name="whats-new-in-windows-server-2016"></a>Windows Server 2016의 새로운 기능

>적용 대상: Windows Server 2016

<img src="media/whats-new.png" style='float:left; padding:.5em;' alt="Icon showing a newspaper">Windows의 최신 기능을 알아보려면 [What's New in Windows Server](whats-new-in-windows-server.md)합니다. 이 섹션은 Windows Server&reg; 2016의 새로운 기능과 변경된 기능을 설명하는 내용입니다. 여기에 나열된 새로운 기능 및 변경 사항은 이 릴리스를 사용할 때 가장 많은 영향을 줄 수 있습니다.  

## <a name="computevirtualizationvirtualizationmd"></a>[계산](../virtualization/virtualization.md)

가상화 영역에는 IT 전문가가 Windows Server를 디자인, 배포 및 유지 관리하는 데 유용한 가상화 제품 및 기능이 포함됩니다.  

### <a name="general"></a>일반  
Win32 시간 및 Hyper-V 시간 동기화 서비스의 향상된 기능으로 인해 실제 및 가상 컴퓨터에서 보다 뛰어난 시간 정확도를 활용할 수 있습니다. 이제 Windows Server에서 UTC 기준 1밀리초 정확도를 요구하는 향후 규정을 준수하는 서비스를 호스트할 수 있습니다.  

### <a name="hyper-v"></a>Hyper-V  
-   [Windows Server 2016에 Hyper-V의 새로운 기능](../virtualization/hyper-v/What-s-new-in-Hyper-V-on-Windows.md). 이 항목에서는 Windows Server 2016의 Hyper-V 역할, Windows 10에서 실행되는 클라이언트 Hyper-V 및 Microsoft Hyper-V Server 2016의 새롭고 변경된 기능을 설명합니다.  

-   [Windows 컨테이너](https://msdn.microsoft.com/virtualization/windowscontainers/containers_welcome):  Windows Server 2016 컨테이너 지원은 Windows 10에서 성능 향상, 간소화 된 네트워크 관리 및 Windows 컨테이너에 대 한 지원을 추가합니다. 컨테이너에 대 한 몇 가지 추가 정보를 참조 하세요. [컨테이너: Docker, Windows 및 추세](https://azure.microsoft.com/blog/2015/08/17/containers-docker-windows-and-trends/)합니다.  

### <a name="nano-server"></a>Nano 서버  
[Nano Server](getting-started-with-nano-server.md)의 새로운 기능. Nano 서버에는 실제 호스트와 게스트 가상 컴퓨터의 추가 분리 기능 및 다양한 Windows Server 버전 지원을 포함하여 Nano Server 이미지 빌드를 위한 업데이트된 모듈이 제공됩니다.   

또한 인바운드 및 아웃바운드 방화벽 규칙 분리, WinRM 구성 복구 기능 등 복구 콘솔도 향상되었습니다.  

### <a name="shielded-virtual-machines"></a>보호된 가상 컴퓨터  
Windows Server 2016에서는 손상된 패브릭에서 모든 2세대 가상 컴퓨터를 보호하는 새로운 Hyper-V 기반 보호된 가상 컴퓨터를 제공합니다. Windows Server 2016에 도입된 기능은 다음과 같습니다.  

- 일반 가상 컴퓨터보다는 강력하고 "보호됨" 모드보다는 약한 보호를 제공하며, 가상 컴퓨터 콘솔 연결 및 Powershell Direct와 같은 직접 패브릭 관리 편의성을 포함하여 vTPM, 디스크 암호화, 실시간 마이그레이션 트래픽 암호화 등의 기능을 여전히 지원하는 새로운 "암호화 지원됨" 모드가 추가되었습니다.  

- 자동화된 디스크 암호화를 포함하여 기존의 보호되지 않는 2세대 가상 컴퓨터를 보호된 가상 컴퓨터로 변환하는 작업을 완벽하게 지원합니다.

- 이제 Hyper-V Virtual Machine Manager에서 보호된 가상 컴퓨터 실행 권한이 부여된 경우 패브릭을 볼 수 있으므로 패브릭 관리자가 보호된 가상 컴퓨터의 KP(키 보호기)를 열고 실행할 수 있는 패브릭을 확인할 수 있습니다.  

- 실행 중인 호스트 보호 서비스에서 증명 모드를 전환할 수 있습니다. 이제 보안 수준은 낮지만 보다 간단한 Active Directory 기반 증명과 TPM 기반 증명 간에 즉시 전환할 수 있습니다.  

- 보호된 Hyper-V 호스트와 호스트 보호 서비스 모두에서 잘못된 구성 또는 오류를 감지할 수 있는 Windows PowerShell 기반의 종단 간 진단 도구가 제공됩니다.  

- 보호된 가상 컴퓨터 자체와 동일한 보호 수준을 제공하는 한편, 패브릭 내에서 정상적으로 실행되는 보호된 가상 컴퓨터를 안전하게 복구하고 문제를 해결할 수 있는 복구 환경을 제공합니다.

- 기존에 안전한 Active Directory에 대한 호스트 보호 서비스 – 호스트 보호 서비스에서 Active Directory로 고유한 Active Directory 인스턴스를 생성하는 대신 기존 Active Directory 포리스트를 사용하도록 지시할 수 있습니다.

보호된 가상 컴퓨터 작업에 대한 지침은 [Windows Server 2016(TPM)에 대한 보호된 VM 및 보호된 패브릭 유효성 검사 가이드](https://aka.ms/shieldedvms)를 참조하세요.  

## <a name="identity-and-accessidentityidentity-and-accessmd"></a>[ID 및 액세스](../identity/Identity-and-Access.md)  
ID의 새로운 기능은 조직에서 Active Directory 환경을 보호하고 클라우드 전용 배포 및 하이브리드 배포(일부 응용 프로그램 및 서비스는 클라우드에서 호스트되고 다른 응용 프로그램 및 서비스는 온-프레미스에서 호스트됨)로 마이그레이션할 수 있는 기능을 개선합니다.  

### <a name="active-directory-certificate-services"></a>Active Directory 인증서 서비스  
Active Directory 인증서 서비스 (AD CS) Windows Server 2016에서 TPM 키 증명에 대 한 지원을 향상 시킵니다. 이제 키 증명에 스마트 카드 KSP를 사용할 수 있습니다 하 고 도메인에 가입 되지 않은 장치 수 등록 사용 하 여 NDES TPM에서 키를 증명할 수 있는 인증서를 가져옵니다.  

### <a name="active-directory-domain-services"></a>Active Directory 도메인 서비스  
Active Directory Domain Services에는 조직이 Active Directory 환경의 보안을 설정하고 회사 및 개인 장치에 향상된 ID 관리 환경을 제공하는 데 도움을 주는 개선 사항이 포함되어 있습니다. 자세한 내용은 [Windows Server 2016에서 AD DS(Active Directory Domain Services)의 새로운 기능](../identity/whats-new-active-directory-domain-services.md)을 참조하세요.   

### <a name="active-directory-federation-services"></a>AD FS(Active Directory Federation Services)  
Active Directory Federation Services의 새로운 기능 Windows Server 2016의 AD FS(Active Directory Federation Services)에서는 LDAP(Lightweight Directory Access Protocol) 디렉터리에 저장된 사용자를 인증하도록 AD FS를 구성할 수 있는 새로운 기능을 제공합니다. 자세한 내용은 [Windows Server 2016용 AD FS의 새로운 기능](../identity/ad-fs/overview/whats-new-active-directory-federation-services-windows-server.md)을 참조하세요.  

### <a name="web-application-proxy"></a>웹 응용 프로그램 프록시  
최신 버전의 웹 응용 프로그램 프록시는 더 많은 응용 프로그램 및 향상된 사용자 환경의 게시 및 사전 인증을 사용할 수 있는 새로운 기능에 초점을 맞춥니다. SharePoint 앱을 더 쉽게 게시할 수 있도록 Exchange ActiveSync 및 와일드카드 도메인과 같은 다양한 클라이언트 앱에 대한 사전 인증을 포함하는 새로운 기능의 전체 목록을 확인하세요. 자세한 내용은 [Windows Server 2016의 웹 응용 프로그램 프록시](../remote/remote-access/web-application-proxy/web-application-proxy-windows-server.md)를 참조하세요.  

##  <a name="administrationadministrationmanage-windows-servermd"></a>[관리](../administration/manage-windows-server.md)  
관리 및 자동화 영역은 Windows PowerShell을 포함하여 Windows Server 2016을 실행하고 관리하려는 IT 전문가를 위한 도구 및 참조 정보에 중점을 둡니다.

Windows PowerShell 5.1에서는 클래스를 사용하는 개발에 대한 지원, 새로운 보안 기능 등 용도를 확장하고, 사용 편의성을 개선하며, Windows 기반 환경을 보다 쉽게 포괄적으로 제어하고 관리할 수 있는 중요한 새로운 기능을 제공합니다. 자세한 내용은 [WMF 5.1의 새 시나리오 및 기능](https://docs.microsoft.com/powershell/wmf/5.1/scenarios-features)을 참조하세요.

Windows Server 2016에 대한 새로운 추가 사항으로는 Nano 서버에서 PowerShell.exe를 로컬로 실행하는 기능, GUI를 대체하는 새로운 로컬 사용자 및 그룹 cmdlet, PowerShell 디버깅을 지원하는 추가 기능, Nano Server에서 보안 로깅 및 기록과 JEA를 지원하는 추가 기능 등 새로운 기능이 포함됩니다.

다음은 이외의 몇 가지 새로운 관리 기능입니다.

### <a name="powershell-desired-state-configuration-dsc-in-windows-management-framework-wmf-5"></a>Windows WMF(Management Framework) 5의 PowerShell DSC(필요한 상태 구성)
Windows Management Framework 5는 Windows PowerShell DSC(필요한 상태 구성), WinRM(Windows Remote Management) 및 WMI(Windows Management Instrumentation)의 업데이트를 포함하고 있습니다.

Windows Management Framework 5의 DSC 기능 테스트에 대한 자세한 내용은 [PowerShell DSC 기능의 유효성 검사](https://blogs.msdn.microsoft.com/powershell/2015/07/06/validate-features-of-powershell-dsc/)에서 언급한 블로그 게시물을 참조하세요. 다운로드하려면 [Windows Management Framework 5.1](https://docs.microsoft.com/powershell/wmf/5.1/install-configure)을 참조하세요.

### <a name="packagemanagement-unified-package-management-for-software-discovery-installation-and-inventory"></a>소프트웨어 검색, 설치 및 재고에 대한 PackageManagement 통합 패키지 관리
Windows Server 2016 및 Windows 10에는 IT 전문가 및 개발 운영자가 설치 관리자 기술 및 소프트웨어 위치에 상관없이 로컬 또는 원격으로 SDII(소프트웨어 검색, 설치 및 인벤토리)를 자동화할 수 있도록 해주는 새로운 PackageManagement 기능(이전의 OneGet)이 포함되어 있습니다. 

자세한 정보는 [https://github.com/OneGet/oneget/wiki](https://github.com/OneGet/oneget/wiki)를 참조하세요.

### <a name="powershell-enhancements-to-assist-digital-forensics-and-help-reduce-security-breaches"></a>디지털 범죄 조사를 지원하고 보안 위험을 줄이도록 도와주는 PowerShell의 향상된 기능
"blue team"이라고도 부르는 손상된 시스템을 검사할 책임이 있는 팀을 도와주기 위해 추가적인 PowerShell 로깅 및 기타 디지털 범죄 조사 기능이 추가되었으며, 제한된 PowerShell 스크립트처럼 스크립트의 취약점을 줄이고 CodeGeneration API를 보호하는 기능이 추가되었습니다.

자세한 내용은 [Blue Team을 소중히 여기는 PowerShell](https://blogs.msdn.microsoft.com/powershell/2015/06/09/powershell-the-blue-team/)을 참조하세요.

## <a name="networkingnetworkingnetworkingmd"></a>[네트워킹](../networking/Networking.md)  
이 영역에서는 IT 전문가가 Windows Server 2016을 디자인, 배포 및 유지 관리하는 데 유용한 네트워킹 제품과 기능을 설명합니다.  

### <a name="software-defined-networking"></a>소프트웨어 정의 네트워킹
이제 신규 또는 기존 가상 어플라이언스로 트래픽을 미러링 및 라우팅할 수 있습니다. 이는 분산된 방화벽 및 네트워크 보안 그룹과 함께 Azure와 유사한 방식으로 워크로드를 동적으로 분할하고 보호해 줍니다. 둘째, System Center Virtual Machine Manager를 사용하여 전체 SDN(소프트웨어 정의 네트워킹) 스택을 배포하고 관리할 수 있습니다. 마지막으로, Docker를 사용하여 Windows Server 컨테이너 네트워킹을 관리하고 가상 컴퓨터뿐만 아니라 컨테이너에도 SDN 정책을 연결할 수 있습니다. 자세한 내용은 [소프트웨어 정의 네트워크 인프라 계획](../networking/sdn/plan/plan-a-software-defined-network-infrastructure.md)을 참조하세요.

### <a name="tcp-performance-improvements"></a>TCP 성능 향상
기본 초기 정체 창(ICW)이 4에서 10으로 늘어났으며 TFO(TCP Fast Open)가 구현되었습니다. TFO는 TCP 연결을 설정하는 데 필요한 시간을 줄여 주며 늘어난 ICW로 초기 버스트에서 더 큰 개체를 전송할 수 있습니다. 이 조합은 클라이언트와 클라우드 간에 인터넷 개체를 전송하는 데 필요한 시간을 크게 단축시킬 수 있습니다.

패킷 손실로부터 복구할 때 TCP 동작을 개선하기 위해 TCP 테일 손실 검색(TLP) 및 최근 승인(RACK)을 구현했습니다. TLP를 통해 다시 전송 시간 제한(RTO)을 빠른 복구로 변환할 수 있으며 RACK은 빠른 복구로 손실된 패킷을 다시 전송하는 데 필요한 시간을 단축시켜 줍니다. 

## <a name="security-and-assurancesecuritysecurity-and-assurancemd"></a>[보안 및 보증](../security/Security-and-Assurance.md)  
IT 전문가가 데이터 센터 및 클라우드 환경에서 배포할 수 있는 보안 솔루션 및 기능이 포함됩니다. Windows Server 2016에서 일반적인 보안에 대한 자세한 내용은 [보안 및 보증](../security/Security-and-Assurance.md)을 참조하세요.  

### <a name="just-enough-administration"></a>Just Enough Administration  
Windows Server 2016의 Just Enough Administration은 Windows PowerShell로 관리할 수 있는 모든 항목에 대한 위임된 관리를 지원하는 보안 기술입니다. 네트워크 ID를 통한 실행, PowerShell Direct를 통한 연결, JEA 끝점과의 보안 파일 복사, 기본적으로 JEA 컨텍스트에서 시작하도록 PowerShell 콘솔 구성 등에 대한 지원이 추가되었습니다. 자세한 내용은 [GitHub의 JEA](https://aka.ms/JEA)를 참조하세요.

### <a name="credential-guard"></a>Credential Guard
Credential Guard는 가상화 기반 보안을 사용하여 권한 있는 시스템 소프트웨어만 액세스할 수 있도록 암호를 격리합니다. [Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)를 참조하세요.

###  <a name="remote-credential-guard"></a>원격 Credential Guard
Credential Guard에는 RDP 세션에 대한 지원이 포함되어 사용자 자격 증명이 클라이언트 쪽에서 그대로 유지되며 서버 쪽에 노출되지 않습니다. 또한 원격 데스크톱에 대한 Single Sign On도 제공합니다. [Windows Defender Credential Guard를 사용하여 파생된 도메인 자격 증명 보호](https://docs.microsoft.com/windows/access-protection/credential-guard/credential-guard)를 참조하세요.   

### <a name="device-guard-code-integrity"></a>Device Guard(코드 무결성)
Device Guard는 서버에서 어떤 코드를 실행할 수 있는지를 지정하는 정책을 만들어 커널 모드 코드 무결성(KMCI) 및 사용자 모드 코드 무결성(UMCI)를 제공합니다. [Windows Defender Device Guard 소개: 가상화 기반 보안 및 코드 무결성 정책](https://docs.microsoft.com/windows/device-security/device-guard/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)을 참조하세요.


### <a name="windows-defender"></a>Windows Defender  
[Windows Server 2016에 대한 Windows Defender 개요](../security/windows-defender/windows-defender-overview-windows-server.md). Windows Server Antimalware는 Windows Server 2016에 기본적으로 설치되어 사용되지만 Windows Server Antimalware에 대한 사용자 인터페이스는 설치되지 않습니다. 그러나 Windows Server Antimalware는 맬웨어 방지 정의를 업데이트하고 사용자 인터페이스 없이 컴퓨터를 보호합니다. Windows Server Antimalware에 대한 사용자 인터페이스가 필요하면 운영 체제 설치 후 역할 및 기능 추가 마법사를 사용하여 설치할 수 있습니다.

### <a name="control-flow-guard"></a>제어 흐름 보호
제어 흐름 보호(CFG)는 메모리 손상 취약점에 대처하기 위해 만든 플랫폼 보안 기능입니다. 자세한 내용은 [제어 흐름 보호](https://msdn.microsoft.com/library/windows/desktop/mt637065(v=vs.85).aspx)를 참조하세요.


## <a name="storagestoragestoragemd"></a>[저장소](../storage/storage.md)

Windows Server 2016의 저장소에는 소프트웨어 정의 저장소와 기존의 파일 서버에 대한 새로운 기능과 향상된 기능이 포함됩니다. 몇 가지 새로운 기능은 다음과 같으며 향상된 기능 및 추가 정보는 [Windows Server 2016에서 제공되는 저장소의 새로운 기능](../storage/whats-new-in-storage.md)을 참조하세요.

### <a name="storage-spaces-direct"></a>저장소 공간 다이렉트

저장소 공간 다이렉트는 로컬 저장소가 있는 서버를 사용하여 확장 가능한 고가용성 저장소를 구축하도록 지원합니다. 이는 소프트웨어 정의 저장소 시스템의 배포 및 관리를 간소화하고 SATA SSD 및 NVMe 디스크 장치와 같이 이전에 공유 디스크를 사용하는 클러스터형 저장소 공간에서는 불가능했던 새로운 등급의 디스크 장치를 사용합니다.

자세한 내용은 [저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md)를 참조하세요.

### <a name="storage-replica"></a>저장소 복제본

저장소 복제본을 통해 사이트 간에 장애 조치(failover) 클러스터를 확장할 뿐만 아니라 재해 복구를 위해 서버 또는 클러스터 간에 저장소에 상관없는 블록 수준의 동기 복제를 사용할 수 있습니다. 동기 복제를 사용하면 파일 시스템 수준에서 데이터가 손실되지 않고 크래시 일관성이 있는 볼륨을 사용하여 실제 사이트의 데이터를 미러링할 수 있습니다. 비동기 복제는 대도시 범위를 넘어 사이트를 확장합니다(데이터가 손실될 수도 있음).

자세한 내용은 [저장소 복제본](../storage/storage-replica/storage-replica-overview.md)을 참조하세요.

### <a name="storage-quality-of-service-qos"></a>저장소 서비스 품질(QoS)

이제 저장소 QoS(서비스 품질)를 사용하여 중앙에서 종단 간 저장소 성능을 모니터링하고 Windows Server 2016의 Hyper-V 및 CSV 클러스터를 통해 관리 정책을 만들 수 있습니다.

자세한 내용은 [저장소 서비스 품질](../storage/storage-qos/storage-qos-overview.md)을 참조하세요.

## <a name="failover-clusteringfailover-clusteringwhats-new-in-failover-clusteringmd"></a>[장애 조치(failover) 클러스터링](../failover-clustering/whats-new-in-failover-clustering.md)

Windows Server 2016에는 여러 새로운 기능과 장애 조치(failover) 클러스터링 기능을 사용하여 여러 서버가 하나의 내결함성 클러스터로 함께 그룹화되는 향상된 기능이 포함됩니다. 몇 가지 추가 사항이 아래에 나와 있으며 전체 목록을 보려면 [Windows Server 2016 장애 조치(failover) 클러스터의 새로운 기능](../failover-clustering/whats-new-in-failover-clustering.md)을 참조하세요.

### <a name="cluster-operating-system-rolling-upgrade"></a>클러스터 운영 체제 롤링 업그레이드

클러스터 운영 체제 롤링 업그레이드로 관리자는 Hyper-V 또는 스케일 아웃 파일 서버 워크로드를 중지하지 않고 클러스터 노드의 운영 체제를 Windows Server 2012 R2에서 Windows Server 2016으로 업그레이드할 수 있습니다. 이 기능을 사용하면 SLA(서비스 수준 계약)의 가동 중지 시간 위반을 피할 수 있습니다.

자세한 내용은 [클러스터 운영 체제 롤링 업그레이드](../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)를 참조하세요.

### <a name="cloud-witness"></a>클라우드 감시

클라우드 감시는 중재 지점으로 Microsoft Azure를 활용하는 Windows Server 2016에서 새로운 유형의 장애 조치 클러스터 쿼럼 감시 기능입니다. 다른 쿼럼 감시와 마찬가지로 클라우드 감시는 응답을 가져오고 쿼럼 계산에 참여할 수 있습니다. 클러스터 쿼럼 구성 마법사를 사용하여 쿼럼 감시로 클라우드 감시를 구성할 수 있습니다.

자세한 내용은 [클라우드 감시 배포](../failover-clustering/deploy-cloud-witness.md)를 참조하세요.

### <a name="health-service"></a>상태 관리 서비스

상태 관리 서비스는 저장소 공간 다이렉트 클러스터에서 클러스터 리소스의 일상적인 모니터링, 작업 및 유지 관리 환경을 개선합니다.

자세한 내용은 [상태 관리 서비스](../failover-clustering/health-service-overview.md)를 참조하세요.

## <a name="application-development"></a>응용 프로그램 개발

### <a name="internet-information-services-iis-100"></a>IIS(인터넷 정보 서비스) 10.0
Windows Server 2016의 IIS 10.0 웹 서버에서 제공하는 새로운 기능은 다음과 같습니다.

- 네트워킹 스택의 HTTP/2 프로토콜을 지원하고 IIS 10.0과 통합되어 IIS 10.0 웹 사이트가 지원 구성에 대한 HTTP/2 요청을 자동으로 지원할 수 있습니다. 이렇게 하면 HTTP/1.1을 통해 연결을 더욱 효율적으로 재사용하고 대기 시간을 줄이는 등 여러 기능을 향상시킬 수 있고 웹 페이지의 로드 시간을 개선할 수 있습니다. 
- Nano 서버에서 IIS 10.0을 실행하고 관리할 수 있는 기능. [Nano 서버의 IIS](iis-on-nano-server.md)를 참조하세요.
- 도메인에 대 한 웹 서버를 설정 한 후 모든 하위 도메인에 대 한 요청을 처리 하는 웹 서버 관리자를 사용 하도록 설정 하면 와일드 카드 호스트 헤더를 지원 합니다.
- IIS를 관리하기 위한 새로운 PowerShell 모듈(IISAdministration). 

자세한 내용은 [IIS](https://iis.net/learn) 항목을 참조하십시오.

### <a name="distributed-transaction-coordinator-msdtc"></a>MSDTC(Distributed Transaction Coordinator)
Microsoft Windows 10 및 Windows Server 2016에 다음과 같은 새로운 기능 세 개가 추가되었습니다.

- Resource Manager Rejoin의 새 인터페이스는 오류로 인해 데이터베이스를 다시 시작한 후 리소스 관리자가 확실하지 않은 트랜잭션의 결과를 판단하는 데 사용될 수 있습니다. 자세한 내용은 [IResourceManagerRejoinable::Rejoin](https://msdn.microsoft.com/en-us/library/mt203799(v=vs.85).aspx)을 참조하세요.

- DSN 이름 제한은 256바이트에서 3072바이트로 확대됩니다. 자세한 내용은 [IDtcToXaHelperFactory::Create](https://msdn.microsoft.com/en-us/library/ms686861(v=vs.85).aspx), [IDtcToXaHelperSinglePipe::XARMCreate](https://msdn.microsoft.com/en-us/library/ms679248(v=vs.85).aspx) 또는 [IDtcToXaMapper::RequestNewResourceManager](https://msdn.microsoft.com/en-us/library/ms680310(v=vs.85).aspx)를 참조하세요.

- 추적 로그 파일 이름에 이미지 파일 경로를 포함하도록 레지스트리 키를 설정하여 어떤 추적 로그 파일을 확인할지 파악할 수 있는 기능이 개선되었습니다. MSDTC 추적 구성에 대한 자세한 내용은 [Windows 기반 컴퓨터에서 MS DTC에 대한 진단 추적을 활성화하는 방법](https://support.microsoft.com/en-us/kb/926099)을 참조하세요.



## <a name="see-also"></a>관련 항목  
-   [릴리스 정보: Windows Server 2016의 중요한 이슈](Windows-Server-2016-GA-Release-Notes.md)  

