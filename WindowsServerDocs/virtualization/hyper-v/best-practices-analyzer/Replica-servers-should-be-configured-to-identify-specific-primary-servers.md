---
title: 복제 트래픽을 보낼 수 있는 권한이 고유한 기본 서버를 식별 하도록 복제 서버를 구성 해야
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 649af22f615f2f36baceb1fa23b79c54b038f9c2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861836"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>복제 트래픽을 보낼 수 있는 권한이 고유한 기본 서버를 식별 하도록 복제 서버를 구성 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*구성 된 대로이 복제 서버는 모든 주 서버에서 복제 트래픽을 받아서 단일 위치에 저장 합니다.*  
  
### <a name="impact"></a>영향  
*모든 주 서버의 모든 복제는 한 위치에 저장 되므로 개인 정보나 보안 문제가 발생할 수 있습니다.*  
  
## <a name="resolution"></a>해상도  
*Hyper-v 관리자를 사용 하 여 특정 주 서버에 대 한 새 권한 부여 항목을 만들고 각각에 대해 별도의 저장소 위치를 지정 합니다. 와일드 카드 문자를 사용 하 여 각 권한 부여 항목에 대 한 기본 서버를 집합으로 그룹화 할 수 있습니다.*  
  
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
  
## <a name="see-also"></a>참고 항목  
[New-vmreplicationauthorizationentry](https://technet.microsoft.com/library/hh848606.aspx)  
  


