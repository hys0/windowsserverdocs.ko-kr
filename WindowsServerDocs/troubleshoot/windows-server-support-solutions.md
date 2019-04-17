---
title: "Windows Server를 위한 상위 지원 솔루션"
description: "Windows Server 문제에 대한 해결 방법에 대한 링크 가져오기"
ms.prod: windows-server-threshold
ms.service: na
manager: alant
ms.technology: server-general
ms.date: 09/06/2017
ms.topic: article
author: kaushika-msft
ms.author: elizapo
ms.openlocfilehash: 070331c8886011035e712f485af45d36b77613fa
ms.sourcegitcommit: 58dde3f9ae761116b2c9f71c6917f96bff075af1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2017
---
# <a name="top-support-solutions-for-windows-server-2016"></a>Windows Server 2016을 위한 상위 지원 솔루션

Microsoft는 Windows Server에 대한 업데이트 및 솔루션을 정기적으로 릴리스합니다. 서버가 보안 업데이트를 포함한 향후 업데이트를 받을 수 있도록 업데이트된 상태로 유지해야 합니다. 릴리스된 업데이트의 전체 목록은 [Windows 10 및 Windows Server 2016 업데이트 기록](https://support.microsoft.com/en-us/help/4000825/windows-10-windows-server-2016-update-history)을 확인하세요.

Windows Server 2016을 사용할 때 경험하는 가장 일반적인 문제에 대한 최고의 Microsoft 지원 해결 방법입니다. 아래 링크는 참조 자료 문서, 업데이트 및 라이브러리 문서에 대한 링크를 포함합니다.

## <a name="solutions-for-installing-or-upgrading-windows-server"></a>Windows Server 설치 또는 업그레이드 솔루션

- [Windows 10 업그레이드 오류 해결: IT 전문가용 기술 정보](\windows\deployment\upgrade\resolve-windows-10-upgrade-errors)
- [Windows 10 버전 1607 및 Windows Server 2016용 스택 업데이트 서비스: 2017년 8월 8일](https://support.microsoft.com/en-US/help/4035631)
- [Windows 10 버전 1607 및 Windows Server 2016 업그레이드를 위한 호환성 업데이트: 2017년 8월 3일](https://support.microsoft.com/en-US/help/4033524)
- [Windows 기반 Azure VM에서 전체 시스템 업그레이드가 지원되지 않습니다.](https://support.microsoft.com/en-US/help/4014997)
- [Windows Server 2016에 대한 업그레이드 및 변환 옵션](..\get-started\supported-upgrade-paths.md)
- [Windows Server 2016에 대한 서버 역할 업그레이드 및 마이그레이션 매트릭스](..\get-started\server-role-upgradeability-table.md)
- [Windows Server 설치 및 업그레이드](..\get-started\installation-and-upgrade.md)
- [릴리스 정보: Windows Server 2016의 주요 문제점](..\get-started\windows-server-2016-ga-release-notes.md)
- [WindowsServer 2016 전환 권장 사항](..\get-started\recommendations-moving-to-server2016.md)

## <a name="solutions-for-volume-activation"></a>볼륨 정품 인증 솔루션
- [Windows Server 2016 정품 인증](../get-started/server-2016-activation.md)
- [정품 인증 방법 확인 및 선택](https://technet.microsoft.com/library/jj134256(ws.11).aspx)
- [볼륨 정품 인증에 대한 정품 인증 오류 코드](https://technet.microsoft.com/library/dn502528.aspx)
- [KMS(키 관리 서비스) 문제 해결 방법](https://technet.microsoft.com/library/ee939272.aspx)
- [볼륨 정품 문제 해결](https://technet.microsoft.com/library/ff793439.aspx)
- [정품 인증 오류 코드](https://technet.microsoft.com/library/ff793399.aspx)
- [Windows 설치가 다음 오류 메시지와 함께 실패할 수 있습니다. "입력한 제품 키가 설치 가능한 Windows 이미지와 일치하지 않습니다. 다른 제품 키를 입력하세요."](https://support.microsoft.com/help/2796988/windows-8-or-windows-server-2012-installation-may-fail-with-error-mess)

## <a name="solutions-related-to-dcpromo-and-installing-domain-controllers"></a>DCPromo 및 도메인 컨트롤러 설치 관련 해결 방법
- [Active Directory 및 Active Directory Domain Services 포트 요구 사항](https://technet.microsoft.com/library/dd772723(v=ws.10).aspx)
- [Active Directory 방화벽 포트 – 간단한 사용](http://blogs.msmvps.com/acefekay/2011/11/01/active-directory-firewall-ports-let-s-try-to-make-this-simple/)
- [Windows Server 2016에 대한 Exchange Server 지원](https://technet.microsoft.com/library/ff728623(v=exchg.150).aspx)
- [Ntdsutil.exe를 사용하여 FSMO 역할을 점유하거나 도메인 컨트롤러에 전송](http://support.microsoft.com/kb/255504)
- [도메인 컨트롤러 배포 문제 해결](../identity/ad-ds/deploy/troubleshooting-domain-controller-deployment.md)
- [Active Directory 설치 마법사 문제 해결](https://msdn.microsoft.com/library/bb727058.aspx)
- [AD DS 설치 및 제거 관련 알려진 문제](https://technet.microsoft.com/library/cc754463(v=ws.10).aspx)

## <a name="solutions-for-active-directory-federation-services-ad-fs"></a>AD FS(Active Directory Federation Services)에 대한 해결 방법
- [Azure Active Directory를 통한 Windows 도메인 가입 장치 자동 등록 구성 방법](/azure/active-directory/active-directory-conditional-access-automatic-device-registration-setup)
- [클레임 발급 설정](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup#step-2-setup-issuance-of-claims)
- [LDAP 디렉터리에 저장된 사용자를 인증하도록 AD FS 구성](../identity/ad-fs/operations/configure-ad-fs-to-authenticate-users-stored-in-ldap-directories.md)
- [인증서 인증을 위한 대체 호스트 이름 바인딩에 대한 AD FS 지원](../identity/ad-fs/operations/ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [암호 공격으로부터 보호](https://blogs.technet.microsoft.com/tspring/2017/01/20/federated-to-microsoft-cloud-and-account-lockouts/)
- [WID 데이터베이스를 사용하여 Windows Server 2016에서 AD FS로 업그레이드](../identity/ad-fs/deployment/upgrading-to-ad-fs-in-windows-server-2016.md)
- [Windows 10 로그온 - AD FS로 장치 인증 사용 설정](../identity/ad-fs/operations/configure-device-based-conditional-access-on-premises.md)
- [Windows Server 2016의 AD FS 및 WAP의 SSL 인증서 관리](../identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap-2016.md)
- [Windows Server 2016 AD FS의 액세스 제어 정책](../identity/ad-fs/operations/access-control-policies-in-ad-fs.md)

## <a name="solutions-related-to-active-directory-replication"></a>Active Directory 복제 관련 해결 방법

- [Active Directory 복제 문제 해결](../identity/ad-ds/manage/troubleshoot/troubleshooting-active-directory-replication-problems.md)
- [Microsoft 다운로드 센터에서 Active Directory 복제 상태 도구 다운로드](http://www.microsoft.com/en-in/download/details.aspx?id=30005)
- [e2e: 일반 Active Directory 복제 오류 문제 해결 방법](http://support.microsoft.com/kb/3108513)
- [AD 복제 오류 8606 문제 해결: 개체를 만들기 위해 충분한 특성이 지정되지 않음](http://support.microsoft.com/kb/2028495)
- [Windows 2000 Server 및 Windows Server 2003 Active Directory의 인바운드 복제 도중 이벤트 ID 2108 및 이벤트 ID 1084가 발생](http://support.microsoft.com/kb/837932)
- [AD 복제 오류 8451 문제 해결: 복제 연산에 데이터베이스 오류가 발생함](http://support.microsoft.com/kb/2645996)
- [AD 복제 오류 1127 문제 해결: 하드 디스크에 액세스하는 동안 다시 시도 후에도 디스크 작업에 실패함](http://support.microsoft.com/kb/2025726)
- [서버 메타 데이터 정리](https://technet.microsoft.com/en-us/library/cc816907.aspx)