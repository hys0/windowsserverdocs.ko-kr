---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: Winlogon 자동 다시 시작 로그온 (ARSO)
description: Windows 자동 다시 시작 로그온을 통해 사용자의 생산성을 높일 수 있습니다.
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.reviewer: cahick
ms.date: 08/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 56f485491340b3974d8bf5ba697c6cf01f3e56ac
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868213"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon 자동 다시 시작 로그온 (ARSO)

Windows 업데이트 하는 동안 업데이트를 완료 하기 위해 수행 해야 하는 사용자별 프로세스가 있습니다. 이러한 프로세스를 수행 하려면 사용자가 장치에 로그인 해야 합니다. 업데이트가 시작 된 후 첫 번째 로그인에서 사용자가 장치 사용을 시작 하기 전에 이러한 사용자 특정 프로세스가 완료 될 때까지 기다려야 합니다.

## <a name="how-does-it-work"></a>어떤 방식으로 작동합니까?

Windows 업데이트 자동 재부팅을 시작 하는 경우 ARSO 현재 로그인 한 사용자의 파생 자격 증명을 추출 하 고, 디스크에 유지 하 고, 사용자에 대 한 자동 로그온을 구성 합니다. TCB 권한으로 시스템으로 실행 되는 Windows Update는이 작업을 수행 하는 RPC 호출을 시작 합니다.

최종 Windows 업데이트 다시 부팅 한 후 사용자는 자동 로그온 메커니즘을 통해 자동으로 로그인 되며 사용자의 세션은 지속형 암호와 함께 사용 됩니다. 또한 사용자의 세션을 보호 하기 위해 장치가 잠깁니다. 잠금은 Winlogon을 통해 시작 되지만 자격 증명 관리는 LSA (로컬 보안 기관)에 의해 수행 됩니다. 성공적으로 구성 되 고 로그인 되 면 저장 된 자격 증명이 디스크에서 즉시 삭제 됩니다.

콘솔에서 사용자를 자동으로 로그인 하 고 잠가 사용자가 장치에 반환 하기 전에 사용자 특정 프로세스를 완료할 수 Windows 업데이트. 이러한 방식으로 사용자는 장치를 사용 하 여 바로 시작할 수 있습니다.

ARSO는 관리 되지 않는 장치와 관리 되는 장치를 다르게 처리 합니다. 관리 되지 않는 장치의 경우 장치 암호화가 사용 되지만 사용자가 ARSO를 가져오는 데 필요 하지 않습니다. 관리 장치의 경우 ARSO에 TPM 2.0, SecureBoot 및 BitLocker가 필요 합니다. IT 관리자는 그룹 정책를 통해이 요구 사항을 재정의할 수 있습니다. 관리 장치에 대 한 ARSO는 현재 Azure Active Directory에 가입 된 장치에만 사용할 수 있습니다.

|   | Windows 업데이트| 종료-g-t 0  | 사용자가 시작한 다시 부팅 | SHUTDOWN_ARSO/EWX_ARSO 플래그를 사용 하는 Api |
| --- | :---: | :---: | :---: | :---: |
| 관리 되는 장치 | :heavy_check_mark:  | :heavy_check_mark: |   | :heavy_check_mark: |
| 관리 되지 않는 장치 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

> [!NOTE]
> 재부팅 Windows 업데이트 발생 한 후 마지막 대화형 사용자가 자동으로 로그인 되 고 세션이 잠깁니다. 이렇게 하면 Windows 업데이트 다시 부팅 하더라도 사용자의 잠금 화면 앱이 계속 실행 될 수 있습니다.

![설정 페이지](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/gtr-adds-lockscreenapp.png)

## <a name="policy-1"></a>정책 #1

### <a name="sign-in-and-lock-last-interactive-user-automatically-after-a-restart"></a>다시 시작한 후 로그인 하 고 마지막 대화형 사용자 자동 잠금

Windows 10에서는 서버 Sku에 대해 ARSO을 사용 하지 않도록 설정 하 고 클라이언트 Sku를 옵트아웃 합니다.

**그룹 정책 위치:** Windows 관리 템플릿 > 컴퓨터 구성 > windows 로그온 옵션 >

**Intune 정책:**

- Platform.string Windows 10 이상
- 프로필 유형: 관리 템플릿
- 경로: \Windows s 로그온 옵션

**지원 되는 위치:** Windows 10 버전 1903 이상

**설명:**

이 정책 설정은 시스템이 다시 시작 되거나 종료 및 콜드 부팅 후에 장치가 자동으로 로그인 하 고 마지막 대화형 사용자를 잠글지 여부를 제어 합니다.

이는 마지막 대화형 사용자가 다시 시작 하거나 종료 하기 전에 로그 아웃 하지 않은 경우에만 발생 합니다.

장치가 Active Directory 또는 Azure Active Directory에 가입 되어 있는 경우이 정책은 Windows 업데이트 다시 시작에만 적용 됩니다. 그렇지 않으면 Windows 업데이트 다시 시작 및 사용자가 시작한 다시 시작 및 종료 모두에 적용 됩니다.

이 정책 설정을 구성 하지 않으면 기본적으로 사용 하도록 설정 됩니다. 이 정책을 사용 하도록 설정 하면 사용자가 자동으로 로그인 되며 장치가 부팅 된 후 해당 사용자에 대해 구성 된 모든 잠금 화면 앱과 함께 세션이 자동으로 잠깁니다.

이 정책을 사용 하도록 설정한 후에는 다시 시작 또는 콜드 부팅 후에 자동으로 로그인 하 고 마지막 대화형 사용자를 잠그는 모드를 구성 하는 ConfigAutomaticRestartSignOn 정책을 통해 해당 설정을 구성할 수 있습니다.

이 정책 설정을 사용 하지 않도록 설정 하면 장치에서 자동 로그인을 구성 하지 않습니다. 사용자의 잠금 화면 앱은 시스템이 다시 시작 된 후 다시 시작 되지 않습니다.

**레지스트리 편집기:**

| 값 이름 | 형식 | data |
| --- | --- | --- |
| DisableAutomaticRestartSignOn | DWORD | 0 (ARSO를 사용 하도록 설정) |
|   |   | 1 (ARSO 사용 안 함) |

**정책 레지스트리 위치:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

**유형:** DWORD

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/gtr-adds-signinpolicy.png)

## <a name="policy-2"></a>정책 #2

### <a name="configure-the-mode-of-automatically-signing-in-and-locking-last-interactive-user-after-a-restart-or-cold-boot"></a>다시 시작 또는 콜드 부팅 후에 자동으로 로그인 하 고 마지막 대화형 사용자 잠금 모드 구성

**그룹 정책 위치:** Windows 관리 템플릿 > 컴퓨터 구성 > windows 로그온 옵션 >

**Intune 정책:**

- Platform.string Windows 10 이상
- 프로필 유형: 관리 템플릿
- 경로: \Windows s 로그온 옵션

**지원 되는 위치:** Windows 10 버전 1903 이상

**설명:**

이 정책 설정은 다시 시작 또는 콜드 부팅 후에 자동 다시 시작 및 로그온 및 잠금이 발생 하는 구성을 제어 합니다. "다시 시작 후 자동으로 로그인 및 마지막 대화형 사용자 잠금" 정책에서 "사용 안 함"을 선택한 경우에는 자동 로그온이 발생 하지 않으며이 정책을 구성할 필요가 없습니다.

이 정책 설정을 사용 하도록 설정 하는 경우 다음 두 가지 옵션 중 하나를 선택할 수 있습니다.

1. "BitLocker가 켜져 있고 일시 중단 되지 않는 경우 사용"은 BitLocker가 활성 상태이 고 다시 부팅 또는 종료 하는 동안 일시 중단 되지 않은 경우에만 자동 로그온 및 잠금이 발생 하도록 지정 합니다. 업데이트 중에 BitLocker가 켜져 있지 않거나 일시 중지 되지 않은 경우이 시점에서 장치의 하드 드라이브에 개인 데이터에 액세스할 수 있습니다. BitLocker 일시 중단은 시스템 구성 요소 및 데이터에 대 한 보호를 일시적으로 제거 하지만 부팅에 중요 한 구성 요소를 성공적으로 업데이트 하려면 특정 상황에서 필요할 수 있습니다.
   - 다음의 경우 업데이트 중 BitLocker가 일시 중단 됩니다.
      - 장치에 TPM 2.0 및 PCR7이 없습니다. 또는
      - 장치에서 TPM 전용 보호기를 사용 하지 않습니다.
2. "Always Enabled"는 다시 부팅 하거나 종료 하는 동안 BitLocker가 꺼져 있거나 일시 중단 된 경우에도 자동 로그인이 수행 되도록 지정 합니다. BitLocker를 사용 하지 않는 경우 하드 드라이브에서 개인 데이터에 액세스할 수 있습니다. 구성 된 장치가 안전한 물리적 위치에 있는 것으로 확신 하는 경우에만 자동 다시 시작 및 로그온이이 조건에서 실행 되어야 합니다.

이 설정을 사용 하지 않도록 설정 하거나 구성 하지 않으면 "BitLocker가 켜져 있고 일시 중단 되지 않은 경우" 동작이 자동으로 설정 됩니다.

**레지스트리 편집기**

| 값 이름 | 형식 | data |
| --- | --- | --- |
| AutomaticRestartSignOnConfig | DWORD | 0 (보안을 사용 하는 경우 ARSO 사용) |
|   |   | 1 (ARSO 항상 사용) |

**정책 레지스트리 위치:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

**유형:** DWORD

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/arso-policy-setting.png)

## <a name="troubleshooting"></a>문제 해결

WinLogon를 자동으로 잠그는 경우에 WinLogon의 상태 추적 WinLogon 이벤트 로그에 저장 됩니다.

자동 로그온 구성 시도의 상태는 기록

- 성공한 경우
   - 따라서 기록
- 실패 인 경우
   - 하면 오류를 기록 합니다.
- BitLocker의 상태가 변경 될 때:
   - 자격 증명 제거가 로깅됩니다.
   - LSA에 대 한 작업 로그에 저장 됩니다.

### <a name="reasons-why-autologon-might-fail"></a>자동 로그온 수 실패 하는 이유

자동 사용자 로그인 달성 되지 않을 수 없는 몇 가지 경우가 있습니다.  이 섹션은이 발생할 수 있는 알려진된 시나리오 캡처 위한 것입니다.

### <a name="user-must-change-password-at-next-login"></a>다음 로그인할 때 반드시 암호 변경

다음 로그인 시 암호 변경이 필요한 경우 사용자 로그인 차단 된 상태를 입력할 수 있습니다.  대부분의 경우에서 다시 시작 하기 전에 검색 된 전부는 아니지만이 수 있습니다 (예를 들어 암호 만료를 연결할 수 사이의 종료 및 다음 로그인 합니다.

### <a name="user-account-disabled"></a>사용자 계정 사용 안 함

사용 하지 않도록 설정 하는 경우에 기존 사용자 세션을 유지할 수 있습니다.  사용 하지 않도록 하는 계정에 대 한 다시 시작을 검색할 수 로컬로 대부분의 경우에서 사전에 따라 gp 도메인 계정 (일부 도메인 DC에서 계정이 비활성화 되어 있는 경우에 로그인 시나리오 작업 캐시)에 대 한 아닐 수 있습니다.

### <a name="logon-hours-and-parental-controls"></a>로그온 시간 및 자녀 보호

로그온 시간 및 자녀 보호 하지 못할 수 있습니다 새 사용자 세션이 만들어지지 않도록 합니다.  다시 시작이이 기간 동안 발생 한다면 사용자 하지 로그인 허용 됩니다.  잠금 또는 규정 준수 동작으로 로그 아웃 시키는 추가 정책이 있습니다. 자동 로그온 구성 시도의 상태가 기록 됩니다.

## <a name="security-details"></a>보안 정보

### <a name="credentials-stored"></a>자격 증명 저장

|   | 암호 해시 | 자격 증명 키 | 티켓 허용 티켓 | 기본 새로 고침 토큰 |
| --- | :---: | :---: | :---: | :---: |
| 로컬 계정 | :heavy_check_mark: | :heavy_check_mark: |   |   |
| MSA 계정 | :heavy_check_mark: | :heavy_check_mark: |   |   |
| Azure AD 조인 계정 | :heavy_check_mark: | :heavy_check_mark: | : heavy_check_mark: (하이브리드 인 경우) | :heavy_check_mark: |
| 도메인 가입 계정 | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | : heavy_check_mark: (하이브리드 인 경우) |

### <a name="credential-guard-interaction"></a>Credential Guard 상호 작용

장치에서 Credential Guard를 사용 하도록 설정한 경우 사용자의 파생 된 비밀은 현재 부팅 세션과 관련 된 키로 암호화 됩니다. 따라서 현재는 Credential Guard를 사용 하는 장치에서 ARSO가 지원 되지 않습니다.

## <a name="additional-resources"></a>추가 자료

자동 로그온은 Windows에 몇 가지 릴리스에 제공 된 기능입니다. Windows에 대 한 자동 로그온 [http:/sysinternals/bb963905](https://technet.microsoft.com/sysinternals/bb963905.aspx)와 같은 도구도 포함 된 windows의 문서화 된 기능입니다. 단일 사용자를 장치의 자격 증명을 입력 하지 않고 자동으로 로그인 할 수 있습니다. 자격 증명 구성 되 고 레지스트리에 암호화 된 LSA 암호로 저장 됩니다. 이 유지 관리 기간이이 시간 동안 일반적으로 경우에 특히 평판 시간 사이의 절전, 계정 잠금 발생할 수 있는 많은 자식 경우 문제가 될 수 있습니다.
