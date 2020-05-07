---
title: Sc.exe 삭제
description: Sc.exe 유틸리티를 사용 하 여 서비스를 등록 취소 하는 방법 알아보기
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2fe94fb3-e4d1-47b5-b999-39995ecbb644
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 284012cf6799df52832e62c3eea1b2f0fcd84805
ms.sourcegitcommit: 95b60384b0b070263465eaffb27b8e3bb052a4de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2020
ms.locfileid: "82850114"
---
# <a name="scexe-delete"></a>Sc.exe 삭제

레지스트리에서 서비스 하위 키를 삭제합니다. 서비스가 실행 중인지 또는 다른 프로세스에서 열린 핸들을 서비스 하는 경우 서비스 삭제 되도록 표시 됩니다.

이 명령을 사용하는 방법의 예는 [예](#examples)를 참조하세요.

## <a name="syntax"></a>구문

```
sc.exe [<ServerName>] delete [<ServiceName>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|Description|
|---------|-----------|
|\<ServerName>|서비스 위치는 원격 서버의 이름을 지정 합니다. 이름은 UNC (범용 명명 규칙) 형식 (예: \\ \\myserver)을 사용 해야 합니다. SC.exe를 로컬로 실행 하려면이 매개 변수를 생략 합니다.|
|\<ServiceName>|반환 된 서비스 이름을 지정는 **getkeyname** 작업 합니다.|
|?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Sc.exe를 사용 하 여 DHCP, DNS 또는 인터넷 정보 서비스 같은 기본 제공 운영 체제 서비스를 삭제 하지 않는 것이 좋습니다. 운영 체제 역할, 서비스 및 구성 요소를 설치, 제거 또는 다시 구성 하려면 [역할, 역할 서비스 또는 기능 설치 또는 제거](/WindowsServerDocs/administration/server-manager/install-or-uninstall-roles-role-services-or-features.md) 를 참조 하세요.

## <a name="examples"></a>예

서비스 하위 키를 삭제 하려면 **NewServ** 로컬 컴퓨터에서 레지스트리를에서 다음 명령을 입력 합니다.
```
sc.exe delete newserv
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
