---
title: 소프트웨어 제한 정책을 사용하여 전자 메일 바이러스로부터 컴퓨터 보호
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 02f23979-f832-4e46-bdea-21fd77db35b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 680d0435d77164e101f045b439be6ccb6601dfef
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855736"
---
# <a name="use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus"></a>소프트웨어 제한 정책을 사용하여 전자 메일 바이러스로부터 컴퓨터 보호

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 SRP (소프트웨어 제한 정책)를 사용 하 여 응용 프로그램 제어 정책을 설정 하는 방법에 대 한 정보를 제공 하 여 Windows Server 2008 및 Windows Vista부터 전자 메일 바이러스 로부터 컴퓨터를 보호 합니다.

## <a name="introduction"></a>소개
SRP(소프트웨어 제한 정책)는 도메인의 컴퓨터에서 실행 중인 소프트웨어 프로그램을 식별하고, 실행할 해당 프로그램의 기능을 제어하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책을 사용하면 명확하게 식별된 애플리케이션만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 이러한 기능은 Microsoft Active Directory Domain Services 및 그룹 정책와 통합 되어 있지만 독립 실행형 컴퓨터 에서도 구성할 수 있습니다. SRP에 대 한 시작 지점은 [소프트웨어 제한 정책](software-restriction-policies.md)을 참조 하세요.

Windows Server 2008 R2 및 Windows 7 부터는 응용 프로그램 제어 전략의 일부에 대 한 SRP를 사용 하거나 사용 하지 않고 Windows AppLocker를 사용할 수 있습니다. 

#### <a name="configure-srp-to-help-protect-against-an-e-mail-virus"></a>전자 메일 바이러스 로부터 보호 하는 데 도움이 되는 SRP 구성

1.  소프트웨어 제한 정책에 대 한 모범 사례를 검토 하 여 SRP의 작동 방식을 파악 합니다.

    -   [모범 사례](software-restriction-policies-technical-overview.md#BKMK_Best_Practices)

    -   [소프트웨어 제한 정책의 작동 방식](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx)

2.  소프트웨어 제한 정책을 엽니다.

    -   [로컬 컴퓨터의 경우](administer-software-restriction-policies.md#BKMK_1)

    -   [도메인, 사이트 또는 조직 구성 단위의 경우 도메인에 가입 된 워크스테이션 또는 구성원 서버에 있는 경우](administer-software-restriction-policies.md#BKMK_2)

3.  이전에 소프트웨어 제한 정책을 정의 하지 않은 경우 새 소프트웨어 제한 정책을 만듭니다.

    -   [새 소프트웨어 제한 정책을 만들려면](administer-software-restriction-policies.md#BKMK_Create_SRP)

4.  전자 메일 프로그램에서 전자 메일 첨부 파일을 실행 하는 데 사용 하는 폴더에 대 한 경로 규칙을 만든 다음 보안 수준을 **허용 안 함**으로 설정 합니다.

    -   [경로 규칙 작업](work-with-software-restriction-policies-rules.md#BKMK_Path_Rules)

5.  규칙이 적용 되는 파일 형식을 지정 합니다.

    -   [지정 된 파일 형식을 추가 하거나 삭제 하려면](administer-software-restriction-policies.md#BKMK_Add_Del)

6.  원하는 사용자 및 그룹에 적용 되도록 정책 설정을 수정 합니다.

    -   그룹 정책 개체의 GPO () 정책 설정을 적용 하지 않으려는 사용자 또는 그룹을 지정 합니다.

    -   그룹 정책의 특정 정책 설정에 대 한 소프트웨어 제한 정책에서 로컬 관리자를 제외 하 고 관리자에 게 나머지 그룹 정책 적용 합니다.

        -   [소프트웨어 제한 정책이 로컬 관리자에 게 적용 되지 않도록 하려면](administer-software-restriction-policies.md#BKMK_Prevent_Admin)

7.  정책을 테스트 합니다.


