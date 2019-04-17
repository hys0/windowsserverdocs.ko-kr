---
title: "서버 백업 사용자 지정"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 19b2559c-6090-45af-9a08-2eefc28473c8
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d18dca276bccdf672664a5a3c2bd28e0221fff94
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="customize-server-backup"></a>서버 백업 사용자 지정

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

## <a name="turn-off-server-backup-by-default"></a>기본적으로 서버 백업을 해제합니다  
 기본적으로 서버 백업을 해제 하도록 선택할 수 있습니다. 값을 설정 해야 할 **를 Server\ServerBackup\ProviderDisabled** 1 하려면이 옵션을 사용 합니다.  
  
 이 키가 설정 서버 백업 사용자 인터페이스 대시보드 또는 실행 패드를 통해 표시 되지 않습니다. 제 3 자 서버 백업 응용 프로그램을 이용할 수 있습니다.  
  
#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>ServerBackup\ProviderDisabled 추가? 레지스트리 키와 1 값 설정  
  
1.  서버에서 **시작**, 클릭 **실행**, 입력 **regedit** 에 **열기** 텍스트 상자를 클릭 한 다음 **확인**합니다.  
  
2.  탐색 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**, 다음를 확장 하 고 **ServerBackup**합니다.  
  
3.  마우스 오른쪽 단추로 클릭 **ServerBackup**, 클릭 **새로**을 차례로 클릭 하 고 **DWARD 값**합니다.  
  
4.  이름 입력 **ProviderDisabled**합니다.  
  
5.  이름을 마우스 오른쪽 단추로 선택 **수정**, 입력 **1** 값 데이터 및 클릭 **확인**합니다.  
  
## <a name="turn-on-server-backup"></a>서버 백업 켜기  
 만들어 꺼져 있으면 서버 백업 켤 수 **ProviderDisabled** 레지스트리 키 (이 문서의 앞에 설명 참조).  
  
 키를 삭제 해야 **를 Server\ServerBackup\ProviderDisabled** 기본 서버 백업을 사용 하도록 설정, Windows Server 서버 백업 서비스의 서비스 시작 유형 변경 하 고, 서버를 다시 시작 합니다.  
  
#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>ServerBackup\ProviderDisabled 삭제? 레지스트리 키  
  
1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
2.  검색 상자에 입력 **regedit**을 차례로 클릭 하 고 있는 **Regedit** 응용 프로그램입니다.  
  
3.  탐색 창에서 확장 **HKEY_LOCAL_MACHINE**, 확장 **소프트웨어**, 확장 **Microsoft**, 확장 **Windows Server**, 다음를 확장 하 고 **ServerBackup**합니다.  
  
4.  마우스 오른쪽 단추로 클릭 **ProviderDisabled**을 차례로 클릭 하 고 **삭제**합니다.  
  
#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Windows Server 서버 백업 서비스의 시작 유형 변경  
  
1.  서버에서 화면 오른쪽 위 모서리에 마우스를 이동 하 고 클릭 **검색**합니다.  
  
2.  검색 상자에 입력 **services.msc**을 차례로 클릭 하 고 **서비스** 응용 프로그램입니다.  
  
3.  서비스 창에서 마우스 오른쪽 단추로 클릭는 **Windows Server 서버 백업 서비스**를 클릭 하 고 **속성**합니다.  
  
4.  **일반** 탭을 선택 하 고 **자동** 에 대 한 **시작 유형**합니다.  
  
5.  클릭 **확인** 은 대화 상자를 닫습니다.  
  
#### <a name="restart-the-server"></a>서버를 다시 시작  
  
1.  서버에서 마우스를 화면의 오른쪽 위 모서리 이동한 클릭 **설정**, 클릭 **전원**, 클릭 한 다음 다시 시작 하 고 있습니다.