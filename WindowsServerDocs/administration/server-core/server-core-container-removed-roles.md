---
title: 역할, 역할 서비스 및 서버 코어 컨테이너-Windows Server 버전 1803에 없는 기능
description: 역할 및 Windows server의 Server Core 컨테이너 이미지에서 제거 되었습니다 기능에 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 0ad574a04ba7ecd235f1825bd25c247a1565edf6
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1859916"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>역할, 역할 서비스 및 서버 코어 컨테이너-Windows Server 버전 1803에 없는 기능

> 적용 대상: Windows Server, 1803 버전

Windows Server, 1803, 버전에서에서 [ **1.58 g B**로 Server Core 컨테이너 이미지의 전체 크기가 감소](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/)했습니다. 이 작업을 완료 했을 때는 방법은 아키텍처를 최적화 하 고 [Server Core 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/about/)에 하지 않아도 되는 작업을 제거 하 여입니다. 컨테이너에서 작동 하지 않은 작업 된 일부, 일부 역할 및 아무도 사용 하는 기능을 했습니다. 

> [!IMPORTANT]
> 이러한 특성을 [자체 Server Core](server-core-roles-and-services.md)하지 Server Core **컨테이너** 이미지에서 제거 되었습니다. 

기능 및 Server Core 컨테이너 이미지에서 제거 하는 역할의 전체 목록은 다음과 같습니다.

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>AuthManager
<br>Bitlocker 유틸리티
<br>BitLocker
<br>비트
<br>BITSExtensions 업로드
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>CertificateServices
<br>ClientForNFS 인프라
<br>컨테이너
<br>CoreFileServer
<br>DataCenterBridging-LLDP-도구
<br>DataCenterBridging
<br>Dedup 코어
<br>DeviceHealthAttestationService
<br>DFSN 서버
<br>DFSR-인프라-ServerEdition
<br>위해 ADAM
<br>위해 도메인 컨트롤러
<br>DiskIo QoS
<br>EnhancedStorage
<br>FailoverCluster AdminPak
<br>FailoverCluster AutomationServer
<br>FailoverCluster CmdInterface
<br>FailoverCluster FullServer
<br>FailoverCluster PowerShell
<br>파일 서비스
<br>FileServerVSSAgent
<br>FRS 인프라
<br>FSRM-인프라-서비스
<br>FSRM 인프라
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService 패키지
<br>IdentityServer SecurityTokenService
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>iSCSITargetServer PowerShell
<br>iSCSITargetServer
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>라이선싱
<br>LightweightServer
<br>Microsoft-하이퍼-V-관리-클라이언트
<br>Microsoft-하이퍼-V-오프 라인
<br>Microsoft-하이퍼-V-온라인
<br>Microsoft Hyper-v가
<br>Microsoft Windows-FCI-클라이언트-패키지
<br>Microsoft Windows-GroupPolicy-ServerAdminTools-업데이트
<br>Microsoft Windows-하위 시스템 Linux
<br>MSRDC 인프라
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P PnrpOnly
<br>PeerDist
<br>인쇄-클라이언트-Gui
<br>인쇄 LPDPrintService
<br>인쇄 서버-Foundation 기능
<br>인쇄 서버 역할
<br>QWAVE
<br>RasRoutingProtocols
<br>원격 데스크톱 서비스
<br>원격 액세스
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices 역할
<br>RightsManagementServices
<br>RMS 페더레이션
<br>SBMgr UI
<br>ServerCore 드라이버-일반 WOW64
<br>ServerCore-드라이버-일반
<br>ServerForNFS 인프라
<br>ServerManager-코어-RSAT-기능-도구
<br>ServerMediaFoundation
<br>ServerMigration
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol 서버
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>SoftwareLoadBalancer
<br>저장소-복제 데이터베이스-AdminPack
<br>저장소 복제
<br>Tpm-PSH-Cmdlet
<br>UpdateServices 데이터베이스
<br>UpdateServices-서비스
<br>UpdateServices WidDatabase
<br>UpdateServices
<br>VmHostAgent
<br>VolumeActivation-전체-역할
<br>웹 응용 프로그램 프록시
<br>웹 액세스
<br>WebEnrollmentServices
<br>Windows Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders 서버
<br>WSS 제품 패키지

</div>