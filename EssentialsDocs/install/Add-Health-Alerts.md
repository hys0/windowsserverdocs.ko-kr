---
title: 상태 경고 추가
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 270e0aac-dc42-46f3-a20b-a68ffbded06d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cf0c062b92c687f5f7b33b419eafdca2dd3bbbfc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828514"
---
# <a name="add-health-alerts"></a>상태 경고 추가

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

상태 추가 기능은 알림, 상태 검사 및 네트워크 문제 복구에 대한 정의를 제공합니다. 상태 추가 기능은 특정 기능에 대한 상태 정보를 평가하기 위해 사용하는 코드나 데이터에 주석을 추가하는 xml 파일로 구성되어 있습니다. 상태 추가 기능은 개발자가 만들고 관리자에 의해 서버 및 클라이언트 컴퓨터에 설치됩니다.  
  
 상태 추가 기능을 만드는 방법에 대한 자세한 내용은 [Windows Server Solutions SDK](https://go.microsoft.com/fwlink/?LinkID=248648) 를 참조하세요.  
  
## <a name="installing-health-add-in-files"></a>상태 추가 기능 파일 설치  
 개발자가 xml 파일을 만들고 나면 사용자는 서버와 클라이언트 컴퓨터에서 적절한 위치에 파일의 복사본을 배치해야 합니다.  
  
#### <a name="to-install-the-xml-files-on-the-server"></a>서버에 xml 파일을 설치하려면  
  
1.  **%ProgramFiles%\Windows Server\Bin\Feature Definitions** 폴더에서 이름이 **MyHealthAddIn**인 새 폴더를 만듭니다. 이 폴더에 임의의 이름을 지정할 수 있습니다. 폴더 이름은 기능 이름과 동일하게 지정하는 것이 좋습니다.  
  
2.  Definition.xml 및 Definition.xml.config 파일을 새 폴더에 복사합니다.  
  
3.  조건이나 작업에 대한 이진 파일을 만든 경우 이러한 파일을 **%ProgramFiles%\Windows Server\Bin**에도 복사해야 합니다.  
  
 클라이언트 컴퓨터는 XML 파일을 적절한 위치로 가져오는 예약된 작업을 6시간마다 실행합니다. 작업을 수동으로 실행하여 클라이언트 컴퓨터와 서버 간 동기화를 강제로 실행할 수 있습니다.  
  
#### <a name="to-install-the-xml-files-on-the-client-computer"></a>클라이언트 컴퓨터에 xml 파일을 설치하려면  
  
1.  작업 Scheduler를 엽니다.  
  
2.  작업 Scheduler에서 **HealthDefintionUpdateTask**를 실행합니다.  
  
    > [!NOTE]
    >  이 작업은 이진 파일을 설치하지 않습니다. 클라이언트 컴퓨터의 **%ProgramFiles%\Windows Server\Bin** 폴더에 이진 파일을 수동으로 복사해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가 사용자 지정](Additional-Customizations.md)   
 [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)   
 [사용자 환경 테스트](Testing-the-Customer-Experience.md)