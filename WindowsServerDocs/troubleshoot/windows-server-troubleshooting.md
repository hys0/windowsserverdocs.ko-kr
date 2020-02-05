---
title: Windows Server 문제 해결
description: Windows Server 문제에 대 한 문제 해결 문서 링크 가져오기
layout: LandingPage
ms.prod: windows-server
ms.custom:
- CI 113175
- CSSTroubleshooting
audience: Admin
ms.service: na
manager: ''
ms.technology: server-general
ms.date: 1/24/2020
ms.topic: landing-page
author: kaushika-msft
ms.author: kaushika
ms.openlocfilehash: 593fc4abbdce3ed53fa8d7ef73d529558b100bcc
ms.sourcegitcommit: 3f9bcd188dda12dc5803defb47b2c3a907504255
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/04/2020
ms.locfileid: "77001798"
---
# <a name="troubleshooting-windows-server-components"></a>Windows Server 구성 요소 문제 해결

> [!TIP]
> 이전 버전의 Windows Server에 대한 정보를 찾으시나요? docs.microsoft.com에서 다른 [Windows Server 라이브러리](/previous-versions/windows/)를 확인하세요.  
>   
> [이 사이트에서 특정 정보를 검색](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)할 수도 있습니다.

Microsoft에서는 Windows Server 용 업데이트를 정기적으로 모두 릴리스 합니다. 서버가 보안 업데이트를 포함한 향후 업데이트를 받을 수 있도록 업데이트된 상태로 유지해야 합니다. 릴리스된 업데이트의 전체 목록은 [Windows 10 및 Windows Server 2016 업데이트 기록](https://support.microsoft.com/help/4000825/windows-10-windows-server-2016-update-history)을 확인하세요.

이 섹션에서는 Windows Server의 문제를 해결 하는 데 도움이 되는 고급 문제 해결 항목 및 링크를 제공 합니다. 추가 항목이 사용 가능 해지면 추가 됩니다.

## <a name="troubleshoot-activation"></a>정품 인증 문제 해결

- [Windows 볼륨 정품 인증 문제 해결](https://docs.microsoft.com/windows-server/get-started/activation-troubleshooting-guide)
- [KMS 문제 해결을 위한 지침](https://docs.microsoft.com/windows-server/get-started/activation-troubleshoot-kms-general)
- [볼륨 정품 인증 정보를 얻기 위한 Slmgr.vbs 옵션](https://docs.microsoft.com/windows-server/get-started/activation-slmgr-vbs-options)
- [Windows 정품 인증 오류 코드 해결](https://docs.microsoft.com/windows-server/get-started/activation-error-codes)
- [KMS 정품 인증의 알려진 문제](https://docs.microsoft.com/windows-server/get-started/activation-troubleshoot-kms-issues)
- [MAK 정품 인증의 알려진 문제](https://docs.microsoft.com/windows-server/get-started/activation-troubleshoot-mak-issues)
- [DNS 관련 정품 인증 문제 해결을 위한 지침](https://docs.microsoft.com/windows-server/get-started/common-troubleshooting-procedures-kms-dns)
- [Tokens.dat 파일 다시 빌드](https://docs.microsoft.com/windows-server/get-started/activation-rebuild-tokens-dat-file)
- [ADBA 클라이언트 문제 해결](https://docs.microsoft.com/windows-server/get-started/activation-troubleshoot-adba-clients)

## <a name="troubleshoot-startup-and-restart"></a>시작 및 다시 시작 문제 해결

- [Windows 시작에 대 한 고급 문제 해결](https://docs.microsoft.com/windows/client-management/troubleshoot-windows-startup.md)
- [How to determine the appropriate page file size for 64-bit versions of Windows](https://docs.microsoft.com/windows/client-management/determine-appropriate-page-file-size.md)(Windows 64비트 버전에 적절한 페이지 파일 크기를 결정하는 방법)
- [커널 또는 전체 크래시 덤프 생성](https://docs.microsoft.com/windows/client-management/generate-kernel-or-complete-crash-dump.md)
- [페이지 파일 소개](https://docs.microsoft.com/windows/client-management/introduction-page-file.md)
- [Windows에서 시스템 오류 및 복구 옵션 구성](https://docs.microsoft.com/windows/client-management/system-failure-recovery-options.md)
- [Windows 부팅 문제에 대 한 고급 문제 해결](https://docs.microsoft.com/windows/client-management/advanced-troubleshooting-boot-problems.md)
- [Windows 기반 컴퓨터 중지에 대 한 고급 문제 해결](https://docs.microsoft.com/windows/client-management/troubleshoot-windows-freeze.md)
- [중지 오류 또는 블루 스크린 오류에 대 한 고급 문제 해결](https://docs.microsoft.com/windows/client-management/troubleshoot-stop-errors.md)
- [중지 오류 7B 또는 Inaccessible_Boot_Device에 대 한 고급 문제 해결](https://docs.microsoft.com/windows/client-management/troubleshoot-inaccessible-boot-device.md)
- [이벤트 ID 41에 대 한 고급 문제 해결 "시스템을 처음부터 종료 하지 않고 다시 부팅 했습니다."](https://docs.microsoft.com/windows/client-management/troubleshoot-event-id-41-restart.md)
- [기본 Broadcom 네트워크 어댑터 드라이버를 업데이트할 때 중지 오류가 발생 합니다.](https://docs.microsoft.com/windows/client-management/troubleshoot-stop-error-on-broadcom-driver-update.md)

## <a name="troubleshoot-ad-forest-recovery"></a>AD 포리스트 복구 문제 해결

- [AD 포리스트 복구 - FAQ](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/ad-forest-recovery-faq)

## <a name="troubleshoot-ad-replication"></a>AD 복제 문제 해결

- [Active Directory 복제 문제 해결](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems)
- [가상화된 도메인 컨트롤러 문제 해결](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/virtual-dc/virtualized-domain-controller-troubleshooting)
- [도메인 컨트롤러 배포 문제 해결](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/troubleshooting-domain-controller-deployment)
- [문제 해결을 위한 컴퓨터 구성](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/troubleshoot/configuring-a-computer-for-troubleshooting)

## <a name="troubleshoot-ad-fs"></a>문제 해결 AD FS

- [문제 해결 AD FS](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-overview)
- [AD FS 문제 해결-감사 이벤트 및 로깅](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging)
- [AD FS 문제 해결-SQL 연결](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-sql)
- [AD FS 문제 해결-클레임 발급](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-claims-issuance)
- [AD FS 문제 해결-루프 검색](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-loop)
- [AD FS 문제 해결-인증서](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-certs)
- [AD FS 문제 해결-Fiddler](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-fiddler)
- [AD FS 문제 해결-Fiddler](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-fiddler-ws-fed)
- [AD FS 문제 해결-클레임 규칙](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-claims-rules)
- [AD FS 문제 해결-Windows 통합 인증](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-iwa)
- [AD FS 문제 해결-Azure AD](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-azure)
- [AD FS FAQ](https://docs.microsoft.com/windows-server/identity/ad-fs/overview/ad-fs-faq)
- [AD FS 도움말 진단 분석기](https://docs.microsoft.com/windows-server/identity/ad-fs/troubleshooting/ad-fs-diagnostics-analyzer)

## <a name="troubleshoot-aovpn"></a>AoVPN 문제 해결

- [Always On VPN 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy-troubleshooting)

## <a name="troubleshoot-converged-nic"></a>수렴 형 NIC 문제 해결

- [수렴 형 NIC 구성 문제 해결](https://docs.microsoft.com/windows-server/networking/technologies/conv-nic/cnic-app-troubleshoot)

## <a name="troubleshoot-dfsr"></a>DFSR 문제 해결

- [DFS 복제: FAQ (질문과 대답)](https://docs.microsoft.com/windows-server/storage/dfs-replication/dfsr-faq)

## <a name="troubleshoot-directaccess"></a>DirectAccess 문제 해결

- [DirectAccess 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/directaccess/troubleshooting-directaccess)

## <a name="troubleshoot-disk-management"></a>디스크 관리 문제 해결

- [디스크의 관리 문제 해결](https://docs.microsoft.com/windows-server/storage/disk-management/troubleshooting-disk-management)

## <a name="troubleshoot-dns"></a>DNS 문제 해결

- [DNS (Domain Name System) 문제 해결](https://docs.microsoft.com/windows-server/networking/dns/troubleshoot/troubleshoot-dns-data-collection)
- [DNS 클라이언트 문제 해결](https://docs.microsoft.com/windows-server/networking/dns/troubleshoot/troubleshoot-dns-client)
- [DNS 클라이언트에서 DNS 클라이언트 쪽 캐싱 비활성화](https://docs.microsoft.com/windows-server/networking/dns/troubleshoot/disable-dns-client-side-caching)
- [DNS 서버 문제 해결](https://docs.microsoft.com/windows-server/networking/dns/troubleshoot/troubleshoot-dns-server)

## <a name="troubleshoot-failover-cluster"></a>장애 조치 (failover) 클러스터 문제 해결

- [Windows 오류 보고를 사용하여 장애 조치(failover) 클러스터 문제 해결](https://docs.microsoft.com/windows-server/failover-clustering/troubleshooting-using-wer-reports)
- [클러스터 인식 업데이트-질문과 대답](https://docs.microsoft.com/windows-server/failover-clustering/cluster-aware-updating-faq)

## <a name="troubleshoot-fsrm"></a>FSRM 문제 해결

- [파일 서버 리소스 관리자 문제 해결](https://docs.microsoft.com/windows-server/storage/fsrm/troubleshooting-file-server-resource-manager)

## <a name="troubleshoot-guarded-fabric"></a>보호 된 패브릭 문제 해결

- [보호 된 패브릭 진단 도구를 사용 하 여 문제 해결](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-diagnostics)
- [호스트 보호자 서비스 문제 해결](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hgs)
- [호스트 보호자 서비스 문제 해결](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-hosts)

## <a name="troubleshoot-multi-site-ras"></a>다중 사이트 RAS 문제 해결

- [멀티 사이트 사용 관련 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/ras/multisite/troubleshoot/troubleshooting-enabling-multisite)
- [진입점 추가 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/ras/multisite/troubleshoot/troubleshooting-adding-entry-points)
- [진입점 도메인 컨트롤러 설정 관련 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/ras/multisite/troubleshoot/troubleshooting-setting-the-entry-point-domain-controller)
- [웹 프로브 URL 관련 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/ras/multisite/troubleshoot/troubleshooting-web-probe-urls)

## <a name="troubleshoot-nano-server"></a>Nano 서버 문제 해결

- [Nano 서버 문제 해결](https://docs.microsoft.com/windows-server/get-started/troubleshooting-nano-server)

## <a name="troubleshoot-nic-teaming"></a>NIC 팀 문제 해결

- [NIC 팀 문제 해결](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/troubleshooting-nic-teaming)

## <a name="troubleshoot-otp-authentication"></a>OTP 인증 문제 해결

- [인증 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/troubleshoot/troubleshooting-authentication-issues)
- [OTP 사용 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/ras/otp/troubleshoot/troubleshooting-enabling-otp)

## <a name="troubleshoot-qos"></a>QoS 문제 해결

- [QoS 질문과 대답](https://docs.microsoft.com/windows-server/networking/technologies/qos/qos-policy-faq)

## <a name="troubleshoot-s2d"></a>S2D 문제 해결

- [스토리지 공간 다이렉트 문제 해결](https://docs.microsoft.com/windows-server/storage/storage-spaces/troubleshooting-storage-spaces)
- [스토리지 공간 다이렉트-질문과 대답](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-faq)
- [상태 및 작동 상태 스토리지 공간 다이렉트](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-states)
- [스토리지 공간 다이렉트를 사용 하 여 진단 데이터 수집](https://docs.microsoft.com/windows-server/storage/storage-spaces/data-collection)
- [Windows의 저장소 클래스 메모리 (NVDIMM-N) 상태 관리](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-class-memory-health)

## <a name="troubleshoot-sdn"></a>SDN 문제 해결

- [SDN 문제 해결](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-software-defined-networking)
- [Windows Server 소프트웨어 정의 네트워킹 스택 문제 해결](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)

## <a name="troubleshoot-rds-session-connectivity"></a>RDS 세션 연결 문제 해결

- [일반 원격 데스크톱 연결 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/rdp-error-general-troubleshooting)
- [클라이언트에서 연결할 수 없으며 클래스가 등록 되지 않음 오류가 발생 합니다.](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/rdp-error-class-not-registered)
- [클라이언트에서 연결할 수 없고 사용 가능한 라이선스 없음 오류가 표시 됩니다.](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/rdp-error-no-licenses-available)
- [사용자가 인증할 수 없거나 두 번 인증해야 함](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/cannot-authenticate-or-must-authenticate-twice)
- [연결할 때 사용자가 원격 데스크톱 서비스를 수신 합니다. 메시지는 현재 사용 중입니다.](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/remote-desktop-service-currently-busy)
- [원격 데스크톱 클라이언트의 연결이 끊어지고 동일한 세션에 다시 연결할 수 없음](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/rdp-client-disconnects-cannot-reconnect-same-session)
- [무선 네트워크에서 원격 랩톱 연결 끊김](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/remote-laptop-disconnects-wireless-network)
- [원격 데스크톱 연결 중 성능 저하 또는 애플리케이션 문제 발생](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/troubleshoot/poor-performance-or-application-problems)

## <a name="troubleshoot-shielded-vm"></a>차폐 VM 문제 해결

- [차폐 Vm 문제 해결](https://docs.microsoft.com/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-troubleshoot-shielded-vms)

## <a name="troubleshoot-software-restriction-policies"></a>소프트웨어 제한 정책 문제 해결

- [소프트웨어 제한 정책 문제 해결](https://docs.microsoft.com/windows-server/identity/software-restriction-policies/troubleshoot-software-restriction-policies)

## <a name="troubleshoot-storage-migration"></a>저장소 마이그레이션 문제 해결

- [저장소 마이그레이션 서비스의 알려진 문제](https://docs.microsoft.com/windows-server/storage/storage-migration-service/known-issues)
- [Storage Migration Service 질문과 대답 (FAQ)](https://docs.microsoft.com/windows-server/storage/storage-migration-service/faq)

## <a name="troubleshoot-storage-replica"></a>저장소 복제본 문제 해결

- [저장소 복제본의 알려진 문제](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-known-issues)
- [저장소 복제본에 대 한 질문과 대답](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-frequently-asked-questions)

## <a name="troubleshoot-user-profiles"></a>사용자 프로필 문제 해결

- [이벤트를 사용 하 여 사용자 프로필 문제 해결](https://docs.microsoft.com/windows-server/storage/folder-redirection/troubleshoot-user-profiles-events)

## <a name="troubleshoot-vrss"></a>VRSS 문제 해결

- [vRSS 질문과 대답](https://docs.microsoft.com/windows-server/networking/technologies/vrss/vrss-faq)

## <a name="troubleshoot-webproxy"></a>WebProxy 문제 해결

- [웹 애플리케이션 프록시 문제 해결](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/troubleshooting-web-application-proxy)

## <a name="troubleshoot-windows-admin-center"></a>Windows Admin Center 문제 해결

- [Windows 관리 센터 일반적인 문제 해결 단계](https://docs.microsoft.com/windows-server/manage/windows-admin-center/support/troubleshooting)
- [Windows 관리 센터의 알려진 문제](https://docs.microsoft.com/windows-server/manage/windows-admin-center/support/known-issues)
- [Windows 관리 센터 질문과 대답](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/faq)
