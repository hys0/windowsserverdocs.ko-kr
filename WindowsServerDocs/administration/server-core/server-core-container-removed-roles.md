---
title: Server Core 컨테이너에 없는 역할, 역할 서비스 및 기능-Windows Server, 버전 1803
description: Windows Server 용 Server Core 컨테이너 이미지에서 제거한 역할 및 기능에 대해 알아봅니다.
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 05/07/2018
ms.openlocfilehash: 41b5a9ac32066f1b2a41de84f66b9be79252c336
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383415"
---
# <a name="roles-role-services-and-features-not-in-server-core-containers---windows-server-version-1803"></a>Server Core 컨테이너에 없는 역할, 역할 서비스 및 기능-Windows Server, 버전 1803

> 적용 대상: Windows Server, 버전 1803

Windows Server 버전 1803에서는 [Server Core 컨테이너 이미지의 전체 크기를 **1.58 GB**로 줄였습니다](https://blogs.technet.microsoft.com/virtualization/2018/01/22/a-smaller-windows-server-core-container-with-better-application-compatibility/). 이 작업을 수행 하는 방법은 아키텍처를 최적화 하 고 [Server Core 컨테이너](https://docs.microsoft.com/virtualization/windowscontainers/about/)에서 필요 하지 않은 항목을 제거 하는 것입니다. 컨테이너에서 작동 하지 않는 몇 가지 작업이 있습니다. 일부는 사용 되지 않는 역할 및 기능입니다. 

> [!IMPORTANT]
> [Server core가 아닌 Server](server-core-roles-and-services.md)core **컨테이너** 이미지에서 제거 되었습니다. 

다음은 Server Core 컨테이너 이미지에서 제거 된 기능 및 역할의 전체 목록입니다.

<div style='font-size:9.0pt'>

<br>ADCertificateServicesRole
<br>AuthManager
<br>Bitlocker-유틸리티
<br>BitLocker
<br>BITS
<br>BITSExtensions-업로드
<br>CCFFilter
<br>CertificateEnrollmentPolicyServer
<br>CertificateEnrollmentServer
<br>CertificateServices
<br>ClientForNFS-인프라
<br>컨테이너
<br>CoreFileServer
<br>DataCenterBridging-LLDP-Tools
<br>DataCenterBridging
<br>중복 제거-코어
<br>DeviceHealthAttestationService
<br>DFSN-서버
<br>DFSR-Infrastructure-ServerEdition
<br>DirectoryServices-ADAM
<br>DirectoryServices-DomainController
<br>DiskIo-QoS
<br>EnhancedStorage
<br>FailoverCluster-AdminPak
<br>FailoverCluster-AutomationServer
<br>FailoverCluster-CmdInterface
<br>FailoverCluster-FullServer
<br>FailoverCluster-PowerShell
<br>파일-서비스
<br>FileServerVSSAgent
<br>FRS-인프라
<br>FSRM-인프라-서비스
<br>FSRM-인프라
<br>HardenedFabricEncryptionTask
<br>HostGuardian
<br>HostGuardianService-패키지
<br>IdentityServer
<br>IPAMClientFeature
<br>IPAMServerFeature
<br>인 add-windowsfeature fs-iscsitargetserver-PowerShell
<br>인 add-windowsfeature fs-iscsitargetserver
<br>iSCSITargetStorageProviders
<br>iSNS_Service
<br>라이선싱
<br>LightweightServer
<br>Microsoft-Hyper-v-관리-클라이언트
<br>Microsoft-Hyper-v-오프 라인
<br>Microsoft-Hyper-v-온라인
<br>Microsoft-Hyper-v
<br>Microsoft-Windows FCI-클라이언트-패키지
<br>Microsoft-ServerAdminTools-업데이트
<br>Microsoft-Windows-하위 시스템-Linux
<br>MSRDC-인프라
<br>MultipathIo
<br>NetworkController
<br>NetworkControllerTools
<br>NetworkDeviceEnrollmentServices
<br>NetworkLoadBalancingFullServer
<br>NetworkVirtualization
<br>OnlineRevocationServices
<br>P2P-PnrpOnly
<br>PeerDist
<br>인쇄-클라이언트-Gui
<br>인쇄-LPDPrintService
<br>인쇄-서버-기본 기능
<br>인쇄-서버-역할
<br>QWAVE
<br>RasRoutingProtocols
<br>원격 데스크톱-서비스
<br>RemoteAccess
<br>RemoteAccessMgmtTools
<br>RemoteAccessPowerShell
<br>RemoteAccessServer
<br>ResumeKeyFilter
<br>RightsManagementServices-역할
<br>RightsManagementServices
<br>RMS-페더레이션
<br>SBMgr-UI
<br>ServerCore-일반-WOW64
<br>ServerCore-드라이버-일반
<br>ServerForNFS-인프라
<br>ServerManager-RSAT-기능 도구
<br>ServerMediaFoundation
<br>Servermigration.log
<br>SessionDirectory
<br>SetupAndBootEventCollection
<br>ShieldedVMToolsAdminPack
<br>SMB1Protocol-서버
<br>SmbDirect
<br>SMBHashGeneration
<br>SmbWitness
<br>SNMP
<br>\Loadbalancer Loadbalancer
<br>저장소 복제본-AdminPack
<br>저장소-복제본
<br>Tpm-PSH-Cmdlet
<br>Updateservices-api-데이터베이스
<br>Updateservices-api-서비스
<br>Updateservices-api-와이드 데이터베이스
<br>Updateservices-api
<br>VmHostAgent
<br>VolumeActivation-전체 역할
<br>웹 응용 프로그램-프록시
<br>WebAccess
<br>WebEnrollmentServices
<br>Windows-Defender
<br>WindowsServerBackup
<br>WindowsStorageManagementService
<br>WINSRuntime
<br>WMISnmpProvider
<br>WorkFolders-서버
<br>WSS-제품-패키지

</div>