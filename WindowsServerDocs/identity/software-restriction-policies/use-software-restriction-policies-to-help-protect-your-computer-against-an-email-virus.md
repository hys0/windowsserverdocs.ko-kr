---
title: 소프트웨어 제한 정책을 사용하여 전자 메일 바이러스로부터 컴퓨터 보호
description: Windows Server 보안
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850674"
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>소프트웨어 제한 정책을 사용하여 전자 메일 바이러스로부터 컴퓨터 보호

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 응용 프로그램 제어를 설정 하는 방법을 소프트웨어 제한 정책 (SRP)를 사용 하 여 Windows Server 2008 및 Windows Vista로 시작 하는 전자 메일 바이러스 로부터 컴퓨터를 보호 하기 위해 정책을 설명 합니다.

## <a name="introduction"></a>소개
SRP(소프트웨어 제한 정책)는 도메인의 컴퓨터에서 실행 중인 소프트웨어 프로그램을 식별하고, 실행할 해당 프로그램의 기능을 제어하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책을 사용하면 명확하게 식별된 응용 프로그램만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 이러한 Microsoft Active Directory Domain Services 및 그룹 정책과 통합 되어 있지만 독립 실행형 컴퓨터 에서도 구성할 수 있습니다. SRP에 대 한 시작 지점에 대 한 참조를 [소프트웨어 제한 정책](software-restriction-policies.md)합니다.

Windows Server 2008 R2 및 Windows 7 부터는 Windows AppLocker 용도로 사용할 수 있습니다 또는 SRP 함께 대신 응용 프로그램 제어 전략의 일부입니다. 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>전자 메일 바이러스 로부터 보호 하기 위해 SRP를 구성 합니다.

1.  SRP의 작동 방식을 이해 하려면 소프트웨어 제한 정책에 대 한 모범 사례를 검토 합니다.

    -   [모범 사례](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [소프트웨어 제한 정책의 작동 방식](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  소프트웨어 제한 정책을 엽니다.

    -   [로컬 컴퓨터에 대 한](administer-software-restriction-policies.md#BKMK_1)

    -   [도메인에 대 한 사이트 또는 조직 구성 단위와는 도메인에 가입 되어 있는 워크스테이션 또는 구성원 서버에서](administer-software-restriction-policies.md#BKMK_2)

3.  이전에 소프트웨어 제한 정책은 정의 하지 않은 경우에 새 소프트웨어 제한 정책을 만듭니다.

    -   [새 소프트웨어 제한 정책을 만들려면](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  전자 메일 프로그램에서 사용 하 여 전자 메일 첨부 파일을 실행 하는 폴더에 대 한 경로 규칙을 만들고 설정한 보안 수준을 **허용 안 함**합니다.

    -   [경로 규칙 작업](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  규칙이 적용 되는 파일 형식을 지정 합니다.

    -   [지정 된 파일 형식을 추가 하거나 삭제 하려면](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  사용자 및 그룹에 적용 되도록 정책 설정을 수정 합니다.

    -   사용자 또는 그룹을 원하지 않는 그룹 정책 개체의 (GPO) 지정 정책 설정을 적용 합니다.

    -   로컬 관리자 그룹 정책에서 특정 정책 설정의 소프트웨어 제한 정책에서 제외 하 고 나머지 그룹 정책 관리자에 게 적용 되지 않았습니다.

        -   [소프트웨어 제한 정책은 로컬 관리자에 게 적용 하지 않도록 설정 하려면](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  정책을 테스트 합니다.


