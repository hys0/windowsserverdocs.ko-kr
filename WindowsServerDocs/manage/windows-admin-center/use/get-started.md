---
title: Windows Admin Center 시작
description: Windows Admin Center 시작
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 02/15/2019
ms.openlocfilehash: bd35e439ee3c76af1306bbbd712d754dd79f555f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446093"
---
# <a name="get-started-with-windows-admin-center"></a>Windows Admin Center 시작

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows 10에 설치 된 Windows Admin Center

> [!IMPORTANT]
> Windows 10에서 Windows Admin Center 사용 하려면 로컬 관리자 그룹의 구성원 이어야 합니다.

### <a name="selecting-a-client-certificate"></a>클라이언트 인증서를 선택합니다.

Windows 10에서 Windows Admin Center 열면 처음으로 선택 되어 있는지 확인 합니다 *Windows Admin Center 클라이언트* (그렇지 않은 경우 얻게 "이이 페이지를 가져올 수 없습니다" 라는 HTTP 403 오류가) 인증서입니다.

Microsoft edge에서는이 대화 상자를 사용 하 여 메시지가 표시 되는 경우:
 
1. 클릭 **다른 옵션 선택**

    ![](../media/launch-cert-1.png)

2. 레이블이 지정 된 인증서를 선택 **Windows Admin Center 클라이언트** 를 클릭 하 고 **확인**

    ![](../media/launch-cert-2.png)

3. 했는지 **액세스를 항상 허용** 선택한 클릭 **허용**

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>관리 되는 노드 및 클러스터에 연결

Windows Admin Center 설치를 완료 한 후에 서버 또는 기본 개요 페이지에서 관리 하는 클러스터를 추가할 수 있습니다.

 **단일 서버 또는 클러스터를 관리 노드로 추가**

1. 클릭 **+ 추가** 아래에서 **모든 연결**합니다.

   ![](../media/launch/addserver0.png)

2. 서버, 장애 조치 클러스터 또는 Hyper-Converged 클러스터 연결을 추가 하려면 선택 합니다.
    
   ![](../media/launch/addserver1.png)

3. 서버 또는 관리 하 고 클릭 하는 클러스터의 이름을 입력 **제출**합니다. 서버 또는 클러스터의 개요 페이지에서 연결 목록에 추가 됩니다.

   ![](../media/launch/addserver2.png)

   **-- OR --**

**대량 여러 서버 가져오기**

 1. 에 **서버 연결 추가** 페이지를 선택 합니다 **가져오기 서버** 탭 합니다.

    ![](../media/launch/import-servers.png)

 2. 클릭 **찾아보기** 쉼표를 포함 하는 텍스트 파일을 선택 하거나 새 줄으로 구분 된 추가 하려는 서버에 대 한 Fqdn의 목록입니다.

    **-- OR --**

**Active Directory를 검색 하 여 서버를 추가 합니다.**

 1. 에 **서버 연결 추가** 페이지를 선택 합니다 **Active Directory 검색** 탭 합니다.

    ![](../media/launch/search-ad.png)

 2. 검색 조건을 입력 하 고 클릭 **검색**합니다. 와일드 카드 (*)가 지원 됩니다.

 3. 검색 완료-선택 결과 중 하나 이상을, 필요에 따라 태그를 추가 하 고 클릭 **추가**합니다.

## <a name="authenticate-with-the-managed-node"></a>관리 되는 노드를 사용 하 여 인증 ##

Windows Admin Center 관리 되는 노드를 사용 하 여 인증에 대 한 몇 가지 메커니즘을 지원 합니다. Single sign on 기본값입니다.

**Single sign-on**

관리 되는 노드를 사용 하 여 인증을 현재 Windows 자격 증명을 사용할 수 있습니다. 이 기본값이 며 서버를 추가 하면 Windows Admin Center 로그온 시도 합니다. 

**Single sign on Windows Server에 서비스로 배포 하는 경우**

Windows Server에서 Windows Admin Center 설치한 경우 추가 구성은 필요 single sign on에 대 한 합니다.  [위임 위한 환경 구성](../configure/user-access-control.md)

**-- OR --**

**사용 하 여 *으로 관리* 자격 증명 지정 하려면**

아래 **모든 연결**, 목록에서 서버를 선택 하 고 선택 **으로 관리** 를 관리 노드로 인증에 사용할 자격 증명을 지정 합니다.

![](../media/launch-use-6.png)

Windows Server에서 Windows Admin Center 서비스 모드에서 실행 중인 하지만 Kerberos 위임이 구성 되어 있지 않은 경우 Windows 자격 증명을 다시 입력 해야 합니다.

![](../media/launch-use-7.png)

해당 특정 브라우저 세션에 대 한 캐시는 모든 연결에 자격 증명을 적용할 수 있습니다. 다시 입력 해야 브라우저를 다시 로드 하는 경우에 **으로 관리** 자격 증명입니다.

**로컬 관리자 암호 솔루션 (랩)**

환경에서 사용 하는 경우 [LAPS](https://technet.microsoft.com/mt227395.aspx), 및 Windows 10 PC에 설치 된 Windows Admin Center LAPS 자격 증명을 사용 하 여 관리 되는 노드를 사용 하 여 인증 합니다. **이 시나리오를 사용 하세요** [의견](http://aka.ms/WACFeedback)합니다.

## <a name="using-tags-to-organize-your-connections"></a>태그를 사용 하 여 연결을 구성할 수

태그를 식별 하 여 관련 된 서버 연결 목록에서 필터링에 사용할 수 있습니다.  이 옵션을 사용 하면 연결 목록에서 서버의 하위 집합을 볼 수 있습니다.  많은 연결이 있는 경우 특히 유용 합니다.

### <a name="edit-tags"></a>태그 편집

* 모든 연결 목록에서 서버 또는 여러 서버를 선택 합니다.
* 아래 **모든 연결은**, 클릭 **태그 편집**

![](../media/launch/tags-5.png)

합니다 **연결 태그 편집** 창 수정, 추가 또는 사용자 선택 된 연결에서 태그를 제거할 수 있습니다.

* 선택에 선택 된 연결에 새 태그를 추가 하려면 **태그를 추가** 사용 하려는 태그 이름을 입력 합니다.

* 기존 태그 이름 사용 하 여 선택한 연결 태그를 적용할 태그 이름 옆의 확인란을 선택 합니다.

* 선택한 모든 연결에서 태그를 제거 하려면 제거 하려는 태그 옆의 확인란의 선택을 취소 합니다.

* 태그는 선택된 된 연결의 하위 집합에 적용 되는 경우 확인란 중간 상태에 표시 됩니다. 확인 하 고 모든 선택한 연결에 태그를 적용 하거나 선택 취소 하 고 모든 선택한 연결에서 태그를 제거 하려면 다시 클릭 하 여 상자 클릭 수 있습니다.

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>태그 필터 연결

하나 이상의 서버 연결에 태그를 추가한 후에 연결 목록에 태그를 볼 수 있으며 태그로 연결 목록을 필터링 할 수 있습니다.

* 태그로 필터링 하려면 검색 상자 옆에 있는 필터 아이콘을 선택 합니다.
![](../media/launch/tags-7.png)
* 선택할 수 있습니다 "또는", "및" 또는 "not" 선택한 태그의 필터 동작을 수정 합니다.
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>PowerShell을 사용 하 여 가져오기 또는 내보내기 (태그)로 연결

> 적용 대상: Windows Admin Center 미리 보기

Windows Admin Center 미리 보기 PowerShell 모듈을 가져오기 또는 내보내기 연결 목록에 포함 됩니다.

```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to .csv files
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
```

### <a name="csv-file-format-for-importing-connections"></a>연결을 가져오기 위한 CSV 파일 형식

CSV 파일의 형식은 4 개의 머리글과 함께 시작 ```"name","type","tags","groupId"```고 뒤에 새 줄에 각 연결 합니다.

**이름** 은 연결의 FQDN

**형식** 연결 형식입니다. Windows Admin Center 포함 된 기본 연결에 다음 중 하나를 사용할 수 있습니다.

| 연결 형식 | 연결 문자열 |
|------|-------------------------------|
| Windows Server | msft.sme.connection-type.server |
| Windows 10 PC | msft.sme.connection-type.windows-client |
| 장애 조치(failover) 클러스터 | msft.sme.connection-type.cluster |
| 하이퍼 수렴 형 클러스터 | msft.sme.connection-type.hyper-converged-cluster |

**태그** 파이프 구분 됩니다.

**groupId** 공유 연결에 사용 됩니다. 값을 사용 하 여 ```global``` 이 공유 연결을 설정 하려면이 열에 있습니다.

### <a name="example-csv-file-for-importing-connections"></a>연결 가져오기에 대 한 예제 CSV 파일

```
"name","type","tags","groupId"
"myServer.contoso.com","msft.sme.connection-type.server","hyperv"
"myDesktop.contoso.com","msft.sme.connection-type.windows-client","hyperv"
"teamcluster.contoso.com","msft.sme.connection-type.cluster","legacyCluster|WS2016","global"
"myHCIcluster.contoso.com,"msft.sme.connection-type.hyper-converged-cluster","myHCIcluster|hyperv|JIT|WS2019"
"teamclusterNode.contoso.com","msft.sme.connection-type.server","legacyCluster|WS2016","global"
"myHCIclusterNode.contoso.com","msft.sme.connection-type.server","myHCIcluster|hyperv|JIT|WS2019"
```

## <a name="import-rdcman-connections"></a>가져오기 RDCman 연결

아래 스크립트를 사용 하 여 저장 된 연결을 내보내려면 [RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) 파일로. 가져올 수 있습니다 파일 Windows Admin Center 태그를 사용 하 여 RDCMan 그룹화 계층 유지 관리 합니다. 사용해 보세요!

1. 복사 하 여 PowerShell 세션에 아래 코드를 붙여넣습니다.

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

2. 만들려는 합니다. CSV 파일에서 다음 명령을 실행 합니다.

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 결과 가져옵니다. CSV 파일에서 Windows Admin Center 및 모든 RDCMan 그룹화 계층 연결 목록에서 태그로 표시 됩니다. 세부 정보를 참조 하세요 [가져오기 및 내보내기 (태그)로 연결 하려면 PowerShell을 사용 하 여](#use-powershell-to-import-or-export-your-connections-with-tags)입니다.

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Windows Admin Center 사용 되는 PowerShell 스크립트 보기

서버, 클러스터 또는 PC를 연결한 후 수 보면 PowerShell 스크립트를 구동 하는 사용 가능한 UI 작업 Windows Admin Center. 도구를 응용 프로그램 위쪽 표시줄에서 PowerShell 아이콘을 클릭 합니다. 해당 PowerShell 스크립트를 이동할 드롭다운 목록에서 관심 명령을 선택 합니다.

![](../media/launch/showscript.png)