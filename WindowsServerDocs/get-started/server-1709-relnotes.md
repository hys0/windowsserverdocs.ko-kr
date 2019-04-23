---
title: 릴리스 정보--Windows Server, 버전 1709의 중요한 문제
description: 충돌, 중단, 설치 실패, 데이터 손실 등을 방지하기 위한 해결책이 필요한 중요한 문제를 요약합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 04/23/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 4eebc498289a81c7f27fcf4b84d81ae13bc38e4f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861984"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>릴리스 정보: Windows Server 버전 1709의에서 중요 한 문제

>적용 대상: Windows Server 반기 채널

이러한 릴리스 정보에서는 문제를 방지하거나 해결하는 방법(알려진 경우)을 포함하여 Windows Server&reg; 운영 체제의 가장 중요한 문제를 요약합니다. 이 릴리스의 계획된 변경 사항, 새로운 기능 및 해결 방법에 대한 자세한 내용은 [Windows Server, 버전 1709의 새로운 기능](whats-new-in-windows-server-1709.md) 및 해당하는 기능 팀의 공지를 참조하세요. 별도로 지정하지 않는 이상, 보고된 각 문제는 Windows Server 2016의 모든 버전 및 설치 옵션에 적용됩니다.  

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.  
  
## <a name="storage-spaces-direct"></a>저장소 공간 다이렉트
[comment]: # (ID: 알 수 있습니다. 제출자: stevenek; 상태: 로그 오프)  
저장소 공간 다이렉트는 Windows Server, 버전 1709에 포함되지 않습니다. *Enable-ClusterStorageSpacesDirect* 또는 그 별칭인 *Enable-ClusterS2D*를 호출하는 경우 Windows Server, 버전 1709를 실행하는 서버에서 "요청한 작업이 지원되지 않습니다"라는 메시지와 함께 오류가 표시됩니다.

또한 Windows Server, 버전 1709를 실행하는 서버를 Windows Server 2016 저장소 공간 다이렉트 배포에 도입하는 것 역시 지원되지 않습니다.

Windows Server 릴리스 모델은 [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) 및 [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US)와 유사한 릴리스 및 서비스 모델로 맞추기 위한 새 옵션을 제공합니다. 반기 채널 릴리스는 빠른 빈도로 이동하고자 하는 고객을 위한 새로운 기능을 제공하고 1년에 2번, 봄과 가을에 새로 릴리스됩니다.

Windows Server 반기 채널은 컨테이너에서 더 빠르게 혁신을 활용 하는 응용 프로그램 시나리오에 초점을 맞춘이 참조 하세요 [블로그](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update) 추가 정보에 대 한 합니다. 저장소 공간 다이렉트와 같은 인프라 역할을 찾고 있는 고객은 Windows Server 2016 (사용할 수 있는 지금은)와 같은 장기 서비스 채널 릴리스를 사용 해야 하 고 [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview) (올해 후반 출시). 하이퍼 수렴 형 인프라에 대 한 최고의 플랫폼을 구축 하는 데 노력할 것입니다. 및 새 기능을 개발 하 고 사용자 의견에 따라 기존 향상을 계속 합니다. 

저장소 공간 다이렉트는 Windows Server 2016에 도입되었고, 하이퍼 수렴형 플랫폼의 기초입니다. Microsoft 하이퍼 수렴형 플랫폼의 성공적인 도입에 매우 기쁘고, 고객을 위해 최선을 다하고 있습니다.

사용자 의견에 귀 했습니다 하 고 제공 하는 중 합니다 [혁신의 다음 집합](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/) 하이퍼 수렴 형 플랫폼에 대 한 합니다. 이러한 기능은에서 현재 사용 가능한 [Windows 참가자](https://insider.windows.com/for-business/) 빌드에서 해 주시길 부탁 해 사용자 의견을 공유할 수 있습니다. 유효성 검사가 완료된 하이퍼 수렴형 솔루션을 찾는 고객의 경우 [Windows Server 소프트웨어 정의](http://microsoft.com/wssd) 프로그램을 권장합니다.
