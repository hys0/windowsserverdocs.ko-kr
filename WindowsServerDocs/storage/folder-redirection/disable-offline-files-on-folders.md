---
title: 개별 리디렉션된 폴더에서 오프 라인 파일을 사용 하지 않도록 설정
description: 폴더 리디렉션 사용 하 여 네트워크 공유로 리디렉션됩니다 개별 폴더에 오프 라인 파일 캐싱을 사용 하지 않도록 설정 하는 방법.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc93906cb7ff958fc1db7b00abdc557623e764e
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339311"
---
# 개별 리디렉션된 폴더에서 오프 라인 파일을 사용 하지 않도록 설정

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

이 항목에서는 폴더 리디렉션 사용 하 여 네트워크 공유로 리디렉션됩니다 개별 폴더에 오프 라인 파일 캐싱을 사용 하지 않도록 설정 하는 방법을 설명 합니다. 폴더를 로컬로 캐시에서 제외를 지정 하는 기능이 제공, 오프 라인 파일 캐시를 줄이면 크기 및 시간이 필요한 오프 라인 파일을 동기화 합니다.

>[!NOTE]
>이 항목에 설명 된 절차 중 일부를 자동화 하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet을 포함 됩니다. 자세한 내용은 [Windows PowerShell의 기본 사항을](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)참조 하세요.

## 필수 구성 요소

특정 리디렉션된 폴더의 오프 라인 파일 캐싱을 사용 하지 않으려면 환경에는 다음과 같은 필수 조건을 충족 해야 합니다.

- 도메인에 가입 된 클라이언트 컴퓨터와의 Active Directory Domain Services (AD DS) 도메인입니다. 도메인 또는 포리스트 기능 수준 요구 사항 또는 스키마 요구 사항 없이 있습니다.
- Windows 10, Windows 8.1, Windows 8, Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 클라이언트 컴퓨터.
- 설치 된 그룹 정책 관리를 사용 하 여 컴퓨터입니다.

## 개별 리디렉션된 폴더에서 오프 라인 파일을 사용 하지 않도록 설정

오프 라인 파일 캐싱을 특정 리디렉션된 폴더를 사용 하지 않으려면 그룹 정책을 사용 하 여 **특정 리디렉션된 폴더를 오프 라인으로 자동으로** 정책 설정에 대 한 적절 한 그룹 정책 개체 (GPO)를 사용 하도록 설정 합니다. **사용 안 함** 또는 **구성 되지 않음** 이 정책 설정을 구성 리디렉션된 폴더를 모든 사용 가능한 오프 라인으로 만듭니다.

>[!NOTE]
>도메인 관리자, 엔터프라이즈 관리자 및 그룹 정책 작성자 소유자 그룹의 구성원만 Gpo를 만들 수 있습니다.

### 특정 리디렉션된 폴더에서 오프 라인 파일을 사용 하지 않도록 설정

1. **그룹 정책 관리**를 엽니다.
2. 선택적으로 지정 있는 사용자는 오프 라인으로 사용할 수 있는에서 제외 된 폴더 리디렉션가 해야 하는 새 GPO를 만들려면 적절 한 도메인 또는 OU (조직 단위)를 마우스 오른쪽 단추로 클릭 한 다음 선택이 도메인에서 GPO 만들기 **하 고 여기에 연결 **.
3. 콘솔 트리에서 폴더 리디렉션 설정을 구성 하 고 다음 **편집**을 선택 하 고 GPO를 마우스 오른쪽 단추로 클릭 합니다. 그룹 정책 관리 편집기에 표시 됩니다.
4. **사용자 구성**콘솔 트리에서 **정책**, **관리 템플릿**, **시스템**확장 및 **폴더 리디렉션**확장 합니다.
5. **특정 리디렉션된 폴더를 오프 라인으로 자동으로** 마우스 오른쪽 단추로 클릭 하 고 **편집**을 선택 합니다. **특정 리디렉션된 폴더를 오프 라인으로 자동으로** 창이 나타납니다.
6. **사용**을 선택합니다. **옵션** 창 해야 사용 될 수 없는 오프 라인으로 적절 한 확인란을 선택 하 여 폴더를 선택 합니다. **확인**을 선택합니다.

### 해당 하는 Windows PowerShell 명령

다음 Windows PowerShell cmdlet 또는 cmdlet 동일한 기능을 [사용 하지 않도록 설정에서 오프 라인 파일 개별 리디렉션된 폴더에서](#disabling-offline-files-on-individual-redirected-folders)에서 설명 하는 절차를 수행 합니다. 서식 제약 조건으로 인해 여기에 여러 줄 바꿈 표시 수 있지만 한 줄에 각 cmdlet을 입력 합니다.

이 예제에서는 *contoso.com* 도메인의 *MyOu* 조직 구성 단위에서 *오프 라인 파일 설정* 라는 새 GPO를 만듭니다 (LDAP 고유 이름은 "ou = MyOU, dc = contoso, dc = com"). 다음 동영상 리디렉션된 폴더에 대 한 오프 라인 파일을 비활성화합니다.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

다음 레지스트리 키 이름 (폴더 Guid) 각 리디렉션된 폴더에 사용할 목록 표를 참조 하세요.

|리디렉션된 폴더|레지스트리 키 이름 (폴더 GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|데스크톱|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|시작 메뉴|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|문서|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|그림|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|음악|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|비디오|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|Favorites|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|연락처|{56784854-C6CB-462b-8169-88E350ACB882}|
|다운로드|{374DE290-123F-4565-9164-39C4925E467B}|
|링크|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|Searches|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|저장 된 게임이|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## 자세한 정보

- [폴더 리디렉션, 오프 라인 파일 및 로밍 사용자 프로필 개요](folder-redirection-rup-overview.md)
- [폴더 리디렉션과 오프 라인 파일을 사용 하 여 배포](deploy-folder-redirection.md)