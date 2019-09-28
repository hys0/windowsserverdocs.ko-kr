---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: 포리스트 루트 도메인 컨트롤러 배치 계획
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e619d5f5e9cc317f9ba1548d5ed3a32e7bd12c2c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402551"
---
# <a name="planning-forest-root-domain-controller-placement"></a>포리스트 루트 도메인 컨트롤러 배치 계획

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

포리스트 루트 도메인 컨트롤러는 자체가 아닌 도메인의 리소스에 액세스 해야 하는 클라이언트에 대 한 트러스트 경로를 만드는 데 필요 합니다. 허브 위치 및 데이터 센터를 호스트 하는 위치에 포리스트 루트 도메인 컨트롤러를 추가 합니다. 지정 된 위치의 사용자가 같은 위치에 있는 다른 도메인의 리소스에 액세스 해야 하 고 데이터 센터와 사용자 위치 간의 네트워크 가용성이 안정적이 지 않은 경우 해당 위치에 포리스트 루트 도메인 컨트롤러를 추가 하거나 만들 수 있습니다. 두 도메인 간의 바로 가기 트러스트입니다. 다른 이유로 포리스트 루트 도메인 컨트롤러를 해당 위치에 배치 해야 하는 경우가 아니면 도메인 간에 바로 가기 트러스트를 만드는 것이 더 효율적입니다.  
  
바로 가기 트러스트는 두 도메인에 있는 사용자 로부터 만든 인증 요청을 최적화 하는 데 도움이 됩니다. 도메인 간의 바로 가기 트러스트에 대 한 자세한 내용은 [바로 가기 트러스트를 만들어야 하는 경우 이해](https://go.microsoft.com/fwlink/?LinkId=107061)문서를 참조 하세요.  
  
포리스트 루트 도메인 컨트롤러 배치를 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://go.microsoft.com/fwlink/?LinkID=102558), 다운로드 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services 및 열기 "도메인을 참조 하세요. 컨트롤러 배치 "(DSSTOPO_4).  
  
포리스트 루트 도메인을 만들 때이 정보를 참조 해야 합니다. 포리스트 루트 도메인을 배포 하는 방법에 대 한 자세한 내용은 참조 [Windows Server 2008 포리스트 루트 도메인 배포](https://technet.microsoft.com/library/cc731174.aspx)합니다.  
