---
title: 무선 네트워크 지원 구성
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4d7020d4-fd46-4858-a406-de5c0f21ea06
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 4ce5f167339d7910b10f90bea5bbeae5606b5cf2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312212"
---
# <a name="configure-support-for-a-wireless-network"></a>무선 네트워크 지원 구성

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

무선 네트워크를 지원하도록 운영 체제를 구성할 수 있습니다. 서버에서 무선 지원을 사용하도록 설정하려면 다음 요구 사항을 충족해야 합니다.  
  
-   서버에 유선 네트워크 어댑터가 설치되어 있어야 합니다.  
  
-   운영 체제에서 네트워크 어댑터가 지원되지 않는 경우 무선 네트워크 어댑터에 대해 올바른 드라이버를 사전 설치해야 합니다.  
  
-   무선 네트워크 어댑터를 사용하거나 사용하지 않도록 설정하는 기능을 사용할 수 있어야 합니다. 이를 수행하기 위한 방법으로 서버의 물리적 단추 또는 대시보드의 사용자 지정 사용자 인터페이스가 포함될 수 있습니다. 제품 설명서에서는 무선 네트워크 어댑터를 사용하거나 사용하지 않도록 설정하는 단계를 제공해야 합니다.  
  
-   무선 네트워크를 선택하고 연결하는 기능을 사용할 수 있어야 합니다. 이 작업은 대시보드에 사용자 지정 사용자 인터페이스를 추가하여 수행해야 합니다. 제품 설명서에서는 무선 네트워크를 선택하고 연결하는 단계를 제공해야 합니다.  
  
-   무선 임시 네트워크를 지원하는 기능이 필요한 경우 대시보드에서 확장된 사용자 인터페이스를 제공해야 합니다. 사용자 인터페이스는 Windows Server 2008 R2의 제어판에서 무선 임시 네트워크 설정 마법사를 시작하는 단추이거나 링크일 수 있습니다.  
  
## <a name="additional-considerations"></a>추가 고려 사항  
 무선 네트워크 지원을 구성할 경우 다음 정보도 고려해야 합니다.  
  
-   설치를 실행하려면 서버를 네트워크에 유선으로 연결해야 합니다.  
  
-   완전 복원을 수행하는 네트워크 컴퓨터는 유선으로 네트워크에 연결해야 합니다.  
  
-   서버의 완전 복원을 수행하려면 서버를 네트워크에 유선으로 연결해야 합니다.  
  
-   서버에 임시 네트워크를 만든 경우 무선 네트워크 어댑터는 임시 네트워크 전용이므로 사용자는 항상 네트워크 케이블을 서버에 연결하여 인터넷에 연결해야 합니다.  
  
> [!NOTE]
>  네트워크 연결 구성에 대한 자세한 내용은 [라우터 사전 구성](Preconfiguring-a-Router.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포할 이미지를 준비 하는 중](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)