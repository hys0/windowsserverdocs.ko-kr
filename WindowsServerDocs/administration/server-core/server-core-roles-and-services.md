---
title: Windows Server-Server Core에 포함 된 역할, 역할 서비스 및 기능
description: Windows Server의 Server Core 설치 옵션에 포함 된 역할 및 기능은 무엇입니까?
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 7b5d5d5ad38b1b03e409c26485860f43799f1322
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383335"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>Windows Server-Server Core에 포함 된 역할, 역할 서비스 및 기능

> 적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

일반적으로 [Server Core에 포함 *되지 않는* ](server-core-removed-roles.md) 기능에 대해 설명 합니다. 이제 다른 방법을 사용해 보고 *포함* 되는 항목과 *기본적으로 설치*된 항목이 무엇 인지를 알 수 있습니다. Windows Server의 Server Core 설치 옵션 *에* 는 다음과 같은 역할, 역할 서비스 및 기능이 있습니다. 이 정보를 사용 하 여 사용자 환경에 대 한 Server Core 옵션이 작동 하는지 파악할 수 있습니다. 이 목록은 매우 크기 때문에 관심 있는 특정 역할 또는 기능을 검색 하는 것이 좋습니다. 검색에서 찾고 있는 항목을 반환 하지 않는 경우에는 Server Core에 포함 되지 않습니다.

예를 들어 "원격 데스크톱 세션 호스트"를 검색 하는 경우이 페이지에서 찾을 수 없습니다. RD 세션 호스트은 Server Core 이미지에 포함 되지 않기 때문입니다.

[항상](server-core-removed-roles.md) 포함 *되지 않은* 것을 확인할 수 있습니다. 이것은 무엇 보다도 다양 한 방법으로 볼 수 있습니다.

## <a name="roles-included-in-server-core"></a>Server Core에 포함 된 역할
Server Core 설치 옵션에는 다음과 같은 서버 역할이 포함 되어 있습니다.

| 역할                                            | 이름                           | 기본적으로 설치 되어 있습니까? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 인증서 서비스           | 광고-인증서                 | N                     |
| Active Directory 도메인 서비스                | AD-도메인 서비스             | N                     |
| AD FS(Active Directory Federation Services)            | ADFS-페더레이션                | N                     |
| Active Directory LDS(Lightweight Directory Services) | ADLDS                          | N                     |
| Active Directory Rights Management Services     | ADRMS                          | N                     |
| 디바이스 상태 증명                       | DeviceHealthAttestationService | N                     |
| DHCP 서버                                     | DHCP                           | N                     |
| DNS 서버                                      | DNS                            | N                     |
| 파일 및 저장소 서비스                       | FileAndStorage-서비스        | Y                     |
| 호스트 보호 서비스                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| 인쇄 및 문서 서비스                     | 인쇄-서비스                 | N                     |
| 원격 액세스                                   | RemoteAccess                   | N                     |
| 원격 데스크톱 서비스                         | 원격 데스크톱-서비스        | N                     |
| 볼륨 정품 인증 서비스                      | VolumeActivation               | N                     |
| 웹 서버 IIS                                  | 웹 서버                     | N                     |
| Windows Server 필수 패키지 환경            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | Updateservices-api                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core에 포함 된 역할 서비스
Server Core 설치 옵션에는 다음과 같은 역할 서비스가 포함 되어 있습니다.

| 역할                                  | 역할 서비스                                                   | 이름                    | 기본적으로 설치 되어 있습니까? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 인증서 서비스 | 인증 기관                                        | ADCS     | N                     |
|                                       | 인증서 등록 정책 웹 서비스                      | ADCS-Registry.pol     | N                     |
|                                       | 인증서 등록 웹 서비스                             | ADCS-웹 Svc     | N                     |
|                                       | 인증 기관 웹 등록                         | ADCS-웹 등록     | N                     |
|                                       | 네트워크 장치 등록 서비스                              | ADCS-장치 등록  | N                     |
|                                       | 온라인 응답기                                               | ADCS-온라인-인증서        | N                     |
| Active Directory Rights Management    | Active Directory Rights Management Server                      | ADRMS-서버            | N                     |
|                                       | ID 페더레이션 지원                                    | ADRMS-Id          | N                     |
| 파일 및 저장소 서비스             | 파일 및 iSCSI 서비스                                        | 파일-서비스           | N                     |
|                                       | 파일 서버                                                    | FileServer           | N                     |
|                                       | 네트워크 파일용 BranchCache                                  | FS-BranchCache          | N                     |
|                                       | 데이터 중복 제거                                             | FS-데이터-중복 제거   | N                     |
|                                       | DFS 네임스페이스                                                 | FS-DFS-네임 스페이스        | N                     |
|                                       | DFS 복제                                                | FS-DFS-복제      | N                     |
|                                       | 파일 서버 리소스 관리자                                   | FS-리소스 관리자     | N                     |
|                                       | 파일 서버 VSS 에이전트 서비스                                  | FS-VSS-에이전트            | N                     |
|                                       | iSCSI 대상 서버                                            | iSCSITarget-서버      | N                     |
|                                       | iSCSI 대상 저장소 공급자 (VDS 및 VSS 하드웨어 공급자) | iSCSITarget     | N                     |
|                                       | NFS용 서버                                                 | FS-NFS-서비스          | N                     |
|                                       | 클라우드 폴더                                                   | FS-SyncShareService     | N                     |
|                                       | 저장소 서비스                                               | 저장소 서비스        | Y                     |
| 인쇄 및 문서 서비스           | 인쇄 서버                                                   | 인쇄-서버            | N                     |
|                                       | LPD 서비스                                                    | 인쇄-LPD-서비스       | N                     |
| 원격 액세스                         | DirectAccess 및 VPN (RAS)                                     | DirectAccess-VPN        | N                     |
|                                       | 라우팅                                                        | 라우팅                 | N                     |
|                                       | 웹 응용 프로그램 프록시                                          | 웹 응용 프로그램-프록시   | N                     |
| 원격 데스크톱 서비스               | 원격 데스크톱 연결 브로커                               | RDS-연결-Broker   | N                     |
|                                       | 원격 데스크톱 라이선싱                                       | RDS-라이선스           | N                     |
|                                       | 원격 데스크톱 가상화 호스트                             | RDS-가상화      | N                     |
| 웹 서버(IIS)                      | 웹 서버                                                     | 웹 웹 서버           | N                     |
|                                       | 일반 HTTP 기능                                           | 웹-공용-Http         | N                     |
|                                       | 기본 문서                                               | 웹-기본-Doc         | N                     |
|                                       | 디렉터리 검색                                             | 웹-Dir-검색        | N                     |
|                                       | HTTP 오류                                                    | 웹-Http-오류         | N                     |
|                                       | 정적 콘텐츠                                                 | 웹-정적-콘텐츠      | N                     |
|                                       | HTTP 리디렉션                                               | 웹-Http-리디렉션       | N                     |
|                                       | WebDAV 게시                                              | 웹-DAV-게시      | N                     |
|                                       | 상태 및 진단                                         | 웹 상태              | N                     |
|                                       | HTTP 로깅                                                   | 웹-Http-로깅        | N                     |
|                                       | 사용자 지정 로깅                                                 | 웹-사용자 지정-로깅      | N                     |
|                                       | 로깅 도구                                                  | 웹 로그 라이브러리       | N                     |
|                                       | ODBC 로깅                                                   | 웹-ODBC-로깅        | N                     |
|                                       | 요청 모니터                                              | 웹 요청-모니터     | N                     |
|                                       | 추적                                                        | 웹-Http-추적        | N                     |
|                                       | 성능                                                    | 웹-성능         | N                     |
|                                       | 정적 콘텐츠 압축                                     | 웹-상태-압축    | N                     |
|                                       | 동적 콘텐츠 압축                                    | 웹 Dyn-압축     | N                     |
|                                       | 보안                                                       | 웹-보안            | N                     |
|                                       | 요청 필터링                                              | 웹 필터링           | N                     |
|                                       | 기본 인증                                           | 웹-기본-인증          | N                     |
|                                       | 중앙 SSL 인증서 지원                            | 웹-CertProvider        | N                     |
|                                       | 클라이언트 인증서 매핑 인증                      | 웹-클라이언트-인증         | N                     |
|                                       | 다이제스트 인증                                          | 웹-다이제스트-인증         | N                     |
|                                       | IIS 클라이언트 인증서 매핑 인증                  | 웹-인증서-인증           | N                     |
|                                       | IP 및 도메인 제한                                     | 웹 IP-보안         | N                     |
|                                       | URL 권한 부여                                              | 웹 Url-인증            | N                     |
|                                       | Windows 인증                                         | 웹-Windows-인증        | N                     |
|                                       | 애플리케이션 개발                                        | 웹 앱-개발             | N                     |
|                                       | .NET 확장성 3.5                                         | 웹-Net-Ext             | N                     |
|                                       | .NET 확장성 4.6                                         | 웹-Ext45           | N                     |
|                                       | 응용 프로그램 초기화                                     | 웹-AppInit             | N                     |
|                                       | ASP                                                            | 웹-ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | 웹-Asp-Net             | N                     |
|                                       | ASP.NET 4.6                                                    | 웹-Asp-Net45           | N                     |
|                                       | CGI                                                            | 웹-CGI                 | N                     |
|                                       | ISAPI 확장                                               | 웹-ISAPI-Ext           | N                     |
|                                       | ISAPI 필터                                                  | 웹-ISAPI-필터        | N                     |
|                                       | 서버 쪽 포함                                           | 웹-포함            | N                     |
|                                       | WebSocket 프로토콜                                             | 웹-Websocket          | N                     |
|                                       | FTP 서버                                                     | 웹-Ftp-서버          | N                     |
|                                       | FTP 서비스                                                    | 웹-Ftp-서비스         | N                     |
|                                       | FTP 확장성                                              | 웹-Ftp-Ext             | N                     |
|                                       | 관리 도구                                               | 웹 관리-도구          | N                     |
|                                       | IIS 6 관리 호환성                                 | 웹 관리-호환성         | N                     |
|                                       | IIS 6 메타베이스 호환성                                   | 웹-메타 베이스            | N                     |
|                                       | IIS 6 스크립팅 도구                                          | 웹 Lgcy-스크립팅      | N                     |
|                                       | IIS 6 WMI 호환성                                        | 웹-WMI                 | N                     |
|                                       | IIS 관리 스크립트 및 도구                               | 웹 스크립팅-도구     | N                     |
|                                       | 관리 서비스                                             | 웹 관리 서비스        | N                     |
| Windows Server Update Services        | WID 연결                                               | Updateservices-api-WidDB    | N                     |
|                                       | WSUS 서비스                                                  | Updateservices-api-서비스 | N                     |
|                                       | SQL Server 연결                                        | Updateservices-api-DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core에 포함 된 기능
Server Core 설치 옵션에는 다음과 같은 기능이 포함 되어 있습니다.

| 기능                                                | 이름                               | 기본적으로 설치 되어 있습니까? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET Framework 3.5 기능                            | .NET Framework-기능             | N                     |
| .NET Framework 3.5 (.NET 2.0 및 3.0 포함)       | 네트워크 프레임 워크-코어                 | 제거             |
| HTTP 활성화                                        | NET-HTTP-활성화                | N                     |
| 비 HTTP 활성화                                    | NET-비-의 활성                 | N                     |
| .NET Framework 4.6 기능                            | .NET Framework-45-기능          | Y                     |
| .NET framework 4.6                                     | NET.PIPE-45-Core              | Y                     |
| ASP.NET 4.6                                            | .NET-프레임 워크-45-ASPNET            | N                     |
| WCF Services                                           | Services45                 | Y                     |
| HTTP 활성화                                        | NET-Activation45          | N                     |
| MSMQ (메시지 큐) 활성화                      | NET-Activation45          | N                     |
| 명명 된 파이프 활성화                                  | NET.PIPE-Activation45          | N                     |
| TCP 활성화                                         | NET-Activation45           | N                     |
| TCP 포트 공유                                       | NET-PortSharing45          | Y                     |
| BITS(Background Intelligent Transfer Service)         | BITS                               | N                     |
| Compact 서버                                         | 비트 압축 서버                | N                     |
| BitLocker 드라이브 암호화                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS용 클라이언트                                         | NFS-클라이언트                         | N                     |
| 컨테이너                                             | 컨테이너                         | N                     |
| 데이터 센터 브리징                                   | 데이터 센터-브리징               | N                     |
| 강화된 저장소                                       | EnhancedStorage                    | N                     |
| 장애 조치(failover) 클러스터링                                    | 장애 조치 (Failover)-클러스터링                | N                     |
| 그룹 정책 관리                                | GPMC                               | N                     |
| I/O 서비스 품질                                 | DiskIo-QoS                         | N                     |
| IIS 호스팅 가능한 웹 코어                                  | 웹-WHC                            | N                     |
| IPAM(IP 주소 관리) 서버                    | IPAM                               | N                     |
| iSNS 서버 서비스                                    | ISNS                               | N                     |
| 관리 OData IIS 확장                         | ManagementOdata                    | N                     |
| 미디어 파운데이션                                       | 서버-미디어-기본            | N                     |
| 메시지 큐                                        | MSMQ                               | N                     |
| 메시지 큐 서비스                               | MSMQ-서비스                      | N                     |
| 메시지 큐 서버                                 | MSMQ-서버                        | N                     |
| 디렉터리 서비스 통합                          | MSMQ-디렉터리                     | N                     |
| HTTP 지원                                           | MSMQ-HTTP 지원                  | N                     |
| 메시지 큐 트리거                               | MSMQ-트리거                      | N                     |
| 라우팅 서비스                                        | MSMQ-라우팅                       | N                     |
| 메시지 큐 DCOM 프록시                             | MSMQ-DCOM                          | N                     |
| 다중 경로 I/O                                          | 다중 경로-IO                       | N                     |
| MultiPoint 커넥터                                   | MultiPoint-커넥터               | N                     |
| MultiPoint 커넥터 서비스                          | MultiPoint-커넥터-서비스      | N                     |
| 다중 포인트 관리자 및 다중 포인트 대시보드            | MultiPoint-도구                   | N                     |
| 네트워크 부하 분산                                 | NLB                                | N                     |
| 피어 이름 확인 프로토콜                          | PNRP                               | N                     |
| qWave(Quality Windows Audio Video Experience)                 | qWave                              | N                     |
| 원격 차등 압축                        | RDC                                | N                     |
| 원격 서버 관리 도구                     | RSAT                               | N                     |
| 기능 관리 도구                           | RSAT-기능 도구                 | N                     |
| BitLocker 드라이브 암호화 관리 유틸리티  | RSAT-기능 도구-BitLocker       | N                     |
| DataCenterBridging LLDP 도구                          | RSAT-DataCenterBridging-LLDP-Tools | N                     |
| 장애 조치(failover) 클러스터링 도구                              | RSAT-클러스터링                    | N                     |
| Windows PowerShell 용 장애 조치 (Failover) 클러스터 모듈         | RSAT-클러스터링-PowerShell         | N                     |
| 장애 조치 (Failover) 클러스터 자동화 서버                     | RSAT-클러스터링-AutomationServer   | N                     |
| 장애 조치 (Failover) 클러스터 명령 인터페이스                     | RSAT-클러스터링-CmdInterface       | N                     |
| IPAM (IP 주소 관리) 클라이언트                    | IPAM-클라이언트 기능                | N                     |
| 차폐 VM 도구                                      | RSAT-차폐-VM 도구             | N                     |
| Windows PowerShell 용 저장소 복제본 모듈          | RSAT-저장소-복제본               | N                     |
| 역할 관리 도구                              | RSAT-역할-도구                    | N                     |
| AD DS 및 AD LDS 도구                                 | RSAT-AD 도구                      | N                     |
| Windows PowerShell용 Active Directory 모듈         | RSAT-AD-PowerShell                 | N                     |
| AD DS 도구                                            | RSAT-추가                          | N                     |
| Active Directory 관리 센터                 | RSAT-AD-AdminCenter                | N                     |
| AD DS 스냅인 및 명령줄 도구                  | RSAT-추가 도구                    | N                     |
| AD LDS 스냅인 및 명령줄 도구                 | RSAT-ADLDS                         | N                     |
| Hyper-V 관리 도구                               | RSAT-Hyper-v-도구                 | N                     |
| Windows PowerShell용 Hyper-V 모듈                  | Hyper-V-PowerShell                 | N                     |
| Windows Server Update Services 도구                   | Updateservices-api-RSAT                | N                     |
| API 및 PowerShell cmdlet                             | Updateservices-api-API                 | N                     |
| DHCP 서버 도구                                      | RSAT-DHCP                          | N                     |
| DNS 서버 도구                                       | RSAT-DNS 서버                    | N                     |
| 원격 액세스 관리 도구                         | RSAT-원격 액세스                  | N                     |
| Windows PowerShell용 원격 액세스 모듈            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC over HTTP 프록시                                    | RPC-HTTP-프록시                | N                     |
| 이벤트 컬렉션 설치 및 부팅                        | 설정 및 부팅-이벤트 수집    | N                     |
| 단순 TCP/IP 서비스                                 | 단순-TCPIP                       | N                     |
| SMB 1.0/CIFS 파일 공유 지원                      | FS-SMB1                            | Y                     |
| SMB 대역폭 제한                                    | SMBBW                           | N                     |
| SNMP 서비스                                           | SNMP-서비스                       | N                     |
| SNMP WMI 공급자                                      | SNMP-WMI-공급자                  | N                     |
| 텔넷 클라이언트                                          | 텔넷-클라이언트                      | N                     |
| 패브릭 관리를 위한 VM 보호 도구               | FabricShieldedTools                | N                     |
| Windows Defender 기능                              | Windows-Defender-기능          | Y                     |
| Windows Defender                                       | Windows-Defender                   | Y                     |
| Windows 내부 데이터베이스                              | Windows-내부 데이터베이스          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0 엔진                          | PowerShell-V2                      | 제거             |
| Windows PowerShell 필요한 상태 구성 서비스 | DSC-서비스                        | N                     |
| Windows PowerShell 웹 액세스                          | WindowsPowerShellWebAccess         | N                     |
| Windows Process Activation Service                     | 을                                | N                     |
| 프로세스 모델                                          | WAS-프로세스 모델                  | N                     |
| .NET 환경 3.5                                   | WAS-넷-환경                | N                     |
| 구성 API                                     | WAS-구성-Api                    | N                     |
| Windows Server 백업                                  | Windows-서버 백업              | N                     |
| Windows Server 마이그레이션 도구                         | 마이그레이션                          | N                     |
| Windows 표준 기반 저장소 관리             | WindowsStorageManagementService    | N                     |
| WinRM IIS 확장                                    | WinRM-IIS-Ext                      | N                     |
| WINS 서버                                            | WINS                               | N                     |
| WoW64 지원                                          | WoW64-지원                      | Y                     |
|                                                        |                                    |                       |
