---
title: 사용자가 인증할 수 없거나 두 번 인증해야 함
description: 원격 데스크톱 연결을 시작할 때 사용자가 인증할 수 없거나 두 번 인증해야 하는 문제를 해결합니다.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8fd7cfda8814347f8bab9dc7b3f7632e3b992ecb
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857236"
---
# <a name="user-cant-authenticate-or-must-authenticate-twice"></a>사용자가 인증할 수 없거나 두 번 인증해야 함

이 문서에서는 사용자 인증에 영향을 주는 문제를 일으킬 수 있는 몇 가지 문제를 해결합니다.

## <a name="access-denied-restricted-type-of-logon"></a>액세스 거부됨, 제한된 로그온 유형

이 경우 Windows 10 또는 Windows Server 2016 컴퓨터에 연결하려고 시도하는 Windows 10 사용자는 다음 메시지와 함께 액세스가 거부됩니다.

> 원격 데스크톱 연결:  
> 시스템 관리자가 사용자가 사용할 수 있는 로그온 유형(네트워크 또는 대화형)을 제한했습니다. 도움이 필요한 경우 시스템 관리자 또는 기술 지원 팀에 문의하세요.

RDP 연결에 NLA(네트워크 수준 인증)가 필요하고 사용자가 **원격 데스크톱 사용자** 그룹의 구성원이 아닌 경우에 이 이슈가 발생합니다. **원격 데스크톱 사용자** 그룹이 **네트워크에서 이 컴퓨터 액세스** 사용자 권한에 할당되지 않은 경우에도 발생할 수 있습니다.

이 문제를 해결하려면 다음 작업 중 하나를 수행합니다.

  - [사용자의 그룹 멤버 자격 또는 사용자 권한 할당을 수정합니다](#modify-the-users-group-membership-or-user-rights-assignment).
  - NLA를 끕니다(권장하지 않음).
  - Windows 10이 아닌 다른 원격 데스크톱 클라이언트를 사용합니다. 예를 들어 Windows 7 클라이언트에서는 이 이슈가 발생하지 않습니다.

### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>사용자의 그룹 멤버 자격 또는 사용자 권한 할당 수정

이 이슈가 사용자 한 명에게만 영향을 주는 경우 가장 간단한 해결 방법은 **원격 데스크톱 사용자** 그룹에 해당 사용자를 추가하는 것입니다.

해당 사용자가 이미 이 그룹의 구성원인 경우(또는 여러 그룹 구성원에게 동일한 문제가 있는 경우) 원격 Windows 10 또는 Windows Server 2016 컴퓨터의 사용자 권한 구성을 확인합니다.

1. GPE(그룹 정책 개체 편집기)를 열고 원격 컴퓨터의 로컬 정책에 연결합니다.
2. **컴퓨터 구성\\Windows 설정\\보안 설정\\로컬 정책\\사용자 권한 할당**으로 이동하여 **네트워크에서 이 컴퓨터 액세스**를 마우스 오른쪽 단추로 클릭한 다음, **속성**을 선택합니다.
3. **원격 데스크톱 사용자**(또는 부모 그룹)의 사용자 및 그룹 목록을 확인합니다.
4. 목록에 **원격 데스크톱 사용자** 또는 부모 그룹(예: **모두**)이 없는 경우 목록에 이를 추가해야 합니다. 배포에 둘 이상의 컴퓨터가 있으면 그룹 정책 개체를 사용합니다.  
    예를 들어 **네트워크에서 이 컴퓨터 액세스**의 기본 구성원은 **모두**를 포함합니다. **모두**를 제거하기 위해 배포에서 그룹 정책 개체를 사용하는 경우 **원격 데스크톱 사용자**를 추가하도록 그룹 정책 개체를 업데이트하여 액세스를 복원해야 할 수도 있습니다.

## <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>액세스 거부됨, SAM 데이터베이스에 대한 원격 호출이 거부됨

이 동작은 도메인 컨트롤러가 Windows Server 2016 이상을 실행하고 사용자가 사용자 지정된 연결 앱을 사용하여 연결하려고 시도하는 경우에 발생할 가능성이 가장 높습니다. 특히, Active Directory에서 사용자의 프로필 정보에 액세스하는 애플리케이션은 액세스가 거부됩니다.

이 동작의 원인은 Windows 변경입니다. Windows Server 2012 R2 이하 버전에서 사용자가 원격 데스크톱에 로그인하면 RCM(원격 연결 관리자)에서 DC(도메인 컨트롤러)에 연결하여 AD DS(Active Directory Domain Services)의 사용자 개체에 대한 원격 데스크톱 관련 구성을 쿼리합니다. 이 정보는 Active Directory 사용자 및 컴퓨터 MMC 스냅인에서 사용자 개체 속성의 원격 데스크톱 서비스 프로필 탭에 표시됩니다.

Windows Server 2016부터 RCM은 더 이상 AD DS의 사용자 개체를 쿼리하지 않습니다. 원격 데스크톱 서비스 특성을 사용하고 있어 RCM에서 AD DS를 쿼리해야 하는 경우 쿼리를 사용하도록 수동으로 설정해야 합니다.

> [!IMPORTANT]  
> 이 섹션의 단계를 신중하게 따릅니다. 레지스트리를 잘못 수정할 경우 심각한 문제가 발생할 수 있습니다. 수정하기 전에, 문제가 발생할 경우를 대비하여 [복원을 위해 레지스트리를 백업](https://support.microsoft.com/help/322756)해 두세요.

RD 세션 호스트 서버에서 레거시 RCM 동작을 사용하려면 다음 레지스트리 항목을 구성하고 **원격 데스크톱 서비스**를 다시 시작합니다.  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Services**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation name\>\\**  
      - 이름: **fQueryUserConfigFromDC**
      - 다음을 입력합니다. **Reg\_DWORD**
      - 값: **1**(10진수)

RD 세션 호스트 서버가 아닌 다른 서버에서 레거시 RCM 동작을 사용하려면 다음 레지스트리 항목 및 추가 레지스트리 항목을 구성하고 서비스를 다시 시작합니다.
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

이 동작에 대한 자세한 내용은 KB 3200967 [Windows Server에서 원격 연결 관리자 변경](https://support.microsoft.com/help/3200967/changes-to-remote-connection-manager-in-windows-server)을 참조하세요.

## <a name="user-cant-sign-in-using-a-smart-card"></a>사용자가 스마트 카드를 사용하여 로그인할 수 없음

이 섹션에서는 사용자가 스마트 카드를 사용하여 원격 데스크톱에 로그인할 수 없는 세 가지 일반적인 시나리오를 다룹니다.

### <a name="cant-sign-in-with-a-smart-card-in-a-branch-office-with-a-read-only-domain-controller-rodc"></a>RODC(읽기 전용 도메인 컨트롤러)를 사용하는 지점에 스마트 카드로 로그인할 수 없음

이 이슈는 RODC를 사용하는 지사 사이트에 RDSH 서버가 있는 배포에서 발생합니다. RDSH 서버는 루트 도메인에 호스트됩니다. 지사 사이트의 사용자는 자식 도메인에 속하며, 스마트 카드를 사용하여 인증합니다. RODC는 사용자 암호를 캐시하도록 구성됩니다(RODC는 **허용된 RODC 암호 복제 그룹** 소속). 사용자가 RDSH 서버의 세션에 로그인하려고 시도하면 "시도한 로그온이 잘못되었습니다. 사용자 이름이 잘못되었거나 인증 정보가 잘못되었기 때문입니다"라는 내용의 메시지가 수신됩니다.

이 문제는 루트 DC 및 RDOC에서 사용자 자격 증명 암호화를 관리하는 방법으로 인해 발생합니다. 루트 DC는 암호화 키를 사용하여 자격 증명을 암호화하고, RODC는 클라이언트에 암호 해독 키를 제공합니다. 사용자가 "잘못됨" 오류를 받으면 두 키가 일치하지 않는다는 의미입니다.

이 문제를 해결하려면 다음 작업 중 하나를 수행합니다.

- RODC에서 암호 캐싱을 해제하여 DC 토폴로지를 변경하거나, 쓰기 가능한 DC를 지점 사이트에 배포합니다.
- RDSH 서버를 사용자와 동일한 자식 도메인으로 이동합니다.
- 사용자가 스마트 카드 없이 로그인할 수 있게 합니다.

이러한 모든 솔루션은 성능 또는 보안 수준에서 절충할 필요가 있습니다.

### <a name="user-cant-sign-in-to-a-windows-server-2008-sp2-computer-using-a-smart-card"></a>사용자가 스마트 카드를 사용하여 Windows Server 2008 SP2 컴퓨터에 로그인 할 수 없음

사용자가 KB4093227(2018.4B)로 업데이트된 Windows Server 2008 SP2 컴퓨터에 로그인하려고 시도하면 이 이슈가 발생합니다. 사용자가 스마트 카드를 사용하여 로그인하려고 시도하면 "올바른 인증서가 없습니다. 카드를 꽉 맞도록 올바르게 삽입했는지 확인합니다"라는 내용의 메시지와 함께 액세스가 거부됩니다. 그와 동시에, Windows Server 컴퓨터는 "삽입한 스마트 카드에서 디지털 인증서를 검색하는 동안 오류가 발생했습니다. 서명이 잘못되었습니다"라는 애플리케이션 이벤트를 기록합니다.

이 문제를 해결하려면 Windows Server 컴퓨터를 KB 4093227 [Windows Server 2008의 Windows RDP(원격 데스크톱 프로토콜) 서비스 거부 취약성에 대한 보안 업데이트 설명: 2018년 4월 10일](https://support.microsoft.com/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)의 2018.06 B 재릴리스로 업데이트합니다.

### <a name="cant-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>스마트 카드를 사용하여 로그인 상태를 유지할 수 없고 원격 데스크톱 서비스가 중지됨

사용자가 KB 4056446으로 업데이트된 Windows 또는 Windows Server 컴퓨터에 로그인하려고 시도하면 이 이슈가 발생합니다. 처음에는 사용자가 스마트 카드를 사용하여 시스템에 로그인할 수도 있지만, 그 후 "SCARD\_E\_NO\_SERVICE" 오류 메시지가 수신됩니다. 원격 컴퓨터가 응답하지 않을 수 있습니다.

이 이슈를 해결하려면 원격 컴퓨터를 다시 시작합니다.

이 이슈를 해결하려면 원격 컴퓨터를 적절한 픽스로 업데이트합니다.

  - Windows Server 2008 SP2: KB 4090928, [Windows의 lsm.exe 프로세스에서 핸들이 누수되어 스마트 카드 애플리케이션이 "SCARD\_E\_NO\_SERVICE" 오류를 표시할 수 있음](https://support.microsoft.com/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2: KB 4103724, [2018년 5월 17일 - KB4103724(월별 롤업 미리 보기)](https://support.microsoft.com/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 및 Windows 10 버전 1607: KB 4103720, [2018년 5월 17일 - KB4103720(OS 빌드 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)

## <a name="if-the-remote-pc-is-locked-the-user-needs-to-enter-a-password-twice"></a>원격 PC가 잠겨 있는 경우 사용자가 암호를 두 번 입력해야 함

이 문제는 사용자가 RDP 연결에 NLA가 필요하지 않은 배포에서 Windows 10 버전 1709를 실행하는 원격 데스크톱에 연결하려고 하면 발생할 수 있습니다. 이러한 상황에서 원격 데스크톱이 잠겨 있으면 연결 시 사용자가 자격 증명을 두 번 입력해야 합니다.

이 이슈를 해결하려면 Windows 10 버전 1709 컴퓨터를 KB 4343893 [2018년 8월 30일 - KB4343893(OS 빌드 16299.637)](https://support.microsoft.com/help/4343893/windows-10-update-kb4343893)으로 업데이트합니다.

## <a name="user-cant-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>사용자가 로그인할 수 없고 "인증 오류" 및 "CredSSP 암호화 오라클 수정" 메시지가 수신됨

사용자가 Windows Vista SP2 이상 또는 Windows Server 2008 SP2 이상 버전의 Windows 버전을 사용하여 로그인하려고 하면 액세스가 거부되고 다음과 같은 메시지를 받습니다.

```
An authentication error has occurred. The function requested is not supported.
...
This could be due to CredSSP encryption oracle remediation
...
```

"CredSSP 암호화 오라클 수정"은 2018년 3, 4, 5월에 출시된 보안 업데이트 세트를 말합니다. CredSSP는 다른 애플리케이션에 대한 인증 요청을 처리하는 인증 공급 기업입니다. 2018년 3월 13일 "3B" 및 후속 업데이트는 공격자가 사용자 자격 증명을 릴레이하여 대상 시스템에서 코드를 실행할 수 있는 악용을 해결합니다.

초기 업데이트에는 다음과 같은 설정이 가능한 새 그룹 정책 개체인 암호화 오라클 수정 지원이 추가되었습니다.

  - 취약: CredSSP를 사용하는 클라이언트 애플리케이션을 안전하지 않은 버전으로 대체할 수 있지만, 이 동작은 원격 데스크톱을 공격에 노출합니다. CredSSP를 사용하는 서비스는 업데이트되지 않은 클라이언트를 수락합니다.
  - 완화됨: CredSSP를 사용하는 클라이언트 애플리케이션은 안전하지 않은 버전으로 대체할 수 없지만, CredSSP를 사용하는 서비스는 업데이트되지 않은 클라이언트를 허용합니다.
  - 업데이트된 클라이언트 적용: CredSSP를 사용하는 클라이언트 애플리케이션은 안전하지 않은 버전으로 대체할 수 없으며, CredSSP를 사용하는 서비스는 패치되지 않은 클라이언트를 허용하지 않습니다. 
    > [!NOTE]
    > 모든 원격 호스트가 최신 버전을 지원하기 전에는 이 설정을 배포하면 안 됩니다.

2018년 5월 8일 업데이트에서는 기본 암호화 오라클 수정 설정이 취약에서 완화됨으로 변경되었습니다. 이 변경으로 인해 업데이트가 있는 원격 데스크톱 클라이언트는 업데이트가 없는 서버 또는 다시 시작되지 않은 업데이트된 서버에 연결할 수 없습니다. CredSSP 업데이트에 대한 자세한 내용은 [KB 4093492](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)를 참조하세요.

이 문제를 해결하려면 모든 시스템을 업데이트하고 다시 시작합니다. 업데이트 전체 목록 및 취약성에 대한 자세한 내용은 [CVE-2018-0886 | CredSSP 원격 코드 실행 취약성](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2018-0886)을 참조하세요.

업데이트가 완료될 때까지 이 이슈를 해결하려면 KB 4093492에서 허용되는 연결 유형을 확인합니다. 가능한 대안이 없는 경우 다음 방법 중 하나를 고려해 볼 수 있습니다.

- 영향을 받는 클라이언트 컴퓨터에서 암호화 오라클 수정 정책을 **취약**으로 다시 설정합니다.
- **컴퓨터 구성\\관리 템플릿\\Windows 구성 요소\\원격 데스크톱 서비스\\원격 데스크톱 세션 호스트\\보안** 그룹 정책 폴더에서 다음 정책을 수정합니다.  
  - **원격(RDP) 연결에 특정 보안 계층 사용**: **사용**으로 설정하고 **RDP**를 선택합니다.
  - **네트워크 수준 인증을 사용하여 원격 연결에 대한 사용자 인증**: **사용 안 함**으로 설정합니다.
    > [!IMPORTANT]  
    > 이러한 그룹 정책을 변경하면 배포의 보안이 저하됩니다. 일시적으로만 사용하는 것이 좋습니다.

그룹 정책 사용에 대한 자세한 내용은 [차단 GPO 수정](rdp-error-general-troubleshooting.md#modifying-a-blocking-gpo)을 참조하세요.

## <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>클라이언트 컴퓨터를 업데이트한 후 일부 사용자가 두 번 로그인해야 함

사용자가 Windows 7 또는 Windows 10 버전 1709를 실행하는 컴퓨터를 사용하여 원격 데스크톱에 로그인하는 즉시 두 번째 로그인 프롬프트가 표시됩니다. 이 문제는 클라이언트 컴퓨터에 다음과 같은 업데이트가 있는 경우에 발생합니다.

  - Windows 7: KB 4103718, [2018년 5월 8일 - KB4103718(월별 롤업)](https://support.microsoft.com/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727, [2018년 5월 8일 - KB4103727(OS 빌드 16299.431)](https://support.microsoft.com/help/4103727/windows-10-update-kb4103727)

이 이슈를 해결하려면 사용자가 연결하려는 컴퓨터(그리고 RDSH 또는 RDVI 서버)를 2018년 6월까지 완전히 업데이트해야 합니다. 여기에는 다음 업데이트가 포함됩니다.

  - Windows Server 2016: KB 4284880, [2018년 6월 12일 - KB4284880(OS 빌드 14393.2312)](https://support.microsoft.com/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2: KB 4284815, [2018년 6월 12일 - KB4284815(월별 롤업)](https://support.microsoft.com/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855, [2018년 6월 12일 - KB4284855(월별 롤업)](https://support.microsoft.com/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2: KB 4284826, [2018년 6월 12일 - KB4284826(월별 롤업)](https://support.microsoft.com/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Windows Server 2008, Windows Embedded POSReady 2009 및 Windows Embedded Standard 2009의 CredSSP 원격 코드 실행 취약성에 대한 보안 업데이트 설명: 2018년 3월 13일](https://support.microsoft.com/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

## <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>여러 RD 연결 브로커가 있는 원격 Credential Guard를 사용하는 배포에 대한 사용자 액세스가 거부됨

Windows Defender 원격 Credential Guard를 사용하는 경우 두 개 이상의 원격 데스크톱 연결 브로커를 사용하는 고가용성 배포에서 이 이슈가 발생합니다. 사용자는 원격 데스크톱에 로그인할 수 없습니다.

이 이슈는 원격 Credential Guard에서 인증에 Kerberos를 사용하고 NTLM을 제한하기 때문에 발생합니다. 그러나 부하 분산을 사용하는 고가용성 구성에서는 RD 연결 브로커에서 Kerberos 작업을 지원할 수 없습니다.

RD 연결 브로커의 부하가 분산되는 고가용성 구성을 사용해야 하는 경우 원격 Credential Guard를 사용하지 않도록 설정하여 이 이슈를 해결할 수 있습니다. Windows Defender 원격 Credential Guard를 관리하는 방법에 대한 자세한 내용은 [Windows Defender 원격 Credential Guard를 사용하여 원격 데스크톱 자격 증명 보호](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)를 참조하세요.
