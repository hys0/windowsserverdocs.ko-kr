---
ms.assetid: 0cd1ac70-532c-416d-9de6-6f920a300a45
title: 장애 조치 클러스터에 대 한 클라우드 감시 배포
ms.prod: windows-server-threshold
manager: eldenc
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.topic: article
author: JasonGerend
ms.date: 01/18/2019
description: Microsoft Azure를 사용 하 여-클라우드에서 Windows Server 장애 조치 클러스터에 대 한 미러링 모니터 서버를 호스트 하는 방법을 클라우드 감시 배포 방법 즉, 합니다.
ms.openlocfilehash: f7e1c84e54f08044a772f06e591588c1add33026
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857984"
---
# <a name="deploy-a-cloud-witness-for-a-failover-cluster"></a>장애 조치(failover) 클러스터용 클라우드 감시 배포

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

클라우드 감시는 클러스터 쿼럼의 투표 수 있도록 Microsoft Azure를 사용 하는 장애 조치 클러스터 쿼럼 감시의 형식입니다. 이 항목에서는 클라우드 감시 기능, 시나리오, 지원 및 장애 조치 클러스터에 대 한 클라우드 감시를 구성 하는 방법에 대 한 지침 개요를 제공 합니다.

## <a name="CloudWitnessOverview"></a>클라우드 미러링 모니터 개요

그림 1 Windows Server 2016을 사용 하 여 다중 사이트 확장 된 장애 조치 클러스터 쿼럼 구성을 보여 줍니다. (그림 1)에이 예제에서는 구성에서에 노드 2 개의 데이터 센터 (사이트 라고 함). Note 2 개 데이터 센터에 걸쳐 클러스터에 대 한 것이 가능 합니다. 또한 각 데이터 센터에는 2 개 이상의 노드가 있을 수 있습니다. (자동 장애 조치 SLA)이 설치이 프로그램에서 일반적인 클러스터 쿼럼 구성 각 노드에 투표를 제공합니다. 정전이 발생 하나 데이터 센터 중 하나를 실행 중인 경우에 유지 하는 클러스터를 허용 하도록 쿼럼 감시 추가 투표 지정 됩니다. 수학 간단-총 투표 수를 5 가지 하 고 클러스터가 실행 되도록 하는 데 3 투표를 해야 합니다.  

![다른 사이트 2 노드 2 개를 사용 하 여 사이트에서 세 번째 별도 파일 공유 감시](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_1.png "파일 공유 감시")  
**그림 1: 쿼럼 감시 파일 공유 감시를 사용 하 여**  

하나의 데이터 센터에서 전원 중단이 계속 실행 하기 위해 다른 데이터 센터에서 클러스터에 대 한 기회를 제공 것이 좋습니다 두 데이터 센터와 다른 위치에서 쿼럼 감시를 호스트 합니다. 이 일반적으로 세 번째 요구 하는 방법을 구분 데이터 센터 (사이트) 파일 서버를 호스팅하도록이 쿼럼 감시 (파일 공유 감시)로 사용 되는 파일 공유를 지원 합니다.  

대부분의 조직에서는 세 번째 파일 공유 미러링 모니터 서버를 백업 하는 파일 서버를 호스트 하는 데이터 센터를 구분 하지 않습니다. 즉, 조직에서는 기본적으로 확장 하는 기본 데이터 센터는 해당 데이터 센터를 사용 하면 두 데이터 센터 중 하나에서 파일 서버를 호스트 합니다. 시나리오에서 다른 데이터 센터에는 필요한 3 개 응답의 쿼럼 과반수 아래에 있는 2 응답으로 클러스터는 다운 정전에 있는 경우 기본 데이터 센터 위치입니다. 파일 서버를 호스트 하는 각기 다른 세 번째 데이터 센터에 있는 고객, 파일 공유 감시를 지 원하는 항상 사용 가능한 파일 서버를 유지 관리 오버 헤드입니다. 상당한 오버 헤드가 설치 및 유지 관리는 게스트 OS에서 실행 되는 파일 공유 감시에 대 한 파일 서버는 공용 클라우드의 가상 컴퓨터를 호스트 합니다.  

클라우드 감시는 새로운 유형의 장애 조치 클러스터 쿼럼 감시는 중재 지점 (그림 2)으로 Microsoft Azure를 활용 하는 기능입니다. 스플릿 브레인 확인 시 중재 지점으로 사용 되는 blob 파일에 대 한 읽기/쓰기 Azure Blob Storage를 사용 합니다.  

중요 한 가지는이 이렇게 혜택:
1. Microsoft Azure (별도 세 번째 데이터 센터에 대 한 필요 없음)를 활용합니다.  
2. 표준 사용 가능한 Azure Blob 저장소 (추가 유지 관리 오버 헤드 없이 공용 클라우드에서 호스팅되는 가상 컴퓨터의)을 사용 합니다.  
3. 여러 클러스터 (클러스터로 파일을 하나의 blob; blob 파일 이름으로 사용 하는 고유한 클러스터 id)에 대해 동일한 Azure Storage 계정은 사용할 수 있습니다.  
4. 저장소 계정 (매우 작은 데이터 blob 파일에는 클러스터 노드의 상태가 변경 될 때 한 번만 업데이트 된 blob 파일 마다 기록)에 지속적으로 $cost 매우 낮은 합니다.  
5. 기본 제공 클라우드 감시 리소스 형식입니다.  

![쿼럼 감시로 클라우드 감시를 사용 하 여 다중 사이트 확장된 클러스터를 보여 주는 다이어그램](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_2.png)  
**그림 2: 쿼럼 감시로 클라우드 감시를 사용 하 여 다중 사이트 확장된 클러스터**  

그림 2와 같이 필요한 별도 세 번째 사이트가 있습니다. 다른 쿼럼 감시와 같은 클라우드 감시는 응답을 가져오고 쿼럼 계산에 참여할 수 있습니다.  

## <a name="CloudWitnessSupportedScenarios"></a>클라우드 감시 합니다. 단일 미러링 모니터 서버 유형에 대 한 지원 되는 시나리오
경우 장애 조치 클러스터 배포 시 모든 노드 (Azure의 확장)에 의해 인터넷에 연결할 수 있는 쿼럼 감시 리소스와 클라우드 감시를 구성 하는 것이 좋습니다.  

지원 되는 시나리오의 일부 사용 클라우드 감시 쿼럼 감시는 다음과 같습니다.  
- 재해 복구는 다중 사이트 클러스터 (그림 2 참조)를 확장 합니다.  
- 공유 저장소 (SQL 항상에서 등) 하지 않고 장애 조치 클러스터입니다.  
- Microsoft Azure 가상 컴퓨터 역할 (또는 다른 공용 클라우드)에서 호스트 되는 게스트 OS 내에서 실행 되는 장애 조치 클러스터입니다.  
- 장애 조치 클러스터 내에서 게스트 OS Virtual Machines의 사설 클라우드에서 호스트를 실행 합니다.
- 스케일 아웃 파일 서버 클러스터와 같은 저장소 클러스터 공유 저장소 없이 합니다.  
- 소규모 지점 클러스터 (2 노드 클러스터)  

Windows Server 2012 R2부터 것이 좋습니다 항상 클러스터 감시 응답을 자동으로 관리 및 노드 투표 동적 쿼럼 감시를 구성 합니다.  

## <a name="CloudWitnessSetUp"></a> 클러스터에 대 한 클라우드 감시를 설정
클러스터용 쿼럼 감시로 클라우드 감시를 설정 하려면 다음 단계를 수행 합니다.
1. 클라우드 감시를 사용 하려면 Azure Storage 계정 만들기
2. 클러스터용 쿼럼 감시로 클라우드 감시를 구성 합니다.

## <a name="create-an-azure-storage-account-to-use-as-a-cloud-witness"></a>클라우드 감시를 사용 하려면 Azure Storage 계정 만들기

이 섹션에서는 저장소 계정, 보기 및 복사 끝점 Url를 만들고 해당 계정에 대 한 키 액세스 하는 방법을 설명 합니다.

클라우드 감시를 구성 하려면 (중재에 사용) 하 여 blob 파일을 저장할 수 있는 유효한 Azure 저장소 계정의 있어야 합니다. 클라우드 감시는 잘 알려진 컨테이너를 만듭니다 **msft 클라우드 감시** Microsoft Storage 계정. 클라우드 감시 쓰기 해당 단일 blob 파일을 클러스터의 고유 ID가이 아래에 있는 blob 파일의 파일 이름으로 사용 **msft 클라우드 감시** 컨테이너입니다. 이 여러 다른 클러스터에 대 한 클라우드 감시를 구성 하는 동일한 Microsoft Azure Storage 계정을 사용할 수는 것을 의미 합니다.

여러 다양 한 클라우드 감시를 구성 하기 위한 동일한 Azure Storage 계정을 사용 하는 경우 클러스터를 단일 **msft 클라우드 감시** 컨테이너는 자동으로 생성 됩니다. 이 컨테이너에는 클러스터당 하나 blob 파일이 포함 됩니다.

### <a name="to-create-an-azure-storage-account"></a>Azure storage 계정을 만들려면

1. 에 로그인 합니다 [Azure Portal](http://portal.azure.com)합니다.
2. 허브 메뉴에서 선택-> 새 데이터 + 저장소-저장소 계정 >.
3. 만들기의 저장소 계정 페이지에서 다음을 수행 합니다.
    1. 저장소 계정의 이름을 입력 합니다.
    <br>Storage 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다. 저장소 계정 이름은 Azure 내에서 고유 수도 있어야 합니다.
        
    2. 에 대 한 **계정 종류**를 선택 **범용**합니다.
    <br>Blob 저장소 계정을 클라우드 감시를 사용할 수 없습니다.
    3. 에 대 한 **성능**를 선택 **표준**합니다.
    <br>클라우드 감시에 대 한 Azure Premium Storage를 사용할 수 없습니다.
    2. 에 대 한 **복제**를 선택 **로컬 중복 저장소 (LRS)** 합니다.
    <br>장애 조치 클러스터링 데이터를 읽을 때 일부 일관성 보장 해야 하는 중재 지점으로 blob 파일을 사용 합니다. 따라서 선택 해야 합니다 **로컬 중복 저장소** 에 대 한 **복제** 형식입니다.

### <a name="view-and-copy-storage-access-keys-for-your-azure-storage-account"></a>Azure 저장소 계정의 저장소 액세스 키 보기 및 복사

Microsoft Azure 저장소 계정을 만들면 2 개의 액세스 키-자동으로 생성 된 기본 액세스 키 및 보조 액세스 키를 사용 하 여 연결 됩니다. 첫 번째 클라우드 감시 만들기를 사용 합니다 **기본 액세스 키**합니다. 클라우드 감시에 사용할 키에 대 한 제한은 없습니다.  

#### <a name="to-view-and-copy-storage-access-keys"></a>보기 및 저장소 액세스 키를 복사 하려면

Azure Portal에서 저장소 계정으로 이동, 클릭 **모든 설정** 클릭 하 고 **액세스 키** 보기, 복사 및 계정 액세스 키 다시 생성 합니다. 액세스 키 블레이드에서 (그림 4 참조) 응용 프로그램에서 사용 하 여 복사할 수 있는 기본 및 보조 키를 사용 하 여 미리 구성된 된 연결 문자열도 포함 됩니다.

![Microsoft Azure에서 액세스 키 관리 대화 상자의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_4.png)  
**그림 4: 저장소 액세스 키**

### <a name="view-and-copy-endpoint-url-links"></a>보기 및 끝점 URL 링크를 복사 합니다.  
저장소 계정을 만든 경우 다음 Url 형식을 사용 하 여 생성 됩니다. `https://<Storage Account Name>.<Storage Type>.<Endpoint>`  

클라우드 감시는 항상 사용 **Blob** 저장 유형으로 합니다. Azure 사용 **. core.windows.net** 끝점으로 합니다. 클라우드 감시를 구성할 때 구성 하는 다른 끝점을 사용 하 여 (예: 다른 끝점에 중국의 Microsoft Azure 데이터 센터) 시나리오에 따라 가능한 것입니다.  

> [!NOTE]  
> 끝점 URL은 클라우드 감시 리소스에서 자동으로 생성 됩니다 하 고는 URL에 대해 필요한 구성의 추가 단계가 없습니다.  

#### <a name="to-view-and-copy-endpoint-url-links"></a>끝점 URL 링크 보기 및 복사
Azure Portal에서 저장소 계정으로 이동를 클릭 **모든 설정** 클릭 하 고 **속성** 를 보고 (그림 5 참조) 끝점 Url을 복사 합니다.  

![클라우드 감시 끝점 링크의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_5.png)  
**그림 5: 클라우드 미러링 모니터 서버 끝점 URL 링크**

Azure Storage 계정을 만들고 관리 하는 방법에 대 한 자세한 내용은 참조 하세요. [Azure Storage 계정 정보](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)

## <a name="configure-cloud-witness-as-a-quorum-witness-for-your-cluster"></a>클러스터 쿼럼 감시로 클라우드 감시를 구성 합니다.
클라우드 미러링 모니터 서버 구성은 장애 조치 클러스터 관리자를 작성 하 여 기존 쿼럼 구성 마법사 내에서 잘 통합 합니다.  

### <a name="to-configure-cloud-witness-as-a-quorum-witness"></a>쿼럼 감시로 클라우드 감시를 구성 하려면
1. 장애 조치 클러스터 관리자를 시작 합니다.
2. 클러스터-> 마우스 오른쪽 단추로 클릭 **기타 작업** -> **클러스터 쿼럼 설정 구성** (그림 6 참조). 클러스터 쿼럼 구성 마법사가 시작 됩니다.  
    ![장애 조치 클러스터 관리자 UI에서 구성 클러스터 쿼럼 설정 메뉴 경로의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_7.png) **그림 6. 클러스터 쿼럼 설정**

3. 에 **쿼럼 구성 선택** 페이지에서 선택 **쿼럼 감시 선택** (그림 7 참조).  

    !['Select quotrum 미러링 모니터 서버'의 스냅숏이 라디오 단추에서 클러스터 쿼럼 마법사](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_8.png)  
    **그림 7입니다. 쿼럼 구성 선택**

4. 에 **쿼럼 감시 선택** 페이지에서 선택 **클라우드 감시를 구성** (그림 8 참조).  

    ![클라우드 감시를 선택 하려면 적절 한 라디오 단추의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_9.png)  
    **그림 8입니다. 쿼럼 감시 선택**  

5. 에 **클라우드 감시 구성** 페이지에서 다음 정보를 입력 합니다.  
    1. (필수 매개 변수) Azure Storage 계정 이름입니다.  
    2. (필수 매개 변수) 저장소 계정에 해당 하는 액세스 키입니다.  
        1. 를 처음 만들 때 사용할 기본 액세스 키 (그림 5 참조)  
        2. 보조 액세스 키를 사용 하 여 기본 액세스 키를 회전 하는 경우 (그림 5 참조)  
    3. (선택적 매개 변수) 다른 Azure 서비스 끝점 (예: 중국의 Microsoft Azure 서비스)을 사용 하려는 경우에 서버 엔드포인트를 업데이트 합니다.  

    ![클러스터 쿼럼 마법사에서 클라우드 감시 구성 창의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_10.png)  
    **그림 9: 클라우드 감시를 구성 합니다.**

6. 클라우드 미러링 모니터의 구성을 성공적으로으로 볼 수 있습니다 새로 만든된 감시 리소스 장애 조치 클러스터 관리자 스냅인 (그림 10 참조).

    ![성공적인 클라우드 감시 구성](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_11.png)  
    **그림 10: 성공적인 클라우드 감시 구성**

### <a name="configuring-cloud-witness-using-powershell"></a>PowerShell을 사용 하 여 클라우드 감시를 구성 합니다.  
기존 Set-clusterquorum PowerShell 명령에 해당 클라우드 감시 하는 새 추가 매개 변수입니다.  

클라우드 감시를 사용 하 여 구성할 수 있습니다 합니다 [ `Set-ClusterQuorum` ](https://technet.microsoft.com/library/ee461013.aspx) 다음 PowerShell 명령을:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey>
```

경우에서 다른 끝점 (드 묾)을 사용 해야 합니다.  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> -Endpoint <servername>  
```

### <a name="azure-storage-account-considerations-with-cloud-witness"></a>클라우드 감시를 사용 하 여 azure 저장소 계정 고려 사항  
장애 조치 클러스터용 쿼럼 감시로 클라우드 감시를 구성할 때 다음 사항을 고려 합니다.
* 액세스 키를 저장 하는 대신 장애 조치 클러스터 생성 되며 안전 하 게 공유 액세스 보안 (SAS) 토큰을 저장 합니다.  
* 생성된 된 SAS 토큰 액세스 키를 유효한 동안 유효 합니다. 기본 액세스 키를 회전 하는 경우에 먼저 기본 액세스 키 다시 생성 하기 전에 보조 액세스 키를 사용 하 여 (해당 저장소 계정을 사용 하는 모든 클러스터)에서 클라우드 감시를 업데이트 해야 합니다.  
* 클라우드 감시는 Azure Storage 계정 서비스의 HTTPS REST 인터페이스를 사용합니다. 즉, HTTPS 포트를 모든 클러스터 노드에서 열어야 필요 합니다.

### <a name="proxy-considerations-with-cloud-witness"></a>클라우드 감시를 사용 하 여 프록시 고려 사항  
클라우드 감시는 Azure blob 서비스에 연결 하려면 HTTPS (기본 포트 443)를 사용 합니다. HTTPS 포트에 네트워크 프록시를 통해 액세스할 수 있는지 확인 합니다.

## <a name="see-also"></a>관련 항목
- [Windows Server에서 장애 조치 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)
