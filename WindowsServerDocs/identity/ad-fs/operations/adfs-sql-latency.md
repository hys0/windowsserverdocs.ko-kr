---
title: SQL 튜닝 고 AD FS 사용 하 여 대기 시간 문제 해결
description: 이 문서에서는 AD FS 사용 하 여 SQL을 미세 조정 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 06/20/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb699a1f92013f5657d2fbb48b203f96a5e5a5ba
ms.sourcegitcommit: 6b6c3601fb7493ab145ccff02db26d7123df9a3d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/21/2019
ms.locfileid: "67322850"
---
# <a name="fine-tuning-sql-and-addressing-latency-issues-with-ad-fs"></a>SQL 튜닝 고 AD FS 사용 하 여 대기 시간 문제 해결
에 대 한 업데이트 [AD FS 2016](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) 데이터베이스 대기 시간이 간 줄이기 위해 다음과 같은 개선 사항이 도입 되었습니다. AD FS 2019에 대해 예정 된 업데이트를이 개선이 포함 됩니다.

## <a name="in-memory-cache-update-in-background-thread"></a>백그라운드에서 메모리 내 캐시 업데이트 
가용성 (AoA) 배포에 이전 항상에서 대기 시간이 존재에 대 한 "읽기" 작업으로 마스터 노드에 각기 다른 데이터 센터에서 찾을 수 없습니다. 대기 시간에 두 개의 서로 다른 데이터 센터 간의 호출이 했습니다.  

AD FS에 최신 업데이트에서는 대기 시간이 감소는 백그라운드 스레드를 AD FS 구성 캐시를 새로 고치고 새로 고침 시간을 설정 하려면 설정의 추가 통해 대상으로 합니다. 요청 스레드의 데이터베이스 조회에 소요 된 시간이 줄어듭니다 크게 데이터베이스 캐시 업데이트를 백그라운드 스레드로 이동 됩니다.  

경우는 `backgroundCacheRefreshEnabled` 로 설정 된 true, AD FS 통해 캐시 업데이트를 실행 하는 백그라운드 스레드입니다. 캐시에서 데이터를 가져오는 빈도 사용자 지정할 수 있습니다 시간 값을 설정 하 여 `cacheRefreshIntervalSecs`입니다. 기본값을 300 초로 설정 되어 경우 `backgroundCacheRefreshEnabled` 설정할지 true로 합니다. 집합 값 기간 후 AD FS의 캐시 새로 고침을 시작 하 고 업데이트가 진행에서 중일 이전 캐시 데이터를 계속 사용할 수 있습니다.  

>[!NOTE]
> 캐시의 데이터가 외부 고쳐집니다는 `cacheRefreshIntervalSecs` ADFS에서 SQL 데이터베이스에 변경 되었음을 나타내는 알림을 수신 하는 경우 값입니다. 이 알림은 캐시를 새로 고칠 수 트리거됩니다. 

### <a name="recommendations-for-setting-the-cache-refresh"></a>캐시 새로 고침 설정에 대 한 권장 사항 
캐시 새로 고침에 대 한 기본값은 **5 분**합니다. 로 설정 하는 것이 좋습니다. **1 시간** SQL 변경 발생 하는 경우 캐시 데이터를 새로 고쳐집니다 때문에 AD FS에서 불필요 한 데이터 새로 고침을 줄일 수 있습니다.  

AD FS SQL 변경 내용에 대 한 콜백을 등록 하 고 변경 되 면 ADFS는 알림을 받습니다. 이 메서드를 통해 ADFS 발생 하는 즉시 SQL에서 각 새 변경을 받습니다. 

SQL notification 누락 된 AD FS에서 발생 하는 AD FS는 캐시에서 지정 된 간격으로 새로 고쳐집니다 네트워크 결함 시 값을 새로 고칩니다. 모든 연결 문제는 AD FS와 SQL 간의 의심 되는, 경우에 1 시간 보다 낮게 캐시 새로 고침 값을 설정 하는 것이 좋습니다.  

### <a name="configuration-instructions"></a>구성 지침 
구성 파일을 여러 캐시 항목을 지원합니다. 아래에 나열 된 다음 모든 구성할 수 있습니다 조직의 필요에 따라. 

다음 예제에서는 백그라운드 캐시 새로 고침을 사용 하도록 설정 하 고 캐시 새로 고침 기간 1800 초 또는 30 분을 설정 합니다. 각 ADFS 노드에서 수행 해야 하 고 ADFS 서비스를 나중에 다시 시작 해야 합니다. 변경 내용이 영향을 기타 노드 및 모든 노드에서 변경 하기 전에 첫 번째 노드를 테스트 하지. 

  1. "Microsoft.IdentityServer.Service" 섹션에서 AD FS 구성 파일을 이동, 추가 된 항목 아래:  
  
  - `backgroundCacheRefreshEnabled`  -백그라운드 캐시 기능 사용 되는지 여부를 지정 합니다. "true/false" 값입니다.
  - `cacheRefreshIntervalSecs` -ADFS는 캐시에 새로 고치는 초 단위의 값입니다. SQL의 모든 변경 사항이 있는 경우 AD FS에서 캐시를 새로 고쳐집니다. AD FS SQL 알림을 받고 캐시 새로 고침 됩니다.  
 
 >[!NOTE]
 > 구성 파일의 항목을 모두 대/소문자를 구분 합니다.  
 &lt;cache cacheRefreshIntervalSecs="1800" backgroundCacheRefreshEnabled="true" /&gt; 
 
추가 지원 되는 구성 가능한 값: 

   - **maxRelyingPartyEntries** 최대-AD FS는 메모리에 유지 하는 신뢰 당사자 항목 수입니다. OAuth 응용 프로그램 사용 권한 캐시에서이 값도 사용 됩니다. Rp 및 메모리에 저장 됩니다 모든 보다 더 많은 응용 프로그램 권한이 없으면이 값은 응용 프로그램 사용 권한 수를 해야 합니다. 기본값은 1000입니다.
   - **maxIdentityProviderEntries** -이 클레임의 최대 수를 AD FS는 메모리에 유지 하는 공급자 항목입니다. 기본값은 200입니다. 
   - **maxClientEntries** -AD FS는 메모리에 유지 하는 OAuth 클라이언트 항목의 최대 수입니다. 기본값은 500입니다. 
   - **maxClaimDescriptorEntries** 최대-AD FS는 메모리에 유지 하는 클레임 설명자 항목 수입니다. 기본값은 500입니다. 
   - **maxNullEntries** -부정 캐시로 사용 됩니다. AD FS 데이터베이스에서 항목을 찾을 수 없습니다 하는 경우 AD FS 부정 캐시에 추가 합니다. 캐시의 최대 크기입니다. 개체의 각 형식에 대 한 부정 캐시를 단일 캐시를 사용 하는 모든 개체에 대 한 것입니다. 기본값은 50,0000 합니다. 

## <a name="multiple-artifact-db-support-across-datacenters"></a>데이터 센터에서 여러 아티팩트 DB 지원 
여러 데이터 센터의 이전 구성에 대 한 AD FS 간 center 데이터 센터 대기 시간 검색 호출 중 발생 한 아티팩트 데이터베이스를 에서만 있습니다.  

데이터 센터 간 대기 시간을 줄이려면 AD FS 관리자는 이제 여러 아티팩트 DB 인스턴스를 배포 하 고 다른 아티팩트 DB 인스턴스를 가리키도록 AD FS 노드를 구성 파일을 수정할 수 있습니다. 노드 별 아티팩트 DB 수 있도록 구성 파일에서 아티팩트 데이터베이스 연결 문자열을 제공할 수 있습니다. 연결 문자열 구성 파일에 없는 경우 노드 구성 DB에에서 존재 하는 아티팩트 데이터베이스를 사용 하도록 이전 디자인에 대체 됩니다.  
이 구성 하이브리드 환경 에서도 지원 됩니다.  

### <a name="requirements"></a>요구 사항: 
여러 아티팩트 데이터베이스 지원, 설정 하기 전에 모든 노드에서 업데이트를 실행 하 고이 기능을 통해 다중 노드 호출이 발생 하므로 이진 파일을 업데이트 합니다. 
  1. 아티팩트 DB를 만들려면 배포 스크립트를 생성 합니다. 여러 아티팩트 DB 인스턴스를 배포 하려면 관리자로 아티팩트 DB에 대 한 SQL 배포 스크립트를 생성 해야 합니다. 기존에이 업데이트의 일부로 `Export-AdfsDeploymentSQLScript`cmdlet는 지정 하는 AD FS 데이터베이스에 대 한 SQL 배포 스크립트를 생성 하는 매개 변수에서 필요에 따라 수행 하도록 업데이트 되었습니다. 
 
 예를 들어 방금 아티팩트 DB에 대 한 배포 스크립트를 생성 하려면 지정 된 `-DatabaseType` 매개 변수 및 값 "아티팩트"를 전달 합니다. 선택적 `-DatabaseType` 매개 변수는 AD FS 데이터베이스 형식을 지정 하 고 설정할 수 있습니다. 모두 (기본값), 아티팩트 또는 구성 합니다. 없으면 `-DatabaseType` 매개 변수에 지정 된 경우 스크립트는 아티팩트 및 구성 스크립트를 구성 합니다.  

   ```PowerShell
   PS C:\> Export-AdfsDeploymentSQLScript -DestinationFolder <script folder where scripts will be created> -ServiceAccountName <domain\serviceaccount> -DatabaseType "Artifact" 
   ```
생성된 된 스크립트를 필요한 데이터베이스를 만들고 AD FS 서비스 계정, 해당 데이터베이스를 SQL SA 권한을 부여 하는 SQL 컴퓨터에서 실행 되어야 합니다.

 2. 배포 스크립트를 사용 하 여 아티팩트 DB를 만듭니다. SQL server 컴퓨터에는 새로 생성 된 CreateDB.sql 및 SetPermissions.sql 배포 스크립트를 복사 하 고 하 여 로컬 아티팩트 DB를 실행 합니다. 
 
 3. 아티팩트 DB 연결을 추가 하려면 구성 파일을 수정 합니다. 
 AD FS 노드 구성 파일을 이동한 "Microsoft.IdentityServer.Service" 섹션에서 새로 구성된 된 ArtifactDB에 진입점을 추가 합니다. 

 >[!NOTE] 
 > artifactStore 및 connectionString은 대/소문자 구분 값입니다. 제대로 구성 되어 있는지 확인 합니다. &lt;artifactStore connectionString="Data Source=.\SQLInstance;Integrated Security=True;Initial Catalog=AdfsArtifactStore" /&gt; 
>
>Sql 연결을 일치 하는 데이터 원본 값을 사용 합니다.



 4. 변경 내용을 적용 하려면 AD FS 서비스를 다시 시작 합니다. 
 
 >[!NOTE] 
 > 하지 SQL 복제 또는 아티팩트 데이터베이스 간에 동기화를 사용 하는 것이 좋습니다. / 데이터 센터당 하나의 아티팩트 데이터베이스를 설정 하는 것이 좋습니다. 
 
### <a name="cross-datacenter-failover-and-database-recovery"></a>장애 조치 및 데이터베이스 복구 데이터 센터 간  
장애 조치 아티팩트 데이터베이스 아티팩트를 master 데이터베이스와 동일한 데이터 센터를 만들 수는 것이 좋습니다. 장애 조치가 발생 하는 경우 대기 시간이 증가 안 함 됩니다. 데이터 센터 간에 장애 조치 아티팩트 데이터베이스 권장 되지 않습니다. 다음 OAuth, SAML, ESL, 및 토큰에 대 한 호출에서 여러 아티팩트 데이터베이스를 사용 하 여 검색 함수를 재생 하는 방법을 자세히 설명 합니다. 
 - **OAuth 및 SAML** 

   OAuth 및 SAML 아티팩트 요청에 대 한 노드가 만들어집니다 아티팩트 DB 아티팩트에 구성 파일에 있습니다. 구성 파일에 아티팩트 데이터베이스 연결을 찾을 수 없는 경우에 일반적인 아티팩트 DB를 사용 합니다. 다음 아티팩트를 가져오는 요청을 다른 노드로 전환 되 면 다른 노드로 아티팩트 DB에서에서 아티팩트를 가져올 첫 번째 노드를 rest API를 만듭니다. 다른 노드는 다른 아티팩트 데이터베이스 있을 노드 모르는 이것이 필요 합니다. 첫 번째 노드 다운 된 경우 아티팩트 확인 하지 못합니다. 이 디자인으로 인해 다른 데이터 센터에서 DB 아티팩트를 복제할 필요는 없습니다. 하나의 전체 데이터 센터 다운 된 경우 대부분 아티팩트를 생성 하는 노드는도, 즉 해당 아티팩트를 더 이상 확인할 수 없습니다.  

 - **엑스트라넷 잠금** 

    엑스트라넷 잠금 데이터에 대 한 구성 파일에서 참조 하는 아티팩트 데이터베이스 사용 됩니다. 그러나 ESL 기능에 대 한 AD FS는 이러한 아티팩트 DB에에서 데이터를 기록 하는 마스터를 선택 합니다. 노드를 모두 가져오고 각 사용자에 대 한 최신 정보를 설정 하는 마스터 노드를 호출 하는 REST API를 확인 합니다. 여러 아티팩트 DB 사용 중인 경우 관리자는 각 아티팩트 DB 또는 데이터 센터에 대 한 마스터 노드를 선택 해야 합니다. 

    ESL 마스터를 ADFS 노드 구성 파일을 이동한 "Microsoft.IdentityServer.Service" 섹션에서 한 노드를 선택 하려면 다음을 추가 합니다.       
    
    마스터에서 다음 항목을 추가 합니다. 모든 세 개의 키 대/소문자를 구분 하는 참고 합니다. 

    &lt;useractivityfarmrole masterFQDN [선택한 주 FQDN] isMaster = = "true" /&gt;
    
    항목 다음 다른 노드를 추가 합니다.

   &lt;useractivityfarmrole masterFQDN [선택한 주 FQDN] isMaster = = "false" /&gt;
 
    >[!NOTE] 
    >여러 아티팩트 데이터베이스에서 데이터를 동기화 하지 않습니다, 이후 ESL 값 아티팩트 Db 간에 동기화 되지 않습니다.
    사용자 수 잠재적으로 적중 요청에 대해 다른 데이터 센터 아티팩트 Db, ExtranetLockoutThreshold의 수에 종속 된 ExtranetLockoutThreshold 있으므로 * 아티팩트 Db의 수입니다. 
 
  - **토큰 재생 검색** 
    
    토큰 재생 검색 데이터는 항상 중앙 아티팩트 데이터베이스에서 호출 됩니다. AD FS에 저장 클레임 공급자 트러스트에서 동일한 토큰을 재생할 수 없습니다 확인 토큰입니다. 공격자에 동일한 토큰 재생 하려고 하는 경우 AD FS 토큰 아티팩트 DB에 존재 하는지 확인 합니다. 토큰이 있는 경우 요청이 거부 됩니다. 중앙 아티팩트 데이터베이스는 보안에 대 한 아티팩트 DB 데이터를 복제 되지 때문 공격자 다른 데이터 센터에 요청을 보냅니다 한 토큰 재생 합니다. ArtifactDB 추가 읽기 전용 복사본을 만드는 중앙 아티팩트 데이터베이스에만 사용 되는이 시나리오에서는 데이터 센터 간 대기 시간을 방지 하지 됩니다.    
 
 