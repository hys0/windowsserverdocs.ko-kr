---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: 포리스트 루트 도메인 컨트롤러 배치 계획
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 57eafcc884a827d98c249e2da0c0af6888abc5b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823644"
---
# <a name="planning-forest-root-domain-controller-placement"></a>포리스트 루트 도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 루트 도메인 컨트롤러 자체 이외의 도메인의 리소스에 액세스 해야 하는 클라이언트에 대 한 트러스트 경로 만드는 데 필요한 합니다. 허브 위치 및 데이터 센터를 호스팅하는 곳에는 포리스트 루트 도메인 컨트롤러를 배치 합니다. 지정된 된 위치에서 사용자가 동일한 위치에서 다른 도메인의 리소스에 액세스 해야 하는 경우 데이터 센터와 사용자 위치 간의 네트워크 가용성 안정적이 지 않습니다. 위치에는 포리스트 루트 도메인 컨트롤러를 추가 하거나 만들기를 두 도메인 간에 바로 가기 트러스트 합니다. 보다 비용 효과적으로 포리스트 루트 도메인 컨트롤러를 해당 위치에 배치 하는 다른 이유가 없다면 도메인 간에 바로 가기 트러스트를 만들 것입니다.  
  
바로 가기 트러스트는 도메인에 위치한 사용자의 인증 요청을 최적화 하는 데 도움이 됩니다. 바로 가기 트러스트 도메인 간에 대 한 자세한 내용은 문서를 참조 하세요 [바로 가기 트러스트를 만들어야 할 경우 이해](https://go.microsoft.com/fwlink/?LinkId=107061)합니다.  
  
포리스트 루트 도메인 컨트롤러 배치를 문서화 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 다운로드 "도메인 컨트롤러 배치" (DSSTOPO_4.doc)를 엽니다.  
  
포리스트 루트 도메인을 만들 때이 정보를 참조 해야 합니다. 포리스트 루트 도메인을 배포 하는 방법에 대 한 자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
