---
title: SQL을 미세 조정 하 고 AD FS의 대기 시간 문제 해결
description: 이 문서에서는 AD FS를 사용 하 여 SQL을 미세 조정 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: daveba
ms.date: 06/20/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 785ecd4de86c06dd12eb57e41efaa1103f2afdc5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357809"
---
# <a name="fine-tuning-sql-and-addressing-latency-issues-with-ad-fs"></a>SQL을 미세 조정 하 고 AD FS의 대기 시간 문제 해결
[AD FS 2016](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) 에 대 한 업데이트에서는 데이터베이스 간 대기 시간을 줄이기 위해 다음과 같은 향상 된 기능이 도입 되었습니다. AD FS 2019의 예정 된 업데이트에는 이러한 향상 된 기능이 포함 됩니다.

## <a name="in-memory-cache-update-in-background-thread"></a>백그라운드 스레드의 메모리 내 캐시 업데이트 
이전에는 AoA (Always on 가용성) 배포에서 마스터 노드가 별도의 데이터 센터에 있을 수 있으므로 "읽기" 작업에 대 한 대기 시간이 있었습니다. 서로 다른 두 데이터 센터 간의 호출로 인해 대기 시간이 발생 했습니다.  

AD FS에 대 한 최신 업데이트에서 대기 시간 감소는 AD FS 구성 캐시를 새로 고치는 백그라운드 스레드를 추가 하 고 새로 고침 기간을 설정 하는 설정입니다. 데이터베이스 조회에 소요 된 시간은 데이터베이스 캐시 업데이트가 백그라운드 스레드로 이동 되기 때문에 요청 스레드에서 크게 줄어듭니다.  

`backgroundCacheRefreshEnabled` 이 true로 설정 된 경우 AD FS는 백그라운드 스레드에서 캐시 업데이트를 실행할 수 있도록 합니다. 을 설정 `cacheRefreshIntervalSecs`하 여 캐시에서 데이터를 가져오는 빈도를 시간 값으로 사용자 지정할 수 있습니다. 이 true로 설정 된 경우 `backgroundCacheRefreshEnabled` 기본값은 300 초로 설정 됩니다. 값 설정 기간 후에는 AD FS 캐시 새로 고침을 시작 하 고 업데이트가 진행 되는 동안에는 이전 캐시 데이터가 계속 사용 됩니다.  

>[!NOTE]
> ADFS가 데이터베이스에서 변경이 발생 했음을 나타내는 SQL에서 `cacheRefreshIntervalSecs` 알림을 수신 하는 경우 캐시의 데이터가 값의 외부에서 새로 고쳐집니다. 이 알림은 새로 고칠 캐시를 트리거합니다. 

### <a name="recommendations-for-setting-the-cache-refresh"></a>캐시 새로 고침 설정에 대 한 권장 사항 
캐시 새로 고침의 기본값은 **5 분**입니다. SQL 변경이 발생 하는 경우 캐시 데이터를 새로 고칠 수 있으므로 AD FS 하 여 불필요 한 데이터 새로 고침을 줄이기 위해 **1 시간** 으로 설정 하는 것이 좋습니다.  

AD FS는 SQL 변경에 대 한 콜백을 등록 하 고, 변경 되 면 ADFS에서 알림을 받습니다. 이 방법을 통해 ADFS는 발생 하는 즉시 SQL에서 각각의 새로운 변경 내용을 받습니다. 

AD FS 발생 하는 네트워크 결함의 경우 SQL 알림이 누락 AD FS는 캐시 새로 고침 값에 지정 된 간격으로 새로 고쳐집니다. AD FS와 SQL 간에 연결 문제가 의심 되는 경우 캐시 새로 고침 값을 1 시간 이하로 설정 하는 것이 좋습니다.  

### <a name="configuration-instructions"></a>구성 지침 
구성 파일은 여러 캐시 항목을 지원 합니다. 아래에 나열 된 다음은 조직의 요구에 따라 모두 구성할 수 있습니다. 

다음 예에서는 백그라운드 캐시 새로 고침을 사용 하도록 설정 하 고 캐시 새로 고침 기간을 1800 초 또는 30 분으로 설정 합니다. 각 ADFS 노드에서이 작업을 수행 해야 하며 나중에 ADFS 서비스를 다시 시작 해야 합니다. 모든 노드에서 변경 작업을 수행 하기 전에 다른 노드에 영향을 주지 않고 첫 번째 노드를 테스트 합니다. 

  1. AD FS 구성 파일로 이동 하 고 "IdentityServer" 섹션 아래에 다음 항목을 추가 합니다.  
  
  - `backgroundCacheRefreshEnabled`-백그라운드 캐시 기능을 사용 하도록 설정할지 여부를 지정 합니다. "true/false" 값입니다.
  - `cacheRefreshIntervalSecs`-ADFS가 캐시를 새로 고치는 값 (초)입니다. SQL에 변경 내용이 있으면 AD FS가 캐시를 새로 고칩니다. AD FS는 SQL 알림을 수신 하 고 캐시를 새로 고칩니다.  
 
 >[!NOTE]
 > 구성 파일의 모든 항목은 대/소문자를 구분 합니다.  
 &lt;cache cacheRefreshIntervalSecs = "1800" backgroundCacheRefreshEnabled = "true"/&gt; 
 
지원 되는 추가 구성 가능한 값: 

   - **maxRelyingPartyEntries** -AD FS 메모리에 유지 되는 신뢰 당사자 항목의 최대 수입니다. 이 값은 oAuth 응용 프로그램 권한 캐시에도 사용 됩니다. RPs 보다 많은 응용 프로그램 권한이 있고 모두 메모리에 저장 되는 경우이 값은 응용 프로그램 권한 수 여야 합니다. 기본값은 1000입니다.
   - **maxIdentityProviderEntries** -메모리에 유지할 AD FS 클레임 공급자 항목의 최대 수입니다. 기본값은 200입니다. 
   - **maxClientEntries** -메모리에 유지할 OAuth 클라이언트 항목 AD FS의 최대 수입니다. 기본값은 500입니다. 
   - **maxClaimDescriptorEntries** -AD FS 된 클레임 설명자 항목의 최대 수는 메모리에 유지 됩니다. 기본값은 500입니다. 
   - **Maxnullentries** -이는 음의 캐시로 사용 됩니다. AD FS에서 데이터베이스의 항목을 찾을 수 없는 경우 AD FS는 음수 캐시에 추가 됩니다. 이 캐시의 최대 크기입니다. 각 개체 형식에 대 한 캐시는 음수 이며 모든 개체에 대 한 단일 캐시는 아닙니다. 기본값은 50, 0000입니다. 

## <a name="multiple-artifact-db-support-across-datacenters"></a>데이터 센터 간 다중 아티팩트 DB 지원 
여러 데이터 센터의 이전 구성에서 AD FS는 단일 아티팩트 데이터베이스만 지원 하 여 검색 호출 중에 교차 센터 데이터 센터 대기 시간을 발생 시킵니다.  

데이터 센터 간 대기 시간을 줄이기 위해 AD FS 관리자는 이제 여러 아티팩트 DB 인스턴스를 배포 하 고 다른 아티팩트 DB 인스턴스를 가리키도록 AD FS 노드의 구성 파일을 수정할 수 있습니다. 아티팩트 데이터베이스 연결 문자열은 노드 당 아티팩트 DB를 허용 하는 구성 파일에 제공 될 수 있습니다. 구성 파일에 연결 문자열이 없는 경우 노드는 구성 DB에 있는 아티팩트 데이터베이스를 사용 하도록 이전 디자인으로 대체 됩니다.  
이 구성에서는 하이브리드 환경도 지원 됩니다.  

### <a name="requirements"></a>요구 사항: 
다중 아티팩트 데이터베이스 지원을 설정 하기 전에이 기능을 통해 다중 노드 호출이 발생 하므로 모든 노드에서 업데이트를 실행 하 고 이진 파일을 업데이트 합니다. 
  1. 아티팩트 DB를 만드는 배포 스크립트를 생성 합니다. 여러 아티팩트 DB 인스턴스를 배포 하기 위해 관리자는 아티팩트 DB에 대 한 SQL 배포 스크립트를 생성 해야 합니다. 이 업데이트의 일부로 기존 `Export-AdfsDeploymentSQLScript`cmdlet은 SQL 배포 스크립트를 생성할 AD FS 데이터베이스를 지정 하는 매개 변수를 선택적으로 사용 하도록 업데이트 되었습니다. 
 
 예를 들어 아티팩트 DB에 대해서만 배포 스크립트를 생성 하려면 `-DatabaseType` 매개 변수를 지정 하 고 값 "아티팩트"를 전달 합니다. 선택적 `-DatabaseType` 매개 변수는 AD FS 데이터베이스 유형을 지정 하 고 다음과 같이 설정할 수 있습니다. 모두 (기본값), 아티팩트 또는 구성입니다. 매개 변수 `-DatabaseType` 를 지정 하지 않으면 스크립트는 아티팩트와 구성 스크립트를 모두 구성 합니다.  

   ```PowerShell
   PS C:\> Export-AdfsDeploymentSQLScript -DestinationFolder <script folder where scripts will be created> -ServiceAccountName <domain\serviceaccount> -DatabaseType "Artifact" 
   ```
SQL 컴퓨터에서 생성 된 스크립트를 실행 하 여 필요한 데이터베이스를 만들고 해당 데이터베이스에 대 한 SQL SA 사용 권한을 AD FS 서비스 계정에 부여 해야 합니다.

 2. 배포 스크립트를 사용 하 여 아티팩트 DB를 만듭니다. 새로 생성 된 CreateDB. .sql 및 SetPermissions 배포 스크립트를 SQL server 컴퓨터에 복사 하 고 실행 하 여 로컬 아티팩트 DB를 만듭니다. 
 
 3. 구성 파일을 수정 하 여 아티팩트 DB 연결을 추가 합니다. 
 AD FS 노드의 구성 파일로 이동 하 고 "IdentityServer" 섹션 아래에서 새로 구성 된 ArtifactDB에 진입점을 추가 합니다. 

 >[!NOTE] 
 > artifactStore 및 connectionString은 대/소문자를 구분 합니다. 올바르게 구성 되었는지 확인 합니다. &lt;artifactStore connectionString = "Data Source = .\SQLInstance; Integrated Security = True; 초기 카탈로그 = AdfsArtifactStore"/&gt; 
>
>Sql 연결에 일치 하는 데이터 원본 값을 사용 합니다.



 4. 변경 내용을 적용 하려면 AD FS 서비스를 다시 시작 합니다. 
 
 >[!NOTE] 
 > SQL 복제 또는 아티팩트 데이터베이스 간의 동기화를 사용 하지 않는 것이 좋습니다. 데이터 센터 당 하나의 아티팩트 데이터베이스를 설정 하는 것이 좋습니다. 
 
### <a name="cross-datacenter-failover-and-database-recovery"></a>데이터 센터 간 장애 조치 (failover) 및 데이터베이스 복구  
마스터 아티팩트 데이터베이스와 동일한 데이터 센터에 장애 조치 아티팩트 데이터베이스를 만드는 것이 좋습니다. 장애 조치 (failover)가 발생 하는 경우 대기 시간이 증가 하지 않습니다. 데이터 센터에서 아티팩트 데이터베이스를 장애 조치 (Failover) 하지 않는 것이 좋습니다. 다음은 여러 아티팩트 데이터베이스에서 OAuth, SAML, ESL 및 token 재생 검색 기능을 호출 하는 방법에 대 한 세부 정보입니다. 
 - **OAuth 및 SAML** 

   OAuth 및 SAML 아티팩트 요청의 경우 노드는 구성 파일에 있는 아티팩트 DB에 아티팩트를 만듭니다. 구성 파일이 아티팩트 데이터베이스 연결을 포함 하지 않는 경우에는 공통 아티팩트 DB를 사용 합니다. 아티팩트를 인출 하는 다음 요청이 다른 노드로 이동 하면 다른 노드는 아티팩트 DB에서 아티팩트를 인출 하기 위해 rest API를 첫 번째 노드로 만듭니다. 이는 다른 노드에 아티팩트 데이터베이스가 여러 개 있을 수 있으며 노드에서이를 알지 못하는 경우에 필요 합니다. 첫 번째 노드가 다운 되 면 아티팩트 확인이 실패 합니다. 이 설계로 인해 여러 데이터 센터에 걸쳐 아티팩트 DB를 복제 하는 것은 필요 하지 않습니다. 하나의 전체 데이터 센터가 다운 된 경우 아티팩트를 만든 노드도 다운 되어 아티팩트를 더 이상 확인할 수 없습니다.  

 - **엑스트라넷 잠금** 

    구성 파일에서 참조 되는 아티팩트 데이터베이스는 엑스트라넷 잠금 데이터에 사용 됩니다. 그러나 ESL 기능의 경우 AD FS는 아티팩트 DB에 데이터를 기록 하는 마스터를 선택 합니다. 모든 노드는 마스터 노드에 대 한 REST API 호출을 수행 하 여 각 사용자에 대 한 최신 정보를 가져오고 설정 합니다. 여러 아티팩트 DB를 사용 하는 경우 관리자는 각 아티팩트 DB 또는 데이터 센터에 대 한 마스터 노드를 선택 해야 합니다. 

    ESL 마스터로 사용할 노드를 선택 하려면 ADFS 노드의 구성 파일로 이동 하 고 "IdentityServer" 섹션 아래에 다음을 추가 합니다.       
    
    마스터에서 다음 항목을 추가 합니다. 세 키는 모두 대/소문자를 구분 합니다. 

    &lt;useractivityfarmrole masterFQDN = [선택한 주 복제본의 FQDN] isMaster = "true"/&gt;
    
    다른 노드에서 다음 항목을 추가 합니다.

   &lt;useractivityfarmrole masterFQDN = [선택한 기본의 FQDN] isMaster = "false"/&gt;
 
    >[!NOTE] 
    >여러 아티팩트 데이터베이스에서 데이터를 동기화 하지 않기 때문에 ESL 값은 아티팩트 Db 간에 동기화 되지 않습니다.
    사용자는 잠재적으로 요청에 대해 다른 데이터 센터에 도달할 수 있으므로 ExtranetLockoutThreshold는 아티팩트 Db 수, ExtranetLockoutThreshold * 수의 아티팩트 Db 수에 따라 달라 집니다. 
 
  - **토큰 재생 검색** 
    
    토큰 재생 검색 데이터는 항상 중앙 아티팩트 데이터베이스에서 호출 됩니다. AD FS은 클레임 공급자 트러스트에서 토큰을 저장 하 여 동일한 토큰을 재생할 수 없도록 합니다. 공격자가 동일한 토큰을 재생 하려고 하면 AD FS는 해당 토큰이 아티팩트 DB에 있는지를 확인 합니다. 토큰이 있는 경우 요청이 거부 됩니다. 아티팩트 DB 데이터가 복제 되지 않기 때문에 중앙 아티팩트 데이터베이스는 보안에 사용 됩니다. 공격자는 다른 데이터 센터에 요청을 보내고 토큰을 재생할 수 있습니다. ArtifactDB의 추가 읽기 전용 복사본을 만들면 중앙 아티팩트 데이터베이스만 사용 되므로이 시나리오에서 데이터 센터 간 대기 시간이 방지 되지 않습니다.    
 
 