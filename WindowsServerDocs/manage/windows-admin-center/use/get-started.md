---
title: Windows 관리 센터 시작
description: Windows 관리 센터 시작
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 02/15/2019
ms.openlocfilehash: fac17cd5975eeb699f205888edbe3f1c30b43394
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567145"
---
# <a name="get-started-with-windows-admin-center"></a>Windows 관리 센터 시작

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="windows-admin-center-installed-on-windows-10"></a>Windows 10에 설치 된 windows 관리 센터

> [!IMPORTANT]
> Windows 10에서 Windows 관리 센터를 사용 하려면 로컬 관리자 그룹의 구성원 이어야 합니다.

### <a name="selecting-a-client-certificate"></a>클라이언트 인증서 선택

Windows 10에서 windows 관리 센터를 처음 열 때 *Windows 관리 센터 클라이언트* 인증서를 선택 해야 합니다. 그렇지 않으면 "이 페이지로 이동할 수 없습니다." 라는 HTTP 403 오류가 발생 합니다.

Microsoft Edge에서이 대화 상자가 표시 되 면 다음을 수행 합니다.
 
1. **추가 선택 항목** 을 클릭 합니다.

    ![](../media/launch-cert-1.png)

2. **Windows 관리 센터 클라이언트** 라는 레이블이 지정 된 인증서를 선택 하 고 **확인을** 클릭 합니다.

    ![](../media/launch-cert-2.png)

3. **항상 액세스 허용** 이 선택 되어 있는지 확인 하 고 **허용** 을 클릭 합니다.

    ![](../media/launch-cert-3.png)

## <a name="connecting-to-managed-nodes-and-clusters"></a>관리 되는 노드 및 클러스터에 연결

Windows 관리 센터 설치를 완료 한 후에는 기본 개요 페이지에서 관리할 서버 또는 클러스터를 추가할 수 있습니다.

 **단일 서버 또는 클러스터를 관리 노드로 추가**

1. **모든 연결**에서 **+ 추가** 를 클릭 합니다.

   ![](../media/launch/addserver0.png)

2. 서버, 클러스터, Windows PC 또는 Azure VM을 추가 하도록 선택 합니다.
    
   ![](../media/launch/ChooseConnectionType.png)

3. 관리할 서버 또는 클러스터의 이름을 입력 하 고 **제출**을 클릭 합니다. 서버 또는 클러스터가 개요 페이지의 연결 목록에 추가 됩니다.

   ![](../media/launch/addserver2.png)

   **--또는--**

**여러 서버 대량 가져오기**

 1. **서버 연결 추가** 페이지에서 **서버 가져오기** 탭을 선택 합니다.

    ![](../media/launch/import-servers.png)

 2. **찾아보기** 를 클릭 하 고 추가 하려는 서버에 대 한 쉼표 또는 쉼표로 구분 된 새 줄을 포함 하는 텍스트 파일을 선택 합니다.

> [!Note]
> [PowerShell을 사용](#use-powershell-to-import-or-export-your-connections-with-tags) 하 여 연결을 내보내 만든 .csv 파일에는 서버 이름 이외에 추가 정보가 포함 되어 있으며이 가져오기 방법과 호환 되지 않습니다.

  **--또는--**

**Active Directory 검색 하 여 서버 추가**

 1. **서버 연결 추가** 페이지에서 **검색 Active Directory** 탭을 선택 합니다.

    ![](../media/launch/search-ad.png)

 2. 검색 조건을 입력 하 고 **검색**을 클릭 합니다. 와일드 카드 (*)를 사용할 수 있습니다.

 3. 검색이 완료 되 면 하나 이상의 결과를 선택 하 고 필요에 따라 태그를 추가 하 고 **추가**를 클릭 합니다.

## <a name="authenticate-with-the-managed-node"></a>관리 노드를 사용 하 여 인증 ##

Windows 관리 센터는 관리 되는 노드로 인증 하기 위한 여러 메커니즘을 지원 합니다. Single sign-on이 기본값입니다.

**Single Sign-on**

현재 Windows 자격 증명을 사용 하 여 관리 되는 노드에 인증할 수 있습니다. 이는 기본값 이며, Windows 관리 센터에서 서버를 추가할 때 로그온을 시도 합니다. 

**Windows Server에 서비스로 배포 된 경우 Single sign-on**

Windows Server에 Windows 관리 센터를 설치한 경우 Single Sign-On 하려면 추가 구성이 필요 합니다.  [위임할 환경 구성](../configure/user-access-control.md)

**--또는--**

**다음 *으로 관리* 를 사용 하 여 자격 증명 지정**

**모든 연결**아래의 목록에서 서버를 선택 하 고 다음 **으로 관리** 를 선택 하 여 관리 되는 노드에 인증 하는 데 사용할 자격 증명을 지정 합니다.

![](../media/launch-use-6.png)

Windows 관리 센터에서 windows Server의 서비스 모드로 실행 중이지만 Kerberos 위임이 구성 되지 않은 경우 Windows 자격 증명을 다시 입력 해야 합니다.

![](../media/launch-use-7.png)

모든 연결에 자격 증명을 적용할 수 있습니다. 그러면 해당 특정 브라우저 세션에 대 한 자격 증명을 캐시 합니다. 브라우저를 다시 로드 하는 경우 **관리** 자격 증명을 다시 입력 해야 합니다.

**로컬 관리자 암호 솔루션 (LAPS)**

환경에서 [LAPS](https://technet.microsoft.com/mt227395.aspx)를 사용 하 고 WINDOWS 10 PC에 Windows 관리 센터를 설치한 경우 LAPS 자격 증명을 사용 하 여 관리 되는 노드로 인증할 수 있습니다. **이 시나리오를 사용 하는 경우 피드백을 제공 해 주세요** [](https://aka.ms/WACFeedback).

## <a name="using-tags-to-organize-your-connections"></a>태그를 사용 하 여 연결 구성

태그를 사용 하 여 연결 목록에서 관련 서버를 식별 하 고 필터링 할 수 있습니다.  이렇게 하면 연결 목록에서 서버의 하위 집합을 볼 수 있습니다.  많은 연결이 있는 경우 특히 유용 합니다.

### <a name="edit-tags"></a>태그 편집

* 모든 연결 목록에서 서버 또는 여러 서버를 선택 합니다.
* **모든 연결**에서 **태그 편집** 을 클릭 합니다.

![](../media/launch/tags-5.png)

**연결 태그 편집** 창을 사용 하 여 선택한 연결에서 태그를 수정, 추가 또는 제거할 수 있습니다.

* 선택한 연결에 새 태그를 추가 하려면 **태그 추가** 를 선택 하 고 사용할 태그 이름을 입력 합니다.

* 선택한 연결에 기존 태그 이름을 표시 하려면 적용 하려는 태그 이름 옆의 확인란을 선택 합니다.

* 선택한 모든 연결에서 태그를 제거 하려면 제거할 태그 옆에 있는 확인란의 선택을 취소 합니다.

* 선택한 연결의 하위 집합에 태그를 적용 하는 경우에는 확인란이 중간 상태로 표시 됩니다. 확인란을 클릭 하 여 선택한 모든 연결에 태그를 적용 하 고 적용 하거나 다시 클릭 하 여 선택을 취소 하 고 선택한 모든 연결에서 태그를 제거할 수 있습니다.

![](../media/launch/tags-6.png)

### <a name="filter-connections-by-tag"></a>태그별로 연결 필터링

하나 이상의 서버 연결에 태그를 추가한 후에는 연결 목록에서 태그를 보고 태그를 기준으로 연결 목록을 필터링 할 수 있습니다.

* 태그를 기준으로 필터링 하려면 검색 상자 옆에 있는 필터 아이콘을 선택 합니다.
![](../media/launch/tags-7.png)
* "Or", "and" 또는 "not"을 선택 하 여 선택한 태그의 필터 동작을 수정할 수 있습니다.
![](../media/launch/tags-8.png)

## <a name="use-powershell-to-import-or-export-your-connections-with-tags"></a>PowerShell을 사용 하 여 연결 가져오기 또는 내보내기 (태그 포함)

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

CSV 파일의 형식은 ```"name","type","tags","groupId"```4 개의 제목으로 시작 하 여 각 연결을 새 줄에 입력 합니다.

**name** 은 연결의 FQDN입니다.

**유형** 은 연결 유형입니다. Windows 관리 센터에 포함 된 기본 연결의 경우 다음 중 하나를 사용 합니다.

| 연결 형식 | 연결 문자열 |
|------|-------------------------------|
| Windows Server | sme-형식. 서버 |
| Windows 10 PC | msft. sme-client |
| 장애 조치(failover) 클러스터 | msft. sme. |
| 하이퍼 수렴 형 클러스터 | msft. sme-수렴-클러스터 |

**태그** 는 파이프로 구분 됩니다.

**groupId** 는 공유 연결에 사용 됩니다. 이 열에 ```global``` 값을 사용 하 여 공유 연결을 만듭니다.

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

## <a name="import-rdcman-connections"></a>RDCman 연결 가져오기

다음 스크립트를 사용 하 여 [Rdcman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/) 의 저장 된 연결을 파일로 내보냅니다. 그런 다음 태그를 사용 하 여 파일을 Windows 관리 센터에 가져와서 RDCMan 그룹화 계층 구조를 유지 관리할 수 있습니다. 사용해 보세요!

1. 아래 코드를 복사 하 여 PowerShell 세션에 붙여 넣습니다.

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

2. 을 만듭니다. CSV 파일에서 다음 명령을 실행 합니다.

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 결과를 가져옵니다. CSV 파일이 Windows 관리 센터에 있고 모든 RDCMan 그룹화 계층 구조가 연결 목록에서 태그로 표시 됩니다. 자세한 내용은 [PowerShell을 사용 하 여 연결 가져오기 또는 내보내기 (태그 사용)](#use-powershell-to-import-or-export-your-connections-with-tags)를 참조 하세요.

## <a name="view-powershell-scripts-used-in-windows-admin-center"></a>Windows 관리 센터에서 사용 되는 PowerShell 스크립트 보기

서버, 클러스터 또는 PC에 연결 하면 Windows 관리 센터에서 사용할 수 있는 UI 작업을 수행 하는 PowerShell 스크립트를 살펴볼 수 있습니다. 도구 내에서 위쪽 응용 프로그램 표시줄의 PowerShell 아이콘을 클릭 합니다. 드롭다운 목록에서 원하는 명령을 선택 하 여 해당 PowerShell 스크립트로 이동 합니다.

![](../media/launch/showscript.png)
