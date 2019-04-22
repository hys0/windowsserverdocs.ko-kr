---
title: 4 단계 멀티 사이트 배포를 확인 합니다.
description: 이 가이드의 일부인이 항목에서는 여러 원격 액세스 서버 배포 Windows Server 2016에서 멀티 사이트 배포에서 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 345b676a-a397-4d51-9973-8b25bc05fa55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 17b944bd0e2c13f9a3d324eeda09c67b110ce49d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821854"
---
# <a name="step-4-verify-the-multisite-deployment"></a>4 단계 멀티 사이트 배포를 확인 합니다.

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 원격 액세스 멀티 사이트 배포 올바르게 구성 되었는지 확인 하는 방법을 설명 합니다.  
  
### <a name="to-verify-access-to-internal-resources-through-the-multisite-deployment"></a>멀티 사이트 배포를 통해 내부 리소스에 대 한 액세스를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결하고 그룹 정책을 가져옵니다.  
  
2.  외부 네트워크에 클라이언트 컴퓨터를 연결하고 내부 리소스에 액세스를 시도합니다.  
  
    모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
3.  해제 또는 원격 액세스 서버 중 하나를 제외한 모든 외부 네트워크에서 연결 끊기 여 멀티 사이트 배포에서 각 서버를 통해 연결을 테스트 합니다. 클라이언트 컴퓨터에서 회사 리소스에 액세스 하려고 합니다. 다른 멀티 사이트 서버에 대 한 테스트를 반복 합니다. 새로운 진입점에 연결할 클라이언트 컴퓨터에 대 일 분 정도 걸릴 수 있습니다. 이 검색 해제 되어 있으므로 진입점에 대 일 분 후 대역폭 및 배터리 수명을 최적화 하기 위해 연결할 수 없는 경우 간주 됩니다. 또는 수동으로 실행할 때 표시 된 콤보 상자에서 원하는 진입점을 선택 하 여 다양 한 항목 지점 간을 전환할 수 있습니다 **daprop.exe**합니다.  
  
    각 멀티 사이트 서버를 통해 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
4.  Windows 7 연결&reg; 클라이언트 컴퓨터가 회사 네트워크 및 그룹 정책을 합니다.  
  
5.  외부 네트워크에 Windows 7 클라이언트 컴퓨터를 연결 하 고 내부 리소스에 액세스 하려고 합니다.  
  
    모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
6.  Active Directory 사용자 및 컴퓨터 콘솔에 액세스 하 고 각 서버에 해당 하는 보안 그룹에 클라이언트 컴퓨터를 이동 하 여 멀티 사이트 배포에서 각 서버를 통해 Windows 7 클라이언트에 대 한 연결을 테스트 합니다. 변경 내용이 도메인 전체에 복제, 새 그룹 정책을 회사 네트워크에 연결 하는 동안 클라이언트 컴퓨터를 다시 시작 합니다. 회사 리소스에 액세스 하려고 시도 합니다. 다른 멀티 사이트 서버에 대 한 테스트를 반복 합니다.  
  
    각 멀티 사이트 서버를 통해 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
    프로덕션 환경에서이 메서드 변경 도메인 전체에 복제 하는 데 필요한 시간으로 인해 불가능 되지 않을 수 있습니다. 가능한 경우 강제로 복제 하려고 합니다. 테스트는 이미 멀티 사이트 배포에서 서로 다른 Windows 7 보안 그룹의 멤버는 여러 다른 Windows 7 클라이언트 컴퓨터에서 수행할 수도 있습니다.  
  


