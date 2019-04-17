---
title: Windows Admin Center를 사용 하 여 시작
description: Windows Admin Center를 사용 하 여 시작
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/15/2019
ms.openlocfilehash: f4fd9f69e75ed80bbdb345b4041c2337c65ec2e6
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296655"
---
# Windows Admin Center를 사용 하 여 시작

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md) [지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## Windows 10에 설치 된 Windows Admin Center

> [!IMPORTANT]
> Windows 10에서 Windows Admin Center를 사용 하 여 로컬 관리자 그룹의 구성원 이어야 합니다.

### 클라이언트 인증서를 선택합니다.

처음으로 Windows 10에서 Windows Admin Center를 열면 (그렇지 않으면 오류가 HTTP 403 "이이 페이지에 액세스할 수 없습니다" 라는) *Windows Admin Center 클라이언트* 인증서 선택 되어 있는지 확인 합니다.

이 대화 상자를 사용 하 여 메시지가 나타나면 Microsoft Edge에서:
 
1. **다른 옵션** 을 클릭 합니다.

    ![](../media/launch-cert-1.png)

2. **Windows Admin Center 클라이언트** 레이블이 지정 된 인증서를 선택 하 고 **확인** 을 클릭합니다

    ![](../media/launch-cert-2.png)

3. **허용** 을 클릭 하 고 **액세스 항상 허용** 선택 되었는지 확인

    ![](../media/launch-cert-3.png)

## 관리 되는 노드 및 클러스터에 연결

Windows Admin Center 설치를 완료 한 후에 서버 또는 주 개요 페이지에서 관리 하는 클러스터를 추가할 수 있습니다.

 **관리 되는 노드로 단일 서버 또는 클러스터에 추가**

 1. **모든 연결**에서 **+ 추가** 클릭 합니다.

    ![](../media/launch/addserver0.png)

 2. 서버, 장애 조치 클러스터 또는 컨 버 지 드 클러스터 연결을 추가 하려면 선택 합니다.
    
    ![](../media/launch/addserver1.png)

 3. 서버 또는 클러스터를 관리 하 고 **제출**을 클릭의 이름을 입력 합니다. 서버 또는 클러스터 개요 페이지에서 연결 목록에 추가 됩니다.

    ![](../media/launch/addserver2.png)

   **-- 또는 --**

**대량으로 여러 서버 가져오기**

 1. **서버 연결 추가** 페이지에서 **가져오기 서버** 탭을 선택 합니다.

    ![](../media/launch/import-servers.png)

 2. **찾아보기** 를 클릭 하 고 쉼표 또는 새 줄, Fqdn 추가 하려는 서버에 대 한 목록 포함 하는 텍스트 파일을 선택 합니다.

    **-- 또는 --**

**Active Directory를 검색 하 여 서버를 추가 합니다.**

 1. **서버 연결 추가** 페이지에서 **검색 Active Directory** 탭을 선택 합니다.

    ![](../media/launch/search-ad.png)

 2. 검색어를 입력 하 고 **검색**을 클릭 합니다. 와일드 카드 (*)가 지원 됩니다.

 3. 검색 끝나면-결과 중 하나 이상을 선택, 선택적으로 태그를 추가 하 고 **추가**클릭 합니다.

## 관리 되는 노드를 사용 하 여 인증 ##

Windows Admin Center는 관리 되는 노드를 사용 하 여 인증에 대 한 몇 가지 메커니즘을 지원 합니다. 대 한 single sign-on 기본값입니다.

**Single sign-on**

현재 Windows 자격 증명 관리 노드를 사용 하 여 인증을 사용할 수 있습니다. 이것이 기본값, 및 서버를 추가 하면 Windows Admin Center는 로그온 시도 합니다. 

**대 한 single sign-on 배포 하는 Windows Server에서 서비스 하는 경우**

Windows Server에서 Windows Admin Center를 설치한 경우 추가 구성이 single sign-on에 필요 합니다.  [위임을 위해 환경 구성](..\configure\user-access-control.md)

**-- 또는 --**

***다음으로 관리* 지정 자격 증명을 사용 하 여**

**모든 연결**을에서 서버 목록에서 선택 하 고 선택 **으로 관리** 하는 관리 되는 노드에 인증에 사용할 자격 증명을 지정 합니다.

![](../media/launch-use-6.png)

Windows Admin Center는 Windows Server에서 서비스 모드에서 실행 되지만 Kerberos 위임을 구성 되지 않은 경우 Windows 자격 증명을 다시 입력 해야 합니다.

![](../media/launch-use-7.png)

자격 증명을 해당 특정 브라우저 세션에 대 한 캐시는 모든 연결을 적용할 수 있습니다. 브라우저를 다시 로드 하는 경우 **다음으로 관리** 자격 증명을 다시 입력 해야 합니다.

**로컬 관리자 암호 솔루션 (LAPS)**

환경에서 [랩](https://technet.microsoft.com/mt227395.aspx)를 사용 하는 경우 랩 자격 증명 관리 노드를 사용 하 여 인증을 사용할 수 있습니다. **이 시나리오에서는 하세요 사용 하는 경우** [피드백을 제공](http://aka.ms/WACFeedback)합니다.

## 태그를 사용 하 여 연결을 구성할 수

파악 하 고 관련된 서버 연결 목록에서 필터링 태그를 사용할 수 있습니다.  이렇게 하면 서버 연결 목록에서의 하위 집합을 볼 수 있습니다.  많은 연결을 설정한 경우 특히 유용 합니다.

### 태그 편집

* 모든 연결 목록에서 서버 또는 여러 서버를 선택 합니다.
* **모든 연결** **태그 편집** 을 클릭합니다

![](../media/launch/tags-5.png)

**연결 태그 편집** 창 수정, 추가 또는 태그에 선택 된 연결에서 제거할 수 있습니다.

* 새 태그에 선택한 연결을 추가 하려면 **태그 추가** 선택 하 고 사용 하려면 태그 이름을 입력 합니다.

* 선택한 연결 된 기존 태그 이름으로 태그를 적용 하려면 태그 이름 옆에 있는 확인란을 선택 합니다.

* 선택한 모든 연결에서 태그를 제거 하려면 제거할 태그 옆에 있는 확인란의 선택을 취소 합니다.

* 태그는 선택한 연결의 하위 집합에 적용 하는 경우 확인란 중간 상태에 표시 됩니다. 확인 하 고 선택한 모든 연결에 태그를 적용 하거나 선택을 취소 하 고 모든 선택 된 연결에서 태그를 제거를 다시 클릭 상자를 클릭 합니다.

![](../media/launch/tags-6.png)

### 태그 필터 연결

하나 이상의 서버 연결에 태그를 추가한 후에 연결 목록에 태그를 볼 수 있으며 태그로 연결 목록을 필터링 수 있습니다.

* 태그를 필터링 하려면 검색 상자 옆에 있는 필터 아이콘을 선택 합니다.
![](../media/launch/tags-7.png)
* 선택할 수 있습니다 "또는", "및" 또는 "안 함" 선택 된 태그의 필터 동작을 수정 합니다.
![](../media/launch/tags-8.png)

## PowerShell을 사용 하 여 가져오기 / 내보내기 (태그로)에 연결 하려면

> 적용 대상: Windows Admin Center 미리 보기

Windows Admin Center 미리 보기를 가져오거나 연결 목록 내보내기 PowerShell 모듈을 포함 합니다.

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### CSV 파일 형식 연결을 가져오기 위한

CSV 파일의 형식은 4 개의 머리글을 사용 하 여 시작 ```"name","type","tags","groupId"```새 줄에 각 연결 옵니다.

**이름은 연결의 FQDN**

연결 형식 **형식이** 입니다. Windows Admin Center에 포함 된 기본 연결을 위한 다음 중 하나를 사용 합니다.

| 연결 형식 | 연결 문자열 |
|------|-------------------------------|
| Windows Server | msft.sme.connection type.server |
| Windows 10 PC | msft.sme.connection type.windows 클라이언트 |
| 장애 조치(failover) 클러스터 | msft.sme.connection type.cluster |
| 하이퍼 수렴 형 클러스터 | msft.sme.connection type.hyper-수렴 형-클러스터 |

**태그** 는 파이프 구분 합니다.

**groupId** 공유 연결에 사용 됩니다. 값을 사용 하 여 ```global``` 이 공유 연결을이 열에 있습니다.

### 연결을 가져오는 예제 CSV 파일

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## 가져오기 RDCman 연결

아래의 스크립트를 사용 하 여 [RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) 에 저장 된 연결 파일로 내보냅니다. 가져올 수 있습니다 파일 Windows Admin Center에 태그를 사용 하 여 RDCMan 그룹화 계층을 유지 합니다. 체험해!

1. 복사한 PowerShell 세션에 다음 코드를 붙여 넣습니다.

   ```powershell
   #Helper function for RdgToWacCsv
   function AddServers {
    param (
    [Parameter(Mandatory = $true)]
    [Xml.XmlLinkedNode]
    $node,
    [Parameter()]
    [String[]]
    $tags,
    [Parameter(Mandatory = $true)]
    [String]
    $csvPath
    )
    if ($node.LocalName -eq 'server') {
        $serverName = $node.properties.name
        $tagString = $tags -join "|"
        Add-Content -Path $csvPath -Value ('"'+ $serverName + '","msft.sme.connection-type.server","'+ $tagString +'"')
    } 
    elseif ($node.LocalName -eq 'group' -or $node.LocalName -eq 'file') {
        $groupName = $node.properties.name
        $tags+=$groupName
        $currNode = $node.properties.NextSibling
        while ($currNode) {
            AddServers -node $currNode -tags $tags -csvPath $csvPath
            $currNode = $currNode.NextSibling
        }
    } 
    else {
        # Node type isn't relevant to tagging or adding connections in WAC
    }
    return
   }

   <#
   .SYNOPSIS
   Convert an .rdg file from Remote Desktop Connection Manager into a .csv that can be imported into Windows Admin Center, maintaining groups via server tags. This will not modify the existing .rdg file and will create a new .csv file

    .DESCRIPTION
    This converts an .rdg file into a .csv that can be imported into Windows Admin Center.

    .PARAMETER RDGfilepath
    The path of the .rdg file to be converted. This file will not be modified, only read.

    .PARAMETER CSVdirectory
    Optional. The directory you wish to export the new .csv file. If not provided, the new file is created in the same directory as the .rdg file.

    .EXAMPLE
    C:\PS> RdgToWacCsv -RDGfilepath "rdcmangroup.rdg"
    #>
   function RdgToWacCsv {
    param(
        [Parameter(Mandatory = $true)]
        [String]
        $RDGfilepath,
        [Parameter(Mandatory = $false)]
        [String]
        $CSVdirectory
    )
    [xml]$RDGfile = Get-Content -Path $RDGfilepath
    $node = $RDGfile.RDCMan.file
    if (!$CSVdirectory){
        $csvPath = [System.IO.Path]::GetDirectoryName($RDGfilepath) + [System.IO.Path]::GetFileNameWithoutExtension($RDGfilepath) + "_WAC.csv"
    } else {
        $csvPath = $CSVdirectory + [System.IO.Path]::GetFileNameWithoutExtension($RDGfilepath) + "_WAC.csv"
    }
    New-item -Path $csvPath
    Add-Content -Path $csvPath -Value '"name","type","tags"'
    AddServers -node $node -csvPath $csvPath
    Write-Host "Converted $RDGfilepath `nOutput: $csvPath"
   }
   ```

2. 만들 수는 있습니다. CSV 파일에서 다음 명령을 실행 합니다.

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 결과 가져옵니다. 모든 RDCMan 그룹화 계층 구조 및 CSV 파일에 Windows Admin Center를 태그로 연결 목록에 표시 됩니다. 자세한 내용은 [가져오기 / 내보내기 (태그로)에 연결 하려면 PowerShell을 사용 하 여](#use-powershell-to-import-or-export-your-connections-with-tags)참조 하세요.

## Windows Admin Center에서 사용 되는 PowerShell 스크립트 보기

서버, 클러스터, 또는 PC에 연결한 후를 볼 수 있습니다 PowerShell 스크립트 전원을 사용할 수 있는 UI 작업 Windows 관리 센터에서. 도구를 내에서 응용 프로그램 위쪽 표시줄에 PowerShell 아이콘을 클릭 합니다. 해당 PowerShell 스크립트를 탐색할 수 드롭다운 목록에서 원하는 명령을 선택 합니다.

![](../media/launch/showscript.png)