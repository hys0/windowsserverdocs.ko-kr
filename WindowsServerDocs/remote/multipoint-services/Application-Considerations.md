---
title: 응용 프로그램 고려 사항
description: MultiPoint 서비스에서 앱에 대 한 호환성 정보
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 445e6184-4e1e-4f10-ad3c-042f2a6c2f5f
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 400f87c09f1b2e897d67f94e9b7ac12ae0a1e799
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839834"
---
# <a name="application-considerations"></a>응용 프로그램 고려 사항
  
## <a name="application-compatibility"></a>응용 프로그램 호환성

MultiPoint 서비스 시스템에서 실행 하려는 모든 응용 프로그램에는 다음 요구 사항을 충족 해야 합니다.
  
- 설치 하 고 Windows Server 2016에서 실행 
- 세션 인식 되므로 각 사용자 MultiPoint 시스템에서 앱의 인스턴스를 실행 해야 합니다.
  
응용 프로그램에서이 요구 사항은 지정 하는 경우 응용 프로그램을 설치 해 보십시오. 원격 데스크톱 세션에서 사용 하는 것이 좋습니다. 

## <a name="addressing-application-compatibility-problems"></a>응용 프로그램 호환성 문제 해결  
MultiPoint 서비스는 거의 동일한 호스트 컴퓨터에서 실행 하는 Windows 10 Enterprise 버전의 전체 인스턴스를 사용 하 여 스테이션을 연결 하는 옵션을 제공 합니다. 여러 사용자에 대 한 여러 인스턴스가 실행 되지 않거나 64 비트 운영 체제에 설치 되지 것입니다는 중요 한 응용 프로그램에 대 한 솔루션을 수 있습니다. 이러한 방식으로 데스크톱을 배포 하려면 다중 포인트 관리자에서 가상 데스크톱 탭을 사용 하 여 필요 합니다.  
  
-   가상 데스크톱을 사용 하도록 설정  
-   데스크톱 템플릿 만들기  
-   문제가 응용 프로그램을 사용 하 여 템플릿을 사용자 지정  
-   사용자 지정된 템플릿 사용 하 여 연결 스테이션  

각 스테이션 내용을 컴퓨터가 시작 될 때마다 초기화 됩니다 있도록 동일한 템플릿에서 시작 합니다.  
  
>[!NOTE] 
>MultiPoint에서 실행 하려는 응용 프로그램에 대 한 라이선스 요구를 확인 하는 것이 반드시 합니다. 하지만 설치 하는 하나의 복사 응용 프로그램은 사용자별 라이선스 필요할 수 있습니다.  
  
