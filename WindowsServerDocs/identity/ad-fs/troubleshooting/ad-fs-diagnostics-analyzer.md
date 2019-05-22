---
title: AD FS 도움말 진단 분석기
description: 이 문서에서는 AD FS 도움말 진단 분석기를 설명 하 고 AD FS 진단 PowerShell 모듈을 사용 하 여 확인 하는 방법을 기본 수행할 수 있습니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.reviewer: anandyadavMSFT
ms.date: 03/29/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8d9acd1adcb8d9566b154abfef940e21609a6684
ms.sourcegitcommit: 4ff3d00df3148e4bea08056cea9f1c3b52086e5d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2019
ms.locfileid: "64773378"
---
# <a name="ad-fs-help-diagnostics-analyzer"></a>AD FS 도움말 진단 분석기

AD FS에 다양 한 인증 및 응용 프로그램 개발을 위해 제공 하는 기능을 지 원하는 다양 한 설정이 있습니다. 이 문제를 해결 하는 동안 모든 AD FS 설정이 제대로 구성 되어 있는지 확인 하는 것이 좋습니다. 이러한 설정 중 수동 검사를 수행할 시간이 오래 걸리는 경우도 있습니다. AD FS 도움말 진단 분석기 ADFSToolbox PowerShell 모듈을 사용 하 여 기본 검사를 수행 하는 데 도움이 됩니다. 검사를 수행한 후 AD FS 도움말을 제공 합니다 [진단 분석기](https://aka.ms/adfsdiagnosticsanalyzer) 쉽게 결과 시각화 하 고 수정 단계를 제공 하는 데 있습니다.

간단한 3 단계를 수행 하는 전체 작업:

1. 기본 AD FS 서버 또는 WAP 서버에 ADFSToolbox 모듈 설치
2. 진단 유틸리티를 실행 하 고 AD FS 도움말 파일을 업로드 합니다.
3. 진단 분석을 확인 하 고 문제 해결

로 이동 [AD FS 도움말 진단 분석기 (https://aka.ms/adfsdiagnosticsanalyzer) ](https://aka.ms/adfsdiagnosticsanalyzer) 문제 해결을 시작 합니다.

![AD FS 진단 분석기 도구에 대 한 AD FS 도움말](media/ad-fs-diagonostics-analyzer/home.png)

## <a name="step-1-setup-the-adfstoolbox-module-on-ad-fs-server"></a>1단계: AD FS 서버에서 ADFSToolbox 모듈 설치

실행 하는 [진단 분석기](https://aka.ms/adfsdiagnosticsanalyzer), ADFSToolbox PowerShell 모듈을 설치 해야 합니다. AD FS 서버에 인터넷에 연결 하는 경우에 PowerShell 갤러리에서 직접 ADFSToolbox 모듈을 설치할 수 있습니다. 인터넷에 연결 되지 않은, 경우 수동 설치에 대 한 GitHub 리포지토리를 복제 합니다.

![AD FS 진단 분석기-설치](media/ad-fs-diagonostics-analyzer/step1.png)

### <a name="setup-using-powershell-gallery"></a>PowerShell 갤러리를 사용 하 여 설치

AD FS 서버에 인터넷에 연결 하는 경우에 아래의 PowerShell 명령을 사용 하 여 PowerShell 갤러리에서 직접 ADFSToolbox 모듈을 설치 하는 것이 좋습니다.

   ```powershell
    Install-Module -Name ADFSToolbox -force
    Import-Module ADFSToolbox -force
   ```
### <a name="setup-manually-by-cloning-the-repository"></a>리포지토리를 복제 하 여 수동으로 설치

ADFSToolbox 모듈을 수동으로 설치할 수 있습니다 GitHub에서 직접. 리포지토리를 복제 하 고 AD FS 서버의 ADFSToolbox 모듈 설치에 대 한 아래 지침을 따릅니다.

1. 다운로드는 [리포지토리](https://github.com/Microsoft/adfsToolbox/archive/master.zip)
2. 다운로드 한 파일의 압축을 풀고 % SYSTEMDRIVE %adfsToolbox 마스터 폴더를 복사\\Program Files\\WindowsPowerShell\\모듈\\합니다.
3. PowerShell 모듈을 가져옵니다. 관리자 권한 PowerShell 창에서 다음을 실행 합니다.

   ```powershell
    Import-Module ADFSToolbox -Force
   ```

## <a name="step-2-execute-the-diagnostics-and-upload-the-file-to-ad-fs-help"></a>2단계: 진단 유틸리티를 실행 하 고 AD FS 도움말 파일을 업로드 합니다.

편리 하 게 팜의 모든 AD FS 서버에서 진단 테스트를 실행 하는 단일 명령을 사용할 수 있습니다. PowerShell 모듈을 팜의 다른 서버에 걸쳐 진단 테스트를 실행 하려면 원격 PS 세션을 사용 합니다.

```powershell
    Export-AdfsDiagnosticsFile [-adfsServers <list of servers>]
```

Server 2016 AD FS 팜에서 명령을 AD FS 구성에서 AD FS 서버 목록을 읽습니다. 진단 테스트 목록의 각 서버에 대해 다음 시도 됩니다. AD FS 서버 목록에 사용할 수 없는 경우 (예 2012R2) 다음 테스트를 로컬 컴퓨터에 대해 실행 됩니다. 테스트를 실행할 수는 서버 목록을 지정 하려면 사용 합니다 **adfsServers** 서버 목록을 제공 하는 인수입니다. 아래 예제

```powershell
    Export-AdfsDiagnosticsFile -adfsServers @("sts1.contoso.com", "sts2.contoso.com", "sts3.contoso.com")
```

결과 명령이 실행 된 동일한 디렉터리에 생성 된 JSON 파일. 파일의 이름은 ADFSDiagnosticsFile-\<타임 스탬프\>합니다. 파일 이름의 예는 ADFSDiagnosticsFile 20180716124030 합니다.

2 단계에서 [ https://aka.ms/adfsdiagnosticsanalyzer ](https://aka.ms/adfsdiagnosticsanalyzer) 파일 브라우저를 사용 하 여 업로드할 결과 파일을 선택 합니다.

![AD FS 진단 분석기 도구-실행 하 고 결과 업로드 합니다.](media/ad-fs-diagonostics-analyzer/step2.png)

클릭할 **업로드** 업로드를 완료 하 여 다음 단계로 이동 합니다.


Microsoft 계정으로 로그인 하 여 진단 결과 보기 나중에 저장할 수 있는 및 Microsoft에 보낼 수 있습니다를 지원 합니다. 언제 든 지 지원 사례를 열 경우 Microsoft 진단 분석기 결과 확인 하 고 더 빠르게 문제를 해결 하는 일을 할 수 있습니다.

![AD FS 진단 분석기 도구에 로그인](media/ad-fs-diagonostics-analyzer/sign_in_step.png)

## <a name="step-3-view-diagnostics-analysis-and-resolve-any-issues"></a>3단계: 진단 분석을 확인 하 고 문제 해결

테스트 결과의 네 섹션 가지가 있습니다.

1. 실패 했습니다. 이 섹션에는 실패 한 테스트 목록이 포함 됩니다. 각 결과 구성 됩니다.
2. 경고: 이 섹션에는 경고가 발생 한 테스트의 목록을 포함 합니다. 이러한 문제 광범위 한 규모에서 인증 관련 문제가 발생 하지 않지만 사용 가능한 한 빨리 해결 해야 합니다.
3. 해당 없음: 이 섹션에서는 테스트 명령은 실행 하는 특정 서버에 적용할 수 없기 때문에 실행 되지 않은 목록을 포함 합니다.
4. 전달 합니다. 이 섹션에서는 사용자에 대 한 작업 항목이 있고 전달 하는 테스트의 목록을 포함 합니다.

![AD FS 진단 분석기 도구-테스트 결과 목록](media/ad-fs-diagonostics-analyzer/step3a_v2.png) 테스트 및 확인 단계를 설명 하는 세부 정보를 사용 하 여 각 테스트 결과가 표시 됩니다.

1. 테스트 이름: 실행 된 테스트의 이름
2. 세부 정보: 테스트 중 수행 된 전체 작업의 설명
3. 해결 단계: 테스트에서 강조 표시 된 문제를 해결 하는 제안된 단계

![AD FS 진단 분석기 도구-실패 해결](media/ad-fs-diagonostics-analyzer/step3b_v2.png)

## <a name="next"></a>다음

- [AD FS 도움말 troublehshooting 가이드를 사용 합니다.](https://aka.ms/adfshelp/troubleshooting )
- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
