---
ms.assetid: 56fc7f80-9558-467e-a6e9-a04c9abbee33
title: 오류 도메인 인식
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-failover-clustering
ms.topic: article
author: cosmosdarwin
ms.date: 09/16/2016
ms.openlocfilehash: 4e42333ecc80ab7401b6e39151377baa86dcf190
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827756"
---
# <a name="fault-domain-awareness"></a>오류 도메인 인식

> 적용 대상: Windows Server 2019 및 Windows Server 2016

장애 조치(failover) 클러스터링을 사용하면 여러 서버가 함께 작동하여 고가용성을 제공하거나, 또 다른 방식으로 노드 내결함성을 제공할 수 있습니다. 하지만 오늘날의 기업은 인프라에서 더 높은 가용성을 요구 합니다. 클라우드와 같은 가동 시간을 달성하려면 섀시 고장, 랙 가동 중단 또는 자연 재해와 같은 발생할 가능성이 거의 없는 사고로부터 보호해야 합니다. Windows Server 2016의 장애 조치 (Failover) 클러스터링에는 섀시, 랙 및 사이트 내결함성도 도입 되었습니다.

## <a name="fault-domain-awareness"></a>오류 도메인 인식

장애 도메인과 내결함성을 매우 밀접한 관련이 있는 개념입니다. 장애 도메인은 단일 실패 지점을 공유하는 하드웨어 구성 요소 집합입니다. 특정 수준까지 결함에 견디려면 해당 수준에 여러 장애 도메인이 필요합니다. 예를 들어 랙 내결함성을 위해서는 서버와 데이터를 여러 랙에 분산시켜야 합니다.

이 짧은 비디오에서는 Windows Server 2016의 장애 도메인에 대 한 개요를 제공 합니다.  
[![이 이미지를 클릭 하면 Windows Server 2016의 장애 도메인에 대 한 개요를 볼 수 있습니다.](media/Fault-Domains-in-Windows-Server-2016/Part-1-Fault-Domains-Overview.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-1-Overview)

### <a name="fault-domain-awareness-in-windows-server-2019"></a>Windows Server 2019의 장애 도메인 인식

장애 도메인 인식은 Windows Server 2019에서 사용할 수 있지만 기본적으로 사용 하지 않도록 설정 되어 있으며 Windows 레지스트리를 통해 사용 하도록 설정 해야 합니다.

Windows Server 2019에서 오류 도메인 인식을 사용 하도록 설정 하려면 Windows 레지스트리로 이동 하 여 (hyper-v)를 설정 합니다. AutoAssignNodeSite 레지스트리 키를 1로 입력 합니다.

```Registry
    (Get-Cluster).AutoAssignNodeSite=1
```

Windows 2019에서 오류 도메인 인식을 사용 하지 않도록 설정 하려면 Windows 레지스트리로 이동 하 여 (hyper-v)를 설정 합니다. AutoAssignNodeSite 레지스트리 키를 0으로 입력 합니다.

```Registry
    (Get-Cluster).AutoAssignNodeSite=0
```

## <a name="benefits"></a>이점
- **스토리지 공간 다이렉트를 포함 한 저장소 공간은 장애 도메인을 사용 하 여 데이터 안전을 최대화 합니다.**  
    저장소 공간의 복원력은 분산된 소프트웨어 정의 RAID와 개념적으로 유사합니다. 모든 데이터의 여러 복사본이 동기화된 상태로 유지되므로 하드웨어가 실패하고 하나의 복사본이 손실된 경우 나머지 복사본을 다시 복사하여 복원력을 복원할 수 있습니다. 최상의 복원력을 달성하려면 복사본을 별도의 장애 도메인에 보관해야 합니다.

- **[상태 관리 서비스](health-service-overview.md) 는 장애 도메인을 사용 하 여 더 유용한 경고를 제공 합니다.**  
    각 장애 도메인을 위치 메타데이터와 연결하여 이후의 모든 경고에 자동으로 포함할 수 있습니다. 이러한 설명자는 운영 또는 유지 관리 담당자를 지원하고 하드웨어를 명확히 구분하여 오류를 줄일 수 있습니다.  

- **스트레치 클러스터링은 저장소 선호도에 장애 도메인을 사용 합니다.** 확장 클러스터링을 사용하면 멀리 떨어진 서버를 공통 클러스터에 가입시킬 수 있습니다. 최상의 성능을 위해 응용 프로그램 또는 가상 컴퓨터는 해당 스토리지를 제공하는 서버에 인접한 서버에서 실행되어야 합니다. 장애 도메인 인식을 통해이 저장소 선호도를 사용할 수 있습니다.   

## <a name="levels-of-fault-domains"></a>장애 도메인 수준  
장애 도메인에는 네 가지 정식 수준(사이트, 랙, 섀시 및 노드)이 있습니다. 노드는 자동으로 검색되며 각 추가 수준은 선택 사항입니다. 예를 들어 배포에서 블레이드 서버를 사용하지 않는 경우 섀시 수준이 의미가 없을 수 있습니다.  

![다양 한 수준의 장애 도메인에 대 한 다이어그램](media/Fault-Domains-in-Windows-Server-2016/levels-of-fault-domains.png)

## <a name="usage"></a>사용법  
PowerShell 또는 XML 태그를 사용 하 여 장애 도메인을 지정할 수 있습니다. 두 방법 모두 동일하며 전체 기능을 제공합니다.

>[!IMPORTANT]
> 가능한 경우 저장소 공간 다이렉트를 사용하기 전에 장애 도메인을 지정합니다. 그러면 섀시 또는 랙 내결함성을 위한 풀, 계층 및 설정(예: 복원력 및 열 개수) 준비가 자동으로 구성됩니다. 풀 및 볼륨을 만든 후에는 장애 도메인 토폴로지 변경에 대한 응답으로 데이터가 소급적으로 이동하지 않습니다. 저장소 공간 다이렉트를 사용하도록 설정한 후 섀시 또는 랙 간에 노드를 이동하려면 먼저 `Remove-ClusterNode -CleanUpDisks`를 사용하여 노드와 해당 드라이브를 풀에서 제거해야 합니다.

### <a name="defining-fault-domains-with-powershell"></a>PowerShell을 사용 하 여 장애 도메인 정의
Windows Server 2016에는 장애 도메인을 사용 하는 다음과 같은 cmdlet이 도입 되었습니다.
* `Get-ClusterFaultDomain`
* `Set-ClusterFaultDomain`
* `New-ClusterFaultDomain` 
* `Remove-ClusterFaultDomain`

이 짧은 비디오에서는 이러한 cmdlet의 사용 방법을 보여 줍니다.
[클러스터 장애 도메인 cmdlet을 사용 하는 방법에 대 한 짧은 비디오를 시청 하려면이 이미지를 클릭 ![합니다.](media/Fault-Domains-in-Windows-Server-2016/Part-2-Using-PowerShell.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-2-Using-PowerShell)

`Get-ClusterFaultDomain`를 사용 하 여 현재 장애 도메인 토폴로지를 확인 합니다. 사용자가 만든 모든 섀시, 랙 또는 사이트와 함께 클러스터의 모든 노드가 나열됩니다. **-Type** 또는 **-Name**과 같은 매개 변수를 사용하여 필터링할 수 있지만 이는 필수 사항은 아닙니다.

```PowerShell
Get-ClusterFaultDomain
Get-ClusterFaultDomain -Type Rack
Get-ClusterFaultDomain -Name "server01.contoso.com"
```

`New-ClusterFaultDomain`를 사용 하 여 새 섀시, 랙 또는 사이트를 만들 수 있습니다. `-Type` 및 `-Name` 매개 변수가 필요 합니다. `-Type`에 사용할 수 있는 값은 `Chassis`, `Rack`및 `Site`입니다. `-Name`는 임의의 문자열일 수 있습니다. `Node` 형식 오류 도메인의 경우 이름은 자동으로 설정 된 실제 노드 이름 이어야 합니다.

```PowerShell
New-ClusterFaultDomain -Type Chassis -Name "Chassis 007"
New-ClusterFaultDomain -Type Rack -Name "Rack A"
New-ClusterFaultDomain -Type Site -Name "Shanghai"
```

> [!IMPORTANT]  
> Windows Server는 생성 하는 장애 도메인이 실제 세계의 모든 항목에 해당 하는지 여부를 확인할 수 없습니다. 이는 명확 하 게 들리지만 이해 하는 것이 중요 합니다. 실제 세계에서 노드가 모두 하나의 랙에 있는 경우 소프트웨어에서 두 개의 `-Type Rack` 장애 도메인을 만들면 랙 내결함성을 제공 하지 않습니다. 따라서 사용자는 이러한 cmdlet을 사용하여 만든 토폴로지가 하드웨어의 실제 배열과 일치하는지 확인해야 합니다.

`Set-ClusterFaultDomain`를 사용 하 여 장애 도메인 하나를 다른 장애 도메인으로 이동 합니다. "부모" 및 "자식"이라는 용어는 이러한 중첩 관계를 설명하는 데 자주 사용됩니다. `-Name` 및 `-Parent` 매개 변수가 필요 합니다. `-Name`에서 이동 하는 장애 도메인의 이름을 제공 합니다. `-Parent`에서 대상의 이름을 제공 합니다. 여러 장애 도메인을 한 번에 이동하려면 해당 이름을 나열합니다.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent "Rack A"
Set-ClusterFaultDomain -Name "Rack A", "Rack B", "Rack C", "Rack D" -Parent "Shanghai"
```

> [!IMPORTANT]  
> 장애 도메인을 이동하면 해당 자식이 함께 이동합니다. 위 예에서 Rack A가 server01.contoso.com의 부모인 경우 후자를 별도로 Shanghai 사이트로 이동할 필요가 없습니다. 실제와 마찬가지로 해당 부모가 그곳에 있기 때문에 이미 그곳에 있습니다.

`Get-ClusterFaultDomain`출력의 `ParentName` 및 `ChildrenNames` 열에서 부모-자식 관계를 볼 수 있습니다.

`Set-ClusterFaultDomain`를 사용 하 여 장애 도메인의 특정 속성을 수정할 수도 있습니다. 예를 들어 장애 도메인에 대 한 선택적 `-Location` 또는 `-Description` 메타 데이터를 제공할 수 있습니다. 이 정보를 제공하면 상태 관리 서비스의 하드웨어 경고에 포함됩니다. `-NewName` 매개 변수를 사용 하 여 장애 도메인의 이름을 바꿀 수도 있습니다. `Node` 형식 장애 도메인의 이름을 바꾸지 마십시오.

```PowerShell
Set-ClusterFaultDomain -Name "Rack A" -Location "Building 34, Room 4010"
Set-ClusterFaultDomain -Type Node -Description "Contoso XYZ Server"
Set-ClusterFaultDomain -Name "Shanghai" -NewName "China Region"
```

`Remove-ClusterFaultDomain`를 사용 하 여 만든 섀시, 랙 또는 사이트를 제거 합니다. `-Name` 매개 변수는 필수입니다. 자식을 포함 하는 장애 도메인은 제거할 수 없습니다. 먼저 자식을 제거 하거나 `Set-ClusterFaultDomain`를 사용 하 여 외부로 이동 합니다. 장애 도메인을 다른 모든 장애 도메인 밖으로 이동 하려면 해당 `-Parent`을 빈 문자열 ("")로 설정 합니다. `Node` 유형 장애 도메인은 제거할 수 없습니다. 여러 장애 도메인을 한 번에 제거하려면 해당 이름을 나열합니다.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent ""
Remove-ClusterFaultDomain -Name "Rack A"
```

### <a name="defining-fault-domains-with-xml-markup"></a>XML 태그를 사용하여 장애 도메인 정의
XML 기반 구문을 사용하여 장애 도메인을 지정할 수 있습니다. 자주 사용하는 텍스트 편집기(예: Visual Studio Code( *[여기](https://code.visualstudio.com/)* 에서 무료로 제공) 또는 메모장)를 사용하여 XML 문서를 만들어 저장하고 재사용할 수 있습니다.  

이 짧은 비디오에서는 XML 태그를 사용하여 장애 도메인을 지정하는 방법을 보여 줍니다.

[이 이미지 ![XML을 사용 하 여 장애 도메인을 지정 하는 방법에 대 한 짧은 비디오를 시청 하세요.](media/Fault-Domains-in-Windows-Server-2016/Part-3-Using-XML-Markup.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-3-Using-XML)

PowerShell에서 다음 cmdlet을 실행 합니다. `Get-ClusterFaultDomainXML`. 클러스터의 현재 장애 도메인 사양이 XML로 반환됩니다. 이는 검색 된 모든 `<Node>`를 반영 하 여 여는 태그와 닫는 `<Topology>` 태그로 래핑됩니다.  

이 출력을 파일에 저장하려면 다음을 실행합니다.  

```PowerShell
Get-ClusterFaultDomainXML | Out-File <Path>  
```

파일을 열고 `<Site>`, `<Rack>`및 `<Chassis>` 태그를 추가 하 여 사이트, 랙 및 섀시에 이러한 노드를 배포 하는 방법을 지정 합니다. 모든 태그는 고유한 **Name**으로 식별되어야 합니다. 노드의 경우 노드 이름을 기본적으로 채워진 대로 유지해야 합니다.  

> [!IMPORTANT]  
> 모든 추가 태그는 선택 사항이지만 전이적 Site &gt; Rack &gt; Chassis &gt; Node 계층을 준수해야 하며, 적절히 닫혀야 합니다.  
이름 외에도 자유형 `Location="..."` 및 `Description="..."` 설명자를 태그에 추가할 수 있습니다.  

#### <a name="example-two-sites-one-rack-each"></a>예: 두 개의 사이트, 각각 하나의 랙  

```XML
<Topology>  
  <Site Name="SEA" Location="Contoso HQ, 123 Example St, Room 4010, Seattle">  
    <Rack Name="A01" Location="Aisle A, Rack 01">  
      <Node Name="Server01" Location="Rack Unit 33" />  
      <Node Name="Server02" Location="Rack Unit 35" />  
      <Node Name="Server03" Location="Rack Unit 37" />  
    </Rack>  
  </Site>  
  <Site Name="NYC" Location="Regional Datacenter, 456 Example Ave, New York City">  
    <Rack Name="B07" Location="Aisle B, Rack 07">  
      <Node Name="Server04" Location="Rack Unit 20" />  
      <Node Name="Server05" Location="Rack Unit 22" />  
      <Node Name="Server06" Location="Rack Unit 24" />  
    </Rack>  
  </Site>  
</Topology> 
``` 

#### <a name="example-two-chassis-blade-servers"></a>예: 두 개의 섀시, 블레이드 서버  
```XML
<Topology>  
  <Rack Name="A01" Location="Contoso HQ, Room 4010, Aisle A, Rack 01">  
    <Chassis Name="Chassis01" Location="Rack Unit 2 (Upper)" >  
      <Node Name="Server01" Location="Left" />  
      <Node Name="Server02" Location="Right" />  
    </Chassis>  
    <Chassis Name="Chassis02" Location="Rack Unit 6 (Lower)" >  
      <Node Name="Server03" Location="Left" />  
      <Node Name="Server04" Location="Right" />  
    </Chassis>  
  </Rack>  
</Topology>  
```

새 장애 도메인 사양을 설정 하려면 XML을 저장 하 고 PowerShell에서 다음을 실행 합니다.  

```PowerShell
$xml = Get-Content <Path> | Out-String  
Set-ClusterFaultDomainXML -XML $xml
```

이 가이드에서는 두 가지 예만 제공 하지만 `<Site>`, `<Rack>`, `<Chassis>`및 `<Node>` 태그를 여러 가지 방법으로 혼합 하 고 일치 시켜 배포의 실제 토폴로지를 반영할 수 있습니다. 위 예에서는 이러한 태그의 유연성과 이러한 태그를 명확히 구분하는 자유형 위치 설명자의 가치를 보여드리려 했습니다.  

### <a name="optional-location-and-description-metadata"></a>선택 사항: 위치 및 설명 메타 데이터

장애 도메인에 대 한 선택적 **위치** 또는 **설명** 메타 데이터를 제공할 수 있습니다. 이 정보를 제공하면 상태 관리 서비스의 하드웨어 경고에 포함됩니다. 이 짧은 비디오에서는 이러한 설명자를 추가 하는 값을 보여 줍니다.

[![장애 도메인에 위치 설명자를 추가 하는 값을 보여 주는 짧은 비디오를 보려면 클릭 하세요.](media/Fault-Domains-in-Windows-Server-2016/part-4-location-description.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-4-Location-Description)

## <a name="see-also"></a>관련 항목  
- [Windows Server 2019 시작](https://docs.microsoft.com/windows-server/get-started-19/get-started-19)  
- [Windows Server 2016 시작](https://docs.microsoft.com/windows-server/get-started/server-basics)  
-   [스토리지 공간 다이렉트 개요](../storage/storage-spaces/storage-spaces-direct-overview.md) 
