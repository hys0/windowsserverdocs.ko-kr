---
title: 코드 무결성에 대 한 Windows Server 가상화 기반 보호와 호환 되는 하드웨어
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 15ded82c-f70f-4efb-9e26-2731127931af
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5a9a4b91cc3528ce59f8ef3e4952b6162ca5c74e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403686"
---
# <a name="compatible-hardware-with-windows-server-virtualization-based-protection-of-code-integrity"></a>코드 무결성에 대 한 Windows Server 가상화 기반 보호와 호환 되는 하드웨어

>적용 대상: Windows server 2019, Windows Server (반기 채널), Windows Server 2016

Windows Server 2016에는 시스템 코드를 수정 하는 공격 으로부터 실제 및 가상 컴퓨터를 보호 하는 데 도움이 되는 새로운 가상화 기반 코드 보호가 도입 되었습니다. 이러한 높은 보호 수준을 실현 하기 위해 Microsoft는 컴퓨터 하드웨어 제조업체 (원래 장비 제조업체 또는 Oem)와 협력 하 여 악의적인 쓰기를 시스템 실행 코드로 방지 합니다. 이 보호는 모든 시스템에 적용할 수 있으며 보호 된 Vm (가상 컴퓨터)에 대 한 Hyper-v 호스트 상태를 구현 하는 구성 요소 중 하나로 사용 됩니다. 

모든 하드웨어 기반 보호와 마찬가지로 일부 시스템은 메모리 페이지를 실행 파일로 잘못 표시 하거나 런타임에 코드를 수정 하려고 하는 등의 문제로 인해 호환 되지 않을 수 있습니다 .이로 인해 데이터 손실이 나 blue를 포함 하 여 예기치 않은 오류가 발생할 수 있습니다. 화면 오류 (중지 오류가 라고도 함) 

새 보안 기능을 완벽 하 게 지원 하기 위해 Oem은 1 월 2016에 게시 된 UEFI 2.6에 정의 된 메모리 주소 테이블을 구현 해야 합니다. 새 UEFI 표준 도입에는 시간이 소요 됩니다. 그 동안에는 고객이 문제를 발생 하는 것을 방지 하기 위해이 기능 집합을 테스트 한 시스템 및 구성과 호환 되지 않는 것으로 알고 있는 시스템에 대 한 정보를 제공 하려고 합니다. 

## <a name="non-compatible-systems"></a>호환 되지 않는 시스템

다음 구성은 코드 무결성의 가상화 기반 보호와 호환 되지 않는 것으로 알려져 있으며 보호 된 Vm의 호스트로 사용할 수 없습니다.

- PERC H330 RAID 컨트롤러를 실행 하는 dell PowerEdge 서버 자세한 내용은 다음 문서를 참조 하세요. [Win 2016 OS에서 "호스트 보호자 Hyper-v 지원" 또는 "Device Guard"를 사용 하도록 설정 하는 경우에는 os 부팅 오류가 발생](http://www.dell.com/Support/Article/us/en/19/QNA44045)합니다.  


## <a name="compatible-systems"></a>호환 시스템

이러한 시스템은 microsoft의 환경에서 테스트 하 고 있습니다. 사용자 환경에서 시스템이 예상 대로 작동 하는지 확인 합니다. 

- Virtual Machines – Windows Server 2016부터 시작 하 여 Hyper-v 호스트에서 실행 되는 가상 컴퓨터에서 코드 무결성의 가상화 기반 보호를 사용 하도록 설정할 수 있습니다.



