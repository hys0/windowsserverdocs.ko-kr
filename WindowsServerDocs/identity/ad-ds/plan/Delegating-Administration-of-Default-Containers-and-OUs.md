---
ms.assetid: ac6604b0-7459-4ff3-af1c-4936897f5d14
title: "기본 컨테이너 및 Ou 관리 위임"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2504208210c03193451d19478f3bc8c98ec98f23
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="delegating-administration-of-default-containers-and-ous"></a>기본 컨테이너 및 Ou 관리 위임

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 Active Directory 도메인 표준 집합이 컨테이너 및 조직 (Ou) Active Directory (AD DS 도메인 서비스)를 설치 하는 동안 만든 포함 되어 있습니다. 다음은 다음과 같습니다.  
  
-   계층을 루트 컨테이너로 사용 되는 도메인 컨트롤러  
  
-   기본 서비스 관리자 계정을 보유 하는 기본 제공 컨테이너  
  
-   도메인에서 만든 새 사용자 계정 및 그룹에 대 한 기본 위치는 사용자가 컨테이너  
  
-   새 컴퓨터 계정에 대 한 기본 위치는 컴퓨터 컨테이너 도메인에 작성  
  
-   도메인 컨트롤러 컴퓨터 계정의 컴퓨터 계정에 대 한 기본 위치는 도메인 컨트롤러 OU  
  
숲 소유자 이러한 기본 컨테이너 및 Ou 제어할 수 있습니다.  
  
## <a name="domain-container"></a>도메인 컨트롤러  
도메인 컨트롤러 루트 컨테이너 도메인 계층입니다. 정책이 나이 컨테이너에 액세스 제어 목록 (ACL)에 대 한 변경 도메인 전체 영향을 미칠 수 있습니다. 이 컨테이너; 제어 위임 되지 않으면 서비스 관리자가 제어할 수 있어야 합니다.  
  
## <a name="users-and-computers-containers"></a>사용자와 컴퓨터 컨테이너  
Windows Server 2008를 Windows Server 2003에서 현재 위치에서 도메인 업그레이드를 수행 하면 기존 사용자와 컴퓨터 사용자 및 컨테이너 컴퓨터에 자동으로 배치 됩니다. 만드는 경우 Active Directory 도메인, 사용자와 컴퓨터 컨테이너는 모든 사용자 계정 새 및 도메인 컨트롤러 비 컴퓨터 도메인 계정에 대 한 기본 위치 합니다.  
  
> [!IMPORTANT]  
> 사용자 또는 컴퓨터 제어 권한을 위임 필요한 경우 사용자와 컴퓨터의 기본 설정을 수정 하지 컨테이너 합니다. 대신 필요에 따라 새 Ou 만들기 및 사용자와 컴퓨터 개체 기본 컨테이너에서 새로운 Ou로 이동 합니다. 필요에 따라 새 Ou 제어할을 위임 합니다. 하지 수정 하는 기본 컨테이너를 제어 하는 것이 좋습니다.  
  
그룹 정책 설정 기본 사용자와 컴퓨터에 적용할 수 없습니다 또한 컨테이너 합니다. 그룹 정책을 사용자와 컴퓨터에 적용할 새로운 Ou 만들고 사용자와 컴퓨터 개체 Ou 해당로 이동 합니다. 그룹 정책 설정을 새 Ou에 적용 됩니다.  
  
필요에 따라 기본 컨테이너 컨테이너 선택한에 사용할 수 있는 개체에 생성을 리디렉션합니다 수 있습니다.  
  
## <a name="well-known-users-and-groups-and-built-in-accounts"></a>알려진 사용자 및 그룹 기본 제공 된 계정  
기본적으로 몇 가지 알려진 사용자 및 그룹 기본 제공 된 계정에 새 도메인 만들어집니다. 이러한 계정 관리 된 서비스 관리자에 제어 유지 하는 것이 좋습니다. 이러한 계정 관리 사용자가 서비스 관리자에 위임 하지 않습니다. 다음 표에서 잘 알려져 사용자 및 그룹 서비스 관리자에 제어 유지 해야 하는 기본 제공 된 계정 합니다.  
  
|알려진 사용자 및 그룹|기본 제공 된 계정|  
|--------------------------------|----------------------|  
|인증 게시자<br /><br />도메인 컨트롤러<br /><br />그룹 정책 Creator 소유자<br /><br />KRBTGT<br /><br />도메인 게스트<br /><br />관리자<br /><br />도메인 관리<br /><br />스키마 관리자 (이렇게만)<br /><br />엔터프라이즈 관리자 (이렇게만)<br /><br />사용자 도메인|관리자<br /><br />Guest<br /><br />Guest<br /><br />계정에서<br /><br />관리자<br /><br />백업 관리자<br /><br />수신 숲 신뢰 빌더<br /><br />연산자 인쇄<br /><br />Windows 2000 호환 액세스<br /><br />서버 연산자<br /><br />사용자가|  
  
## <a name="domain-controller-ou"></a>OU 도메인 컨트롤러  
도메인 컨트롤러 도메인에 추가 되 면 해당 컴퓨터 개체 도메인 컨트롤러를 자동으로 추가 됩니다. 이 OU 정책이 적용 기본 집합을 있습니다. 이 정책이 모든 도메인 컨트롤러에 동일 하 게 적용 되 되도록이 OU 아웃 도메인 컨트롤러의 컴퓨터 개체 이동 하지 하는 것이 좋습니다. 기본 정책이 적용 하는 도메인 컨트롤러 제대로 작동 하지 않을 수 있습니다.  
  
기본적으로 서비스 관리자가이 OU를 제어합니다. 개인 이외의 서비스 관리자에 게이 OU 제어를 위임 하지 않습니다.  
  


