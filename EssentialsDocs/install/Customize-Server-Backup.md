---
title: 서버 백업 사용자 지정
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838544"
---
# <a name="customize-server-backup"></a>서버 백업 사용자 지정

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="turn-off-server-backup-by-default"></a>기본적으로 Server Backup을 끔  
 기본적으로 Server Backup을 끌 수 있습니다. **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** 값을 1로 설정해야 이 옵션을 사용할 수 있습니다.  
  
 이 키가 설정된 경우 Server Backup 사용자 인터페이스가 대시보드나 실행패드를 통해 노출되지 않습니다. 이것은 타사 응용 프로그램을 Server Backup에 사용할 수 있게 합니다.  
  
#### <a name="to-add-serverbackupproviderdisabled-registry-key-and-set-the-value-to-1"></a>ServerBackup\ProviderDisabled 추가? 레지스트리 키 및 값을 1로 설정  
  
1.  서버에서 **시작**, **실행**을 차례로 클릭하고 **열기** 텍스트 상자에 **regedit**를 입력한 다음 **확인**을 클릭합니다.  
  
2.  탐색 창에서 **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**, **ServerBackup**을 차례로 확장합니다.  
  
3.  **ServerBackup**을 마우스 오른쪽 단추로 클릭하고 **신규**를 클릭한 다음 **DWARD 값**을 클릭합니다.  
  
4.  이름으로 **ProviderDisabled**를 입력합니다.  
  
5.  이름을 마우스 오른쪽 단추로 클릭하고 **수정**을 선택한 다음 데이터 값으로 **1** 을 입력하고 **확인**을 클릭합니다.  
  
## <a name="turn-on-server-backup"></a>Server Backup 켜기  
 앞에서 설명한 것처럼 **ProviderDisabled** 레지스트리 키를 생성하여 서버 백업이 꺼진 경우 서버 Backup을 켤 수 있습니다.  
  
 **HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Server\ServerBackup\ProviderDisabled** 키를 삭제해야 기본 서버 백업을 활성화하고 Windows Server Server Backup Service의 서비스 시작 유형을 변경하며 서버를 다시 시작할 수 있습니다.  
  
#### <a name="to-delete-serverbackupproviderdisabled-registry-key"></a>ServerBackup\ProviderDisabled를 삭제 하를 시겠습니까? 레지스트리 키  
  
1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.  
  
2.  검색 상자에 **regedit**를 입력하고 **Regedit** 응용 프로그램을 클릭합니다.  
  
3.  탐색 창에서 **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**, **ServerBackup**을 차례로 확장합니다.  
  
4.  **ProviderDisabled**를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 클릭합니다.  
  
#### <a name="change-the-start-type-of-windows-server-server-backup-service"></a>Windows Server Server Backup Service의 시작 유형 변경  
  
1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.  
  
2.  검색 상자에 **services.msc**를 입력한 다음 **서비스** 응용 프로그램을 클릭합니다.  
  
3.  서비스 창에서 **Windows Server Server Backup Service**를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
4.  **일반** 탭에서 **시작 유형** 으로 **자동**을 선택합니다.  
  
5.  **확인**을 클릭하여 대화 상자를 닫습니다.  
  
#### <a name="restart-the-server"></a>서버를 다시 시작하세요.  
  
1.  서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **설정**, **전원**, 다시 시작을 차례로 클릭합니다.