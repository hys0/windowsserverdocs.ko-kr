---
title: 키 배포 서비스 KDS 루트 키 만들기
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 42e5db8f-1516-4d42-be0a-fa932f5588e9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: fd335d61eae7cf753d09436d54f14c7d6004d643
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386897"
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>키 배포 서비스 KDS 루트 키 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 항목에서는 windows PowerShell을 사용 하 여 Windows Server 2012 이상에서 그룹 관리 서비스 계정 암호를 생성 하는 도메인 컨트롤러에서 Microsoft 키 배포 서비스 (kdssvc.dll) 루트 키를 만드는 방법을 설명 합니다.

DC (도메인 컨트롤러)는 gMSA 암호 생성을 시작 하는 데 루트 키가 필요 합니다. 도메인 컨트롤러는 gMSA 만들기를 허용하기 전에 모든 도메인 컨트롤러가 해당 AD 복제를 수렴할 때까지 최대 10시간을 대기하게 됩니다. 이 10시간은 환경 내의 모든 DC에서 gMSA 요청에 응답할 수 있기 전에 암호 생성이 발생하지 않도록 하기 위한 안전 조치입니다.  GMSA를 너무 빨리 사용 하려고 하면 키가 모든 도메인 컨트롤러에 복제 되지 않을 수 있으므로 gMSA 호스트에서 암호 검색을 시도할 때 암호 검색에 실패할 수 있습니다. 또한 gMSA 암호 검색 실패는 복제 일정이 제한된 DC를 사용하거나 복제 문제가 있는 경우에도 발생할 수 있습니다.

> [!NOTE]
> 루트 키를 삭제 하 고 다시 만들면 키 캐싱에 인해 삭제 후 이전 키가 계속 사용 되는 문제가 발생할 수 있습니다. 루트 키를 다시 만들 경우 모든 도메인 컨트롤러에서 KDC (키 배포 서비스)를 다시 시작 해야 합니다.

이 절차를 수행하려면 최소한 **Domain Admins** 또는 **Enterprise Admins** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다. 적절한 계정과 그룹 구성원 사용에 대한 자세한 내용은 [로컬 및 도메인 기본 그룹](https://technet.microsoft.com/library/dd728026(WS.10).aspx)을 참조하세요.

> [!NOTE]
> 64비트 아키텍처에서는 그룹 관리 서비스 계정을 관리하는 데 사용되는 Windows PowerShell 명령을 실행해야 합니다.

#### <a name="to-create-the-kds-root-key-using-the-add-kdsrootkey-cmdlet"></a>New-kdsrootkey cmdlet을 사용 하 여 KDS 루트 키를 만들려면

1.  Windows Server 2012 이상 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **New-kdsrootkey-EffectiveImmediately**

    > [!TIP]
    > 유효 시간 매개 변수를 사용하여 키가 사용 전에 모든 DC에 전파될 수 있는 시간을 제공할 수 있습니다. New-kdsrootkey-EffectiveImmediately을 사용 하면 KDS 서비스에서 즉시 사용할 루트 키가 대상 DC에 추가 됩니다. 그러나 다른 도메인 컨트롤러는 복제가 성공할 때까지 루트 키를 사용할 수 없습니다.

DC가 하나뿐인 테스트 환경의 경우 키 생성 대기를 방지하기 위해 다음 절차에 따라 KDS 루트 키를 만들고 과거의 시간으로 시작 시간을 설정할 수 있습니다. 4004 이벤트가 kds 이벤트 로그에 기록되었는지 확인합니다.

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>테스트 환경에서 즉시 적용되는 KDS 루트 키를 만들려면

1.  Windows Server 2012 이상 도메인 컨트롤러의 작업 표시줄에서 Windows PowerShell을 실행 합니다.

2.  Windows PowerShell Active Directory 모듈에 대한 명령 프롬프트에서 다음 명령을 입력하고 Enter 키를 누릅니다.

    **$a = 가져오기-날짜**

    **$b = $a. AddHours (-10)**

    **New-kdsrootkey-EffectiveTime $b**

    또는 다음 단일 명령을 사용합니다.

    **New-kdsrootkey-EffectiveTime ((가져오기-날짜). addhours (-10))**

## <a name="see-also"></a>관련 항목
[그룹 관리 서비스 계정 시작](getting-started-with-group-managed-service-accounts.md)


