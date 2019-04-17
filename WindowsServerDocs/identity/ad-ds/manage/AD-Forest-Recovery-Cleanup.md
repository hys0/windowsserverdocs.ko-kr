---
title: "광고 숲 복구 정리"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 2f652d08304a17ecbfde51bbb6f35e4666cd9eca
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---cleanup"></a>광고 숲 복구 정리 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 다음과 같이 게시물 복구 필요에 따라 다음과 같습니다.  
  
-   전체 숲 복구한 구성 dc 각에 기본 및 보조 DNS 서버를 포함 하 여 원래 DNS 구성으로 되돌릴 수 있습니다. DNS 서버가 오작동 전에 했을 때 구성 요소를 이전의 이름을 확인 기능 복원 됩니다. DNS 레코드에 대 한 복구 되지 Dc 삭제 합니다.  
  
-   복구 되지 모든 dc Windows 인터넷 이름 서비스 (WINS) 기록이 삭제 됩니다.  
  
-   작업 마스터 역할 다른 dc 도메인 또는 숲에 전송 하 고 오류가 발생 하기 구성에 따라 글로벌 더 카탈로그 서버 추가할 수 있습니다.  
  
-   전체 숲을 이전 상태로 복원 되 면 때문에 추가 된 개체 (예: 사용자와 컴퓨터) 및이 시점 후에 기존 개체 수행 된 모든 업데이트 (예: 암호 변경) 손실 됩니다. 따라서 누락 개체를 다시 만드는 하 고 적절 하 게 누락 된 업데이트를 적용 해야 합니다.  
  
-   백업에서 이러한 외부 신뢰 관계를 자동으로 복원 되지 않는 때문에 보내는 신뢰 외부 도메인와 숲 복원 해야 할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  



