---
title: 추가 LSA 보호 구성
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 038e7c2b-c032-491f-8727-6f3f01116ef9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: bd5863a46f77fd4ac53c8559ff17279271dc5c46
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849694"
---
# <a name="configuring-additional-lsa-protection"></a>추가 LSA 보호 구성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가를 위한 이 항목에서는 LSA(로컬 보안 기관) 프로세스에 대한 추가 보호를 구성하여 자격 증명을 손상시킬 수 있는 코드 삽입을 방지하는 방법에 대해 설명합니다.

LSASS(로컬 보안 기관 서버 서비스) 프로세스를 포함하는 LSA는 사용자의 로컬 및 원격 로그인에 대한 유효성을 검사하고 로컬 보안 정책을 적용합니다. Windows 8.1 운영 체제 메모리 읽기를 방지 하 고 보호 되지 않은 프로세스에 의해 코드 삽입을 위해 LSA에 대 한 추가 보호를 제공 합니다. 이로 인해 LSA에서 저장 및 관리하는 자격 증명에 대한 보안이 강화됩니다. LSA에 대 한 보호 된 프로세스 설정은 Windows 8.1 구성할 수 있습니다 하지만 Windows RT 8.1에서 구성할 수 없습니다. 이 설정을 보안 부팅과 함께 사용하면 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa 레지스트리 키를 사용 안 함으로 설정해도 적용되지 않으므로 추가 보호가 실현됩니다.

### <a name="protected-process-requirements-for-plug-ins-or-drivers"></a>플러그 인 또는 드라이버에 대한 보호된 프로세스 요구 사항
LSA 플러그 인 또는 드라이버에서 보호된 프로세스를 로드하려면 다음 조건을 충족해야 합니다.

1.  서명 확인

    보호 모드에서는 LSA로 로드되는 모든 플러그 인이 Microsoft 서명으로 디지털 서명되어야 합니다. 따라서 서명되지 않거나 Microsoft 서명이 아닌 다른 방식으로 서명된 플러그 인은 LSA로 로드되지 않습니다. 이러한 플러그 인에는 스마트 카드 드라이버, 암호화 플러그인, 암호 필터 등이 있습니다.

    스마트 카드 드라이버와 같은 드라이버인 LSA 플러그 인은 WHQL 인증을 사용하여 서명해야 합니다. 자세한 내용은 [WHQL 릴리스 서명](https://msdn.microsoft.com/library/windows/hardware/ff553976%28v=vs.85%29.aspx)합니다.

    WHQL 인증 프로세스가 없는 LSA 플러그 인은 [LSA에 대한 파일 서명 서비스](https://go.microsoft.com/fwlink/?LinkId=392590)를 사용하여 서명해야 합니다.

2.  Microsoft SDL(Security Development Lifecycle) 프로세스 지침 준수

    모든 플러그 인은 적용 가능한 SDL 프로세스 지침을 준수해야 합니다. 자세한 내용은 [Microsoft SDL(Security Development Lifecycle) 부록](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)을 참조하세요.

    플러그 인이 Microsoft 서명으로 올바르게 서명된 경우에도 SDL 프로세스를 준수하지 않으면 플러그 인이 로드되지 않을 수 있습니다.

#### <a name="recommended-practices"></a>권장 방법
기능을 광범위하게 배포하기 전에 다음 목록을 사용하여 LSA 보호가 사용되는지 철저하게 테스트합니다.

-   조직 내에서 사용 중인 모든 LSA 플러그 인 및 드라이버를 확인합니다. 
    여기에는 스마트 카드 드라이버 및 암호화 플러그 인과 같은 타사 드라이버 또는 플러그 인, 암호 필터나 암호 변경 알림을 적용하는 데 사용되는 내부에서 개발한 모든 소프트웨어가 포함됩니다.

-   플러그 인 로드 실패가 발생하지 않도록 모든 LSA 플러그 인이 Microsoft 인증서로 디지털 서명되어 있는지 확인합니다.

-   올바르게 서명된 모든 플러그 인을 LSA로 로드할 수 있으며 이러한 플러그 인이 정상적으로 작동하는지 확인합니다.

-   감사 로그를 사용하여 보호된 프로세스로 실행되지 않은 LSA 플러그 인 및 드라이버를 확인합니다.

#### <a name="limitations-introduced-with-enabled-lsa-protection"></a>설정 된 LSA 보호를 사용 하 여 도입 된 제한 사항

LSA 보호를 사용 하는 경우 LSA 플러그 인을 사용자 지정을 디버깅할 수 없습니다.
보호 된 프로세스 경우 LSASS에 디버거를 연결할 수 없습니다.
일반적으로 실행 중인 보호 된 프로세스를 디버깅 하려면 없는 지원 되는 방법이 있습니다.

## <a name="how-to-identify-lsa-plug-ins-and-drivers-that-fail-to-run-as-a-protected-process"></a>보호된 프로세스로 실행되지 않은 LSA 플러그 인 및 드라이버를 확인하는 방법
이 섹션에 설명된 이벤트는 응용 프로그램 및 서비스 로그\Microsoft\Windows\CodeIntegrity 아래의 작업 로그에 있습니다. 이러한 이벤트를 통해 서명 때문에 로드되지 않은 LSA 플러그 인 및 드라이버를 확인할 수 있습니다. 이러한 이벤트를 관리하려면 **wevtutil** 명령줄 도구를 사용하면 됩니다. 이 도구에 대한 자세한 내용은 [Wevtutil](../../administration/windows-commands/Wevtutil.md)을 참조하십시오.

### <a name="before-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>옵트인하기 전: lsass.exe를 통해 로드되는 플러그 인 및 드라이버를 확인하는 방법
감사 모드를 사용하여 LSA 보호 모드에서 로드되지 않는 LSA 플러그 인 및 드라이버를 확인할 수 있습니다. 감사 모드에서는 LSA 보호를 사용하는 경우 LSA로 로드되지 않는 모든 플러그 인 및 드라이버를 식별하는 이벤트 로그가 생성됩니다. 플러그 인 또는 드라이버를 차단하지 않고 메시지가 기록됩니다.

##### <a name="to-enable-the-audit-mode-for-lsassexe-on-a-single-computer-by-editing-the-registry"></a>레지스트리를 편집하여 단일 컴퓨터에서 Lsass.exe에 대한 감사 모드를 사용하도록 설정하려면

1.  레지스트리 편집기(RegEdit.exe)를 열고 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe에 있는 레지스트리 키로 이동합니다.

2.  레지스트리 키 값을 **AuditLevel=dword:00000008**로 설정합니다.

3.  컴퓨터를 다시 시작합니다.

이벤트 3065 및 이벤트 3066의 결과를 분석합니다.

그런 다음 이벤트 뷰어에서이 이벤트를 볼 수 있습니다. Microsoft Windows-Codeintegrity/작동 합니다.

-   **이벤트 3065**: 이 이벤트는 코드 무결성 확인에서 공유 섹션에 대한 보안 요구 사항을 충족하지 않는 특정 드라이버로 프로세스(일반적으로 lsass.exe)를 로드하려는 시도가 발견되었음을 기록합니다. 그러나 설정된 시스템 정책으로 인해 이미지는 로드가 허용됩니다.

-   **이벤트 3066**: 이 이벤트는 코드 무결성 확인에서 Microsoft 서명 수준 요구 사항을 충족하지 않는 특정 드라이버로 프로세스(일반적으로 lsass.exe)를 로드하려는 시도가 발견되었음을 기록합니다. 그러나 설정된 시스템 정책으로 인해 이미지는 로드가 허용됩니다.

> [!IMPORTANT]
> 이러한 작업 이벤트는 커널 디버거가 연결되고 시스템에서 사용되는 경우에는 생성되지 않습니다.
> 
> 플러그 인 또는 드라이버에 공유 섹션이 포함된 경우 이벤트 3066은 이벤트 3065와 함께 기록됩니다. 공유 섹션을 제거하면 플러그 인이 Microsoft 서명 수준 요구 사항을 충족하지 않는 경우를 제외하고는 두 이벤트 모두 발생하지 않습니다.

도메인의 여러 컴퓨터에 감사 모드를 사용하도록 설정하려면 그룹 정책 클라이언트 쪽 확장 레지스트리를 사용하여 Lsass.exe 감사 수준 레지스트리 값을 배포하면 됩니다. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe 레지스트리 키를 수정해야 합니다.

##### <a name="to-create-the-auditlevel-value-setting-in-a-gpo"></a>GPO에서 AuditLevel 값 설정을 만들려면

1.  GPMC(그룹 정책 관리 콘솔)를 엽니다.

2.  도메인 수준에서 연결되거나 컴퓨터 계정을 포함하는 조직 구성 단위에 연결된 새 GPO(그룹 정책 개체)를 만듭니다. 또는 이미 배포된 GPO를 선택할 수 있습니다.

3.  GPO를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 클릭하여 그룹 정책 관리 편집기를 엽니다.

4.  **컴퓨터 구성**, **기본 설정**, **Windows 설정**을 차례로 확장합니다.

5.  **레지스트리**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **레지스트리 항목**을 클릭합니다. **새 레지스트리 속성** 대화 상자가 나타납니다.

6.  **하이브** 목록에서 **HKEY_LOCAL_MACHINE.** 을 클릭합니다.

7.  **키 경로** 목록에서 **SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe**를 찾습니다.

8.  **값 이름** 상자에 **AuditLevel**을 입력합니다.

9. **값 종류** 상자에서 **REG_DWORD**를 클릭하여 선택합니다.

10. 에 **값 데이터** 상자에 입력 **00000008**합니다.

11. **확인**을 클릭합니다.

> [!NOTE]
> GPO를 적용하려면 도메인의 모든 도메인 컨트롤러에 GPO 변경 내용을 복제해야 합니다.

여러 컴퓨터에서 추가 LSA 보호를 옵트인하려면 그룹 정책 클라이언트 쪽 확장 레지스트리를 사용하여 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa를 수정합니다. 이 작업을 수행하는 방법에 대한 자세한 단계는 이 항목의 [자격 증명에 대한 추가 LSA 보호를 구성하는 방법](#BKMK_HowToConfigure)을 참조하십시오.

### <a name="after-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>옵트인한 후: lsass.exe를 통해 로드되는 플러그 인 및 드라이버를 확인하는 방법
이벤트 로그를 사용하여 LSA 보호 모드에서 로드하지 못한 LSA 플러그 인 및 드라이버를 확인할 수 있습니다. LSA 보호 프로세스를 사용하는 경우 LSA로 로드하지 못한 모든 플러그 인 및 드라이버를 식별하는 이벤트 로그가 생성됩니다.

이벤트 3033 및 이벤트 3063의 결과를 분석합니다.

그런 다음 이벤트 뷰어에서이 이벤트를 볼 수 있습니다. Microsoft Windows-Codeintegrity/작동 합니다.

-   **이벤트 3033**: 이 이벤트는 코드 무결성 확인에서 Microsoft 서명 수준 요구 사항을 충족하지 않는 드라이버로 프로세스(일반적으로 lsass.exe)를 로드하려는 시도가 발견되었음을 기록합니다.

-   **이벤트 3063**: 이 이벤트는 코드 무결성 확인에서 공유 섹션에 대한 보안 요구 사항을 충족하지 않는 드라이버로 프로세스(일반적으로 lsass.exe)를 로드하려는 시도가 발견되었음을 기록합니다.

공유 섹션은 일반적으로 인스턴스 데이터가 같은 보안 컨텍스트를 사용하는 다른 프로세스와 상호 작용하도록 허용하는 프로그래밍 방법으로 인해 생성됩니다. 이로 인해 보안 취약점이 발생할 수 있습니다.

## <a name="BKMK_HowToConfigure"></a>자격 증명 추가 LSA 보호를 구성 하는 방법
(보안 부팅 또는 UEFI 없이 또는) Windows 8.1 실행 하는 장치에서 구성이 불가능이 섹션에 설명 된 절차를 수행 하 여 합니다. Windows RT 8.1을 실행 하는 장치의 경우 lsass.exe 보호가 항상 사용 하도록 설정 및 해제할 수 없습니다.

### <a name="on-x86-based-or-x64-based-devices-using-secure-boot-and-uefi-or-not"></a>보안 부팅 및 UEFI를 사용하거나 사용하지 않는 x86 기반 또는 x64 기반 장치
보안 부팅 및 UEFI를 사용하는 x86 기반 또는 x64 기반 장치에서는 LSA 보호가 레지스트리 키를 사용하여 설정될 때 UEFI 변수가 UEFI 펌웨어에 설정됩니다. 이 설정이 펌웨어에 저장되면 레지스트리 키에서 UEFI 변수를 삭제하거나 변경할 수 없습니다. UEFI 변수를 다시 설정해야 합니다.

UEFI를 지원하지 않거나 보안 부팅을 사용하지 않는 x86 기반 또는 x64 기반 장치는 LSA 보호 구성을 펌웨어에 저장할 수 없으며 레지스트리 키의 존재 여부만을 기반으로 합니다. 이 시나리오에서는 장치에 대한 원격 액세스를 사용하여 LSA 보호를 사용하지 않도록 설정할 수 있습니다.

다음 절차를 사용하여 LSA 보호를 사용하거나 사용하지 않도록 설정할 수 있습니다.

##### <a name="to-enable-lsa-protection-on-a-single-computer"></a>단일 컴퓨터에서 LSA 보호를 사용하도록 설정하려면

1.  레지스트리 편집기(RegEdit.exe)를 열고 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa에 있는 레지스트리 키를 찾습니다.

2.  레지스트리 키 값을 "RunAsPPL"=dword:00000001 값을 삭제합니다.

3.  컴퓨터를 다시 시작합니다.

##### <a name="to-enable-lsa-protection-using-group-policy"></a>그룹 정책을 사용하여 LSA 보호를 사용하도록 설정하려면

1.  GPMC(그룹 정책 관리 콘솔)를 엽니다.

2.  도메인 수준에서 연결되거나 컴퓨터 계정을 포함하는 조직 구성 단위에 연결된 새 GPO를 만듭니다. 또는 이미 배포된 GPO를 선택할 수 있습니다.

3.  GPO를 마우스 오른쪽 단추로 클릭한 다음 **편집** 을 클릭하여 그룹 정책 관리 편집기를 엽니다.

4.  **컴퓨터 구성**, **기본 설정**, **Windows 설정**을 차례로 확장합니다.

5.  **레지스트리**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 가리킨 다음 **레지스트리 항목**을 클릭합니다. **새 레지스트리 속성** 대화 상자가 나타납니다.

6.  **하이브** 목록에서 **HKEY_LOCAL_MACHINE**을 클릭합니다.

7.  **키 경로** 목록에서 **SYSTEM\CurrentControlSet\Control\Lsa**를 찾습니다.

8.  **값 이름** 상자에 **RunAsPPL**을 입력합니다.

9. **값 종류** 상자에서 **REG_DWORD**를 클릭합니다.

10. **값 데이터** 상자에 **00000001**을 입력합니다.

11. **확인**을 클릭합니다.

##### <a name="to-disable-lsa-protection"></a>LSA 보호를 사용하지 않도록 설정하려면

1.  레지스트리 편집기(RegEdit.exe)를 열고 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa에 있는 레지스트리 키를 찾습니다.

2.  레지스트리 키에서 "RunAsPPL"=dword:00000001 값을 삭제합니다.

3.  장치에서 보안 부팅을 사용하는 경우 LSA(로컬 보안 기관) 보호된 프로세스 옵트아웃 도구를 사용하여 UEFI 변수를 삭제합니다.

    옵트아웃 도구에 대한 자세한 내용은 [공식 Microsoft 다운로드 센터에서 LSA(로컬 보안 기관) 보호된 프로세스 옵트아웃 다운로드](https://www.microsoft.com/download/details.aspx?id=40897)를 참조하세요.

    보안 부팅을 관리하는 방법에 대한 자세한 내용은 [UEFI 펌웨어](https://technet.microsoft.com/library/hh824898.aspx)를 참조하세요.

    > [!WARNING]
    > 보안 부팅을 해제하면 모든 보안 부팅 및 UEFI 관련 구성이 다시 설정됩니다. 따라서 LSA 보호를 사용하지 않도록 설정하는 다른 모든 방법이 실패한 경우에만 보안 부팅을 해제해야 합니다.

### <a name="verifying-lsa-protection"></a>LSA 보호 확인
Windows를 시작할 때 LSA가 보호 모드로 시작되었는지 확인하려면 **Windows 로그** 아래의 **시스템** 로그에서 다음 WinInit 이벤트를 검색합니다.

-   12: LSASS.exe가 다음 수준의 보호된 프로세스로 시작되었습니다. 4

## <a name="additional-resources"></a>추가 자료
[자격 증명 보호 및 관리](credentials-protection-and-management.md)

[파일 서명 LSA에 대 한 서비스](https://go.microsoft.com/fwlink/?LinkId=392590)


