---
title: 역할, 역할 서비스 및 Windows Server-Server Core에에서 포함 된 기능
description: Windows Server의 Server Core 설치 옵션에 어떤 역할 및 기능 사용 되나요?
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 65729eb68c9590fd6316f5650be48f33c19c926d
ms.sourcegitcommit: 439edac95e1427086268cab469ed03b94db630da
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "2217743"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>역할, 역할 서비스 및 Windows Server-Server Core에에서 포함 된 기능

> 적용 대상: Windows Server (세미콜론 연간 회의 채널) 및 Windows Server 2016

일반적으로 여기에 대해서 [기능의 *하지* Server Core에](server-core-removed-roles.md) 하겠습니다 이제-다른 방법을 *포함* 하는 것이 이란 무엇 이며 *기본적으로 설치 된*이 있는지 여부를 알려 하 합니다. 다음 역할, 역할 서비스 및 기능에서 *에서* Windows Server의 Server Core 설치 옵션 됩니다. Server Core 옵션 환경에 대해 작동 하는 경우 포트당를이 정보를 사용 합니다. 큰 목록 이기 때문에 특정 역할 또는 기능에 관심이-검색을 원하는 항목을 반환 하지 않습니다 하는 경우 검색 고려 Server Core에 포함 되지 않습니다.

예 "원격 데스크톱 세션 호스트"-검색 하는 경우이 페이지에서 찾이 되지 않습니다. RD 세션 호스트 서버 코어 이미지에 포함 되지 않은 때문입니다.

기억 [항상 찾을](server-core-removed-roles.md) 수 있는 기능에 포함 *되지* 않습니다. 이 바로 하는 방법은 다른 작업을 살펴봅니다.

## <a name="roles-included-in-server-core"></a>Server Core에 포함 된 역할
Server Core 설치 옵션에는 다음과 같은 서버 역할 포함 됩니다.

| 역할                                            | 이름                           | 기본적으로 설치 되어 있습니까? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 인증서 서비스           | AD 인증서                 | N                     |
| Active Directory 도메인 서비스                | AD-도메인-서비스             | N                     |
| ADFS(Active Directory Federation Services)            | ADFS 페더레이션                | N                     |
| Active Directory LDS(Lightweight Directory Services) | ADLDS                          | N                     |
| Active Directory Rights Management Services     | ADRMS                          | N                     |
| 장치 상태 증명                       | DeviceHealthAttestationService | N                     |
| DHCP 서버                                     | DHCP                           | N                     |
| DNS 서버                                      | DNS                            | N                     |
| File and Storage Services                       | FileAndStorage-서비스        | 예                     |
| 호스트 보호 서비스                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| 인쇄 및 문서 서비스                     | 인쇄 서비스                 | N                     |
| 원격 액세스                                   | 원격 액세스                   | N                     |
| 원격 데스크톱 서비스                         | 원격 데스크톱 서비스        | N                     |
| 볼륨 정품 인증 서비스                      | VolumeActivation               | N                     |
| IIS 웹 서버                                  | 웹 서버                     | N                     |
| Windows Server Essentials Experience            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core에 포함 된 역할 서비스
Server Core 설치 옵션은 다음 역할 서비스를 포함합니다.

| 역할                                  | 역할 서비스                                                   | 이름                    | 기본적으로 설치 되어 있습니까? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 인증서 서비스 | 인증 기관                                        | ADC-Cert-기관     | N                     |
|                                       | 인증서 등록 정책 웹 서비스                      | ADC-등록-웹-Pol     | N                     |
|                                       | 인증서 등록 웹 서비스                             | ADC-등록-웹-서비스     | N                     |
|                                       | 인증 기관 웹 등록                         | ADC 웹 등록     | N                     |
|                                       | 네트워크 장치 등록 서비스                              | ADC 장치 등록  | N                     |
|                                       | 온라인 응답자                                               | 온라인 인증서 ADC        | N                     |
| Active Directory 권한 관리    | Active Directory Rights Management Server                      | ADRMS 서버            | N                     |
|                                       | Id 페더레이션 지원                                    | ADRMS-Identity          | N                     |
| File and Storage Services             | 파일 및 iSCSI 서비스                                        | 파일 서비스           | N                     |
|                                       | 파일 서버                                                    | FS 파일 서버           | N                     |
|                                       | 네트워크 파일용 BranchCache                                  | FS BranchCache          | N                     |
|                                       | 데이터 중복 제거                                             | 중복-데이터-FS 제거   | N                     |
|                                       | DFS 네임스페이스                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS 복제                                                | FS-DFS-복제      | N                     |
|                                       | 파일 서버 리소스 관리자                                   | FS 자원 관리자     | N                     |
|                                       | 파일 서버 VSS 에이전트 서비스                                  | FS VSS 에이전트            | N                     |
|                                       | iSCSI Target Server                                            | iSCSITarget 서버      | N                     |
|                                       | iSCSI 대상 저장소 공급자 (VDS 및 VSS 하드웨어 공급자) | iSCSITarget-VSS-VDS     | N                     |
|                                       | NFS용 서버                                                 | FS NFS 서비스          | N                     |
|                                       | 작업 폴더                                                   | FS SyncShareService     | N                     |
|                                       | 저장소 서비스                                               | 저장소 서비스        | 예                     |
| 인쇄 및 문서 서비스           | 인쇄 서버                                                   | 인쇄 서버            | N                     |
|                                       | LPD 서비스                                                    | 인쇄 LPD 서비스       | N                     |
| 원격 액세스                         | DirectAccess 및 VPN (RAS)                                     | DirectAccess VPN        | N                     |
|                                       | 라우팅                                                        | 라우팅                 | N                     |
|                                       | 웹 응용 프로그램 프록시                                          | 웹 응용 프로그램 프록시   | N                     |
| 원격 데스크톱 서비스               | 원격 데스크톱 연결 브로커                               | RDS-연결-브로커   | N                     |
|                                       | 원격 데스크톱 라이선싱                                       | RDS 라이선스           | N                     |
|                                       | 원격 데스크톱 가상화 호스트                             | RDS 가상화      | N                     |
| 웹 서버(IIS)                      | 웹 서버                                                     | 웹-웹 서버           | N                     |
|                                       | 일반적인 HTTP 기능                                           | 웹 공통 Http         | N                     |
|                                       | 기본 문서                                               | 웹-기본-Doc         | N                     |
|                                       | 디렉터리 찾아보기                                             | 웹 Dir 검색        | N                     |
|                                       | HTTP 오류                                                    | 웹-Http-오류         | N                     |
|                                       | 정적 콘텐츠                                                 | 웹 정적 콘텐츠      | N                     |
|                                       | HTTP 리디렉션                                               | 웹 Http 리디렉션       | N                     |
|                                       | WebDAV 게시                                              | 웹 DAV 게시      | N                     |
|                                       | 상태 및 진단                                         | 웹 상태              | N                     |
|                                       | HTTP 로깅                                                   | 웹 Http 로깅        | N                     |
|                                       | 사용자 지정 로깅                                                 | 웹-사용자 정의-로깅      | N                     |
|                                       | 로깅 도구                                                  | 웹-로그-라이브러리       | N                     |
|                                       | ODBC 로깅                                                   | 웹 ODBC 로깅        | N                     |
|                                       | 요청 모니터                                              | 웹 요청 모니터     | N                     |
|                                       | 추적                                                        | 웹 Http 추적        | N                     |
|                                       | 성능                                                    | 웹 성능         | N                     |
|                                       | 정적 콘텐츠 압축                                     | 웹-Stat-압축    | N                     |
|                                       | 동적 콘텐츠 압축                                    | 웹-Dyn-압축     | N                     |
|                                       | 보안                                                       | 웹 보안            | N                     |
|                                       | 요청 필터링                                              | 웹 필터링           | N                     |
|                                       | 기본 인증                                           | 웹 기본 인증          | N                     |
|                                       | 중앙 집중화 된 SSL 인증서 지원                            | 웹 CertProvider        | N                     |
|                                       | 클라이언트 인증서 매핑 인증                      | 웹 클라이언트 인증         | N                     |
|                                       | 다이제스트 인증                                          | 웹 다이제스트 인증         | N                     |
|                                       | IIS 클라이언트 인증서 매핑 인증                  | 웹 인증서 인증           | N                     |
|                                       | IP 및 도메인 제한                                     | 웹 IP 보안         | N                     |
|                                       | URL 권한 부여                                              | 웹 Url 인증            | N                     |
|                                       | Windows 인증                                         | 웹 Windows 인증        | N                     |
|                                       | 응용 프로그램 개발                                        | 웹-앱-개발             | N                     |
|                                       | .NET 확장성 3.5                                         | 웹-Net-Ext             | N                     |
|                                       | .NET 확장성 4.6                                         | 웹-Net-Ext45           | N                     |
|                                       | 응용 프로그램을 초기화                                     | 웹 AppInit             | N                     |
|                                       | ASP (영문)                                                            | 웹 ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | 웹 asp (영문) 넷             | N                     |
|                                       | ASP.NET 4.6                                                    | 웹-asp (영문)-Net45           | N                     |
|                                       | CGI                                                            | 웹 CGI                 | N                     |
|                                       | ISAPI 확장                                               | 웹-ISAPI-Ext           | N                     |
|                                       | ISAPI 필터                                                  | 웹 ISAPI 필터        | N                     |
|                                       | 서버측 포함                                           | 웹 포함            | N                     |
|                                       | WebSocket 프로토콜                                             | 웹 WebSockets          | N                     |
|                                       | FTP 서버                                                     | 웹 Ftp 서버          | N                     |
|                                       | FTP 서비스                                                    | 웹 Ftp 서비스         | N                     |
|                                       | FTP 확장성                                              | 웹-Ftp-Ext             | N                     |
|                                       | 관리 도구                                               | 웹 관리 도구          | N                     |
|                                       | IIS 6 관리 호환성                                 | 웹-관리-호환성         | N                     |
|                                       | IIS 6 메타 베이스 호환성                                   | 웹 메타 베이스            | N                     |
|                                       | IIS 6 스크립팅 도구                                          | 웹 Lgcy 스크립팅      | N                     |
|                                       | IIS 6 WMI 호환성                                        | 웹 WMI                 | N                     |
|                                       | IIS 관리 스크립트 및 도구                               | 웹 스크립팅 도구     | N                     |
|                                       | 관리 서비스                                             | 웹 관리 서비스        | N                     |
| Windows Server Update Services        | WID 연결                                               | UpdateServices WidDB    | N                     |
|                                       | WSUS 서비스                                                  | UpdateServices-서비스 | N                     |
|                                       | SQL Server 연결                                        | UpdateServices DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core에 포함 된 기능
Server Core 설치 옵션에는 다음과 같은 기능이 포함 됩니다.

| 특징                                                | 이름                               | 기본적으로 설치 되어 있습니까? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET framework 3.5 기능                            | NET Framework-기능             | N                     |
| .NET framework 3.5 (.NET 2.0 및 3.0 포함)       | NET Framework 코어                 | (제거)             |
| HTTP 활성화                                        | NET HTTP 활성화                | N                     |
| 비 HTTP 활성화                                    | NET-비-HTTP-정품 인증                 | N                     |
| .NET framework 4.6 기능                            | NET Framework-45 기능          | 예                     |
| .NET Framework 4.6                                     | NET Framework-45 코어              | 예                     |
| ASP.NET 4.6                                            | NET Framework-45 ASPNET            | N                     |
| WCF 서비스                                           | NET-WCF-Services45                 | 예                     |
| HTTP 활성화                                        | NET WCF-HTTP Activation45          | N                     |
| 메시지 큐 (MSMQ) 정품 인증                      | NET WCF-MSMQ Activation45          | N                     |
| 명명 된 파이프 정품 인증                                  | NET WCF-파이프 Activation45          | N                     |
| TCP 정품 인증                                         | NET WCF-TCP Activation45           | N                     |
| TCP 포트 공유                                       | NET WCF-TCP PortSharing45          | 예                     |
| BITS(Background Intelligent Transfer Service)         | 비트                               | N                     |
| Compact 서버                                         | 비트 압축 서버                | N                     |
| BitLocker 드라이브 암호화                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS용 클라이언트                                         | NFS 클라이언트                         | N                     |
| 컨테이너                                             | 컨테이너                         | N                     |
| 데이터 센터 브리징                                   | 데이터 센터 브리징               | N                     |
| 강화된 저장소                                       | EnhancedStorage                    | N                     |
| 장애 조치(failover) 클러스터링                                    | 장애 조치 클러스터링                | N                     |
| 그룹 정책 관리                                | GPMC                               | N                     |
| I/O 서비스 품질                                 | DiskIo QoS                         | N                     |
| IIS 호스팅 가능한 웹 코어                                  | 웹 WHC                            | N                     |
| IP 주소 (IPAM) 관리 서버                    | IPAM                               | N                     |
| iSNS 서버 서비스                                    | ISNS                               | N                     |
| 관리 OData IIS 확장                         | ManagementOdata                    | N                     |
| 미디어 파운데이션                                       | 서버-미디어-Foundation            | N                     |
| 메시지 큐                                        | MSMQ                               | N                     |
| 메시지 큐 서비스                               | MSMQ 서비스                      | N                     |
| 메시지 큐 서버                                 | MSMQ 서버                        | N                     |
| 디렉터리 서비스 통합                          | MSMQ 디렉터리                     | N                     |
| HTTP 지원                                           | MSMQ HTTP 지원                  | N                     |
| 메시지 큐 트리거                               | MSMQ 트리거                      | N                     |
| 라우팅 서비스                                        | MSMQ 라우팅                       | N                     |
| 메시지 큐 DCOM 프록시                             | MSMQ DCOM                          | N                     |
| 다중 경로 I/O                                          | 다중 경로 IO                       | N                     |
| MultiPoint 커넥터                                   | MultiPoint 커넥터               | N                     |
| MultiPoint 커넥터 서비스                          | 다중 포인트-커넥터-서비스      | N                     |
| MultiPoint 관리자 및 MultiPoint 대시보드            | MultiPoint 도구                   | N                     |
| 네트워크 부하 분산                                 | NLB                                | N                     |
| 피어 이름 확인 프로토콜                          | PNRP                               | N                     |
| qWave(Quality Windows Audio Video Experience)                 | qWave                              | N                     |
| 원격 차등 압축                        | RDC                                | N                     |
| 원격 서버 관리 도구                     | RSAT                               | N                     |
| 기능 관리 도구                           | RSAT-기능-도구                 | N                     |
| BitLocker 드라이브 암호화 관리 유틸리티  | RSAT 기능-도구 BitLocker       | N                     |
| DataCenterBridging LLDP 도구                          | RSAT DataCenterBridging-LLDP 도구 | N                     |
| 장애 조치 클러스터링 도구                              | RSAT 클러스터링                    | N                     |
| Windows PowerShell에 대 한 장애 조치 클러스터 모듈         | RSAT-클러스터링-PowerShell         | N                     |
| 장애 조치 클러스터 자동화 서버                     | RSAT 클러스터링 AutomationServer   | N                     |
| 장애 조치 클러스터 명령 인터페이스                     | RSAT 클러스터링 CmdInterface       | N                     |
| IP 주소 관리 (IPAM) 클라이언트                    | IPAM-클라이언트-기능                | N                     |
| 차폐 VM 도구                                      | RSAT-보호-VM-도구             | N                     |
| Windows PowerShell에 대 한 저장소 복제본 모듈          | RSAT 저장소 복제               | N                     |
| 역할 관리 도구                              | RSAT-역할-도구                    | N                     |
| AD DS 및 AD LDS 도구                                 | RSAT-AD-도구                      | N                     |
| Windows PowerShell에 대 한 active Directory 모듈         | RSAT-AD-PowerShell                 | N                     |
| AD DS 도구                                            | RSAT 추가                          | N                     |
| Active Directory 관리 센터                 | RSAT-AD-AdminCenter                | N                     |
| AD DS 스냅인 및 명령줄 도구                  | RSAT 추가 하는 도구                    | N                     |
| AD LDS 스냅인 및 명령줄 도구                 | RSAT ADLDS                         | N                     |
| Hyper-v 관리 도구                               | RSAT-하이퍼-V-도구                 | N                     |
| Windows PowerShell에 대 한 Hyper-v 모듈                  | Hyper-V-PowerShell                 | N                     |
| Windows Server Update Services 도구                   | UpdateServices RSAT                | N                     |
| API 및 PowerShell cmdlet                             | UpdateServices API                 | N                     |
| DHCP 서버 도구                                      | RSAT DHCP                          | N                     |
| DNS 서버 도구                                       | RSAT DNS 서버                    | N                     |
| 원격 액세스 관리 도구                         | RSAT 원격 액세스                  | N                     |
| Windows PowerShell에 대 한 원격 액세스 모듈            | RSAT-원격 액세스-PowerShell       | N                     |
| RPC over HTTP 프록시                                    | RPC 조치-HTTP 프록시                | N                     |
| 설정 및 부팅 이벤트 수집                        | 설치 하 고-부팅-이벤트-모음    | N                     |
| 단순 TCP/IP 서비스                                 | 단순 TCPIP                       | N                     |
| SMB 1.0/CIFS 파일 공유 지원                      | FS SMB1                            | 예                     |
| SMB 대역폭 제한                                    | FS SMBBW                           | N                     |
| SNMP 서비스                                           | SNMP 서비스                       | N                     |
| SNMP WMI 공급자                                      | SNMP WMI 공급자                  | N                     |
| 텔넷 클라이언트                                          | 텔넷 클라이언트                      | N                     |
| 패브릭 관리를 위한 VM 보호 도구               | FabricShieldedTools                | N                     |
| Windows Defender 기능                              | Windows-Defender-기능          | 예                     |
| Windows Defender                                       | Windows Defender                   | 예                     |
| Windows 내부 데이터베이스                              | Windows 내부 데이터베이스          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | 예                     |
| Windows PowerShell 5.1                                 | PowerShell                         | 예                     |
| Windows PowerShell 2.0 엔진                          | PowerShell V2                      | (제거)             |
| Windows PowerShell 원하는 상태 구성 서비스 | DSC 서비스                        | N                     |
| Windows PowerShell 웹 액세스                          | WindowsPowerShellWebAccess         | N                     |
| Windows Process Activation Service                     | 되었습니다.                                | N                     |
| 프로세스 모델                                          | 프로세스를-모델                  | N                     |
| .NET 환경 3.5                                   | NET 했습니다-환경                | N                     |
| 구성 api (영문)                                     | 된-Config-api (영문)                    | N                     |
| Windows Server 백업                                  | Windows Server 백업              | N                     |
| Windows Server 마이그레이션 도구                         | 마이그레이션                          | N                     |
| Windows 표준 기반 저장소 관리             | WindowsStorageManagementService    | N                     |
| WinRM IIS 확장                                    | WinRM-IIS-Ext                      | N                     |
| WINS 서버                                            | WINS                               | N                     |
| WoW64 지원                                          | WoW64 지원                      | 예                     |
|                                                        |                                    |                       |
