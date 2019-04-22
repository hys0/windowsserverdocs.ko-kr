---
title: 코드 무결성에 대 한 Windows Server 가상화 기반 보호를 사용 하 여 호환 되는 하드웨어
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: a52ff808af94159fe50c72bf0466768047ceea90
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820374"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>코드 무결성에 대 한 Windows Server 가상화 기반 보호를 사용 하 여 호환 되는 하드웨어

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

Windows Server 2016 시스템 코드를 수정 하는 공격 으로부터 물리적 보호 하기 위해 새 코드 가상화 기반 보호 및 virtual machines를 도입 합니다. 이 높은 보호 수준을 위해 Microsoft는 시스템 실행 코드로 컴퓨터 하드웨어 제조업체 (Original Equipment Manufacturer 또는 Oem) 악의적인 쓰기를 방지 하기 위해 함께에서 작동 합니다. 이 보호 시스템에 적용할 수 있습니다 및 보호 된 가상 컴퓨터 (Vm)에 대 한 Hyper-v 호스트 상태를 구현 하는 것에 대 한 구성 요소 중 하나로 사용 합니다. 

모든 하드웨어 기반 보호와 마찬가지로 일부 시스템 되지 않을 수 있습니다 실행 파일 또는 데이터 손실이 나 파란색을 비롯 한 예기치 않은 오류가 발생할 수 있는 런타임 시 코드를 수정 하 여 잘못 된 메모리 페이지 표시 등의 문제 때문에 규정 화면 오류가 발생 했습니다 (중지 오류 라고도 함). 

호환 되 고 완전히 새로운 보안 기능을 지원 하려면 Oem 2016 1 월에에서 게시 된 UEFI 2.6에 정의 된 메모리 주소 테이블을 구현 해야 합니다. 새 UEFI 표준 채택 시간이; 한편, 문제가 발생 하는 고객을 방지 하려면 하고자 호환 되지 않는 것을 알고 있는 시스템 뿐만 아니라 시스템 및이 기능을 사용 하 여 설정 테스트 된 구성에 대 한 정보를 제공 합니다. 

## <a name="non-compatible-systems"></a>호환 되지 않는 시스템

다음과 같은 구성이 호환 되지 않는 것으로 알려진 가상화 기반 보호를 사용 하 여 코드 무결성 및 보호 된 Vm의 호스트로 사용할 수 없습니다.

- Dell 지원의 다음 문서를 참조 하는 Dell PowerEdge 서버의 PERC H330 RAID 컨트롤러에 대 한 자세한 내용은 실행 [OS 부팅 오류를 유발 하는 H330 – 사용 하도록 설정 하면 "호스트 보호 Hyper-v 지원" 또는 "Device Guard" Win 2016 OS에서](http://www.dell.com/Support/Article/us/en/19/QNA44045)합니다.  


## <a name="compatible-systems"></a>호환 되는 시스템

이들은 환경에서 테스트 하 고 파트너 시스템입니다. 시스템 환경에서 예상 대로 작동을 확인 하는 있는지 확인 하십시오. 

- Virtual Machines-Windows Server 2016 부터는 Hyper-v 호스트에서 실행 되는 virtual machines에서 코드 무결성에 대 한 가상화 기반 보호를 사용할 수 있습니다.



