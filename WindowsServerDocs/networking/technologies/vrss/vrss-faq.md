---
title: vRSS 질문과 대답
description: 이 항목에서는 몇 가지 자주 묻는 질문 및 답변 vRSS를 사용 하 여 찾습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 61ae242e-82a8-430d-b07d-52b86c01e686
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3fafe6c39285e65a9d39a76cc6b652dac5c3efbd
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133819"
---
# vRSS 질문과 대답

이 항목에서는 몇 가지 자주 묻는 질문 및 답변 vRSS를 사용 하 여 찾습니다.

## VRSS를 사용 하는 실제 네트워크 어댑터에 대 한 요구 사항은 무엇입니까?

네트워크 어댑터 가상 컴퓨터 큐 \(VMQ\)와 호환 되어야 하 고 10 g b p s의 연결 속도 이상이 있어야 합니다.

자세한 내용은 [vRSS 사용 계획](vrss-plan.md)을 참조 하세요.

## VRSS는 hyper\ 스레드 프로세서 코어를 사용 하 여 작동 하나요?

아니요. VRSS와 VMQ hyper\ 스레드 프로세서 코어를 무시합니다.

## 호스트 가상 Nic \(vNICs\)에 대 한 vRSS 작동 하나요?

그렇습니다. **Set VMNetworkAdapter** Windows PowerShell 명령에 가상 컴퓨터 \(VM\) 이름과 호스트 vNIC를 **통해 NetAdapterRss** 대신 **-ManagementOS** 매개 변수를 사용 합니다.

자세한 내용은 [Windows PowerShell 명령 RSS 및 vRSS를](vrss-wps.md)참조 하세요.

## VM에서 vRSS를 사용 하 여 몇 개의 논리 프로세서가 필요 합니까?

Vm 두 개 이상의 논리 프로세서 \(LPs\) vRSS 사용할 수 있도록 해야 합니다.

자세한 내용은 [vRSS 사용 계획](vrss-plan.md)을 참조 하세요.

## NIC 팀 호환 vRSS 인가요?

그렇습니다. NIC 팀을 사용 하는 경우에 VMQ NIC 팀 설정과 함께 작동 하도록 적절 하 게 구성 하는 것이 중요 합니다. NIC 팀 배포 및 관리 하는 방법에 대 한 자세한 내용은 [NIC 팀](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)을 참조 하세요.

## vRSS 활성화 되지만 작동 하는지 확인 하는 방법. 

VM에서 작업 관리자를 열고 가상 프로세서 사용률을 검토 하 vRSS 작동을 확인할 수 있습니다. VM에 설정 하는 여러 연결 되어 있는 경우 위에 사용률이 0% 이상의 코어를 볼 수 있습니다.

단일 TCP 세션에는 여러 논리 프로세서 코어 균형 될 수 없으므로, VM 해야 받을 여러 TCP 세션 vRSS 작동 하는지 여부를 확인 합니다.

VM 여러 TCP 세션을 수신 하는 경우 둘 이상의 LP 핵심 사용률이 0% 위에 표시 되지 않으면 완료 [vRSS 사용할 계획인](vrss-plan.md)항목의 준비 단계를 모두 확인 합니다.

## 호스트 보고 및 사용 중인 모든 프로세서. 모든 다른 하나는 건너뛰는 것 같습니다.
  
하이퍼 스레딩를 사용할 수 있는지 확인 합니다. VMQ와 vRSS는 코어 hyper\ 스레드 건너뛸 하도록 설계 되었습니다.

## 다른 Windows PowerShell 명령을 RSS 및 vRSS 있습니까?

그렇기도 하고 그렇지 않기도 하고. 기본 호스트에서 RSS 및 Vm에서 RSS 모두에 동일한 명령을 사용 하는 동안 vRSS 스위치 포트에서 사용할 수와 VM 및 vRSS 물리적 NIC-에서 사용할 수 있는 VMQ 필요 합니다.

자세한 내용은 [Windows PowerShell 명령 RSS 및 vRSS를](vrss-wps.md)참조 하세요.

---
