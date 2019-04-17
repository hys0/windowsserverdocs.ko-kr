---
title: "건강 알림 추가"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="add-health-alerts"></a>건강 알림 추가

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

건강 추가 기능에서 정의 알림과 상태 확인 네트워크 문제에 대 한 수리를 제공합니다. 건강 추가 기능에 코드 또는 특정 기능에 대 한 의료 정보를 확인 하는 데 사용 하는 데이터에 주석을 단 xml 파일 이루어져 있습니다. 건강 추가 기능은 개발자가 만든 및 관리자가 컴퓨터에 설치 되어 있습니다.  
  
 참조 하십시오는 [Windows Server 솔루션 SDK](https://go.microsoft.com/fwlink/?LinkID=248648) 건강 추가 기능에 대 한 자세한 내용은 합니다.  
  
## <a name="installing-health-add-in-files"></a>파일에서 추가 기능 설치 건강  
 개발자가 파일 xml를 만든 후 파일의 복사본 클라이언트 컴퓨터에 적절 한 위치에 배치 해야 합니다.  
  
#### <a name="to-install-the-xml-files-on-the-server"></a>서버에서 xml 파일을 설치 하려면  
  
1.  에 **%ProgramFiles%\Windows Server\Bin\Feature 정의** 폴더를 새 폴더 만들기 **MyHealthAddIn**합니다. 이 폴더 이름을 지정할 수 있습니다. 폴더의 이름을 기능 이름과 같은 된다는 것이 좋습니다.  
  
2.  Definition.xml 및 Definition.xml.config 파일을 새 폴더로 복사 합니다.  
  
3.  해당 파일을 복사도 해야 조건 나 소송에 대해 이진 파일, 만든 경우 **%ProgramFiles%\Windows 실행**합니다.  
  
 클라이언트 컴퓨터 예약된 작업 6 시간 마다 XML 파일 해당 위치를 가져오는 실행 합니다. 직접 작업을 실행 하 여 서버 클라이언트 컴퓨터와 동기화를 할 수 있습니다.  
  
#### <a name="to-install-the-xml-files-on-the-client-computer"></a>가지의 xml 파일을 설치 하려면  
  
1.  작업 스케줄러를 엽니다.  
  
2.  실행는 **HealthDefintionUpdateTask** 작업 스케줄러에서 합니다.  
  
    > [!NOTE]
    >  이 작업 이진 파일을 설치 하지 않습니다. 수동으로 이진 파일을 복사 해야는 **%ProgramFiles%\Windows 실행** 클라이언트 컴퓨터에서 폴더 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [만들기 및 이미지를 사용자 지정](Creating-and-Customizing-the-Image.md)   
 [추가로 사용자 지정](Additional-Customizations.md)   
 [배포에 대 한 이미지를 준비 중](Preparing-the-Image-for-Deployment.md)   
 [고객 만족도 테스트합니다.](Testing-the-Customer-Experience.md)