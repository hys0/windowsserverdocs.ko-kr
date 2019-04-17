---
ms.assetid: ffb9d63c-ba7c-4ad1-b814-6db67f98c943
title: "클레임 파이프라인 역할"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5076a686b5d0b9a539f6cad8594aaf84dccc3edb
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-the-claims-pipeline"></a>클레임 파이프라인 역할
클레임 파이프라인 Active Directory Federation Services \(AD FS\)에서 실행 될 수 있는 하기 전에 Federation 서비스를 통해 클레임 따라야 경로 나타냅니다. Federation 서비스 클레임 파이프라인도 클레임 규칙 엔진에서 클레임 규칙의 처리를 포함 하는 다양 한 단계를 통해 친 클레임 전체 end\ to\ 엔드 프로세스를 관리 합니다.  
  
클레임은 규칙에 대 한 자세한 내용은 참조 [주장 규칙의 역할은](The-Role-of-Claim-Rules.md)합니다. 클레임 규칙 엔진 규칙을 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다.  
  
다음 섹션 Federation 서비스 자세히 감독 프로세스를 설명 합니다.  
  
## <a name="claims-pipeline-process"></a>클레임 파이프라인 프로세스  
청구 파이프라인 프로세스의 세 수준 high\ 단계 구성 됩니다. 이 과정에서 각 단계 단계 관련 된 프로세스 클레임 규칙을 클레임 규칙 엔진을 초기화 합니다. 이러한 단계는 \ (순서에서 했음을 occur\):  
  
1.  클레임 수신 허용 등 클레임 파이프라인에서이 단계 들어오는 클레임 토큰에서 압축을 풀고 클레임 필요 합니다. 또는 신뢰할 수 없는 되지을 제거 하는 데 사용 됩니다. 을 푼 후 수용 규칙 수용 변환 규칙을 구성 하는 공급자 신뢰 실행 청구에 대 한 설정 합니다. 이 규칙 통과 클레임 파이프라인의 다음 단계에 다음 사용할 수 있는 새로운 클레임 추가 하거나 사용할 수 있습니다. 이 단계 출력 세 번째 영웅 입력으로 사용 됩니다.  
  
2.  클레임 요청 자가 승인-클레임 엔진에서 발급 허용 하거나 토큰 요청 자가 여부 지정된 당사자에 대 한 토큰을 가져올 수 있는지 여부에 따라 클레임 거부 하려면이 단계는 사용 합니다. 그러나 하기 전에이 발급 승인 규칙 중 하나를 구성 하는 부여 규칙 설정 하거나 위임 인증 규칙에 대 한 설정 신뢰 파티 신뢰를 실행 합니다.  
  
3.  보내는 클레임 발급-이 단계 보내는 클레임 발급 및 파이프라인와 함께 보낼 보안 토큰으로 패키지 수 있는 하는 데 사용 됩니다. 그러나 전에 신뢰 파티 보안에 대 한에서 발급 변환 규칙을 구성 하는 발급 규칙은 실행 발생할 수 보내는 클레임으로 발생 하는 내용을 주장 결정 됩니다 합니다.  
  
위의 모든 3 단계 처리 클레임 규칙을 수행 하지만 다른 사용 규칙의 합니다. 각 단계 관련된 된 일련의 들어오는 클레임 발행인이에 따라 규칙은 위에서 설명한 대로 \(the acceptance rules\) 또는 대상 서비스는 claimincludes는 발급 \ (인증과 발급 rules\).  
  
클레임은 token\을 알 수 없는 아니지만 보안 토큰에 네트워크로 전송 됩니다. 클레임은 규칙 송수신 보안 토큰 형식에 관계 없이 클레임을 통해 작동합니다.  
  
청구 규칙 administrator\ 정의 논리는 클레임 엔진은 들어오는 클레임을 적용 요청 자가 id를 기반 클레임 권한을 부여 하 고 청구 하는 문제를 포함 한 당사자가 필요 합니다. 결국 클레임 클레임 클레임 파이프라인 통해 흐릅니다 된가 후 발생 하는 보안 토큰으로 지급 됩니다 결정 하는 클레임 엔진입니다.  
  
다음 그림와 같이 클레임 파이프라인은 전체 end\ to\ 엔드 프로세스 신뢰 파티 신뢰를 통해 전송 될 발급된 클레임 결국 하기 위해 다양 한 파이프라인 단계를 통해 클레임 흐르는를 담당 합니다. 그림에서 보내는 클레임이 발급된 클레임을 나타냅니다.  
  
![광고 FS 역할](media/adfs2_pipeline.gif)  
  
그림에서 표시 되지 않는 있지만 규칙의 실제 처리 각 단계를 수행 하는 클레임 엔진입니다. 자세한 내용은 참조 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다.  
  

