---
title: AD FS 도움말 진단 분석기
description: 이 문서에서는 AD FS 진단 PowerShell 모듈을 사용 하 여 기본 검사를 수행 하는 방법 및 도움말 진단 분석기 AD FS 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: anandyadavMSFT
ms.date: 03/29/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5d56a84680467359b68ae1ab115801d82a34c822
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407237"
---
# <a name="ad-fs-help-diagnostics-analyzer"></a>AD FS 도움말 진단 분석기

AD FS에는 인증 및 응용 프로그램 개발을 위해 제공 되는 다양 한 기능을 지 원하는 다양 한 설정이 있습니다. 문제를 해결 하는 동안 모든 AD FS 설정이 올바르게 구성 되어 있는지 확인 하는 것이 좋습니다. 이러한 설정을 수동으로 확인 하는 경우 시간이 많이 걸릴 수 있습니다. AD FS Help Diagnostics Analyzer는 ADFSToolbox PowerShell 모듈을 사용 하 여 기본 검사를 수행 하는 데 도움이 될 수 있습니다. AD FS 검사를 수행한 후에는 [진단 분석기](https://aka.ms/adfsdiagnosticsanalyzer) 를 제공 하 여 결과를 쉽게 시각화 하 고 수정 단계를 제공할 수 있습니다.

전체 작업에는 세 개의 간단한 단계가 필요 합니다.

1. 기본 AD FS 서버 또는 WAP 서버에서 ADFSToolbox 모듈 설정
2. 진단을 실행 하 고 파일을 업로드 하 AD FS 도움말
3. 진단 분석 보기 및 문제 해결

문제 해결을 시작 하려면 [AD FS 도움말 진단 분석기 (https://aka.ms/adfsdiagnosticsanalyzer)를 참조](https://aka.ms/adfsdiagnosticsanalyzer) 하세요.

![AD FS 도움말 AD FS 진단 분석기 도구](media/ad-fs-diagonostics-analyzer/home.png)

## <a name="step-1-setup-the-adfstoolbox-module-on-ad-fs-server"></a>1 단계: AD FS 서버에서 ADFSToolbox 모듈 설정

[진단 분석기](https://aka.ms/adfsdiagnosticsanalyzer)를 실행 하려면 ADFSToolbox PowerShell 모듈을 설치 해야 합니다. AD FS 서버가 인터넷에 연결 되어 있는 경우 PowerShell 갤러리에서 직접 ADFSToolbox 모듈을 설치할 수 있습니다. 인터넷에 연결 되지 않은 경우 수동으로 설치할 수 있습니다. 

[!WARNING]
AD FS 2.1를 사용 하는 경우 ADFSToolbox의 1.0.13 버전을 설치 해야 합니다. ADFSToolbox는 더 이상 최신 버전에서 AD FS 2.1를 지원 하지 않습니다.

![AD FS 진단 분석기-설치](media/ad-fs-diagonostics-analyzer/step1_v2.png)

### <a name="setup-using-powershell-gallery"></a>PowerShell 갤러리를 사용 하 여 설치

AD FS 서버가 인터넷에 연결 되어 있는 경우 아래에 제공 된 PowerShell 명령을 사용 하 여 PowerShell 갤러리에서 직접 ADFSToolbox 모듈을 설치 하는 것이 좋습니다.

   ```powershell
    Install-Module -Name ADFSToolbox -force
    Import-Module ADFSToolbox -force
   ```

### <a name="setup-manually"></a>수동으로 설치

ADFSToolbox 모듈을 AD FS 또는 WAP 서버에 수동으로 복사 해야 합니다. 아래 지침을 따르세요.

1. 인터넷에 액세스할 때 사용 하는 컴퓨터에서 관리자 권한 PowerShell 창을 시작 합니다.
2. AD FS 도구 상자 모듈을 설치 합니다.

    ```powershell
    Install-Module -Name ADFSToolbox -Force
    ```
3. 로컬 컴퓨터에 `%SYSTEMDRIVE%\Program Files\WindowsPowerShell\Modules\` 있는 ADFSToolbox 폴더를 AD FS 또는 WAP 컴퓨터의 동일한 위치에 복사 합니다.

4. AD FS 컴퓨터에서 관리자 권한 PowerShell 창을 시작 하 고 다음 cmdlet을 실행 하 여 모듈을 가져옵니다.

    ```powershell
    Import-Module ADFSToolbox -Force
    ```

## <a name="step-2-execute-the-diagnostics-cmdlet"></a>2 단계: 진단 cmdlet 실행

![AD FS 진단 분석기 도구-결과 실행 및 업로드](media/ad-fs-diagonostics-analyzer/step2_v2.png)

단일 명령을 사용 하 여 팜의 모든 AD FS 서버에서 진단 테스트를 편리 하 게 실행할 수 있습니다. PowerShell 모듈은 팜의 여러 서버에서 진단 테스트를 실행 하는 데 원격 PS 세션을 사용 합니다.

```powershell
    Export-AdfsDiagnosticsFile [-ServerNames <list of servers>]
```

서버 2016 이상 AD FS 팜에서이 명령은 AD FS 구성에서 AD FS 서버 목록을 읽습니다. 그러면 목록의 각 서버에 대해 진단 테스트가 시도 됩니다. AD FS 서버 목록을 사용할 수 없는 경우 (예: 2012R2) 로컬 컴퓨터에 대해 테스트가 실행 됩니다. 테스트를 실행할 서버 목록을 지정 하려면 **ServerNames** 인수를 사용 하 여 서버 목록을 제공 합니다. 아래에 예제가 나와 있습니다.

```powershell
    Export-AdfsDiagnosticsFile -ServerNames @("adfs1.contoso.com", "adfs2.contoso.com")
```

결과는 명령이 실행 된 디렉터리에 생성 되는 JSON 파일입니다. 파일의 이름은 AdfsDiagnosticsFile 타임 스탬프\>\<됩니다. 파일 이름 예는 AdfsDiagnosticsFile-07312019-184201입니다.

## <a name="step-3-upload-the-diagnostics-file"></a>3 단계: 진단 파일 업로드

[https://aka.ms/adfsdiagnosticsanalyzer](https://aka.ms/adfsdiagnosticsanalyzer) 3 단계에서 파일 브라우저를 사용 하 여 업로드할 결과 파일을 선택 합니다.

**업로드를 클릭 하 여** 업로드를 완료 합니다.

Microsoft 계정를 사용 하 여 로그인 하면 이후 표시 지점에 대 한 진단 결과를 저장 하 고 Microsoft 지원으로 보낼 수 있습니다. 언제 든 지 지원 사례를 열면 Microsoft에서 진단 분석기 결과를 확인 하 고 문제 해결을 더 빠르게 도울 수 있습니다.

![AD FS 진단 분석기 도구-로그인](media/ad-fs-diagonostics-analyzer/sign_in_step.png)

## <a name="step-4-view-diagnostics-analysis-and-resolve-any-issues"></a>4 단계: 진단 분석 보기 및 문제 해결

테스트 결과에는 다음의 5 개 섹션이 있습니다.

1. 실패:이 섹션에는 실패 한 테스트 목록이 포함 되어 있습니다. 각 결과는 다음 요소로 구성 됩니다.
2. 경고:이 섹션에는 경고를 발생 시킨 테스트 목록이 포함 되어 있습니다. 이러한 문제로 인해 더 광범위 한 인증에 대 한 문제가 발생 하지는 않지만 가장 빨리 해결 해야 합니다.
3. 통과 됨:이 섹션에는 통과 하 고 사용자에 대 한 작업 항목이 없는 테스트 목록이 포함 됩니다.
4. 실행 되지 않음:이 섹션에는 정보가 누락 되어 실행할 수 없는 테스트 목록이 포함 되어 있습니다.
5. 해당 사항 없음:이 섹션에서는 명령이 실행 되 고 있는 특정 서버에 적용 되지 않기 때문에 실행 되지 않은 테스트 목록을 포함 합니다.

![AD FS 진단 분석기 도구-테스트 결과 목록](media/ad-fs-diagonostics-analyzer/step3a_v3.png) 테스트를 설명 하 고 단계를 해결 하는 세부 정보와 함께 각 테스트 결과가 표시 됩니다.

1. 테스트 이름: 실행 된 테스트의 이름입니다.
2. Description: 테스트에 대 한 설명입니다.
3. 세부 정보: 테스트 중에 수행 된 전체 작업에 대 한 설명
4. 해결 단계: 테스트에 의해 강조 표시 된 문제를 해결 하는 제안 된 단계

![AD FS 진단 분석기 도구-오류 해결](media/ad-fs-diagonostics-analyzer/step3b_v3.png)

## <a name="next"></a>다음

- [AD FS 도움말 troublehshooting 가이드 사용](https://aka.ms/adfshelp/troubleshooting )
- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
