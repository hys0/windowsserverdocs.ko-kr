---
title: 4 단계 멀티 사이트 배포 확인
description: 이 항목은 Windows Server 2016에서 멀티 사이트 배포에서 여러 원격 액세스 서버 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 345b676a-a397-4d51-9973-8b25bc05fa55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3574ef57d18e23668f08dee8b768f0114790f0b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367133"
---
# <a name="step-4-verify-the-multisite-deployment"></a>4 단계 멀티 사이트 배포 확인

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 원격 액세스 멀티 사이트 배포를 올바르게 구성 했는지 확인 하는 방법에 대해 설명 합니다.  
  
### <a name="to-verify-access-to-internal-resources-through-the-multisite-deployment"></a>멀티 사이트 배포를 통해 내부 리소스에 대 한 액세스를 확인 하려면  
  
1.  회사 네트워크에 DirectAccess 클라이언트 컴퓨터를 연결하고 그룹 정책을 가져옵니다.  
  
2.  외부 네트워크에 클라이언트 컴퓨터를 연결하고 내부 리소스에 액세스를 시도합니다.  
  
    모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
3.  원격 액세스 서버 중 하나를 제외 하 고 외부 네트워크에서 연결을 해제 하 여 멀티 사이트 배포의 각 서버를 통해 연결을 테스트 합니다. 클라이언트 컴퓨터에서 회사 리소스에 액세스를 시도 합니다. 다른 멀티 사이트 서버에서 테스트를 반복 합니다. 클라이언트 컴퓨터가 새 진입점에 연결 하는 데 최대 10 분이 걸릴 수 있습니다. 이는 대역폭 및 배터리 수명을 최적화 하기 위해 접근할 수 없는 것으로 간주 되는 진입점의 경우 10 분 동안 검색 기능이 해제 되기 때문입니다. 또는 **daprop**를 실행할 때 표시 되는 콤보 상자에서 원하는 진입점을 선택 하 여 다양 한 진입점 간을 수동으로 전환할 수 있습니다.  
  
    각 멀티 사이트 서버를 통해 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
4.  Windows 7 @ no__t-0 클라이언트 컴퓨터를 회사 네트워크에 연결 하 고 그룹 정책을 가져옵니다.  
  
5.  Windows 7 클라이언트 컴퓨터를 외부 네트워크에 연결 하 고 내부 리소스에 액세스를 시도 합니다.  
  
    모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
6.  Active Directory 사용자 및 컴퓨터 콘솔에 액세스 하 고 각 서버에 해당 하는 보안 그룹으로 클라이언트 컴퓨터를 이동 하 여 멀티 사이트 배포의 각 서버를 통해 Windows 7 클라이언트에 대 한 연결을 테스트 합니다. 도메인 전체에 변경 내용이 복제 된 후에는 회사 네트워크에 연결 된 상태에서 클라이언트 컴퓨터를 다시 시작 하 여 새 그룹 정책을 가져옵니다. 회사 리소스에 대 한 액세스를 시도 합니다. 다른 멀티 사이트 서버에서 테스트를 반복 합니다.  
  
    각 멀티 사이트 서버를 통해 모든 회사 리소스에 액세스할 수 있어야 합니다.  
  
    프로덕션 환경에서는 도메인 전체에 변경 내용을 복제 하는 데 필요한 시간 때문에이 방법이 적합 하지 않을 수 있습니다. 가능 하면 복제를 강제로 수행할 수 있습니다. 멀티 사이트 배포에서 다른 Windows 7 보안 그룹의 이미 구성원 인 여러 다른 Windows 7 클라이언트 컴퓨터에서 테스트를 수행할 수도 있습니다.  
  


