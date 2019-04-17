---
title: "메일 바이러스 로부터 컴퓨터를 보호 하기 위해 제한 정책이 소프트웨어를 사용 하 여"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 41b4c2399a86ef96d34b62295eda4a1ce9300609
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>메일 바이러스 로부터 컴퓨터를 보호 하기 위해 제한 정책이 소프트웨어를 사용 하 여

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 응용 프로그램 컨트롤을 설정 하는 방법을 Windows Server 2008 및 Windows Vista로 시작 하는 메일 바이러스 로부터 컴퓨터를 보호 하기 위해 소프트웨어 제한 정책 (소매가)를 사용 하 여 정책을 정보를 제공 합니다.

## <a name="introduction"></a>소개
소프트웨어 제한 정책 (소매가)은 도메인에 있는 컴퓨터에서 실행 중인 소프트웨어 프로그램으로 식별 하 고 이러한 프로그램을 실행 하는 기능을 제어 하는 그룹 정책 기반 기능입니다. 제한 정책이 소프트웨어를 사용 하 여 매우 제한적된 구성을 식별된 응용 프로그램을 실행 하면 컴퓨터에 대 한 만들 수 있습니다. 이러한 그룹 정책을 Microsoft Active Directory Domain Services와 통합만 독립 실행형 컴퓨터에를 구성할 수도 있습니다. 소매가, 출발점 참조는 [소프트웨어 제한 정책](software-restriction-policies.md)합니다.

Windows Server 2008 R2 및 Windows 7부터, Windows AppLocker에 사용할 수 대신 또는 소매가 협력 제어 전략 응용 프로그램의 일부입니다. 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>메일 바이러스 로부터 보호 하기 위해 소매가 구성

1.  소매가 작동 방식을 이해를 제한 정책 소프트웨어에 대 한 유용한 검토 합니다.

    -   [모범 사례](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [제한 정책이 소프트웨어 작동 하는 방법](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  제한 정책을 소프트웨어를 엽니다.

    -   [로컬 컴퓨터에 대 한](administer-software-restriction-policies.md#BKMK_1)

    -   [도메인에 대 한 사이트 또는 조직 구성원 서버의 또는 작업할 도메인에 가입 워크스테이션](administer-software-restriction-policies.md#BKMK_2)

3.  소프트웨어 제한 정책, 이전에 정의 하지 않은 경우 새 소프트웨어 제한 정책 만듭니다.

    -   [새 소프트웨어 제한 정책 만들려면](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  전자 메일 프로그램 실행 메일 첨부 파일을 사용 하는 폴더에 대 한 경로 규칙 만들고 후 보안을 수준을 설정 **허용 안 함**합니다.

    -   [경로 규칙 작업](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  파일 형식을 여 규칙을 적용할 지정 합니다.

    -   [지정 된 파일 형식 추가 또는 삭제 하려면](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  정책 설정을 사용자 및 그룹 원하는에 적용 되도록 수정 합니다.

    -   사용자 또는 그룹을 하지 않을 그룹 정책 개체의 (GPO) 지정 정책 설정을 적용 합니다.

    -   그룹 정책에서 특정 정책 설정의 소프트웨어 제한 정책에서 로컬 관리자 제외 하 고 그룹 정책의 나머지 부분 관리자에 게 적용 되지 않았습니다.

        -   [소프트웨어 제한 정책이 로컬 관리자에 게 적용 하지 않도록 하려면](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  정책을 테스트 합니다.


