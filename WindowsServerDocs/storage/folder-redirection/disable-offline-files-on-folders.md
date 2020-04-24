---
title: 리디렉션된 개별 폴더에 대한 오프라인 파일 사용 안 함
description: 폴더 리디렉션을 사용하여 네트워크 공유로 리디렉션되는 개별 폴더에 대한 오프라인 파일 캐싱을 사용하지 않도록 설정하는 방법입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: c2614c0180b32a0215454f2d725d6a962986ef1f
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "71394399"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>리디렉션된 개별 폴더에 대한 오프라인 파일 사용 안 함

>적용 대상: Windows 10, Windows 8, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2012 R2, Window (반기 채널)

이 문서는 폴더 리디렉션을 사용하여 네트워크 공유로 리디렉션되는 개별 폴더에 대한 오프라인 파일 캐싱을 사용하지 않도록 설정하는 방법을 설명합니다. 이를 통해 로컬로 캐시에서 제외할 폴더를 지정하여 오프라인 파일을 동기화하는 데 필요한 오프라인 파일 캐시 크기와 시간을 줄일 수 있습니다.

>[!NOTE]
>이 항목에는 설명한 절차의 일부를 자동화하는 데 사용할 수 있는 샘플 Windows PowerShell cmdlet이 포함되어 있습니다. 자세한 내용은 [Windows PowerShell 기본 사항](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)을 참조하세요.

## <a name="prerequisites"></a>필수 구성 요소

리디렉션된 특정 폴더의 오프라인 파일 캐싱을 사용하지 않도록 설정하려면 환경이 다음의 필수 구성 요소를 충족해야 합니다.

- 클라이언트 컴퓨터가 도메인에 가입된 AD DS(Active Directory Domain Services) 도메인 포리스트 또는 도메인 기능 수준 요구 사항 또는 스키마 요구 사항은 없습니다.
- Windows 10, Windows 8.1, Windows 8, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 또는 Windows(반기 채널)를 실행하는 클라이언트 컴퓨터
- 그룹 정책 관리가 설치된 컴퓨터

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>리디렉션된 개별 폴더에 대한 오프라인 파일 사용 안 함

특정 리디렉션된 폴더의 오프라인 파일 캐싱을 사용하지 않도록 설정하려면 그룹 정책을 사용하여 적절한 GPO(그룹 정책 개체그룹 정책 개체)에 대해 **자동으로 리디렉션된 특정 폴더를 오프라인으로 사용할 수 있도록 설정하지 않음** 정책 설정을 활성화합니다. 이 정책 설정을 **사용 안 함** 또는 **구성되지 않음**으로 구성하면 모든 리디렉션된 폴더를 오프라인으로 사용할 수 있습니다.

>[!NOTE]
>도메인 관리자, 엔터프라이즈 관리자 및 Group Policy Creator Owners 그룹의 멤버만 GPO를 만들 수 있습니다.

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>리디렉션된 특정 폴더에 대한 오프라인 파일을 사용하지 않도록 설정하려면

1. **그룹 정책 관리**를 엽니다.
2. 필요에 따라 오프라인에서 사용 가능하게 설정에서 제외된 리디렉션된 폴더를 지정해야 하는 사용자를 지정하는 새 GPO를 만들려면 적절한 도메인 또는 OU(조직 구성 단위)를 마우스 오른쪽 단추로 클릭한 다음, **이 도메인에서 GPO 만들기 및 여기에서 연결**을 선택합니다.
3. 콘솔 트리에서 폴더 리디렉션 설정을 구성하려는 GPO를 마우스 오른쪽 단추로 클릭한 다음, **편집**을 선택합니다. 그룹 정책 관리 편집기가 표시됩니다.
4. 콘솔 트리의 **사용자 구성**에서 **정책**, **관리 템플릿**, **System**, **폴더 리디렉션**을 차례로 확장합니다.
5. **자동으로 리디렉션된 특정 폴더를 오프라인으로 사용할 수 있도록 설정하지 않음**을 마우스 오른쪽 단추를 클릭한 다음, **편집**을 선택합니다. **자동으로 리디렉션된 특정 폴더를 오프라인으로 사용할 수 있도록 설정하지 않음** 창이 나타납니다.
6. **사용**을 선택합니다. **옵션** 창에서 적절한 확인란을 선택하여 오프라인으로 사용할 수 없도록 설정할 폴더를 선택합니다. **확인**을 선택합니다.

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 해당 명령

다음 Windows PowerShell cmdlet은 [리디렉션된 개별 폴더에 대한 오프라인 파일 사용 안 함](#disabling-offline-files-on-individual-redirected-folders)에서 설명하는 절차와 동일한 기능을 수행합니다. 서식 제약 조건으로 인해 각 cmdlet이 여러 줄에 자동 줄 바꿈되어 표시될 수 있지만 각 cmdlet을 한 줄에 입력하세요.

이 예제는 *contoso.com* 도메인의 *MyOu* 조직 구성 단위에서 *오프라인 파일 설정*이라는 새 GPO를 만듭니다(LDAP 고유 이름은 "ou=MyOU,dc=contoso,dc=com"임). 그런 다음, 비디오 리디렉션된 폴더에 대한 오프라인 파일을 사용하지 않도록 설정합니다.

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

리디렉션된 각 폴더에 사용할 레지스트리 키 이름(폴더 GUID) 목록은 다음 표를 참조하세요.

|리디렉션된 폴더|레지스트리 키 이름(폴더 GUID)|
|---|---|
|AppData(로밍)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|데스크톱|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|시작 메뉴|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|Documents|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|사진|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|음악|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|동영상|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|즐겨찾기|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|연락처|{56784854-C6CB-462b-8169-88E350ACB882}|
|다운로드|{374DE290-123F-4565-9164-39C4925E467B}|
|링크|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|검색|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|저장 된 게임|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>자세한 정보

- [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필 개요](folder-redirection-rup-overview.md)
- [오프라인 파일을 사용한 폴더 리디렉션 배포](deploy-folder-redirection.md)