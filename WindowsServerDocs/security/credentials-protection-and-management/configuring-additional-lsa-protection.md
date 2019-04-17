---
title: "추가 LSA 보호 구성"
description: "Windows Server 보안"
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
ms.openlocfilehash: fcfb0dab10d28413cf4ad06dd583274f217c91fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-additional-lsa-protection"></a>추가 LSA 보호 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목 IT 전문가 위한 자격 증명을 손상 시킬 수 있는 코드 삽입 방지 LSA 로컬 보안 기관을 () 프로세스에 대 한 추가 보호 기능을 구성 하는 방법을 설명 합니다.

LSA 로컬 보안 기관을 서버 (LSASS 서비스) 과정을 포함 하는 지역 및 원격 기호 기능에 대 한 사용자의 유효성을 검사 하 고 로컬 보안 정책이 적용 됩니다. Windows 8.1 운영 체제 LSA 읽기 메모리를 방지 하 고 프로세스 보호 되지 않은 삽입 코드에 추가 보호를 제공 합니다. 더 나은 보안 LSA 저장 하 고 관리 자격 증명을 제공 합니다. .1, Windows 8에서에서 LSA에 대 한 보호 프로세스 설정을 구성할 수 있지만 Windows RT 8.1에에서 구성할 수 없습니다. 이 설정을 보안 부팅와 함께에서 사용 하면 아무 효과가 찾아 레지스트리 키를 사용 하지 않도록 설정 때문에 추가 보호를 제공 합니다.

### <a name="protected-process-requirements-for-plug-ins-or-drivers"></a>플러그 인 또는 드라이버에 대 한 보호 프로세스 요구 사항
성공적으로 로드으로 보호 된 프로세스를 LSA 플러그 인 또는 드라이버를 것은 다음 조건을 충족 해야 합니다.

1.  서명 확인

    보호 모드는 LSA에 로드 되는 모든 플러그 인이 디지털 서명으로 서명 Microsoft 필요 합니다. 따라서 모든 플러그 인 서명 되지 않은 또는 Microsoft 서명으로 서명 되지 않은 LSA에 로드 되지 것입니다. 이러한 플러그 인의 예로 스마트 카드 드라이버, 암호화 플러그 인 및 암호 필터 합니다.

    LSA 플러그 인 스마트 카드 드라이버 등의 드라이버는 WHQL 인증서를 사용 하 여 로그인 해야 합니다. 자세한 내용은 참조 [WHQL 릴리스 서명 (Windows 드라이버)](https://msdn.microsoft.com/library/windows/hardware/ff553976%28v=vs.85%29.aspx)합니다.

    LSA 플러그 인 WHQL 인증 프로세스를 설치 하지 않은 사용 하 여 로그인 해야는 [LSA에 대 한 서비스에 로그인 하는 파일](https://go.microsoft.com/fwlink/?LinkId=392590)합니다.

2.  Microsoft SDL(Security Development Lifecycle) 프로세스 지침에 따른 이러한 준수

    모든 플러그 인 해당 SDL 프로세스 지침을 따라야 합니다. 자세한 내용은 참조는 [Microsoft SDL(Security Development Lifecycle) 부록](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx)합니다.

    플러그 인 Microsoft 서명으로 서명 제대로, 플러그 인을 로드 하는 오류 SDL 프로세스 준수 비 될 수 있습니다.

#### <a name="recommended-practices"></a>권장 되는 방법
다음 목록 철저 하 게 테스트 해당 LSA 방지를 사용할 광범위 하 게이 기능을 배포 하기 전에:

-   모든 LSA 플러그 인 및 조직 내에 사용 하에서는 드라이버를 확인 합니다. 
    암호 변경 알림을 또는 암호 필터를 적용 하기 위해 사용 되는 소프트웨어를 내부적으로 개발 된 및 Microsoft가 아닌 타사 드라이버 또는 스마트 카드 드라이버 등 플러그 인 및 암호화 플러그 인이 포함 됩니다.

-   모두 LSA 플러그 인 디지털 서명 되었는지 확인 Microsoft 인증서 플러그 인 하지 못합니다 로드 하 않도록 합니다.

-   모든 올바르게 서명된 플러그 인 LSA에 성공적으로 로드 수 있고 예상 대로 작동 하는지 확인 합니다.

-   감사 로그 LSA 플러그 인 및 보호 된 프로세스도 실행 되지 않는 드라이버를 식별 하기 위해 사용 합니다.

## <a name="how-to-identify-lsa-plug-ins-and-drivers-that-fail-to-run-as-a-protected-process"></a>LSA 플러그 인 및 보호 된 프로세스도 실행 되지 않는 드라이버를 식별 하는 방법
이 섹션에 설명 된 이벤트의 운영에 있는 응용 프로그램 및 서비스 Logs\Microsoft\Windows\CodeIntegrity 로그 합니다. 자녀가 LSA 플러그 인 및 로드 로그인 하는 이유 때문에 실패 하는 드라이버를 식별 하는 데 도움이 됩니다. 이러한 이벤트를 관리 하기 위해 사용할 수 있는 **wevtutil** 명령줄 도구입니다. 이 도구에 대 한 정보를 참조 하세요. [Wevtutil](../../administration/windows-commands/Wevtutil.md)합니다.

### <a name="before-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>옵트인 하기 전에: 플러그 인 및 lsass.exe 로드 드라이버를 식별 하는 방법
LSA 플러그 인 및 LSA 보호 모드에 로드 되지 드라이버를 식별 하는 감사 모드를 사용할 수 있습니다. 감사 모드에서는 시스템 모든 플러그 인 및 LSA 방지 기능을 사용 하는 경우 아래 LSA 로드 되지 드라이버 식별 이벤트 로그 생성 됩니다. 메시지는 플러그 인 또는 드라이버를 차단 하지 않고 기록 됩니다.

##### <a name="to-enable-the-audit-mode-for-lsassexe-on-a-single-computer-by-editing-the-registry"></a>레지스트리 편집 하 여 한 컴퓨터에서 Lsass.exe에 대 한 감사 모드 사용 하려면

1.  레지스트리 편집기 (RegEdit.exe) 열고에 있는 레지스트리 키로 이동: Windows NT HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ \CurrentVersion\Image File Execution Options\LSASS.exe 합니다.

2.  레지스트리 키를 값 설정 **AuditLevel dword:00000008 =**합니다.

3.  컴퓨터를 다시 시작 합니다.

결과 3065 이벤트 및 3066 이벤트를 분석 합니다.

-   **이벤트 3065**:이 이벤트 코드 무결성 확인 프로세스 (일반적으로 lsass.exe) 섹션 공유에 대 한 보안 요구 사항을 충족 하지 있는 특정 드라이버를 로드 하려고 결정을 기록 합니다. 그러나 설정 되어 있는 시스템 정책으로 인해 이미지를 로드할 수 했습니다.

-   **이벤트 3066**:이 이벤트 코드 무결성 확인 프로세스 (일반적으로 lsass.exe) 시도 수준 요구 사항을 로그인 하는 Microsoft에 맞지 않는 특정 드라이버를 로드 결정을 기록 합니다. 그러나 설정 되어 있는 시스템 정책으로 인해 이미지를 로드할 수 했습니다.

> [!IMPORTANT]
> 커널 디버거를 연결 하 고 시스템에서 사용이 작동 이벤트 생성 되지 않습니다.
> 
> 플러그 인 경우 또는 드라이버 공유 섹션에 포함 되어, 이벤트 3066 이벤트 3065 기록 됩니다. 공유 섹션을 제거 해야 두 이벤트에서 발생 하지 않도록 플러그 인 준수 하지 않는 Microsoft 서명 수준 필요 하지 않은 합니다.

도메인에 있는 여러 대의 컴퓨터에 대 한 감사 모드를 사용 하려면 Lsass.exe 감사 수준 레지스트리 값 배포 하는 그룹 정책에 대 한 클라이언트 측 레지스트리 확장을 사용할 수 있습니다. HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ Windows NT \CurrentVersion\Image File Execution Options\LSASS.exe 레지스트리 키 수정 해야 합니다.

##### <a name="to-create-the-auditlevel-value-setting-in-a-gpo"></a>Gpo에서 AuditLevel 값 설정을 만들려면

1.  그룹 정책 관리 콘솔 GPMC ()을 엽니다.

2.  만들기 그룹 정책 개체 () 도메인 수준에서 연결 되어 있는 또는 컴퓨터 계정을 포함 하 고 조직에 연결 되어 있는 합니다. 또는 GPO 이미 배포를 선택할 수 있습니다.

3.  GPO을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **편집** 그룹 정책 관리 편집기를 열 수 있습니다.

4.  확장 **컴퓨터 구성**, 확장 **기본**, 다음를 확장 하 고 **Windows 설정**합니다.

5.  마우스 오른쪽 단추로 클릭 **레지스트리**를 가리킨 **새로**을 차례로 클릭 하 고 **레지스트리 항목이**합니다. **새 레지스트리 속성** 대화 상자가 나타납니다.

6.  에 **하이브** 목록에서 클릭 **HKEY_LOCAL_MACHINE 합니다.**

7.  에 **키 경로** 목록, 찾아보기 **SOFTWARE\Microsoft\ Windows NT \CurrentVersion\Image File Execution Options\LSASS.exe**합니다.

8.  에 **값 이름** 상자에 입력 **AuditLevel**합니다.

9. 에 **값 형식** 상자를 선택 하 고 **REG_DWORD**합니다.

10. 에 **값 데이터** 상자에 입력 **00000008**합니다.

11. 클릭 **확인**합니다.

> [!NOTE]
> Gpo 적용, GPO 변경 도메인에 있는 모든 도메인 컨트롤러에 복제 해야 합니다.

에 참여 하는 여러 대의 컴퓨터에 추가 LSA 보호 하기 위해, 그룹 정책에 대 한 레지스트리 클라이언트 확장 찾아 수정 하 여 사용할 수 있습니다. 이 작업을 수행 하는 방법에 대 한 단계를 참조 하세요. [자격 증명 추가 LSA 보호 기능을 구성 하는 방법을](#BKMK_HowToConfigure) 이 항목의 합니다.

### <a name="after-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>옵트인 후: 플러그 인 및 lsass.exe 로드 드라이버를 식별 하는 방법
LSA 플러그 인 및 LSA 보호 모드를 로드 하지 못했습니다 드라이버를 식별 하는 이벤트 로그를 사용할 수 있습니다. 보호 LSA 프로세스를 사용 하도록 설정의 모든 플러그 인 및 LSA 아래를 로드 하지 못했습니다 드라이버를 식별 하는 이벤트 로그 생성 됩니다.

이벤트 3033 및 이벤트 3063 결과 분석 합니다.

-   **이벤트 3033**:이 이벤트 코드 무결성 확인 프로세스 (일반적으로 lsass.exe) 시도 수준 요구 사항을 로그인 하는 Microsoft에 맞지 않는 드라이버를 로드 결정을 기록 합니다.

-   **이벤트 3063**:이 이벤트 코드 무결성 확인 프로세스 (일반적으로 lsass.exe) 섹션 공유에 대 한 보안 요구 사항을 충족 하지 않는 드라이버를 로드 하려고 결정을 기록 합니다.

공유 섹션은 일반적으로 인스턴스 같은 보안 컨텍스트를 사용 하는 다른 프로세스와 상호 작용 하는 데이터를 사용할 수 있는 프로그래밍 기술 결과입니다. 이 보안 취약성 만들 수 있습니다.

## <a name="BKMK_HowToConfigure"></a>자격 증명 추가 LSA 보호 기능을 구성 하는 방법
(와 또는 보안 부팅 또는 UEFI 제외).1 Windows 8을 실행 하는 디바이스,이 섹션에 설명 된 절차를 수행 하 여 구성 수는 있습니다. Windows RT 8.1을 실행 하는 디바이스에 대 한 lsass.exe 보호 기능을 설정한 항상 하 고 해제할 수 없습니다.

### <a name="on-x86-based-or-x64-based-devices-using-secure-boot-and-uefi-or-not"></a>X86 기반 x64 기반 또는 디바이스에서 사용 하 여 보안 부팅 하 고 UEFI 여부
보안 부팅 하 고 UEFI를 사용 하는 x86 기반 x64 기반 또는 디바이스에서 UEFI 변수 LSA 보호 레지스트리 키를 사용 하 여 사용 하는 경우의 UEFI 펌웨어에서 설정 됩니다. 펌웨어에 설정이 저장 되어, 경우 UEFI 변수 삭제 하거나 레지스트리 키에서 변경할 수 없습니다. UEFI 변수 다시 설정 해야 합니다.

x86 기반 x64 기반 또는 장치 UEFI 또는 보안 부팅을 지원 하지 않는 비활성화 되어 LSA 보호를 위해 구성 펌웨어에 저장 하 고 레지스트리 키 있는지 여부에만 의존 수 없습니다. 이 경우에 디바이스에 대 한 원격 액세스를 사용 하 여 LSA 보호 기능을 해제 하려면 같습니다.

다음 절차를 사용 하거나 LSA 보호를 사용 하지 않도록 설정 하려면 사용할 수 있습니다.

##### <a name="to-enable-lsa-protection-on-a-single-computer"></a>하나의 컴퓨터에서 LSA 보호를 사용 하도록 설정 하려면

1.  레지스트리 편집기 (RegEdit.exe) 열고에 있는 레지스트리 키로 이동: 찾아 합니다.

2.  레지스트리 키를 설정: "RunAsPPL" = dword: 00000001 합니다.

3.  컴퓨터를 다시 시작 합니다.

##### <a name="to-enable-lsa-protection-using-group-policy"></a>그룹 정책을 사용 하 여 LSA 보호를 사용 하도록 설정 하려면

1.  그룹 정책 관리 콘솔 GPMC ()을 엽니다.

2.  만들기 도메인 수준에서 연결 되어 있는 또는 컴퓨터 계정을 포함 하 고 조직에 연결 되어 있는 합니다. 또는 GPO 이미 배포를 선택할 수 있습니다.

3.  GPO을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **편집** 그룹 정책 관리 편집기를 열 수 있습니다.

4.  확장 **컴퓨터 구성**, 확장 **기본**, 다음를 확장 하 고 **Windows 설정**합니다.

5.  마우스 오른쪽 단추로 클릭 **레지스트리**를 가리킨 **새로**을 차례로 클릭 하 고 **레지스트리 항목이**합니다. **새 레지스트리 속성** 대화 상자가 나타납니다.

6.  에 **하이브** 목록에서 클릭 **HKEY_LOCAL_MACHINE**합니다.

7.  에 **키 경로** 목록, 찾아보기 **SYSTEM\CurrentControlSet\Control\Lsa**합니다.

8.  에 **값 이름** 상자에 입력 **RunAsPPL**합니다.

9. 에 **값 형식** 상자를 클릭는 **REG_DWORD**합니다.

10. 에 **값 데이터** 상자에 입력 **00000001**합니다.

11. 클릭 **확인**합니다.

##### <a name="to-disable-lsa-protection"></a>LSA 보호를 사용 하지 않도록 설정 하려면

1.  레지스트리 편집기 (RegEdit.exe) 열고에 있는 레지스트리 키로 이동: 찾아 합니다.

2.  다음 값 레지스트리 키에서 삭제: "RunAsPPL" = dword: 00000001 합니다.

3.  로컬 보안 기관을 (LSA) 보호 프로세스 옵트아웃 도구를 사용 하 여 장치 보안 부팅을 사용 하는 경우 UEFI 변수를 삭제 합니다.

    옵트아웃이 도구에 대 한 자세한 내용은 참조 [다운로드 LSA 로컬 보안 기관을 () 보호 프로세스 옵트아웃 공식 Microsoft 다운로드 센터에서](https://www.microsoft.com/download/details.aspx?id=40897)합니다.

    보안 부팅을 관리에 대 한 자세한 내용은 참조 [UEFI 펌웨어](https://technet.microsoft.com/library/hh824898.aspx)합니다.

    > [!WARNING]
    > 보안 부팅 꺼진 경우 모든 보안 부팅 및 구성 UEFI 관련 다시 설정 됩니다. 다른 모든 방법 LSA 보호 기능을 해제 하려면 실패 한 경우에 보안 부팅 해제 해야 합니다.

### <a name="verifying-lsa-protection"></a>LSA 보호를 확인합니다.
Windows 시작 시 LSA 보호 모드로 시작 하는 경우 검색, 다음 WinInit 이벤트에 대 한 검색는 **시스템** 로그온 하는 **Windows 로그**:

-   12: LSASS.exe 수준으로 보호 된 프로세스를 시작한: 4

## <a name="additional-resources"></a>추가 리소스
[자격 증명 보호 및 관리](credentials-protection-and-management.md)

[파일 LSA에 서명 서비스](https://go.microsoft.com/fwlink/?LinkId=392590)


