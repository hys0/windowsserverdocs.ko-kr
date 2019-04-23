---
title: 복제 요청을 허용 하도록 복제 서버를 구성 해야
description: 이 모범 사례 분석기 규칙에 의해 보고 된 문제를 해결 하려면 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c5e30ddc50b176b83db081a29c6427356ab946c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827524"
---
# <a name="a-replica-server-must-be-configured-to-accept-replication-requests"></a>복제 요청을 허용 하도록 복제 서버를 구성 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>문제점  
*이 컴퓨터에서 Hyper-v 복제본 서버로 지정 되지만 주 서버에서 들어오는 복제 데이터를 허용 하도록 구성 되지 않았습니다.*  
  
## <a name="impact"></a>영향  
*이 서버는 주 서버에서 복제 트래픽을 받아들일 수 없습니다.*  
  
## <a name="resolution"></a>해결 방법  
*Hyper-v 관리자를 사용 하 여 지정 있는 주 서버가 복제본 서버로 복제 데이터를 허용 해야 합니다.*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 권한 부여 항목 만들기  
  
1.  Hyper-V 관리자를 엽니다. (서버 관리자에서 클릭 **도구** > **Hyper-v 관리자**.)  
  
2.  호스트 목록에서 마우스 오른쪽 단추로 입력 한 후 클릭 **Hyper-v 설정**합니다.  
  
3.  탐색 창에서 **복제 구성**합니다.  
  
4.  아래에서 **권한 부여 및 저장소**, 클릭 **지정된 된 서버 로부터의 복제도 허용**합니다.  
  
5.  서버 목록 아래 **추가**합니다.  
  
6.  아래에서 **권한 부여 항목을 추가**:  
  
    -   첫 번째 서버의 정규화 된 이름을 입력 합니다.  
  
    -   전용된만 해당 서버의 파일을 저장할 위치를 지정 합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  각 주 서버에 대해 반복 합니다.  
  
9. 클릭 **확인** 완료 하 여 창을 닫습니다.  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 권한 부여 항목 만들기  
  
1.  Windows PowerShell을 엽니다. (바탕 화면에서 시작을 클릭 하 고 입력 하기 시작 하면 **Windows PowerShell**.)  
  
2.  마우스 오른쪽 단추로 클릭 **Windows PowerShell** 클릭 **관리자 권한으로 실행**합니다.  
  
3.  다음과 비슷한 명령을 실행, 교체 합니다.  
  
    -   서버의 정규화 된 도메인 이름이 server01.domain01. contoso.com 인의 주 서버 이름입니다.  
  
    -   사용자의 위치와 D:\ReplicaVMStorage의 위치입니다.  
  
    -   신뢰 그룹 기본 이름 명명 된 그룹의 하나를 만든 경우. 그렇지 않으면 기본값을 사용 합니다.  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  


