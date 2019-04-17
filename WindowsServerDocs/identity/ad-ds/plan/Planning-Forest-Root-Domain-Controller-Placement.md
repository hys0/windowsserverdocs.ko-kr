---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: "숲 루트 도메인 컨트롤러 배치 계획"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 374ce31c61c666302e2b00a8f365c289cb8799f8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="planning-forest-root-domain-controller-placement"></a>숲 루트 도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

숲 루트 도메인 컨트롤러 자신의 이외의 도메인에 리소스에 액세스 해야 하는 클라이언트 신뢰 경로 만드는 데 필요한 합니다. 숲 루트 도메인 컨트롤러 허브 위치 및 위치 개최 된 데이터 센터에 배치 합니다. 사용자가 특정된 위치에 동일한 위치에 있는 다른 도메인의 리소스에 액세스 해야 하는 경우 사용자 위치 데이터 센터 사이의 네트워크 가용성은 신뢰할 수 있는 위치에 숲 루트 도메인 컨트롤러 추가 하거나 도메인 사이 바로 가기 신뢰를 만들 수 있습니다. 더 많은 비용 효과적으로 숲 루트 도메인 컨트롤러 해당 위치에 배치 다른 이유로 않은 경우 도메인 간에 바로 가기 신뢰를 만들입니다.  
  
도메인에 있는 사용자 로부터 인증 요청이 최적화 하기 위해 도움말을 신뢰 하는 바로 가기 합니다. 바로 가기 신뢰 하는 도메인 사이 대 한 자세한 내용은 참조 신뢰 하는 바로 가기를 만드는 경우 이해 ([https://go.microsoft.com/fwlink/?LinkId=107061](https://go.microsoft.com/fwlink/?LinkId=107061)).  
  
사용자 숲 루트 도메인 컨트롤러 배치 문서화에 도움을 주고 워크시트를 참조 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))를 다운로드 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 하 고 "도메인 컨트롤러 배치" (DSSTOPO_4.doc) 엽니다.  
  
숲 루트 도메인 만들 때이 정보를 참조할 해야 합니다. 숲 루트 도메인 배포에 대 한 자세한 내용은 참조 [Windows Server 2008 숲 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
  


