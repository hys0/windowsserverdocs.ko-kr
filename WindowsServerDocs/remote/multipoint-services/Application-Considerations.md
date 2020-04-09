---
title: 응용 프로그램 고려 사항
description: MultiPoint 서비스의 앱에 대 한 호환성 정보
ms.prod: windows-server
ms.technology: multipoint-services
ms.topic: article
ms.assetid: 445e6184-4e1e-4f10-ad3c-042f2a6c2f5f
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: 04449db18febdb2e37ac5ef7f5eee4dfc02ba94d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859366"
---
# <a name="application-considerations"></a>응용 프로그램 고려 사항
  
## <a name="application-compatibility"></a>응용 프로그램 호환성

MultiPoint 서비스 시스템에서 실행 하려는 모든 응용 프로그램은 다음 요구 사항을 충족 해야 합니다.
  
- Windows Server 2016에 설치 하 고 실행 해야 합니다. 
- 각 사용자가 MultiPoint 시스템에서 앱 인스턴스를 실행할 수 있도록 세션을 인식 해야 합니다.
  
응용 프로그램에서이 요구 사항을 지정 하는 경우 응용 프로그램을 설치 하 고 원격 데스크톱 세션에서 사용 하는 것이 좋습니다. 

## <a name="addressing-application-compatibility-problems"></a>응용 프로그램 호환성 문제 해결  
MultiPoint 서비스는 동일한 호스트 컴퓨터에서 실행 되는 Windows 10 Enterprise edition의 전체 인스턴스에 스테이션을 연결 하는 옵션을 제공 합니다. 여러 사용자에 대해 여러 인스턴스를 실행 하지 않거나 64 비트 운영 체제에 설치 하지 않는 중요 한 응용 프로그램의 경우이 솔루션을 사용할 수 있습니다. 이러한 방식으로 데스크톱을 배포 하려면 다중 포인트 관리자의 가상 데스크톱 탭을 사용 하 여 다음을 수행 해야 합니다.  
  
-   가상 데스크톱 사용  
-   바탕 화면 템플릿 만들기  
-   문제 응용 프로그램을 사용 하 여 템플릿 사용자 지정  
-   사용자 지정 된 템플릿과 스테이션 연결  

각 스테이션은 동일한 템플릿에서 시작 하므로 컴퓨터가 시작 될 때마다 변경 내용이 모두 지워집니다.  
  
>[!NOTE] 
>MultiPoint에서 실행 하려는 응용 프로그램에 대 한 라이선스 요구 사항을 확인 하는 것이 중요 합니다. 하나의 복사 응용 프로그램을 설치 하는 경우에는 사용자별 라이선스가 필요할 수 있습니다.  
  
