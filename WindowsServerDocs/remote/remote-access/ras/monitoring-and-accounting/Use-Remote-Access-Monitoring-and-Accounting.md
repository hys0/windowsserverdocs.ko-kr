---
title: 원격 액세스 모니터링 및 계정 사용
description: 이 항목은 Windows Server 2016의 원격 액세스 모니터링 및 계정에 대 한 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 92519b49-0df4-43c1-9717-f13570644212
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 03d367f2f981ca3ed649f1ca4d5eca23967c9cfc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860516"
---
# <a name="use-remote-access-monitoring-and-accounting"></a>원격 액세스 모니터링 및 계정 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2016

원격 액세스 모니터링은 DirectAccess 및 VPN 연결에 대한 원격 사용자 활동 및 상태를 보고합니다. 특히, 클라이언트 연결 수 및 기간을 추적하며, 서버의 작업 상태를 모니터링합니다. 사용하기 쉬운 모니터링 콘솔에서 전체 원격 액세스 인프라 보기를 제공합니다. 모니터링 보기는 단일 서버, 클러스터 및 멀티 사이트 구성에 사용할 수 있습니다.  
  
**참고:** Windows Server 2012 DirectAccess 및 라우팅 및 원격 액세스 서비스 (RRAS)를 단일 원격 액세스 역할로 결합 합니다.  
  
> [!NOTE]  
> 이 항목 외에도 원격 액세스 모니터링에 대한 다음 항목을 사용할 수 있습니다.  
>   
> -   [원격 액세스 서버에서 기존 부하 모니터링](Monitor-the-existing-load-on-the-Remote-Access-server.md)  
> -   [원격 액세스 서버의 구성 배포 상태 모니터링](Monitor-the-configuration-distribution-status-of-the-Remote-Access-server.md)  
> -   [원격 액세스 서버 및 해당 구성 요소의 작업 상태를 모니터링 합니다.](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md)  
> -   [원격 액세스 서버 작업 문제 식별 및 해결](Identify-and-resolve-Remote-Access-server-operations-problems.md)  
> -   [연결된 원격 클라이언트에서 활동 및 상태 모니터링](Monitor-connected-remote-clients-for-activity-and-status.md)  
> -   [기록 데이터를 사용하여 원격 클라이언트에 대한 사용 보고서 생성](Generate-a-usage-report-for-remote-clients-using-historical-data.md)  

## <a name="in-this-guide"></a>설명서의 내용  
이 문서에는 DirectAccess 관리 콘솔 및 원격 액세스 서버 역할의 일부로 제공되는 해당 Windows PowerShell cmdlet을 사용하여 원격 액세스의 모니터링 기능을 활용하는 방법에 대한 지침이 수록되어 있습니다.  
  
이 문서에 설명된 모니터링 및 계정 시나리오는 다음과 같습니다.  
  
1.  원격 액세스 서버에서 기존 부하 모니터링  
  
2.  원격 액세스 서버의 구성 배포 상태 모니터링  
  
3.  원격 액세스 서버 및 해당 구성 요소의 작동 상태 모니터링  
  
4.  원격 액세스 서버 작업 문제 식별 및 해결  
  
5.  연결된 원격 클라이언트에서 활동 및 상태 모니터링  
  
6.  기록 데이터를 사용하여 원격 클라이언트에 대한 사용 현황 보고서 생성  
  
### <a name="understand-monitoring-and-accounting"></a>모니터링 및 계정 작업의 이해  
원격 클라이언트에 대한 모니터링 및 계정 작업을 시작하기 전에 두 기능 간의 차이점을 이해해야 합니다.  
  
-   **모니터링**은 지정된 시점에 연결되어 있는 활성 사용자를 보여 줍니다.  
  
-   **계정** 은 회사 네트워크에 연결한 사용자의 기록 및 해당 사용 정보(규정 준수 및 감사용)를 유지합니다.  
  
원격 클라이언트 모니터링은 연결을 기반으로 합니다. DirectAccess 클라이언트에서 설정되는 터널 연결에는 다음 두 가지 유형이 있습니다.  
  
-   **컴퓨터 터널 트래픽 연결**: 이 터널은 컴퓨터에서 이름 확인, 인증, 업데이트 관리 등에 필요한 서버에 액세스하기 위해 시스템 컨텍스트로 설정됩니다.  
  
-   **사용자 터널 트래픽 연결**: 이 터널은 사용자가 회사 네트워크의 리소스에 액세스하려고 할 때 컴퓨터의 사용자 계정에 의해 사용자 컨텍스트로 설정됩니다. 배포 요구 사항에 따라 사용자는 회사 네트워크 리소스에 액세스하기 위해 강력한 자격 증명을 제공(예: 스마트 카드를 사용하거나 일회용 암호 제공)해야 할 수도 있습니다.  
  
DirectAccess의 경우 원격 클라이언트의 IP 주소로 연결이 고유하게 식별됩니다. 예를 들어 클라이언트 컴퓨터에 대한 컴퓨터 터널이 열려 있고 해당 컴퓨터에서 사용자가 연결된 경우 여기에는 동일한 연결이 사용될 수 있습니다. 이 경우 컴퓨터 터널이 활성 상태인 동안 사용자가 연결을 끊었다가 다시 연결하면 단일 연결로 설정됩니다.  
  


