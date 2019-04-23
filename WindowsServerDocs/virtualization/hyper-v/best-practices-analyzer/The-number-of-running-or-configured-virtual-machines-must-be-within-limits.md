---
title: 실행 수 또는 구성 된 가상 컴퓨터는 지원 되는 제한 내에 있어야 합니다.
description: 이 모범 사례 분석기 규칙에 의해 보고 된 문제를 해결 하려면 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9d3c4aa3-8416-46ec-a253-26dc98088d7b
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8a971a48b2d8199a6c279f1bd3f1715039fa6e0d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855354"
---
# <a name="the-number-of-running-or-configured-virtual-machines-must-be-within-supported-limits"></a>실행 수 또는 구성 된 가상 컴퓨터는 지원 되는 제한 내에 있어야 합니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 나타나는 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*더 많은 가상 컴퓨터 실행 중이거나 지 원하는 것 보다 구성 합니다.*  
  
## <a name="impact"></a>영향  
*Microsoft는이 서버에 구성 되어 있거나 실행 중인 가상 컴퓨터의 현재 수를 지원 하지 않습니다.*  
  
## <a name="resolution"></a>해결 방법  
*하나 이상의 가상 머신을 다른 서버로 이동 합니다.*  
  
Hyper-v를 실행 중인 가상 컴퓨터의 수와 같은 지원 되는 최대 구성에 대 한 자세한 참조 [Windows Server 2016의 Hyper-v 확장성에 대 한 계획](../plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)합니다.  
  
가상 컴퓨터를 다른 서버로 이동 하려면 다음을 수행할 수 있습니다.  
  
- 현재 서버에서 가상 컴퓨터를 내보내고 아래 설명 된 대로 새 서버로 가져옵니다.   
- 실시간 마이그레이션을 수행 합니다.   
    - 이 서버에 장애 조치 클러스터에 속한 경우 장애 조치 클러스터링 기능을 제공 하는 도구를 사용 합니다. 자세한 내용은 [실시간 마이그레이션, 빠른 마이그레이션 또는 노드로 노드에서 가상 컴퓨터 이동](https://go.microsoft.com/fwlink/?LinkID=181519)합니다.  
    - 독립 실행형 서버인 경우에 지침을 참조 하십시오. [실시간 마이그레이션 구성 및 장애 조치 클러스터링 없이 가상 컴퓨터 마이그레이션](https://technet.microsoft.com//library/jj134199(v=ws.11).aspx)  
  
### <a name="to-export-a-virtual-machine"></a>가상 컴퓨터를 내보내려면  
  
   > [!IMPORTANT]  
   > 도메인에 속한 Hyper-v 호스트에서 내보내는 원격 위치에 내보낸된 파일을 저장 하려는 경우 제한 된 위임을 위해 Hyper-v 호스트를 구성 합니다. 원격 위치는 공유 네트워크 폴더 또는으로 가져오는 호스트에 있는 폴더 수 있습니다. 제한 된 위임에는 원격 컴퓨터에 인터넷 파일 시스템 CIFS (Common) 서비스에 대 한 위임 된 자격 증명을 제공 합니다. Hyper-v 호스트의 컴퓨터 계정을 수 있습니다. 제한 된 위임 구성에 관한 내보내기 다음 섹션을 참조 하 고 아래 지침을 가져옵니다.  
  
1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 한 다음 클릭 **내보내기**합니다.  
  
3.  에 **가상 컴퓨터를 내보낼** 대화 상자, 형식 또는 모든 가상 컴퓨터 리소스를 저장할 충분 한 여유 공간이 있는 위치로 이동 합니다. 가상 컴퓨터를 내보낼 때 모든 가상 하드 디스크 (.vhd 파일 또는.vhdx 파일), (.avhd 파일), 검사점 및 가상 컴퓨터와 연결 된 저장 된 상태 파일은 지정 된 폴더에 복사 됩니다.  
  
4.  **내보내기**를 클릭합니다.  
  
가상 컴퓨터를 내보낸 후 다른 서버에 가상 컴퓨터를 가져옵니다.  
  
### <a name="to-import-a-virtual-machine-to-another-server"></a>가상 컴퓨터를 다른 서버로 가져오려면  
  
1.  Hyper-v를 실행 하는 서버에 연결 하 고 Hyper-v 관리자를 엽니다.  
  
2.  에 **작업** 창에서 클릭 **가상 컴퓨터 가져오기**합니다.  
  
3.  에 **가상 컴퓨터 가져오기** 대화 상자에서 내보낸 가상 컴퓨터의 위치를 지정 합니다. 이 가상 컴퓨터를 다시 가져오는 하려는 경우가 아니면 가져오기 설정을 그대로 둡니다.  
  
4.  **가져오기**를 클릭합니다.  
  
### <a name="to-configure-constrained-delegation"></a>제한된 위임을 구성하려면  
  
멤버는 **도메인 관리자** 그룹은이 절차를 완료 해야 합니다.  
  
1.  Active Directory 도메인 서비스 도구 기능이 설치 된 컴퓨터에서 **관리 도구**, 개방형 **Active Directory 사용자 및 컴퓨터**, Hyper-v를 실행 하는 컴퓨터에 대 한 컴퓨터 계정으로 이동 합니다.  
  
    > [!NOTE]  
    > **Active Directory 사용자 및 컴퓨터**가 나열되지 않는 경우 Active Directory 도메인 서비스 도구 기능을 설치합니다. 자세한 내용은 [AD DS 용 원격 서버 관리 도구 설치](https://go.microsoft.com/fwlink/?LinkId=140463) (https://go.microsoft.com/fwlink/?LinkId=140463)합니다.  
  
2.  Hyper-v를 실행 하는 컴퓨터에 대 한 컴퓨터 계정을 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **속성**합니다.  
  
3.  **위임** 탭에서 **지정한 서비스에 대한 위임용으로만 이 컴퓨터 트러스트**를 클릭한 다음 **인증 프로토콜 사용**을 클릭합니다.  
  
4.  Hyper-v 컴퓨터 계정이 원격 컴퓨터에 위임 된 자격 증명을 표시 하도록 수 있도록 합니다.  
  
    1.  **추가**를 클릭합니다.  
  
    2.  에 **서비스 추가** 대화 상자를 클릭 하 여 **사용자 또는 컴퓨터**, 원격 컴퓨터를 선택 하 고 클릭 한 다음 **확인**.  
  
    3.  에 **사용 가능한 서비스** 목록에서 선택 된 **cifs** (서버 메시지 블록 (SMB) 프로토콜 라고도 함) 프로토콜을 클릭 하 고 **추가**.  
  
  
  


