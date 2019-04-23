---
title: 추가 기능 설치
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62e4f07-c2ba-4c5e-b30c-bdc287cd654e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d00cb6886e812ee2b780ad79e1fba44442e279ad
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833074"
---
# <a name="install-add-ins"></a>추가 기능 설치

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

이미지를 만들기 전에 추가 기능을 설치하여 모든 서버 또는 클라이언트 컴퓨터에 해당 추가 기능을 포함할 수 있습니다. 이렇게 하면 해당 이미지를 사용하여 복제된 모든 컴퓨터에 이 추가 기능이 자동으로 포함됩니다. .wssx 파일을 실행하여 추가 기능을 설치하거나 각 유형의 추가 기능에 대한 [SDK 문서](https://go.microsoft.com/fwlink/?LinkID=248648)의 지침에 따라 개별 추가 기능 파일을 설치할 수 있습니다. .wssx 파일을 사용하여 설치하는 경우 추가 기능 관리자를 통해 추가 기능을 제거할 수 있습니다. 개별 파일을 설치하는 경우에는 추가 기능 관리자에서 추가 기능이 관리되지 않습니다.  
  
> [!NOTE]
>  서버에 설치되거나 다운로드되는 모든 소프트웨어(대시보드 탭 및 상태 알림 포함)에는 서버에 설치되어 있는 운영 체제의 언어와 일치하는 현지화된 인터페이스가 있어야 합니다.  
  
#### <a name="to-install-an-add-in"></a>추가 기능을 설치하려면  
  
1.  (선택 사항) .wssx 파일을 사용하여 추가 기능을 설치하려면 다음 단계를 수행합니다.  
  
    1.  저장 된 < 추가 기능 이름\>.wssx 파일 참조 컴퓨터에 있습니다.  
  
    2.  추가 기능 설치 마법사를 열려면 .wssx 파일을 두 번 클릭합니다.  
  
    3.  마법사의 지침에 따라 설치를 완료합니다.  
  
2.  (선택 사항) SDK에 정의된 대로 각 추가 기능 유형에 대해 적절한 위치에서 개별 추가 기능 파일을 설치합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)