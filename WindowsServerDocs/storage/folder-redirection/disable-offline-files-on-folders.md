---
title: 개별 리디렉션된 폴더의 오프 라인 파일을 사용 하지 않도록 설정
description: 오프 라인 파일은 폴더 리디렉션을 사용 하 여 네트워크 공유에 리디렉션되어야 하는 개별 폴더에서 캐싱을 사용 하지 않도록 설정 하는 방법.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc93906cb7ff958fc1db7b00abdc557623e764e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834204"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>개별 리디렉션된 폴더의 오프 라인 파일을 사용 하지 않도록 설정

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

이 항목에서는 오프 라인 파일은 폴더 리디렉션을 사용 하 여 네트워크 공유에 리디렉션되어야 하는 개별 폴더에서 캐싱을 사용 하지 않도록 설정 하는 방법을 설명 합니다. 로컬 캐시에서 제외할 폴더를 지정 하는 기능에서는 오프 라인 파일 캐시를 줄이고 시간 및 크기 하는 데 필요한 파일을 오프 라인 동기화.

>[!NOTE]
>이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 [Windows PowerShell 기본 사항](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)합니다.

## <a name="prerequisites"></a>사전 요구 사항

특정 리디렉션된 폴더의 오프 라인 파일 캐시를 사용 하지 않으려면 환경의 다음 필수 조건을 충족 해야 합니다.

- 클라이언트 컴퓨터를 도메인에 가입 된의 Active Directory Domain Services (AD DS) 도메인입니다. 포리스트 또는 도메인 기능 수준 요구 사항 또는 스키마 요구 사항이 없는 합니다.
- Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 클라이언트 컴퓨터입니다.
- 설치 하는 그룹 정책 관리 된 컴퓨터입니다.

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>개별 리디렉션된 폴더의 오프 라인 파일을 사용 하지 않도록 설정

특정 리디렉션된 폴더의 오프 라인 파일 캐시를 사용 하지 않으려면 그룹 정책을 사용 하도록 설정 하려면 사용 합니다 **자동으로 만들지 마십시오 특정 리디렉션된 폴더 사용 가능한 오프 라인** 정책 설정에 대 한 적절 한 그룹 정책 개체 (GPO). 이 정책 설정을 구성 **사용 안 함** 하거나 **구성 되지 않은** 모든 리디렉션된 폴더를 오프 라인으로 사용할 수 있도록 합니다.

>[!NOTE]
>도메인 관리자, 엔터프라이즈 관리자 및 그룹 정책 creator owners 그룹의 구성원만 Gpo를 만들 수 있습니다.

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>특정 리디렉션된 폴더의 오프 라인 파일을 사용 하지 않도록 설정

1. 오픈 **그룹 정책 관리**합니다.
2. 필요에 따라 사용자가 제공 된 오프 라인에서 제외 된 폴더를 리디렉션해야가 지정 하 여 새 GPO를 만들려면 적절 한 도메인 또는 조직 구성 단위 (OU)를 마우스 오른쪽 단추로 클릭 하 고 선택한 **이 도메인에서 GPO를 만들고 연결 여기에 it**합니다.
3. 콘솔 트리에서 폴더 리디렉션 설정을 구성 하 고 선택한 GPO를 마우스 오른쪽 단추로 **편집**합니다. 그룹 정책 관리 편집기가 나타납니다.
4. 콘솔 트리에서 아래 **사용자 구성**, 확장 **정책을**, 확장 **관리 템플릿**를 확장 하 고 **시스템**, 및 확장 **폴더 리디렉션**합니다.
5. 마우스 오른쪽 단추로 클릭 **자동으로 만들지 마십시오 특정 리디렉션된 폴더 사용 가능한 오프 라인** 선택한 후 **편집**합니다. 합니다 **자동으로 만들지 마십시오 특정 리디렉션된 폴더 사용 가능한 오프 라인** 창이 나타납니다.
6. **사용**을 선택합니다. 에 **옵션** 창 해야 사용할 수 오프 라인으로 적절 한 확인란을 선택 하 여 폴더를 선택 합니다. **확인**을 선택합니다.

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet 또는 cmdlet을 절차에 설명 된 대로 동일한 기능을 수행 [사용 하지 않도록 설정에서 오프 라인 파일 개별 리디렉션된 폴더](#disabling-offline-files-on-individual-redirected-folders)합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

이 예제에서는 명명 된 새 GPO를 만듭니다 *오프 라인 파일 설정을* 에 *MyOu* 조직 구성 단위에는 *contoso.com* 도메인 (LDAP 고유 이름 형식이 "ou = MyOU, dc = contoso, dc = com "). 그런 다음 오프 라인 파일에 리디렉션 Videos 폴더는 사용 하지 않습니다.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

각 리디렉션된 폴더에 대해 사용 하도록 레지스트리 키 이름 (폴더 Guid) 목록은 다음 표를 참조 하세요.

|리디렉션된 폴더|레지스트리 키 이름 (폴더 GUID)|
|---|---|
|Appdata\roaming|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|데스크톱|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|시작 메뉴|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|문서|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|사진|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|음악|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|비디오|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|즐겨찾기|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|연락처|{56784854-C6CB-462b-8169-88E350ACB882}|
|다운로드|{374DE290-123F-4565-9164-39C4925E467B}|
|링크|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|검색|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|저장 된 게임|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>자세한 정보

- [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 개요](folder-redirection-rup-overview.md)
- [오프 라인 파일을 사용 하 여 폴더 리디렉션 배포](deploy-folder-redirection.md)