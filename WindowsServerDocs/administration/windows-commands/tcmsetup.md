---
title: tcmsetup
description: TAPI 클라이언트를 설정 하 고 해제 하는 방법에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 15e0c10f-996f-4301-92e5-943f7ee8212d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0c646acef51f06c57f16ec7e5310e3319a11383f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370683"
---
# <a name="tcmsetup"></a>tcmsetup



설정 하거나 TAPI 클라이언트를 사용 하지 않도록 설정 합니다.

## <a name="syntax"></a>구문

```
tcmsetup [/q] [/x] /c <Server1> [<Server2> …] 
tcmsetup  [/q] /c /d
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/q|메시지 상자를 표시를 하지 않습니다.|
|/x|연결 지향 콜백이 사용될지를 많은 네트워크에 패킷 손실이 높습니다 지정 합니다. 이 매개 변수를 생략 하면 연결 없는 콜백이 사용 됩니다.|
|/c|필수. 클라이언트 설치를 지정합니다.|
|\<Server1 >|필수. 원격 서버에 클라이언트에서 사용 되는 TAPI 서비스 공급자의 이름을 지정 합니다. 클라이언트는 서비스 공급자의 회선과 사용 합니다. 클라이언트는 서버가 있는 도메인과 양방향 트러스트 관계를 맺고 있는 도메인 또는 서버와 동일한 도메인에 있어야 합니다.|
|\<Server2 > ...|모든 추가 서버 또는이 클라이언트에서 사용할 수 있는 서버를 지정 합니다. 서버 목록으로 지정 하는 경우 서버 이름을 구분 하는 공간을 사용 합니다.|
|/d|원격 서버의 목록을 지웁니다. 원격 서버에 있는 TAPI 서비스 공급자를 사용 하 여 하지 못하도록 하 여 TAPI 클라이언트를 사용 하지 않도록 설정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

-   이 절차를 수행하려면 로컬 컴퓨터에서 Administrators 그룹의 구성원이거나 적절한 권한을 위임받아야 합니다. 컴퓨터가 도메인에 참가하면 Domain Admins 그룹의 구성원이 이 절차를 수행할 수도 있습니다. 최상의 보안을 사용 하는 것이 좋습니다 **계정으로 실행** 에이 절차를 수행 합니다.
-   제대로 작동 하려면 TAPI 실행 해야 **tcmsetup** TAPI 클라이언트에서 사용 될 원격 서버를 지정 합니다.
-   클라이언트 사용자를 사용 하려면 먼저 전화나 회선 TAPI 서버에서 전화 통신 서버 관리자는 휴대폰 또는 줄에 사용자를 할당 해야 합니다.
-   이 명령으로 만들어진 전화 통신 서버 목록이 있는 기존 클라이언트에 사용할 수 있는 전화 통신 서버 목록을 대체 합니다. 기존 목록에 추가 하려면이 명령을 사용할 수 없습니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[명령 셸 개요](https://technet.microsoft.com/library/cc737438(v=ws.10).aspx)

[클라이언트 컴퓨터의 전화 통신 서버 지정](https://technet.microsoft.com/library/cc759226(v=ws.10).aspx)

[회선이 나 전화에 전화 통신 사용자 할당](https://technet.microsoft.com/library/cc736875(v=ws.10).aspx)

