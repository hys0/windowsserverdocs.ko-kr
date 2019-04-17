---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: "향상 된 Active Directory 복제 및 Windows PowerShell (수준을 200)를 사용 하 여 토폴로지 관리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1e05616b4b594ae54fcaa3ec6496c0917ecde38b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>향상 된 Active Directory 복제 및 Windows PowerShell (수준을 200)를 사용 하 여 토폴로지 관리

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목 새로운 광고 DS 복제 및 자세히를 토폴로지 관리 cmdlet에 설명 하 고 추가적인 예시를 제공 합니다. 대 한 소개 [Active Directory 복제 토폴로지 관리를 사용 하 여 Windows PowerShell 및 #40; 소개 수준을 100 & #41; ](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md).  
  
1.  [소개](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)  
  
2.  [복제와 메타 데이터](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)  
  
3.  [Get ADReplicationAttributeMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)  
  
4.  [Get ADReplicationPartnerMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)  
  
5.  [Get ADReplicationFailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)  
  
6.  [Get ADReplicationQueueOperation 및 다운로드 ADReplicationUpToDatenessVectorTable](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)  
  
7.  [동기화 ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)  
  
8.  [토폴로지](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)  
  
## <a name="BKMK_Intro"></a>소개  
Windows Server 2012 25 새로운 cmdlet 복제 및 숲 토폴로지 관리를 사용 하 여 Windows PowerShell에 대 한 Active Directory 모듈을 확장 합니다. 이 앞서 원본을 사용 해야 했습니다 **\*-AdObject** 명사 또는 통화.NET 기능입니다.  
  
모든 Active Directory Windows PowerShell cmdlet, 마찬가지로이 새로운 기능 설치 필요는 [Active Directory 관리 게이트웨이 서비스](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852) 하나 이상의 도메인 컨트롤러 (와 모든 도메인 컨트롤러)에 있습니다.  
  
다음 표에서 새로운 복제 및 토폴로지 cmdlet Active Directory Windows PowerShell 모듈에 추가 합니다.  
  
|||  
|-|-|  
|Cmdlet|설명|  
|Get ADReplicationAttributeMetadata|반환 특성 개체 복제 메타 데이터|  
|Get ADReplicationConnection|반환 도메인 컨트롤러 연결 개체 세부 정보|  
|Get ADReplicationFailure|최근 실패 도메인 컨트롤러에 대 한 가장 많은 복제 반환|  
|Get ADReplicationPartnerMetadata|도메인 컨트롤러의 반환 복제 구성|  
|Get ADReplicationQueueOperation|현재 복제 큐 백로그 반환|  
|Get ADReplicationSite|반환 사이트 정보|  
|Get ADReplicationSiteLink|반환 사이트 링크 정보|  
|Get ADReplicationSiteLinkBridge|반환 사이트 링크 다리 정보|  
|Get ADReplicationSubnet|반환 광고 서브넷 정보|  
|Get ADReplicationUpToDatenessVectorTable|도메인 컨트롤러의 UTD vector 반환|  
|Get ADTrust|도메인 간 또는 간 숲 보안에 대 한 정보|  
|새 ADReplicationSite|새 사이트를 만듭니다.|  
|새 ADReplicationSiteLink|새 사이트 링크를 만듭니다.|  
|새 ADReplicationSiteLinkBridge|새 사이트 링크 브리지를 만듭니다.|  
|새 ADReplicationSubnet|새 광고 서브넷을 만듭니다.|  
|제거 ADReplicationSite|사이트 삭제|  
|제거 ADReplicationSiteLink|사이트 링크 삭제|  
|제거 ADReplicationSiteLinkBridge|사이트 링크 다리 삭제|  
|제거 ADReplicationSubnet|광고 서브넷 삭제|  
|설정 ADReplicationConnection|수정 하 여 연결|  
|설정 ADReplicationSite|수정 하는 사이트|  
|설정 ADReplicationSiteLink|수정 하는 사이트 링크|  
|설정 ADReplicationSiteLinkBridge|사이트 링크 다리 수정|  
|설정 ADReplicationSubnet|광고 서브넷 수정|  
|동기화 ADObject|단일 개체의 힘 복제|  
  
이러한 cmdlet 대부분은 Repadmin.exe에서 자녀가 별로 있습니다. 다른 cmdlet (나열 되지) 동적 액세스 제어 하 고 그룹 관리 서비스 계정와 같은 기능 처리 합니다.  
  
모든 Active Directory Windows PowerShell cmdlet의 전체 목록은 실행 합니다.  
  
```  
Get-command -module ActiveDirectory  
```  
  
모든 Active Directory Windows PowerShell cmdlet 인수의 전체 목록은에 대 한 도움말을 참조 합니다. 예를 들어:  
  
```  
Get-help New-ADReplicationSite  
  
```  
  
사용 하 여 `Update-Help` cmdlet 다운로드 하 고 도움이 파일을 설치 하려면  
  
### <a name="BKMK_Repl"></a>복제와 메타 데이터  
건강 및 Active Directory 복제 일관성 Repadmin.exe 않았는지 확인합니다. Repadmin.exe 간단한 데이터가 조작 옵션이-일부 인수 지원 CSV 출력 예를 들어 하지만 자동화 일반적으로 텍스트 파일 출력 통해 구문 분석 함으로써 필요 합니다. Windows PowerShell에 대 한 Active Directory 모듈은 실제 반환된 데이터; 제어할 수 있게 하는 옵션을 제공 하는 최초의 시도 이 앞서 스크립트 만들거나 제 3 자 도구를 사용 해야 했습니다.  
  
또한 다음과 같은 cmdlet 구현 새로운 매개 집합이 **대상**, **범위**, 및 **EnumerationServer**:  
  
-   **Get ADReplicationFailure**  
  
-   **Get ADReplicationPartnerMetadata**  
  
-   **Get ADReplicationUpToDatenessVectorTable**  
  
**대상** 인수 허용 쉼표로 구분 목록이 대상 서버, 사이트, 도메인 또는으로 지정 된 숲을 식별 하는 문자열의 **범위** 인수 합니다. 별표 (\ *) 허용 되며 지정된 범위 내에서 서버 모든 것을 의미 합니다. 없는 범위를 지정 하는 경우 현재 사용자 숲 속의 모든 서버 의미 합니다. **범위** 인수 검색 위도 지정 합니다. 사용할 수 있으며 **서버**, **사이트**, **도메인**, 및 **숲**합니다. **EnumerationServer** 열거 목록에 지정 된 도메인 컨트롤러 서버 지정 **대상** 및 **범위**합니다. 같은 작업을 수행 하는 **서버** 인수 지정된 서버 Active Directory 웹 서비스 실행 해야 합니다.  
  
새 cmdlet 기능을 소개 하 다음 일부의 샘플 시나리오가 표시 하는 기능 임파서블 repadmin.exe; 이러한 그림을 갖춘 관리 가능성은 명확 됩니다. 특정 사용 요구 사항에 대 한 cmdlet 도움말을 검토 합니다.  
  
### <a name="BKMK_ReplAttrMD"></a>Get ADReplicationAttributeMetadata  
이 cmdlet 것과 비슷합니다 **repadmin.exe /showobjmeta**합니다. 복제 메타 데이터를 특성 변경 하는 경우, 출처 도메인 컨트롤러, 버전 및 USN 정보 및 특성 데이터 등 되돌릴 수 있습니다. 이 cmdlet 위치 감사 하 고 변경 발생 했을 때 유용 합니다.  
  
달리 Repadmin를 Windows PowerShell 제공 유연한 검색 및 출력을 제어합니다. 예를 들어, 읽기 목록 정렬 도메인 관리자 개체의 메타 데이터를 출력 수 있습니다.  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list  
  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)  
  
또는 표에 repadmin 닮 데이터 정렬할 수 있습니다.  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap  
  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)  
  
또는 열 수 있는 메타 데이터 개체 클래스 전체에 대 한 파이프라인는 **Get Adobject** 모든-있는 그룹 같이 필터를 사용 하 여 cmdlet 다음 결합 하는 특정 날짜 합니다. 파이프라인은 사용 데이터를 전달 하기 위해 여러 cmdlet 간의 채널 합니다. 2012 년 1 월 13 일에서 몇 가지 방식으로 수정 모든 그룹을 보려면:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)  
  
파이프라인을 사용 하 여 더 많은 Windows PowerShell 작업에 대 한 자세한 내용은 참조 [파이핑 및 Windows powershell에서 파이프라인](https://technet.microsoft.com/library/ee176927.aspx)합니다.  
  
또는 알아보려면 모든 그룹을 주지 Tony Wang 멤버와 및 그룹 마지막 수정한:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto  
  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)  
  
또는 모든 개체 정식 찾으려면 사용 하 여 복원 시스템 상태 백업을 도메인에 있는 자신의 인공적 높은 버전에 따라 다음과 같습니다.  
  
```  
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)  
  
또는 모든 사용자 메타 데이터 용 Microsoft Excel의 이후 검사 CSV 파일을 보내려면:  
  
```  
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv  
```  
  
### <a name="BKMK_PartnerMD"></a>Get ADReplicationPartnerMetadata  
이 cmdlet 구성과 복제 모니터링 재고, 하거나 문제를 해결 하도록 허용 하는 도메인 컨트롤러의 상태에 대 한 정보를 반환 합니다. Repadmin.exe과 달리 Windows PowerShell를 사용 하 여 의미 중요 하며, 원하는 형식의 데이터를 표시 합니다.  
  
예를 들어 단일 도메인 컨트롤러의 읽을 수 있는 복제 상태:  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)  
  
또한 지난번 도메인 컨트롤러 복제 돌아오는 및 표에 파트너, 포맷 다음과 같습니다.  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)  
  
또는 모든 도메인 컨트롤러의 숲 속의 연락처 하 고 있는 마지막 시도한 복제 실패 한 모든 디스플레이:  
  
```  
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto  
  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)  
  
### <a name="BKMK_ReplFail"></a>Get ADReplicationFailure  
이 cmdlet 복제에서 최근 오류에 대 한 정보를 반환을 사용할 수 있습니다. 유사 **Repadmin.exe /showreplsum**, 다시 훨씬 더 제어 Windows PowerShell 덕분 하지만 합니다.  
  
예를 들어 도메인 컨트롤러의 최근 오류와 그 실패 문의 파트너 돌아갈 수 있습니다.  
  
```  
Get-ADReplicationFailure dc1.corp.contoso.com  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)  
  
특정 광고 논리 사이트를 쉽게 확인 하 고만 가장 중요 한 데이터가 포함 된 주문한 표 보기 모든 서버에 대 한 환불 또는 다음과 같습니다.  
  
```  
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto  
  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)  
  
### <a name="BKMK_ReplQueue"></a>Get ADReplicationQueueOperation 및 다운로드 ADReplicationUpToDatenessVectorTable  
도메인 컨트롤러의 추가 기능을 반환 모두 이러한 cmdlet "최대 dateness", 보류 중인 복제 및 버전 vector 정보가 포함 됩니다.  
  
### <a name="BKMK_Sync"></a>동기화 ADObject  
실행이이 cmdlet 비슷합니다 **Repadmin.exe /replsingleobject**합니다. 변경한 경우 문제를 해결 하기 특히 band 복제를 활용 해야 하는 매우 유용 합니다.  
  
예를 들어 CEO의 사용자 계정 삭제 사람이 다음 Active Directory 휴지통으로 복원 하는 경우 것 원하는 즉시 모든 도메인 컨트롤러에 복제 합니다. 모든 다른 개체 변경; 복제를 않고도이 작업을 수행 하려고 하는 것도 결국 복제 일정-채우지 WAN 연결 되지 않도록 하는 이유입니다.  
  
```  
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}  
  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)  
  
### <a name="BKMK_Topo"></a>토폴로지  
Repadmin.exe 복제 토폴로지 같은 사이트, 사이트 링크, 사이트 링크 다리 및 연결에 대 한 정보를 환불에, 변경 인수의 포괄적인이 필요가 없습니다. 사실, 없 었는 생성 하 고 수정 AD DS 토폴로지 관리자 위해 특별히 설계 된 스크립트, 기본 Windows 유틸리티 합니다. 대량 필요가 Active Directory 고객 환경 백만에서 성숙 과정은, Active Directory 수정할 논리 정보 드러납니다.  
  
예를 들어, 다른 앱의 통합와 함께 새로운 지점 신속한 확장 이후 실제 위치, 네트워크 변경 내용 및 새로운 용량이 요구 사항에 따라 확인 하는 백 사이트 변경 할 수도 있습니다. Dssites.msc 및 Adsiedit.msc 변경를 사용 하는 대신 자동화 수 있습니다. 네트워크 및 기능 팀에서 제공 하는 데이터의 스프레드시트로 시작 하는 경우 특히 멋진입니다.  
  
**다운로드-Adreplication\ *** cmdlet 복제 토폴로지에 대 한 정보를 반환 하 고에 전달을 대 한 유용한는 **설정-Adreplication\ *** 대량에서 cmdlet 합니다. **다운로드** cmdlet 데이터를 변경 하지 않는 항목이 데이터에만 표시 하거나 세션 개체를 Windows PowerShell 만들 수를 파이프라인 되 **설정-Adreplication\ *** cmdlet 합니다. **새로** 및 **제거** cmdlet 만들거나 토폴로지 Active Directory 개체를 제거 하는 데 유용 합니다.  
  
예를 들어 새 사이트 CSV 파일을 사용 하 여 만들 수 있습니다.  
  
```  
import-csv -path C:\newsites.csv | new-adreplicationsite  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)  
  
또는 사용자 지정 복제 사이트 및 간격 순위가 두 개의 기존 사이트 간의 새 사이트 링크를 만듭니다.  
  
```  
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)  
  
또는 모든 사이트에서 숲 찾아 바꾸는 자신의 **옵션** 사이트 간 수 있도록 플래그 지정 특성 압축 최대 속도로 복제 원활 알림을 변경:  
  
```  
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)  
  
> [!IMPORTANT]  
> 설정 **-또는 5** 에 해당 사이트 링크를 압축 하지 않도록 합니다.  
  
실제 서브넷 해당 위치를 사용 하 여 목록 조정 하려면 서브넷 할당 누락 된 모든 사이트 또는 찾으려면  
  
```  
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name  
```  
  
![powershell와 고급 관리](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)  
  
## <a name="see-also"></a>참조 하십시오  
[Windows PowerShell 및 #40;를 사용 하 여 토폴로지 관리 및 Active Directory 복제 소개 수준을 100 & #41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)  
  

