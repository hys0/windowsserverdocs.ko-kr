---
title: 사용자 환경 테스트
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 1b1a2040-4cfd-48bf-8d04-3ffde9c26b9b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 938b64d96111a3ed128ec184acde56f20cb1abda
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819786"
---
# <a name="testing-the-customer-experience"></a>사용자 환경 테스트

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

고객의 환경을 검증하고 파트너 사용자 지정을 확인하려면 대상 컴퓨터의 초기 구성을 실행합니다. 적어도 한 번 이상 수동으로 초기 구성을 완료하여 사용자 환경을 살펴보는 것이 좋습니다. 대시보드를 공동 브랜드로 만든 경우 초기 구성을 완료하여 브랜딩을 확인해야 합니다. 원격 웹 액세스 사이트를 공동 브랜드로 설정한 경우에는 http://< servername\>에 액세스 하 여 브랜딩을 확인 해야 합니다 (< servername\>은 서버 이름). cfg.ini 파일의 초기 구성 섹션을 사용하여 사용자 환경 테스트를 자동화할 수 있습니다. cfg.ini 파일에서 이 섹션을 만드는 방법에 대한 자세한 내용은 [Cfg.ini 파일 만들기](Create-the-Cfg.ini-File.md)를 참조하세요.  
  
> [!IMPORTANT]
>  초기 구성 환경을 테스트하려면 먼저 Sysprep.exe 명령을 실행하여 배포를 위한 이미지를 준비해야 합니다. Sysprep.exe 실행에 대한 자세한 내용은 [배포 이미지 준비](Preparing-the-Image-for-Deployment.md)를 참조하세요.  
  
> [!IMPORTANT]
>  초기 구성을 테스트하려면 네트워크 연결이 필요합니다. 서버에는 DHCP가 구성되거나 설치되어 있지 않습니다. 즉, 방해를 받지 않고 네트워크 테스트를 수행하도록 설정되어 있습니다.  
  
 파트너 지원 정보를 확인하려면 대시보드에서 도움말 단추 옆에 있는 아래쪽 화살표를 클릭하세요.  
  
## <a name="see-also"></a>관련 항목  
 [이미지  만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)  
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)