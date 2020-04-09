---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: Windows PowerShell을 사용한 고급 Active Directory 복제 및 토폴로지 관리(수준 200)
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6a19e2fb043f6ad870c7f3af83497c2beb436c31
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823036"
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>Windows PowerShell을 사용한 고급 Active Directory 복제 및 토폴로지 관리(수준 200)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 새로운 AD DS 복제 및 토폴로지 관리 cmdlet에 대해 자세히 설명하며, 추가 예제를 제공합니다. 참조에 대 한 소개 [Active Directory 복제 및 토폴로지 관리를 사용 하 여 Windows PowerShell & #40; 소개 수준 100 & #41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)합니다.  
  
1.  [소개](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)  
  
2.  [복제 및 메타 데이터](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)  
  
3.  [ADReplicationAttributeMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)  
  
4.  [ADReplicationPartnerMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)  
  
5.  [ADReplicationFailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)  
  
6.  [Get-adreplicationqueueoperation 및 Get-adreplicationuptodatenessvectortable](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)  
  
7.  [동기화-ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)  
  
8.  [형태가](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)  
  
## <a name="introduction"></a><a name="BKMK_Intro"></a>간략하게  
Windows Server 2012에서는 복제 및 토폴로지를 관리할 수 있도록 Windows PowerShell용 Active Directory 모듈이 25개의 새 cmdlet으로 확장되었습니다. 이전에 제네릭 사용 해야 했습니다 **\*-AdObject** 명사 또는.NET 함수를 호출 합니다.  
  
모든 Active Directory Windows PowerShell cmdlet과 마찬가지로 이 새 기능을 사용하려면 하나 이상의 도메인 컨트롤러(가급적 모든 도메인 컨트롤러)에 [Active Directory 관리 게이트웨이 서비스](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852) 를 설치해야 합니다.  
  
다음 표에는 Active Directory Windows PowerShell 모듈에 추가된 새로운 복제 및 토폴로지 cmdlet이 나와 있습니다.  
  
|||  
|-|-|  
|Cmdlet|설명|  
|Get-ADReplicationAttributeMetadata|개체의 특성 복제 메타데이터를 반환합니다.|  
|Get-ADReplicationConnection|도메인 컨트롤러 연결 개체의 세부 정보를 반환합니다.|  
|Get-ADReplicationFailure|도메인 컨트롤러의 최근 복제 오류를 반환합니다.|  
|Get-ADReplicationPartnerMetadata|도메인 컨트롤러의 복제 구성을 반환합니다.|  
|Get-ADReplicationQueueOperation|현재 복제 큐 백로그를 반환합니다.|  
|Get-ADReplicationSite|사이트 정보를 반환합니다.|  
|Get-ADReplicationSiteLink|사이트 링크 정보를 반환합니다.|  
|Get-ADReplicationSiteLinkBridge|사이트 링크 브리지 정보를 반환합니다.|  
|Get-ADReplicationSubnet|AD 서브넷 정보를 반환합니다.|  
|Get-ADReplicationUpToDatenessVectorTable|도메인 컨트롤러의 UTD 벡터를 반환합니다.|  
|Get-ADTrust|도메인 간 또는 포리스트 간 트러스트에 대한 정보를 반환합니다.|  
|New-ADReplicationSite|새 사이트를 만듭니다.|  
|New-ADReplicationSiteLink|새 사이트 링크를 만듭니다.|  
|New-ADReplicationSiteLinkBridge|새 사이트 링크 브리지를 만듭니다.|  
|New-ADReplicationSubnet|새 AD 서브넷을 만듭니다.|  
|Remove-ADReplicationSite|사이트를 삭제합니다.|  
|Remove-ADReplicationSiteLink|사이트 링크를 삭제합니다.|  
|Remove-ADReplicationSiteLinkBridge|사이트 링크 브리지를 삭제합니다.|  
|Remove-ADReplicationSubnet|AD 서브넷을 삭제합니다.|  
|Set-ADReplicationConnection|연결을 수정합니다.|  
|Set-ADReplicationSite|사이트를 수정합니다.|  
|Set-ADReplicationSiteLink|사이트 링크를 수정합니다.|  
|Set-ADReplicationSiteLinkBridge|사이트 링크 브리지를 수정합니다.|  
|Set-ADReplicationSubnet|AD 서브넷을 수정합니다.|  
|Sync-ADObject|단일 개체를 강제로 복제합니다.|  
  
이러한 cmdlet은 대부분 Repadmin.exe에 기초를 두고 있습니다. 여기에 나열되지 않은 다른 cmdlet은 동적 Access Control 및 그룹 관리 서비스 계정과 같은 기능을 처리합니다.  
  
모든 Active Directory Windows PowerShell cmdlet의 전체 목록을 보려면 다음을 실행하세요.  
  
```  
Get-command -module ActiveDirectory  
```  
  
모든 Active Directory Windows PowerShell cmdlet 인수의 전체 목록은 도움말을 참조하세요. 예를 들면 다음과 같습니다.  
  
```  
Get-help New-ADReplicationSite  
  
```  
  
`Update-Help` cmdlet을 사용하여 도움말 파일을 다운로드하고 설치할 수 있습니다.  
  
### <a name="replication-and-metadata"></a><a name="BKMK_Repl"></a>복제 및 메타 데이터  
Repadmin.exe는 Active Directory 복제의 상태 및 일관성을 확인합니다. Repadmin.exe는 간단한 데이터 조작 옵션(예: 일부 인수는 CSV 출력을 지원함)을 제공하지만 자동화에는 일반적으로 텍스트 파일 출력을 통한 구문 분석이 필요합니다. Windows PowerShell용 Active Directory 모듈은 반환된 데이터를 실제로 제어할 수 있는 옵션을 제공하기 위한 첫 번째 시도입니다. 그 전에는 스크립트를 만들거나 타사 도구를 사용해야 했습니다.  
  
또한 다음 cmdlet은 **Target**, **Scope** 및 **EnumerationServer**의 새로운 매개 변수 집합을 구현합니다.  
  
-   **ADReplicationFailure**  
  
-   **ADReplicationPartnerMetadata**  
  
-   **Get-adreplicationuptodatenessvectortable**  
  
**Target** 인수는 **Scope** 인수에 지정된 대상 서버, 사이트, 도메인 또는 포리스트를 식별하는 문자열의 쉼표로 구분된 목록을 허용합니다. 별표 (\*)를 사용할 수도 및 지정된 된 범위 내 모든 서버를 의미 합니다. 없는 범위를 지정 하는 경우 현재 사용자의 포리스트에 있는 모든 서버를 의미 합니다. **Scope** 인수는 검색 허용 범위를 지정합니다. 사용 가능한 값은 **Server**, **Site**, **Domain** 및 **Forest**입니다. **EnumerationServer** 는 **Target** 및 **Scope**에 지정된 도메인 컨트롤러 목록을 열거하는 서버를 지정합니다. **Server** 인수와 동일하게 작동하며, 지정된 서버에서 Active Directory 웹 서비스를 실행해야 합니다.  
  
새로운 cmdlet을 소개하기 위해 여기에 repadmin.exe로는 불가능한 기능을 보여 주는 몇 가지 예제 시나리오가 나와 있습니다. 이러한 그림을 보면 관리 가능성을 명확히 알 수 있습니다. 특정 사용 요구 사항은 cmdlet 도움말을 검토하세요.  
  
### <a name="get-adreplicationattributemetadata"></a><a name="BKMK_ReplAttrMD"></a>ADReplicationAttributeMetadata  
이 cmdlet은 **repadmin.exe /showobjmeta**와 유사합니다. 이를 사용하여 복제 메타데이터(예: 특성이 변경된 경우), 원래 도메인 컨트롤러, 버전 및 USN 정보, 특성 데이터 등을 반환할 수 있습니다. 이 cmdlet은 변경이 발생한 위치 및 시점을 감사하는 데 유용합니다.  
  
Repadmin과 달리 Windows PowerShell은 유연한 검색 및 출력 제어를 제공합니다. 예를 들어 읽기 가능한 목록으로 정렬된 Domain Admins 개체의 메타데이터를 출력할 수 있습니다.  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list  
  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)  
  
또는 repadmin과 유사하게 데이터를 테이블로 정렬할 수 있습니다.  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap  
  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)  
  
또는 필터(예: 모든 그룹)를 사용하여 **Get-Adobject** cmdlet을 파이프라인하여 전체 개체 클래스에 대한 메타데이터를 가져온 다음 특정 날짜와 조합할 수 있습니다. 파이프라인은 여러 cmdlet 간에 데이터를 전달하는 데 사용되는 채널입니다. 예를 들어 2012년 1월 13일에 다양한 방식으로 수정된 모든 그룹을 확인하려면 다음을 실행합니다.  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)  
  
파이프라인을 사용하는 다양한 Windows PowerShell 작업에 대한 자세한 내용은 [Windows PowerShell의 파이프 및 파이프라인](https://technet.microsoft.com/library/ee176927.aspx)을 참조하세요.  
  
또는 Tony Wang이 구성원으로 속한 모든 그룹과 각 그룹이 마지막으로 수정된 시간을 확인하려면 다음을 실행합니다.  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto  
  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)  
  
또는 인위적 상위 버전을 기반으로 도메인에서 시스템 상태 백업을 사용하여 정식 복원된 모든 개체를 찾으려면 다음을 실행합니다.  
  
```  
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)  
  
또는 나중에 Microsoft Excel에서 검토하기 위해 모든 사용자 메타데이터를 CSV 파일로 보내려면 다음을 실행합니다.  
  
```  
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv  
```  
  
### <a name="get-adreplicationpartnermetadata"></a><a name="BKMK_PartnerMD"></a>ADReplicationPartnerMetadata  
이 cmdlet은 모니터링, 인벤토리 관리 또는 문제 해결을 지원하기 위해 도메인 컨트롤러의 복제 상태 및 구성 정보를 반환합니다. Repadmin.exe와 달리 Windows PowerShell을 사용하면 사용자가 원하는 형식으로 자신에게 중요한 데이터만 볼 수 있습니다.  
  
예를 들어 단일 도메인 컨트롤러의 읽기 가능한 복제 상태를 확인할 수 있습니다.  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)  
  
또는 도메인 컨트롤러에서 인바운드 및 해당 파트너를 마지막으로 복제한 시간을 테이블 형식을 확인할 수 있습니다.  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)  
  
또는 포리스트의 모든 도메인 컨트롤러에 연결하여 이유에 상관없이 마지막으로 시도한 복제에 실패한 모든 대상을 표시할 수 있습니다.  
  
```  
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto  
  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)  
  
### <a name="get-adreplicationfailure"></a><a name="BKMK_ReplFail"></a>ADReplicationFailure  
이 cmdlet은 최근의 복제 오류에 대한 정보를 반환하는 데 사용될 수 있습니다. **Repadmin.exe /showreplsum**과 유사하지만 Windows PowerShell 덕분에 제어 기능이 훨씬 뛰어납니다.  
  
예를 들어 도메인 컨트롤러의 가장 최근 오류와 도메인 컨트롤러에서 연결하는 데 실패한 파트너를 반환할 수 있습니다.  
  
```  
Get-ADReplicationFailure dc1.corp.contoso.com  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)  
  
또는 가장 중요한 데이터만 포함하고 보다 보기 쉽게 정렬하여 특정 AD 논리 사이트의 모든 서버에 대한 테이블 보기를 반환할 수 있습니다.  
  
```  
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto  
  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)  
  
### <a name="get-adreplicationqueueoperation-and-get-adreplicationuptodatenessvectortable"></a><a name="BKMK_ReplQueue"></a>Get-adreplicationqueueoperation 및 Get-adreplicationuptodatenessvectortable  
이 두 cmdlet은 보류 중인 복제 및 버전 벡터 정보를 포함하여 도메인 컨트롤러의 "최신" 정보를 추가로 반환합니다.  
  
### <a name="sync-adobject"></a><a name="BKMK_Sync"></a>동기화-ADObject  
이 cmdlet은 **Repadmin.exe /replsingleobject**와 유사하며, 대역 외 복제가 필요한 변경 작업을 수행할 때, 특히 문제를 해결할 때 매우 유용합니다.  
  
예를 들어 누군가 CEO의 사용자 계정을 삭제한 후 Active Directory 휴지통을 사용하여 복원한 경우 이를 모든 도메인 컨트롤러에 즉시 복제할 수 있습니다. 또한 다른 모든 개체 변경 내용을 강제로 복제하지 않고 이 작업을 수행할 수 있습니다. WAN 링크 오버로드를 방지하기 위해 복제 일정을 예약하는 것도 결국 이 때문입니다.  
  
```  
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}  
  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)  
  
### <a name="topology"></a><a name="BKMK_Topo"></a>형태가  
Repadmin.exe는 사이트, 사이트 링크, 사이트 링크 브리지 및 연결과 같은 복제 토폴로지에 대한 정보를 반환하는 데 유용하지만 변경 작업을 수행할 수 있는 포괄적인 인수 집합이 없습니다. 실제로 관리자가 AD DS 토폴로지를 만들고 수정할 수 있도록 특별히 디자인된 스크립트 가능한 Windows 제공 유틸리티로 제공된 적이 없습니다. Active Directory는 수백만 개의 고객 환경에서 성숙되어 오면서 Active Directory 논리 정보에 대한 대량 수정의 필요성이 명확해졌습니다.  
  
예를 들어 다른 지점의 통합과 함께 새로운 지점의 급속한 확장 후 실제 위치, 네트워크 변경 사항 및 새로운 용량 요구 사항을 기반으로 100여 가지의 사이트 변경 작업을 수행해야 할 수 있습니다. 이 경우 Dssites.msc 및 Adsiedit.msc를 사용하여 변경하는 대신 자동화할 수 있습니다. 이는 네트워크 및 시설 팀에서 제공한 데이터 스프레드시트로 시작하는 경우에 특히 유용합니다.  
  
**Get adreplication\\** * cmdlet은 복제 토폴로지에 대 한 정보를 반환 하 고, 대량으로 **집합 adreplication\\** * cmdlet에 파이프라인에 대 한 유용한 정보를 제공 합니다. **Get** cmdlet은 데이터를 변경 하지 않고 데이터를 표시 하거나 **설정-adreplication\\** * cmdlet으로 파이프라인 될 수 있는 Windows PowerShell 세션 개체를 만들기만 합니다. **New** 및 **Remove** cmdlet은 Active Directory 토폴로지 개체를 만들거나 제거하는 데 유용합니다.  
  
예를 들어 CSV 파일을 사용하여 새 사이트를 만들 수 있습니다.  
  
```  
import-csv -path C:\newsites.csv | new-adreplicationsite  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)  
  
또는 사용자 지정 복제 간격 및 사이트 비용으로 두 개의 기존 사이트 간에 새로운 사이트 링크를 만들 수 있습니다.  
  
```  
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)  
  
또는 압축을 사용하여 최대 속도로 복제하기 위해 포리스트의 모든 사이트를 찾아 사이트 간 변경 알림을 지원하도록 해당 **Options** 특성을 플래그로 바꿀 수 있습니다.  
  
```  
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)  
  
> [!IMPORTANT]  
> **-bor 5**를 설정하여 이러한 사이트 링크에서 압축을 사용하지 않도록 설정할 수도 있습니다.  
  
또는 해당 위치의 실제 서브넷으로 목록을 조정하기 위해 서브넷 할당이 누락된 모든 사이트를 찾을 수 있습니다.  
  
```  
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name  
```  
  
![powershell 사용 하 여 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)  
  
## <a name="see-also"></a>관련 항목  
[Windows PowerShell &#40;수준 100을 사용한 Active Directory 복제 및 토폴로지 관리 소개&#41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)  
  

