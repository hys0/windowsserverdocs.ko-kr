---
title: 릴리스 정보 - Windows Server, 버전 1709의 중요한 문제
description: 충돌, 중단, 설치 실패, 데이터 손실 등을 방지하기 위한 해결책이 필요한 중요한 문제를 요약합니다.
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 7d5f899964414c10350cc22a594a959c940a1514
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391525"
---
# <a name="release-notes-important-issues-in-windows-server-version-1709"></a>릴리스 정보: Windows Server 버전 1709의 중요한 이슈

>적용 대상: Windows Server 반기 채널

이러한 릴리스 정보에서는 문제를 방지하거나 해결하는 방법(알려진 경우)을 포함하여 Windows Server&reg; 운영 체제의 가장 중요한 문제를 요약합니다. 이 릴리스의 계획된 변경 사항, 새로운 기능 및 해결 방법에 대한 자세한 내용은 [Windows Server, 버전 1709의 새로운 기능](whats-new-in-windows-server-1709.md) 및 해당하는 기능 팀의 공지를 참조하세요. 별도로 지정하지 않는 이상, 보고된 각 문제는 Windows Server 2016의 모든 버전 및 설치 옵션에 적용됩니다.  

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.  
  
## <a name="storage-spaces-direct"></a>저장소 공간 다이렉트
[comment]: # (ID: unknown; Submitter: stevenek; state: signed off)  
스토리지 공간 다이렉트는 Windows Server, 버전 1709에 포함되지 않습니다. *Enable-ClusterStorageSpacesDirect* 또는 그 별칭인 *Enable-ClusterS2D*를 호출하는 경우 Windows Server, 버전 1709를 실행하는 서버에서 "요청한 작업이 지원되지 않습니다"라는 메시지와 함께 오류가 표시됩니다.

또한 Windows Server, 버전 1709를 실행하는 서버를 Windows Server 2016 스토리지 공간 다이렉트 배포에 도입하는 것 역시 지원되지 않습니다.

Windows Server 릴리스 모델은 [Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-overview) 및 [Office 365 ProPlus](https://support.office.com/article/Overview-of-the-upcoming-changes-to-Office-365-ProPlus-update-management-78b33779-9356-4cdf-9d2c-08350ef05cca?ui=en-US&rs=en-US&ad=US)와 유사한 릴리스 및 서비스 모델로 맞추기 위한 새 옵션을 제공합니다. 반기 채널 릴리스는 빠른 빈도로 이동하고자 하는 고객을 위한 새로운 기능을 제공하고 1년에 2번, 봄과 가을에 새로 릴리스됩니다.

Windows Server 반기 채널은 더 빠른 혁신을 통해 혜택을 얻는 컨테이너 및 애플리케이션 시나리오에 초점을 맞춥니다. 추가 정보는 이 [블로그](https://cloudblogs.microsoft.com/windowsserver/2018/03/29/windows-server-semi-annual-channel-update)를 참조하세요. 스토리지 공간 다이렉트와 같은 인프라 역할을 찾고 있는 고객은 Windows Server 2016(현재 사용 가능함) 및 [Windows Server 2019](https://cloudblogs.microsoft.com/windowsserver/2018/03/20/introducing-windows-server-2019-now-available-in-preview)(올해 후반 출시)와 같은 장기 서비스 채널 릴리스를 사용해야 합니다. 하이퍼 컨버지드 인프라에 대한 최고의 플랫폼을 구축하기 위해 최선을 다하며 지속적으로 새 기능을 개발하고 사용자 피드백에 따라 기존 기능을 향상시킵니다. 

스토리지 공간 다이렉트는 Windows Server 2016에 도입되었고, 하이퍼 컨버지드 플랫폼의 기초입니다. Microsoft 하이퍼 컨버지드 플랫폼의 성공적인 도입에 매우 기쁘며, 고객을 위해 최선을 다하고 있습니다.

사용자 피드백을 듣고 하이퍼 컨버지드 플랫폼을 위한 [차세대 혁신](https://blogs.technet.microsoft.com/windowsserver/2017/09/07/sneak-peek-2-windows-server-version-1709-hyper-converged-infrastructure/)을 제공해왔습니다. 이러한 기능은 현재 [Windows 참가자](https://insider.windows.com/for-business/) 빌드에서 이용 가능하니 한 번 시험해 보고 피드백을 공유하세요. 유효성 검사가 완료된 하이퍼 컨버지드 솔루션을 찾는 고객의 경우 [Windows Server 소프트웨어 정의](http://microsoft.com/wssd) 프로그램을 권장합니다.
