---
title: Windows 하이퍼바이저를 실행 중 이어야 합니다.
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 501a9beb-c464-46c0-88c5-e3e7e3e70101
author: KBDAzure
ms.date: 10/03/2016
ms.openlocfilehash: 51f863425bd1107894fb5e4d44ed7c742a806394
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393052"
---
# <a name="windows-hypervisor-must-be-running"></a>Windows 하이퍼바이저를 실행 중 이어야 합니다.

>적용 대상: Windows Server 2016
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|사전 요구 사항|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*Windows 하이퍼바이저가 실행 되 고 있지 않습니다.*  
  
## <a name="impact"></a>영향  
  
*Windows 하이퍼바이저가 실행 될 때까지 가상 컴퓨터를 시작할 수 없습니다.*  
  
## <a name="resolution"></a>해결 방법  
  
@no__t-Windows Server 카탈로그를 확인 하 여이 서버가 Hyper-v를 실행 하도록 한정 되어 있는지 확인 합니다. 다음으로, 하드웨어 기반 가상화 및 하드웨어 적용 데이터 실행 방지에 대 한 BIOS 설정 되어 있는지 확인 합니다. 그런 다음 Hyper-v-하이퍼바이저 이벤트 로그를 확인 합니다. *  
  
카탈로그를 확인 하려면 [Windows Server catalog](https://go.microsoft.com/fwlink/?LinkId=111228) (https://go.microsoft.com/fwlink/?LinkId=111228) 을 참조 하세요.  
  
> [!CAUTION]  
> 컴퓨터의 시스템 BIOS에서 특정 매개 변수를 변경 하는 해당 컴퓨터의 운영 체제를 로드 중지 될 수 있습니다 또는 수 있도록 하드 디스크 드라이브 등의 하드웨어 장치를 사용할 수 없습니다. 항상 시스템 BIOS를 구성 하는 적절 한 방법을 결정 하는 컴퓨터에 대 한 사용자 설명서를 참조 하십시오. 또한 매개 변수를 수정 하 고 필요한 경우 나중에 복원할 수 있도록 원래 값을 추적 하는 것이 좋습니다는 항상 있습니다. 시스템 BIOS에서 매개 변수를 변경한 후 문제를 발생 하는 경우 기본 설정 (옵션은 일반적으로 BIOS 구성 유틸리티에서 사용할 수 있는)를 로드 하려고 하거나 컴퓨터 제조업체에 문의 합니다.  
  
#### <a name="to-verify-virtualization-support-in-the-bios-or-uefi"></a>BIOS 또는 UEFI에서 가상화 지원을 확인 하려면  
  
1.  컴퓨터를 다시 시작 하 고 BIOS 또는 UEFI 구성 도구를 통해 액세스 합니다. 일반적으로 컴퓨터가 부팅 프로세스를 통과 하는 경우이 도구에 대 한 액세스는 사용할 수 있는입니다. 대부분의 컴퓨터를 설정한 후에 즉시 키 또는 키를 눌러 구성 도구를 열려면 조합을 나열 하는 몇 초 동안 메시지가 나타납니다.  
  
2.  하드웨어 적용 DEP 데이터 실행 방지 () 및 가상화에 대 한 설정을 찾아에 있다는 것을 확인 합니다. 다음은 구성 도구 및 기능은 이름이 될 수 있습니다의 예에 이러한 설정에 대 한 일반적인 메뉴 위치:  
  
    -   가상화 지원:  
  
        -   주요 프로세서 또는 성능에 대 한 설정에서 일반적으로 사용할 수 있습니다. 경우에 보안 설정 합니다.  
  
        -   "가상화" 또는 "가상화 기술"을 포함 하는 매개 변수 이름을 찾습니다.  
  
    -   하드웨어 적용 DEP:  
  
        -   보안 이나 메모리 설정에서 일반적으로 사용할 수 있습니다.  
  
        -   "실행", "실행" 또는 "방지"를 포함 하는 매개 변수 이름을 찾습니다.  
  
3.  필요한 경우 구성 도구를 사용 하는 지침에 따라 설정에 설정 합니다. 변경 내용을 저장 하 고 종료 합니다.  
  
4.  전원을 끈 다음 다시 로그온 하 변경 내용이 있으면 완료.  
  
    > [!IMPORTANT]  
    > 좋습니다 전원을 끄지 껐다가 다시 켭니다 (전원 주기가 라고도 함)을이 해당할 때까지 일부 컴퓨터에서 변경 내용이 적용 되지 않습니다.  
  
다음으로, 하이퍼-V-하이퍼바이저 이벤트 로그를 확인 합니다. 문제가 있으면 시스템 로그에서 확인할 수 있습니다.  
  
#### <a name="to-check-the-event-logs"></a>이벤트 로그를 확인 하려면  
  
1.  이벤트 뷰어를 엽니다. 클릭 **시작**, 클릭 **관리 도구**, 를 클릭 하 고 **이벤트 뷰어**합니다.  
  
2.  하이퍼-V-하이퍼바이저 이벤트 로그를 엽니다. 탐색 창에서 확장 **응용 프로그램 및 서비스 로그** >> **Microsoft** >> **Windows** >> **하이퍼-V-하이퍼바이저**, 를 클릭 하 고 **Operational**합니다.  
  
3.  Windows 하이퍼바이저를 실행 하는 경우 추가 작업이 없으므로 필요 합니다. Windows 하이퍼바이저 실행 중이 아닌 경우이 작업을 수행 합니다.  
  
4.  시스템 로그를 엽니다. (탐색 창에서 확장 **Windows 로그** 선택한 다음 **시스템**.)  
  
5.  하이퍼-V-하이퍼바이저 이벤트를 찾는 필터를 사용 합니다.   
    1. 에 **작업** 창에서 클릭 **현재 로그 필터링**합니다. 에 대 한 **이벤트 소스**, "하이퍼-V-하이퍼바이저"를 지정 합니다.   
    2. 문제를 보고 하는 이벤트를 찾아보십시오. 예를 들어 이벤트 ID 41은 BIOS 구성에 문제가 있음을 나타냅니다. "Hyper-v를 시작 하지 못했습니다. .VMX가 없거나 BIOS에서 사용 하도록 설정 되어 있지 않습니다. "  
  
### <a name="see-also"></a>관련 항목  
컴퓨터가 하이퍼-V를 실행할 수 있는지 확인 하는 방법을 비롯 하 여 Windows 10에서는 Hyper-v를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [Windows 10 Hyper-v 시스템 요구 사항](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_compatibility)합니다. 


