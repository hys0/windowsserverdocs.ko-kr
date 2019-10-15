---
title: Hyper-v를 실행 하는 서버에는 도메인 구성원 자격이 좋습니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f4578e5-0848-46b4-a50b-7dbd480b80bf
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 48ea52e962f2f476d1428a69bab6c6e38c4ec005
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364917"
---
# <a name="domain-membership-is-recommended-for-servers-running-hyper-v"></a>Hyper-v를 실행 하는 서버에는 도메인 구성원 자격이 좋습니다.

>적용 대상: Windows Server 2016


  
*모범 사례 및 검사에 대한 자세한 내용은* [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*이 서버는 작업 그룹의 구성원입니다.*  
  
## <a name="impact"></a>영향  
  
*이 서버에 대 한 중앙 관리가 없습니다.*  
  
이 컴퓨터를 도메인에 가입 id, 보안 및 감사에 대 한 정책을 통해 중앙에서 관리할 수 있습니다.  
  
## <a name="resolution"></a>해결 방법  
  
*도메인 환경을 사용할 수 있는 경우이 서버를 해당 도메인에 가입 시킵니다.*  
  
> [!IMPORTANT]  
> 이 컴퓨터를 도메인에 참가할의 보안 의미 지 확인 하기 위해이 컴퓨터에 가상 컴퓨터에서 실행 되는 작업을 검토 하는 것이 좋습니다. 가상 컴퓨터가 가상화 된 도메인 컨트롤러인 경우 [가상화 된 도메인 컨트롤러에 대 한 고려 사항 계획](https://go.microsoft.com/fwlink/?LinkId=190192) (https://go.microsoft.com/fwlink/?LinkId=190192) 을 참조 하세요.  
  
컴퓨터를 도메인에 추가 컴퓨터와 도메인에 대 한 권한이 필요 합니다.   
- 컴퓨터에서 Administrators 그룹의 구성원 인 사용자 계정이 필요 합니다. 이 유형의 계정으로 로그온 하거나 메시지가 나타나면 계정의 사용자 이름 및 암호를 제공 합니다.   
- 도메인에서 컴퓨터를 도메인에 연결할 수 있는 권한이 있는 사용자 계정이 필요 합니다. 사용자 이름 및 암호에 대 한 라는 메시지가 표시 됩니다.  
  
지침은 [도메인에 컴퓨터 가입](https://go.microsoft.com/fwlink/?LinkId=190193) (https://go.microsoft.com/fwlink/?LinkId=190193) 을 참조 하세요.  
  


