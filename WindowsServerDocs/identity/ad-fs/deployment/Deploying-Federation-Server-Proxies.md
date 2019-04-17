---
ms.assetid: 1b21b0a9-1fe6-4fd1-8a25-92e578d774ed
title: "Federation 서버 프록시 배포"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b914141a0445febd3961b688aadc2f444b2eee7b
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="deploying-federation-server-proxies"></a>Federation 서버 프록시 배포

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Federation 서버 프록시 Active Directory Federation Services \(AD FS\)를 배포 하려면 각에서 작업을 완료 [검사: 설정을을 Federation 서버 프록시](Checklist--Setting-Up-a-Federation-Server-Proxy.md)합니다.  
  
> [!NOTE]  
> 이 검사를 사용 하면 먼저 federation 서버 프록시 계획의 지침에 대 한 언급을 읽고는 것이 좋습니다는 [Windows Server 2012에서 광고 FS 디자인 가이드](https://technet.microsoft.com/library/dd807036.aspx) 서버 구성 하는 절차를 시작 하기 전에 합니다. Federation에 대 한 배포 및 디자인 프로세스를 더 잘 이해 프록시 서버 제공 검사를 수행 합니다.  
  
## <a name="about-federation-server-proxies"></a>Federation 서버 프록시 정보  
Federation 서버 프록시 역할 프록시 역할에서을 수동으로 구성 된® Windows Server 2012와 ADFS 소프트웨어를 실행 하는 컴퓨터가 있습니다. 인터넷 클라이언트와 회사 네트워크에서 방화벽으로 보호 된 federation 서버 중간 서비스를 제공 하기 위해 federation 서버 프록시 조직에서 사용할 수 있습니다.  
  
> [!NOTE]  
> 하지만 federation 서버 및 federation 서버 프록시 역할 동일한 컴퓨터에 설치할 수 없으므로 federation 서버 federation 서버 프록시 기능을 수행할 수 있습니다. 자세한 내용은 참조 [Federation 서버를 만들 때](https://technet.microsoft.com/library/dd807101.aspx)합니다.  
  
ADFS 소프트웨어® Windows Server 2012 컴퓨터에 설치 하 고 구성 프록시 역할을 처리 하기 위해의 하면 해당 컴퓨터 federation 서버 프록시 됩니다.  
  

