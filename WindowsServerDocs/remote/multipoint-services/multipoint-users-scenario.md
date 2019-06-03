---
title: MultiPoint 서비스 사용자 계정
description: MultiPoint 서비스, 특히 다른 시나리오에 사용 하는 종류의에서 사용자 계정에 알아봅니다
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f3c6ce5-9b7c-45a0-83c5-3f9b9f5f48d4
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 31279f81d5af597b0b1f1729c953fefaf24a214f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855364"
---
# <a name="example-scenarios-multipoint-services-user-accounts"></a>예제 시나리오: MultiPoint 서비스 사용자 계정
MultiPoint 서비스 환경에 대해 선택한 사용자 계정 시나리오를 구현 하려면 작업을 수행 하 시겠습니까? 다음 표에서 사용자 계정을 구성 하 고 작업 그룹 또는 Active Directory 도메인에 네트워크로 연결 된 서버 또는 독립 실행형 MultiPoint 컴퓨터에서 공유 또는 개별 사용자 계정에 대 한 스테이션을 준비 하기 위해 수행 하는 각 작업에 설명 합니다. 사용자 환경에 적용 되는 시나리오를 선택 합니다. 그런 다음 각 필수 구성 작업을 완료 하기 위해 테이블에 있는 링크를 따릅니다.  
  
> [!NOTE]  
> 사용자 계정을 설정 하는 방법을 아직 결정 하지 않았다면 못했으면 [MultiPoint 서비스 환경에 대 한 사용자 계정을 계획](Plan-user-accounts-for-your-MultiPoint-services-environment.md) 각 선택 사용자에 미치는 영향에 대 한 자세한 내용은 합니다.  
  
## <a name="single-multipoint-services-computer-in-a-stand-alone-environment-no-network"></a>단일 MultiPoint 서비스 컴퓨터에 독립 실행형 환경 (네트워크 없음)  
  
|||  
|-|-|  
|**내 사용자가 로그온 할 필요가 없습니다.** 참여 하는 스테이션을 검색 하는 사람에 게 사용할 수 있습니다. 데이터나 개인 설정된 데스크톱을 저장하기 위한 프라이빗 폴더를 포함하는 개별 Windows 데스크톱 환경은 필요하지 않습니다.|1.  단일 로컬 사용자 계정 만들기 (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br />2.  [여러 세션을 한 계정 허용](Allow-one-account-to-have-multiple-sessions.md)<br />3.  [자동 로그온 스테이션을 구성 합니다.](Configure-stations-for-automatic-logon.md)|  
|**내 사용자에는 동일한 사용자 로그온을 공유할 수 있습니다.** 데이터나 개인 설정된 데스크톱을 저장하기 위한 프라이빗 폴더를 포함하는 개별 Windows 데스크톱 환경은 필요하지 않습니다.|1.  단일 로컬 사용자 계정 만들기 (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br />2.  [여러 세션을 한 계정 허용](Allow-one-account-to-have-multiple-sessions.md)|  
|**내 사용자가 자신의 개별 Windows 데스크톱 경험이 있어야 합니다.**|각 사용자에 대 한 로컬 사용자 계정 만들기 (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)|  
  
## <a name="multiple-multipoint-services-computers-on-a-network-but-with-no-domain"></a>하지만 도메인 네트워크에 여러 MultiPoint 서비스 컴퓨터  
  
|||  
|-|-|  
|**내 사용자가 로그온 할 필요가 없습니다.** 참여 하는 스테이션을 검색 하는 사람에 게 사용할 수 있습니다. 데이터나 개인 설정된 데스크톱을 저장하기 위한 프라이빗 폴더를 포함하는 개별 Windows 데스크톱 환경은 필요하지 않습니다.|1.  각 서버에서 단일 로컬 사용자 계정을 만듭니다. (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br />2.  [여러 세션을 하나의 계정만 허용](Allow-one-account-to-have-multiple-sessions.md) 각 서버에서<br />3.  [자동 로그온 스테이션 구성](Configure-stations-for-automatic-logon.md) 각 서버에서|  
|**내 사용자에는 동일한 사용자 로그온을 공유할 수 있습니다.** 데이터나 개인 설정된 데스크톱을 저장하기 위한 프라이빗 폴더를 포함하는 개별 Windows 데스크톱 환경은 필요하지 않습니다.|1.  각 서버에서 단일 로컬 사용자 계정을 만듭니다. (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br />2.  [여러 세션을 하나의 계정만 허용](Allow-one-account-to-have-multiple-sessions.md) 각 서버에 있습니다.|  
|**내 사용자가 자신의 개별 Windows 데스크톱 경험이 있어야 합니다.**<br /><br />-   **옵션 A** -내 사용자는 항상 동일한 MultiPoint 서비스 컴퓨터에 연결 된 로컬 스테이션을 사용 합니다.<br />-   **옵션 B** -내 사용자가 둘 이상의 MultiPoint 서비스 컴퓨터에서 로컬 스테이션을 사용 합니다.<br />-   **옵션 C** -내 사용자 LAN에 원격 클라이언트를 사용 합니다.|-   **옵션 A** -해당 서버의 사용자를 위해 각 서버에 단일 로컬 사용자 계정을 만듭니다. (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br />-   **옵션 B** -모든 서버에 모든 사용자에 대 한 로컬 사용자 계정을 만듭니다. **참고:** 즉, 각 사용자는 프로필을 각 서버. 즉, 서버 A의 스테이션에 로그온 하는 동안 내 문서에는 파일을 저장 하는 경우은 표시 되지 않습니다 파일 서버 B의 스테이션에 로그온 하는 경우. (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br />-   **옵션 C** -특정 MultiPoint 서비스 컴퓨터에 각 사용자를 할당 합니다. 각 서버에 할당 된 사용자에 대 한 로컬 사용자 계정을 만듭니다. (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)|  
  
## <a name="one-or-more-multipoint-services-computers-in-a-domain-network-environment"></a>도메인 네트워크 환경에서 하나 이상의 MultiPoint 서비스 컴퓨터  
  
|||  
|-|-|  
|**내 사용자가 로그온 할 필요가 없습니다.** 참여 하는 스테이션을 검색 하는 사람에 게 사용할 수 있습니다. 데이터나 개인 설정된 데스크톱을 저장하기 위한 프라이빗 폴더를 포함하는 개별 Windows 데스크톱 환경은 필요하지 않습니다.|1.  서버에 로그온 하기 위해 도메인 계정을 만듭니다.<br />2.  [여러 세션을 하나의 계정만 허용](Allow-one-account-to-have-multiple-sessions.md) 각 서버에 있습니다.<br />3.  [자동 로그온 스테이션 구성](Configure-stations-for-automatic-logon.md) 각 서버에 있습니다.|  
|**내 사용자에는 동일한 사용자 로그온을 공유할 수 있습니다.** 데이터나 개인 설정된 데스크톱을 저장하기 위한 프라이빗 폴더를 포함하는 개별 Windows 데스크톱 환경은 필요하지 않습니다.|1.  각 사용자 또는 그룹에 대 한 도메인 계정을 만듭니다.<br />2.  [여러 세션을 하나의 계정만 허용](Allow-one-account-to-have-multiple-sessions.md) 각 서버에 있습니다.|  
|**내 사용자가 자신의 개별 Windows 데스크톱 경험이 있어야 합니다.**<br /><br />-   **옵션 A** -모든 사용자 도메인 계정으로 MultiPoint 서비스 컴퓨터를 사용할 수 있습니다.<br />-   **옵션 B** -서버에 액세스할 수 있는 도메인 계정을 제한 하려고 합니다.|-   **옵션 A** -설치가 필요 하지 않습니다. 기본적으로 모든 도메인 사용자는 네트워크에서 MultiPoint Service 컴퓨터에 대 한 액세스를 갖습니다.<br />-   **옵션 B** -MultiPoint 서비스 컴퓨터에 도메인 사용자 계정에 대 한 액세스를 제한 합니다. 자세한 내용은 [서버에 대 한 사용자 액세스를 제한](limit-users--access-to-the-server-in-multipoint-services.md)합니다.|  
|**내 도메인 계정에서 별도로 관리 하 고 로컬 사용자 계정을 사용 하려는 경우** 예를 들어 MultiPoint 서비스 있지만 도메인이 아닌 관리 맡기려는 경우 또는 도메인 계정에 모든 MultiPoint 서비스 사용자에 게 부여 하지 않으려는 경우.|각 서버에 하나 이상의 로컬 사용자 계정을 만듭니다. (자세한 내용은 [로컬 사용자 계정을 만드는](Create-local-user-accounts.md).)<br /><br />**참고:** 즉, 각 사용자 계정 들 수 있는 프로필을 각 서버에서. 즉, 서버 A의 스테이션에 로그온 하는 동안 내 문서에는 파일을 저장 하는 경우은 표시 되지 않습니다 파일 서버 B의 스테이션에 로그온 하는 경우.|  