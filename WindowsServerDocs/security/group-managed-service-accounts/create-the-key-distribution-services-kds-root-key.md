---
title: "키 배포 서비스 KDS 루트 키를 만들려면"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 30075e56f3ca8e90a0655508efeacfcf2aaa0337
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-the-key-distribution-services-kds-root-key"></a>키 배포 서비스 KDS 루트 키를 만들려면

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

This topic for the IT professional describes how to create a Microsoft Key Distribution Service (kdssvc.dll) root key on the domain controller using Windows PowerShell to generate group Managed Service Account passwords in Windows Server 2012.

 Windows Server 2012 DC (도메인 컨트롤러) gMSA 암호를 생성 하려면 루트 키가 필요 합니다. 도메인 컨트롤러에서 만들 수 있도록 허용을 gMSA 생성 하기 전에 자녀가 광고 복제 수렴 모든 도메인 컨트롤러에 시간부터 최대 10 시간 기다립니다. 10 시간에 발생 gMSA 요청에 응답 수 있는 환경에서 모든 Dc 하기 전에 암호를 생성 하지 않으려면 안전을 위해입니다.  gMSA 사용 하려고 하면 너무 빨리 키 복제 하지 않은 된 모든 Windows Server 2012 dc 및 gMSA 호스트 암호를 검색할 하려고 할 때 암호 검색 따라서 실패할 수 있습니다. Dc을 사용 하 여 제한 된 복제 일정 또는 복제 문제 인지 gMSA 암호 검색 오류가 발생할 수 있습니다.

구성원에는 **도메인 관리자** 또는 **엔터프라이즈 관리자** 는이 절차를 수행 하는 데 필요한 최소 그룹 또는 오른쪽 단추를 클릭 합니다. For detailed information about using the appropriate accounts and group memberships, see [Local and Domain Default Groups](https://technet.microsoft.com/library/dd728026(WS.10).aspx).

> [!NOTE]
> 64 비트 아키텍처 그룹 관리 서비스 계정 관리 하는 데 사용 되는 Windows PowerShell 명령을 실행 해야 합니다.

#### <a name="to-create-the-kds-root-key-using-the-new-kdsrootkey-cmdlet"></a>사용 하 여 New-KdsRootKey cmdlet KDS 루트 키를 만들려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **Add-KdsRootKey -EffectiveImmediately**

    > [!TIP]
    > 키를 사용 하기 전에 모든 dc 전파에 대 한 시간을 주려면 효과적인 지 매개 변수를 사용할 수 있습니다. Using Add-KdsRootKey -EffectiveImmediately will add a root key to the target DC which will be used by the KDS service immediately. 그러나 다른 Windows Server 2012 Dc 루트 키 복제 완료 될 때까지 사용할 수 없게 됩니다.

하나의 DC로, 테스트 환경에 대 KDS 루트 키 만들고 다음 절차를 사용 하 여 키를 생성 간격 대기 방지 과거에서 시작 시간을 설정 합니다. 4004 이벤트 kds 이벤트 로그에 기록 된 있는지 확인 합니다.

#### <a name="to-create-the-kds-root-key-in-a-test-environment-for-immediate-effectiveness"></a>즉시 효과 대 한 테스트 환경에서 KDS 루트 키를 만들려면

1.  Windows Server 2012 도메인 컨트롤러에서 작업 표시줄에서 Windows PowerShell 실행 합니다.

2.  Active Directory Windows PowerShell 모듈에 대 한 명령 프롬프트 뒤 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

    **$는 = Get 날짜**

    **$b=$a.AddHours(-10)**

    **Add-KdsRootKey -EffectiveTime $b**

    또는 단일 명령을 사용 하 여

    **Add-KdsRootKey -EffectiveTime ((get-date).addhours(-10))**

## <a name="see-also"></a>참조 하십시오
[관리 서비스 계정 하는 그룹 시작](getting-started-with-group-managed-service-accounts.md)


