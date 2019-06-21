---
title: 4 단계 클러스터 확인
description: 이 항목은 Windows Server 2016에서 클러스터에 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22dcf10-b453-4664-a9ef-e40e95c72f63
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 424c4f881c168ea691dd51cd2d86a4a234c41075
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282985"
---
# <a name="step-4-verify-the-cluster"></a>4 단계 클러스터 확인

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 DirectAccess 클러스터 배포 올바르게 구성 되었는지 확인 하는 방법을 설명 합니다.  
  
### <a name="to-verify-access-to-internal-resources-through-the-cluster"></a>클러스터를 통해 내부 리소스에 대 한 액세스를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결하고 그룹 정책을 가져옵니다.  
  
2.  외부 네트워크에 클라이언트 컴퓨터를 연결하고 내부 리소스에 액세스를 시도합니다.  
  
    모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
3.  클러스터 서버 중 하나를 제외한 모든 외부 네트워크에서 연결 끊기 또는 해제, 클러스터의 각 서버를 통해 연결을 테스트 합니다. 클라이언트 컴퓨터에서 회사 리소스에 액세스 하려고 합니다. 다른 클러스터 서버에 대 한 테스트를 반복 합니다.  
  
    각 클러스터 서버를 통해 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  


