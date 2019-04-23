---
title: 역할, 역할 서비스 및 Windows Server에서 Server Core에 포함 된 기능
description: 역할 및 기능 Windows Server의 Server Core 설치 옵션에 포함 되나요?
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 65729eb68c9590fd6316f5650be48f33c19c926d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859294"
---
# <a name="roles-role-services-and-features-included-in-windows-server---server-core"></a>역할, 역할 서비스 및 Windows Server에서 Server Core에 포함 된 기능

> 적용 대상: Windows Server (반기 채널) 및 Windows Server 2016

일반적으로 대 한 이야기 [항목의 *없습니다* Server Core에서](server-core-removed-roles.md) 다른 방법을 시도 하 게 하겠습니다-의 *포함* 무엇인가여부및*기본적으로 설치*합니다. 다음 역할, 역할 서비스 및 기능 *에서* Windows Server의 Server Core 설치 옵션입니다. Server Core 옵션을 사용자 환경에 작동 하는 경우를 파악 하는 데이 정보를 사용 합니다. 큰 목록이 이기 때문에 특정 역할이 나 기능에 관심이 있다면-, 원하는 항목을 검색 하는 반환 하지 않는 경우에 대 한 검색 해 보십시오 Server Core에 포함 되지 않습니다.

예를 들어, "원격 데스크톱 세션 호스트"-검색 하는 경우이 페이지에서 찾이 없습니다. 이것은 RD 세션 호스트는 Server Core 이미지에 포함 되지 않습니다.

기억할 수 있는 [항상 찾습니다](server-core-removed-roles.md) 어떤의 *하지* 포함 합니다. 이 몇 가지 살펴보고 하는 다른 방법입니다.

## <a name="roles-included-in-server-core"></a>Server Core에 포함 된 역할
Server Core 설치 옵션에는 다음 서버 역할이 포함 됩니다.

| 역할                                            | 이름                           | 기본적으로 설치 되어 있습니까? |
|-------------------------------------------------|--------------------------------|-----------------------|
| Active Directory 인증서 서비스           | AD 인증서                 | N                     |
| Active Directory 도메인 서비스                | AD-Domain-Services             | N                     |
| AD FS(Active Directory Federation Services)            | ADFS 페더레이션                | N                     |
| Active Directory LDS(Lightweight Directory Services) | ADLDS                          | N                     |
| Active Directory Rights Management Services     | ADRMS                          | N                     |
| 디바이스 상태 증명                       | DeviceHealthAttestationService | N                     |
| DHCP 서버                                     | DHCP                           | N                     |
| DNS 서버                                      | DNS                            | N                     |
| 파일 및 저장소 서비스                       | FileAndStorage-Services        | Y                     |
| 호스트 보호 서비스                           | HostGuardianServiceRole        | N                     |
| Hyper-V                                         | Hyper-V                        | N                     |
| 인쇄 및 문서 서비스                     | 인쇄 서비스                 | N                     |
| 원격 액세스                                   | RemoteAccess                   | N                     |
| 원격 데스크톱 서비스                         | Remote-Desktop-Services        | N                     |
| 볼륨 정품 인증 서비스                      | VolumeActivation               | N                     |
| IIS 웹 서버                                  | 웹 서버                     | N                     |
| Windows Server 필수 패키지 환경            | ServerEssentialsRole           | N                     |
| Windows Server Update Services                  | UpdateServices                 | N                     |

## <a name="role-services-included-in-server-core"></a>Server Core에 포함 된 역할 서비스
Server Core 설치 옵션을 다음 역할 서비스가 포함 됩니다.

| 역할                                  | 역할 서비스                                                   | 이름                    | 기본적으로 설치 되어 있습니까? |
|---------------------------------------|----------------------------------------------------------------|-------------------------|-----------------------|
| Active Directory 인증서 서비스 | 인증 기관                                        | ADCS-Cert-Authority     | N                     |
|                                       | 인증서 등록 정책 웹 서비스                      | ADCS-Enroll-Web-Pol     | N                     |
|                                       | 인증서 등록 웹 서비스                             | ADCS-Enroll-Web-Svc     | N                     |
|                                       | 인증 기관 웹 등록                         | ADCS 웹 등록     | N                     |
|                                       | 네트워크 장치 등록 서비스                              | ADCS 장치 등록  | N                     |
|                                       | 온라인 응답기                                               | 온라인 인증서 ADCS        | N                     |
| Active Directory Rights Management    | Active Directory Rights Management Server                      | ADRMS 서버            | N                     |
|                                       | ID 페더레이션 지원                                    | ADRMS-Identity          | N                     |
| 파일 및 저장소 서비스             | 파일 및 iSCSI 서비스                                        | File-Services           | N                     |
|                                       | 파일 서버                                                    | FS-FileServer           | N                     |
|                                       | 네트워크 파일용 BranchCache                                  | FS-BranchCache          | N                     |
|                                       | 데이터 중복 제거                                             | FS-데이터-중복 제거   | N                     |
|                                       | DFS 네임스페이스                                                 | FS-DFS-Namespace        | N                     |
|                                       | DFS 복제                                                | FS DFS 복제      | N                     |
|                                       | 파일 서버 리소스 관리자                                   | FS-Resource-Manager     | N                     |
|                                       | 파일 서버 VSS 에이전트 서비스                                  | FS-VSS-Agent            | N                     |
|                                       | iSCSI 대상 서버                                            | iSCSITarget-Server      | N                     |
|                                       | iSCSI 대상 저장소 공급자 (VDS 및 VSS 하드웨어 공급자) | iSCSITarget-VSS-VDS     | N                     |
|                                       | NFS용 서버                                                 | FS-NFS-Service          | N                     |
|                                       | 클라우드 폴더                                                   | FS-SyncShareService     | N                     |
|                                       | 저장소 서비스                                               | Storage-Services        | Y                     |
| 인쇄 및 문서 서비스           | 인쇄 서버                                                   | 인쇄 서버            | N                     |
|                                       | LPD 서비스                                                    | Print-LPD-Service       | N                     |
| 원격 액세스                         | DirectAccess 및 VPN (RAS)                                     | DirectAccess-VPN        | N                     |
|                                       | 라우팅                                                        | 라우팅                 | N                     |
|                                       | 웹 응용 프로그램 프록시                                          | 웹 응용 프로그램 프록시   | N                     |
| 원격 데스크톱 서비스               | 원격 데스크톱 연결 브로커                               | RDS-Connection-Broker   | N                     |
|                                       | 원격 데스크톱 라이선싱                                       | RDS 라이선스           | N                     |
|                                       | 원격 데스크톱 가상화 호스트                             | RDS 가상화      | N                     |
| 웹 서버(IIS)                      | 웹 서버                                                     | Web-WebServer           | N                     |
|                                       | 일반 HTTP 기능                                           | 웹 일반 Http         | N                     |
|                                       | 기본 문서                                               | 웹-기본-문서         | N                     |
|                                       | 디렉터리 검색                                             | 웹 디렉터리 검색        | N                     |
|                                       | HTTP 오류                                                    | 웹 Http 오류         | N                     |
|                                       | 정적 콘텐츠                                                 | 정적 콘텐츠 웹      | N                     |
|                                       | HTTP 리디렉션                                               | Web-Http-Redirect       | N                     |
|                                       | WebDAV 게시                                              | Web-DAV-Publishing      | N                     |
|                                       | 상태 및 진단                                         | 웹 상태              | N                     |
|                                       | HTTP 로깅                                                   | Web-Http-Logging        | N                     |
|                                       | 사용자 지정 로깅                                                 | 웹 사용자 지정 로깅      | N                     |
|                                       | 로깅 도구                                                  | 웹 로그 라이브러리       | N                     |
|                                       | ODBC 로깅                                                   | Web-ODBC-Logging        | N                     |
|                                       | 요청 모니터                                              | 웹 요청 모니터     | N                     |
|                                       | 추적                                                        | 웹 Http 추적        | N                     |
|                                       | 성능                                                    | 웹 성능         | N                     |
|                                       | 정적 콘텐츠 압축                                     | 웹 상태 압축    | N                     |
|                                       | 동적 콘텐츠 압축                                    | 웹 Dyn 압축     | N                     |
|                                       | 보안                                                       | 웹 보안            | N                     |
|                                       | 요청 필터링                                              | 웹 필터링           | N                     |
|                                       | 기본 인증                                           | Web-Basic-Auth          | N                     |
|                                       | 중앙 집중식된 SSL 인증서 지원                            | Web-CertProvider        | N                     |
|                                       | 클라이언트 인증서 매핑 인증                      | 웹 클라이언트 인증         | N                     |
|                                       | 다이제스트 인증                                          | Web-Digest-Auth         | N                     |
|                                       | IIS 클라이언트 인증서 매핑 인증                  | Web-Cert-Auth           | N                     |
|                                       | IP 및 도메인 제한                                     | 웹-IP-보안         | N                     |
|                                       | URL 권한 부여                                              | Web-Url-Auth            | N                     |
|                                       | Windows 인증                                         | Web-Windows-Auth        | N                     |
|                                       | 애플리케이션 개발                                        | Web-App-Dev             | N                     |
|                                       | .NET 확장성 3.5                                         | 웹-Net-Ext             | N                     |
|                                       | .NET 확장성 4.6                                         | Web-Net-Ext45           | N                     |
|                                       | 응용 프로그램 초기화                                     | Web-AppInit             | N                     |
|                                       | ASP                                                            | Web-ASP                 | N                     |
|                                       | ASP.NET 3.5                                                    | Web-Asp-Net             | N                     |
|                                       | ASP.NET 4.6                                                    | Web-Asp-Net45           | N                     |
|                                       | CGI                                                            | Web-CGI                 | N                     |
|                                       | ISAPI 확장                                               | Web-ISAPI-Ext           | N                     |
|                                       | ISAPI 필터                                                  | Web-ISAPI-Filter        | N                     |
|                                       | 서버 측 Include                                           | 웹 포함            | N                     |
|                                       | WebSocket 프로토콜                                             | Web-WebSockets          | N                     |
|                                       | FTP 서버                                                     | Web-Ftp-Server          | N                     |
|                                       | FTP 서비스                                                    | Web-Ftp-Service         | N                     |
|                                       | FTP 확장성                                              | 웹-Ftp-Ext             | N                     |
|                                       | 관리 도구                                               | 웹 관리 도구          | N                     |
|                                       | IIS 6 관리 호환성                                 | 웹 관리 호환성         | N                     |
|                                       | IIS 6 메타베이스 호환성                                   | 웹-메타 베이스            | N                     |
|                                       | IIS 6 스크립팅 도구                                          | 웹 Lgcy 스크립팅      | N                     |
|                                       | IIS 6 WMI 호환성                                        | Web-WMI                 | N                     |
|                                       | IIS 관리 스크립트 및 도구                               | 웹 스크립팅 도구     | N                     |
|                                       | 관리 서비스                                             | Web-Mgmt-Service        | N                     |
| Windows Server Update Services        | WID 연결                                               | UpdateServices-WidDB    | N                     |
|                                       | WSUS 서비스                                                  | UpdateServices-Services | N                     |
|                                       | SQL Server 연결                                        | UpdateServices-DB       | N                     |

## <a name="features-included-in-server-core"></a>Server Core에 포함 된 기능
Server Core 설치 옵션에는 다음과 같은 기능이 있습니다.

| 기능                                                | 이름                               | 기본적으로 설치 되어 있습니까? |
|--------------------------------------------------------|------------------------------------|-----------------------|
| .NET framework 3.5 기능                            | NET Framework 기능             | N                     |
| .NET framework 3.5 (.NET 2.0 및 3.0 포함)       | NET-Framework-Core                 | (제거)             |
| HTTP 활성화                                        | NET HTTP 활성화                | N                     |
| 비 HTTP 활성화                                    | NET-비-HTTP-액티브                 | N                     |
| .NET framework 4.6 기능                            | NET Framework-45 기능          | Y                     |
| .NET framework 4.6                                     | NET-Framework-45-Core              | Y                     |
| ASP.NET 4.6                                            | NET-Framework-45-ASPNET            | N                     |
| WCF Services                                           | NET-WCF-Services45                 | Y                     |
| HTTP 활성화                                        | WCF HTTP Activation45 NET          | N                     |
| 메시지 큐 (MSMQ) 활성화                      | NET-WCF-MSMQ-Activation45          | N                     |
| 명명 된 파이프 활성화                                  | NET WCF-파이프 Activation45          | N                     |
| TCP 활성화                                         | WCF TCP Activation45 NET           | N                     |
| TCP 포트 공유                                       | NET-WCF-TCP-PortSharing45          | Y                     |
| BITS(Background Intelligent Transfer Service)         | BITS                               | N                     |
| Compact 서버                                         | BITS Compact 서버                | N                     |
| BitLocker 드라이브 암호화                             | BitLocker                          | N                     |
| BranchCache                                            | BranchCache                        | N                     |
| NFS용 클라이언트                                         | NFS 클라이언트                         | N                     |
| 컨테이너                                             | 컨테이너                         | N                     |
| 데이터 센터 브리징                                   | 데이터 센터 브리징               | N                     |
| 강화된 저장소                                       | EnhancedStorage                    | N                     |
| 장애 조치(failover) 클러스터링                                    | 장애 조치 클러스터링                | N                     |
| 그룹 정책 관리                                | GPMC                               | N                     |
| I/O 서비스 품질                                 | DiskIo-QoS                         | N                     |
| IIS 호스팅 가능한 웹 코어                                  | 웹 WHC                            | N                     |
| IPAM(IP 주소 관리) 서버                    | IPAM                               | N                     |
| iSNS 서버 서비스                                    | ISNS                               | N                     |
| 관리 OData IIS 확장                         | ManagementOdata                    | N                     |
| 미디어 파운데이션                                       | 서버-미디어-Foundation            | N                     |
| 메시지 큐                                        | MSMQ                               | N                     |
| 메시지 큐 서비스                               | MSMQ-Services                      | N                     |
| 메시지 큐 서버                                 | MSMQ-Server                        | N                     |
| 디렉터리 서비스 통합                          | MSMQ-Directory                     | N                     |
| HTTP 지원                                           | MSMQ-HTTP-Support                  | N                     |
| 메시지 큐 트리거                               | MSMQ-Triggers                      | N                     |
| 라우팅 서비스                                        | MSMQ-Routing                       | N                     |
| 메시지 큐 DCOM 프록시                             | MSMQ-DCOM                          | N                     |
| 다중 경로 I/O                                          | 다중 경로 IO                       | N                     |
| MultiPoint 커넥터                                   | MultiPoint-Connector               | N                     |
| 다중 포인트 커넥터 서비스                          | MultiPoint-Connector-Services      | N                     |
| 다중 포인트 관리자 및 MultiPoint 대시보드            | MultiPoint-Tools                   | N                     |
| 네트워크 부하 분산                                 | NLB                                | N                     |
| 피어 이름 확인 프로토콜                          | PNRP                               | N                     |
| qWave(Quality Windows Audio Video Experience)                 | qWave                              | N                     |
| 원격 차등 압축                        | RDC                                | N                     |
| 원격 서버 관리 도구                     | RSAT                               | N                     |
| 기능 관리 도구                           | RSAT-기능-도구                 | N                     |
| BitLocker 드라이브 암호화 관리 유틸리티  | RSAT-Feature-Tools-BitLocker       | N                     |
| DataCenterBridging LLDP 도구                          | RSAT-DataCenterBridging-LLDP-Tools | N                     |
| 장애 조치(failover) 클러스터링 도구                              | RSAT-클러스터링                    | N                     |
| Windows PowerShell 용 장애 조치 클러스터 모듈         | RSAT-클러스터링-PowerShell         | N                     |
| 장애 조치 클러스터 자동화 서버                     | RSAT-Clustering-AutomationServer   | N                     |
| 장애 조치 클러스터 명령 인터페이스                     | RSAT-클러스터링-CmdInterface       | N                     |
| IP 주소 관리 (IPAM) 클라이언트                    | IPAM 클라이언트 기능                | N                     |
| 차폐 VM 도구                                      | RSAT-Shielded-VM-Tools             | N                     |
| Windows PowerShell 용 저장소 복제본 모듈          | RSAT-Storage-Replica               | N                     |
| 역할 관리 도구                              | RSAT-Role-Tools                    | N                     |
| AD DS 및 AD LDS 도구                                 | RSAT-AD-Tools                      | N                     |
| Windows PowerShell용 Active Directory 모듈         | RSAT-AD-PowerShell                 | N                     |
| AD DS 도구                                            | RSAT-ADDS                          | N                     |
| Active Directory 관리 센터                 | RSAT-AD-AdminCenter                | N                     |
| AD DS 스냅인 및 명령줄 도구                  | RSAT-ADDS-Tools                    | N                     |
| AD LDS 스냅인 및 명령줄 도구                 | RSAT-ADLDS                         | N                     |
| Hyper-V 관리 도구                               | RSAT-Hyper-V-Tools                 | N                     |
| Windows PowerShell용 Hyper-V 모듈                  | Hyper-V-PowerShell                 | N                     |
| Windows Server Update Services 도구                   | UpdateServices-RSAT                | N                     |
| API 및 PowerShell cmdlet                             | UpdateServices-API                 | N                     |
| DHCP 서버 도구                                      | RSAT-DHCP                          | N                     |
| DNS 서버 도구                                       | RSAT-DNS-Server                    | N                     |
| 원격 액세스 관리 도구                         | RSAT-RemoteAccess                  | N                     |
| Windows PowerShell용 원격 액세스 모듈            | RSAT-RemoteAccess-PowerShell       | N                     |
| RPC over HTTP 프록시                                    | RPC-over-HTTP-Proxy                | N                     |
| 이벤트 컬렉션 설치 및 부팅                        | Setup-and-Boot-Event-Collection    | N                     |
| 단순 TCP/IP 서비스                                 | Simple-TCPIP                       | N                     |
| SMB 1.0/CIFS 파일 공유 지원                      | FS-SMB1                            | Y                     |
| SMB 대역폭 제한                                    | FS-SMBBW                           | N                     |
| SNMP 서비스                                           | SNMP-Service                       | N                     |
| SNMP WMI 공급자                                      | SNMP-WMI-Provider                  | N                     |
| 텔넷 클라이언트                                          | 텔넷 클라이언트                      | N                     |
| 패브릭 관리를 위한 VM 보호 도구               | FabricShieldedTools                | N                     |
| Windows Defender 기능                              | Windows Defender 기능          | Y                     |
| Windows Defender                                       | Windows-Defender                   | Y                     |
| Windows 내부 데이터베이스                              | Windows 내부 데이터베이스          | N                     |
| Windows PowerShell                                     | PowerShellRoot                     | Y                     |
| Windows PowerShell 5.1                                 | PowerShell                         | Y                     |
| Windows PowerShell 2.0 엔진                          | PowerShell-V2                      | (제거)             |
| Windows PowerShell Desired State Configuration 서비스 | DSC-Service                        | N                     |
| Windows PowerShell 웹 액세스                          | WindowsPowerShellWebAccess         | N                     |
| Windows Process Activation Service                     | 되었습니다.                                | N                     |
| 프로세스 모델                                          | 가 프로세스 모델                  | N                     |
| .NET 환경 3.5                                   | 가-NET-환경                | N                     |
| 구성 API                                     | 구성 된-Api                    | N                     |
| Windows Server 백업                                  | Windows-Server-Backup              | N                     |
| Windows Server 마이그레이션 도구                         | 마이그레이션                          | N                     |
| Windows 표준 기반 저장소 관리             | WindowsStorageManagementService    | N                     |
| WinRM IIS 확장                                    | WinRM-IIS-Ext                      | N                     |
| WINS 서버                                            | WINS                               | N                     |
| WoW64 지원                                          | WoW64 지원                      | Y                     |
|                                                        |                                    |                       |
