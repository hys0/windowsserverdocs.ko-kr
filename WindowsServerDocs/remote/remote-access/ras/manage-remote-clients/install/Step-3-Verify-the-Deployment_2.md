---
title: 3 단계 배포 확인
description: 이 항목은 Windows Server 2016에서 원격으로 DirectAccess 클라이언트 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 81ac8bf7321df915330d8d706fa5ba3912b8f54c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367301"
---
# <a name="step-3-verify-the-deployment"></a>3 단계 배포 확인

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 DirectAccess 클라이언트의 원격 관리를 위해 배포를 올바르게 구성 했는지 확인 하는 방법에 대해 설명 합니다.  
  
### <a name="to-verify-proper-deployment"></a>적절 한 배포를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결 하 고 그룹 정책 개체를 가져옵니다.  
  
2.  클라이언트 컴퓨터의 알림 영역에서 **네트워크 연결** 아이콘을 클릭 하 여 DirectAccess 미디어 관리자에 액세스 합니다.  
  
3.  **DirectAccess 연결**을 클릭 하면 상태가 **로컬로 연결**됨이 표시 됩니다.  
  
4.  회사 네트워크에서 컴퓨터를 제거 하 고 공용 네트워크에 연결 합니다.  
  
5.  명령 프롬프트에서 **nltest/dsgetdc: [정규화 된 도메인 이름]** 을 입력 합니다. 이 명령은 회사 네트워크를 클라이언트에서 액세스할 수 있는지 확인 합니다. 도메인 컨트롤러에 액세스할 수 없는 경우 다음 오류 메시지가 표시 됩니다. 도메인이 존재 하지 않는 것으로 보고 합니다. ERROR_NO_SUCH_DOMAIN.  
  


