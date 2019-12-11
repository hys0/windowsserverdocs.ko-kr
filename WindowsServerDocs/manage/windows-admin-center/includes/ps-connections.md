```powershell
# Load the module
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ConnectionTools"
# Available cmdlets: Export-Connection, Import-Connection

# Export connections (including tags) to a .csv file
Export-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from a .csv file
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv"
# Import connections (including tags) from .csv files, and remove any connections that are not explictly in the imported file using the -prune switch parameter 
Import-Connection "https://wac.contoso.com" -fileName "WAC-connections.csv" -prune
```
### <a name="csv-file-format-for-importing-connections"></a>연결을 가져오기 위한 CSV 파일 형식

CSV 파일의 형식은 네 개의 제목(```"name","type","tags","groupId"```)으로 시작하고, 그 뒤의 새 줄에 각 연결이 나옵니다.

**name**은 연결의 FQDN입니다.

**type**은 연결 형식입니다. Windows Admin Center에 포함된 기본 연결의 경우 다음 중 하나를 사용합니다.

| 연결 형식 | 연결 문자열 |
|------|-------------------------------|
| Windows Server | msft.sme.connection-type.server |
| Windows 10 PC | msft.sme.connection-type.windows-client |
| 장애 조치(failover) 클러스터 | msft.sme.connection-type.cluster |
| 하이퍼 수렴형 클러스터 | msft.sme.connection-type.hyper-converged-cluster |

**tags**는 파이프로 구분됩니다.

**groupId**는 공유 연결에 사용됩니다. 이 열의 ```global``` 값을 사용하여 해당 열을 공유 연결로 만듭니다.

> [!NOTE]
> 게이트웨이 관리자만 공유 연결을 수정할 수 있으며, 모든 사용자는 PowerShell을 사용하여 자신의 개인 연결 목록을 수정할 수 있습니다.

### <a name="example-csv-file-for-importing-connections"></a>연결을 가져오기 위한 CSV 파일 예제

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

아래 스크립트를 사용하여 [RDCman](https://blogs.technet.microsoft.com/rmilne/2014/11/19/remote-desktop-connection-manager-download-rdcman-2-7/)에 저장된 연결을 파일로 내보냅니다. 그런 다음, 해당 파일을 Windows Admin Center에 가져와서 태그를 사용하여 RDCMan 그룹화 계층 구조를 유지 관리할 수 있습니다. 사용해 보세요!

1. 아래 코드를 복사하여 PowerShell 세션에 붙여넣습니다.

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

2. .CSV 파일을 만들려면 다음 명령을 실행합니다.

   ```powershell
   RdgToWacCsv -RDGfilepath "path\to\myRDCManfile.rdg"
   ```

3. 결과 .CSV 파일을 Windows Admin Center에 가져옵니다. 그러면 모든 RDCMan 그룹화 계층 구조가 연결 목록의 태그로 표시됩니다. 자세한 내용은 [PowerShell을 사용하여 연결 가져오기 또는 내보내기(tags 사용)](#use-powershell-to-import-or-export-your-connections-with-tags)를 참조하세요.