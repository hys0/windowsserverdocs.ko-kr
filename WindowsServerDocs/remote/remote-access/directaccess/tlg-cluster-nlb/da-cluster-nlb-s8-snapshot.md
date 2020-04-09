---
title: 8 단계 DirectAccess 클러스터 스냅숏-NLB 구성
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 915ef7dd-169d-4d58-9174-438d8ffa3584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 99804fb7746e0e45f586f7eaea307d8aac47d0ca
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818997"
---
# <a name="step-8-snapshot-the-directaccess-cluster-nlb-configuration"></a>8 단계 DirectAccess 클러스터 스냅숏-NLB 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

DirectAccess 테스트 랩을 완료 했습니다. NLB 클러스터 구성을 사용 하 여 작업 중인 DirectAccess로 신속 하 게 돌아갈 수 있도록이 구성을 저장 하려면 다른 DirectAccess 모듈식 테스트 랩 가이드, 테스트 랩 가이드 확장을 테스트 하거나 사용자의 실험 및 학습에 대해 다음을 수행 합니다. 다음  
  
1.  테스트 랩에 사용한 모든 물리적 컴퓨터 또는 가상 컴퓨터에서 모든 창을 닫고 정상 종료를 수행합니다.  
  
2.  가상 컴퓨터를 기반으로 하는 랩의 경우 각 가상 컴퓨터의 스냅숏을 저장 하 고 스냅숏 DirectAccess 클러스터 및 NLB의 이름을로 설정 합니다. 실제 컴퓨터를 사용 하는 랩의 경우에는 디스크 이미지를 만들어 DirectAccess 테스트 랩 구성을 저장 합니다.  
