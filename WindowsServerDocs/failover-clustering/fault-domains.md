---
ms.assetid: 56fc7f80-9558-467e-a6e9-a04c9abbee33
title: "오류 도메인 인식"
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-failover-clustering
ms.topic: article
author: cosmosdarwin
ms.date: 09/16/2016
ms.openlocfilehash: f5c64bb8f8b7d4b8d13c76c4e94cfcf52ee32c30
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="fault-domain-awareness-in-windows-server-2016"></a>Windows Server 2016에서 오류 도메인 인식

> 적용: Windows Server 2016

클러스터링 여러 서버를 항상 사용 가능 – 하거나 노드 결함 허용 제공 하기 위해 다른 방법으로 전환 하는 데 사용할 수 있습니다. 하지만 오늘 비즈니스 인프라에서 개가 큰 유용성을 요구 합니다. 구름 모양 가동을 위해 섀시 오류나 랙 중단 자연 장애 처럼 발생 하는 더 높은 거의 로부터 보호 되어야 합니다. 이 때문 랙, 섀시와 사이트 결함 허용도 소개 클러스터링 Windows Server 2016에 있습니다.

오류 도메인 및 결함 허용은 관련된 밀접 하 게 개념입니다. 오류 도메인 단일 실패 한을 공유 하는 하드웨어 구성 요소 집합입니다. 특정 수준으로 허용 오류 되도록 수준에서 여러 오류 도메인 해야 합니다. 예를 들어, 랙 되도록 허용 오류, 서버 및 사용자 데이터 배포 해야 여러 개의 간에 합니다.

이 짧은 동영상 오류 도메인 Windows Server 2016에 간략하게를 설명 합니다.  
[![이 이미지 오류 도메인 Windows Server 2016에 대 한 개요를 시청 하려면 클릭](media/Fault-Domains-in-Windows-Server-2016/Part-1-Fault-Domains-Overview.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-1-Overview)

## <a name="benefits"></a>이점
- **저장소 공간을 포함 하 여 Storage Spaces Direct 데이터 보안을 극대화 하기 오류 도메인을 사용 합니다.**  
    저장소 공간에는 복구 분산, 소프트웨어 정의 RAID 같은 개념입니다. 여러 개 모든 데이터는 동기화, 유지 및 하드웨어 오류가 발생 하는 경우 다른 하나는 손실, 복구를 복원 하려면 recopied 다른 합니다. 최상의 가능한 복구를 위해 별도 오류는 도메인의 복사본을 유지 합니다.

- **[상태 서비스](health-service-overview.md) 결함이 도메인 알아보기 경고를 제공 하기 위해 사용 합니다.**  
    각 오류 도메인 연결 된 위치 메타 데이터를 자동으로 후속 경고에 포함 될 수 있습니다. 이러한 설명자 유지 관리 담당자 또는 작업을 지원 하 고 하드웨어 구체화 하 여 오류를 줄일 수 있습니다.  

- **연장 클러스터링 저장소 선호도 대 한 오류 도메인을 사용합니다.** 벌 리 기 클러스터링 일반적인 클러스터에 가입 떨어진 서버 수 있습니다. 최상의 성능을 응용 프로그램 또는 가상 컴퓨터 근처의 저장소를 제공 하는 서버에 실행 해야 합니다. 오류 도메인 인식이 저장소 선호도 수 있습니다.   

## <a name="levels-of-fault-domains"></a>오류 도메인 수준  
4 개 정식 수준의 오류 도메인-사이트, 랙, 섀시 및 노드 가지가 있습니다. 노드; 자동으로 검색 수준을 선택 사항입니다. 예를 들어, 배포 잎 서버를 사용 하지 않는 경우 섀시 수준 하지 합리적 있습니다.  

![오류 도메인의 여러 수준 다이어그램](media/Fault-Domains-in-Windows-Server-2016/levels-of-fault-domains.png)

## <a name="usage"></a>사용  
PowerShell 또는 XML 태그를 지정 오류 도메인 사용할 수 있습니다. 두 가지 방법을 동일 하 고 전체 기능을 제공 합니다.

>[!IMPORTANT]
> 사용 가능한 경우 Storage Spaces Direct 하기 전에 오류 도메인을 지정 합니다. 이 통해 자동 구성 본체나 랙 결함 허용 풀, 계층을 및 복구 하 고 열 수와 같은 설정을 준비입니다. 풀 및 볼륨을 만든 후 데이터 이동 하지 않습니다은 이전의 변경 내용에 따라에서 오류 도메인 토폴로지 합니다. 노드 본체나 랙 간에 Storage Spaces Direct 사용 하도록 설정한 후을 이동 하려면 해야 먼저를 제거 하면 노드와 사용 하 여 풀에서 드라이브의 `Remove-ClusterNode -CleanUpDisks`합니다.

### <a name="defining-fault-domains-with-powershell"></a>PowerShell 도메인 오류 정의
Windows Server 2016 오류 도메인을 사용 하려면 다음 cmdlet을 가지가 도입 되었습니다.
* `Get-ClusterFaultDomain`
* `Set-ClusterFaultDomain`
* `New-ClusterFaultDomain` 
* `Remove-ClusterFaultDomain`

이 짧은 동영상 이러한 cmdlet 사용 보여 줍니다.
[![클러스터 장애 도메인 cmdlet 사용량 짧은 동영상을 시청 하려면이 이미지를 클릭](media/Fault-Domains-in-Windows-Server-2016/Part-2-Using-PowerShell.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-2-Using-PowerShell)

사용 하 여 `Get-ClusterFaultDomain` 현재 오류 도메인 토폴로지 볼 수 있습니다. 이 모든 노드에서 클러스터에 뿐만 아니라 모든, 걸 본체나 만든 사이트에 나열 됩니다. 같은 매개 변수를 사용 하 여 필터링 할 수 **-유형** 또는 **-이름**, 있지만이 필요 하지 않습니다.

```PowerShell
Get-ClusterFaultDomain
Get-ClusterFaultDomain -Type Rack
Get-ClusterFaultDomain -Name "server01.contoso.com"
```

사용 하 여 `New-ClusterFaultDomain` 새로운 본체나 걸 사이트 만들 수 있습니다. `-Type` 및 `-Name` 매개는 필요 합니다. 가능한 값 `-Type` 는 `Chassis`, `Rack`, 및 `Site`합니다. `-Name` 문자열이 될 수 있습니다. (에 대 한 `Node` 유형 오류가 도메인 이름 자동으로 노드 실제 이름 집합으로 이어야 합니다).

```PowerShell
New-ClusterFaultDomain -Type Chassis -Name "Chassis 007"
New-ClusterFaultDomain -Type Rack -Name "Rack A"
New-ClusterFaultDomain -Type Site -Name "Shanghai"
```

> [!IMPORTANT]  
> Windows Server 수 없으며 만드는 오류 도메인 모든 실제, 실제 세계에서 아무 것도에 해당 하는 확인 하지 않습니다. (이 분명 하 게 보일 수도 있지만 파악 해야 합니다.) 실제 세계에서 노드가 경우 한 랙에 모두, 만드는 두 `-Type Rack` 오류 도메인 소프트웨어가 랙 결함 허용 마술 제공 하지 않습니다. 사용자는 이러한 cmdlet 사용 하 여 만드는 토폴로지 일치 실제 배열을 하드웨어에 대해 책임입니다.

사용 하 여 `Set-ClusterFaultDomain` 한 오류 도메인 다른으로 이동할 수 있습니다. "상위" 및 "자녀가"이 중첩 관계 설명 하기 위해 일반적으로 사용 됩니다. `-Name`및 `-Parent`매개는 필요 합니다. `-Name`, 이동 하는 오류 도메인의 이름을 입력 `-Parent`, 대상의 이름을 입력 합니다. 여러 오류 도메인을 한 번에 이동의 이름을 표시 합니다.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent "Rack A"
Set-ClusterFaultDomain -Name "Rack A", "Rack B", "Rack C", "Rack D" -Parent "Shanghai"
```

> [!IMPORTANT]  
> 오류 도메인 이동 자녀 함께 이동 합니다. 위 예에서 랙 A server01.contoso.com 부모는, 후자의 별도로을 하지 않아도 상하이 사이트로 이동할 수 –는 이미 부모 되 고, 에서처럼 실제에서 않아서 합니다.

출력에서 부모 자녀 관계를 볼 수 `Get-ClusterFaultDomain`에 `ParentName`및 `ChildrenNames`열 합니다.

사용할 수 있습니다 `Set-ClusterFaultDomain`오류 도메인 특정 다른 속성을 수정할 수 있습니다. 예를 들어, 제공할 수 있습니다 (옵션) `-Location`또는 `-Description`메타 데이터를 모두 오류 도메인. 제공 된 경우이 정보 Health 서비스 로부터 경고 하드웨어에 포함 됩니다. 오류 도메인을 사용 하 여 이름을 바꿀 수 있는 `-NewName`매개 합니다. 이름을 변경 하지 않으면 `Node`오류 도메인을 입력 합니다.

```PowerShell
Set-ClusterFaultDomain -Name "Rack A" -Location "Building 34, Room 4010"
Set-ClusterFaultDomain -Type Node -Description "Contoso XYZ Server"
Set-ClusterFaultDomain -Name "Shanghai" -NewName "China Region"
```

사용 하 여 `Remove-ClusterFaultDomain`본체나 걸 만든 사이트를 제거 합니다. `-Name`매개가 필요 합니다. 수 없습니다 어린이 포함 된 오류 도메인 제거 – 먼저 자녀를 제거 하거나 사용 하 여 외부 이동 `Set-ClusterFaultDomain`합니다. 다른 모든 오류 도메인 외 오류 도메인을 이동 하려면 설정의 `-Parent`빈 문자열로 (""). 제거할 수 없는 `Node`오류 도메인을 입력 합니다. 한 번에 여러 오류 도메인 제거 하려면 해당 이름의 나열 합니다.

```PowerShell
Set-ClusterFaultDomain -Name "server01.contoso.com" -Parent ""
Remove-ClusterFaultDomain -Name "Rack A"
```

### <a name="defining-fault-domains-with-xml-markup"></a>오류 도메인 XML 태그와 함께 정의
오류 도메인 XML 표하고자 구문을 사용 하 여 지정할 수 있습니다. Visual Studio Code 등 사용자 좋아하는 텍스트 편집기를 사용 하는 것이 좋습니다 (사용할 수 있는 무료 *[여기](https://code.visualstudio.com/)*) 또는 메모장 저장 하 고 다시 사용할 수 있는 XML 문서를 만듭니다.  

이 짧은 동영상 XML 태그를 지정 오류 도메인을 사용 하는 방법을 보여 줍니다.

[![C이 이미지를 XML 지정 오류 도메인을 사용 하는 방법에 대해 짧은 동영상을 시청 lick](media/Fault-Domains-in-Windows-Server-2016/Part-3-Using-XML-Markup.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-3-Using-XML)

PowerShell의 다음 cmdlet 실행: `Get-ClusterFaultDomainXML`합니다. 클러스터 xml 현재 오류 도메인 사양을 반환합니다. 이 반영 모든 발견 `<Node>`열고 닫는에서 래핑된, `<Topology>`태그 합니다.  

이 출력 파일을 저장 하려면 다음을 실행 합니다.  

```PowerShell
Get-ClusterFaultDomainXML | Out-File <Path>  
```

파일을 열고 추가 `<Site>`, `<Rack>`, 및 `<Chassis>`태그 이러한 노드 사이트, 걸 및 섀시 어떻게 분산 지정할 수 있습니다. 모든 태그 고유한로 식별 해야 **이름**합니다. 노드 기본적으로 채워집니다으로 노드 이름을 유지 해야 합니다.  

> [!IMPORTANT]  
> 전이적 사이트 준수 해야 추가 태그를 모두 선택 사항 이지만, &gt;랙 &gt;섀시 &gt;노드 계층 제대로 종료 해야 합니다.  
이름, 자유형 뿐만 아니라 `Location="..."`및 `Description="..."`설명자 태그를 추가할 수 있습니다.  

#### <a name="example-two-sites-one-rack-each"></a>예: 두 개의 사이트 한 랙  

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

#### <a name="example-two-chassis-blade-servers"></a>예: 두 개의 섀시, 서버 잎  
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

새 오류 도메인 내역이 설정 하려면 XML에 저장 하 고 PowerShell에서 다음을 실행 합니다.  

```PowerShell
$xml = Get-Content <Path> | Out-String  
Set-ClusterFaultDomainXML -XML $xml
```

이 가이드에서는 두 가지 예는 있지만 `<Site>`, `<Rack>`, `<Chassis>`, 및 `<Node>`태그 혼합 및 배포의 실제 토폴로지 반영 하기 위해 추가적인 여러 가지 방법으로 일치 수 수 있는 무엇이 든 합니다. 이러한 태그는 유연성과을 명확 하 게 하려면 자유형 위치 설명자 값 이러한 예 설명 바랍니다.  

### <a name="optional-location-and-description-metadata"></a>옵션: 위치 및 설명을 메타 데이터

(옵션)을 제공할 수 있습니다 **위치** 또는 **설명** 메타 데이터를 모두 오류 도메인. 제공 된 경우이 정보 Health 서비스 로부터 경고 하드웨어에 포함 됩니다. 이 짧은 동영상 이러한 설명자 추가 하는 가치 보여 줍니다.

[![C위치 설명자 오류 도메인에 추가 하는 가치를 보여 주는 짧은 동영상을 확인 하려면 전혀](media/Fault-Domains-in-Windows-Server-2016/part-4-location-description.jpg)](https://channel9.msdn.com/Blogs/windowsserver/Fault-Domain-Awareness-in-WS2016-Part-4-Location-Description)

## <a name="see-also"></a>참조 하십시오  
-   [Windows Server 2016](../get-started/windows-server-2016.md)  
-   [Windows Server 2016에에서 저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 
