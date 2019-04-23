---
title: What's New for Managed Service Accounts
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f2a8b6b-c152-4c40-b712-bfabff0e408b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: cac55d04a40c84ce160eb3883d6095a7db0ef3be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872184"
---
# <a name="what39s-new-for-managed-service-accounts"></a>새로운&#39;관리 서비스 계정에 대 한 새

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 항목에서는 변경 사항이 설명 되어 기능 관리 서비스 계정에 대 한 그룹 관리 서비스 계정 (gMSA) Windows Server 2012 및 Windows 8에 도입 합니다.

관리 서비스 계정을 사용하면 Windows 서비스 및 IIS 응용 프로그램 풀과 같은 서비스 및 작업에서 자체 도메인 계정을 공유할 수 있을 뿐만 아니라, 관리자가 이러한 계정에 대한 암호를 수동으로 관리할 필요가 없습니다. 또한 관리 도메인 계정에서는 자동 암호 관리 기능을 제공합니다.

## <a name="versions"></a>Windows Server 2012 및 Windows 8 관리 서비스 계정의 새로운 기능
다음 기능이 변경 된 Windows Server 2012 및 Windows 8에서 MSA를 설명 합니다.

### <a name="group-managed-service-accounts"></a>그룹 관리 서비스 계정
도메인의 서버에 대해 도메인 계정이 구성되어 있으면 클라이언트 컴퓨터가 해당 서비스에 인증 및 연결할 수 있습니다. 이전에는 두 가지 계정 유형만이 암호 관리를 요구하지 않고 ID를 제공했습니다. 그러나 이러한 계정 유형에는 다음과 같은 제한이 있습니다.

-   컴퓨터 계정이 단일 도메인 서버로 제한되며 컴퓨터가 암호를 관리합니다.

-   관리 서비스 계정이 단일 도메인 서버로 제한되며 컴퓨터가 암호를 관리합니다.

이러한 계정은 여러 시스템에서 공유할 수 없습니다. 따라서 원치 않는 암호 만료를 방지하기 위해 각 시스템에서 개별 서비스에 대해 계정을 정기적으로 유지 관리해야 합니다.

**이와 같은 변경을 통해 더해지는 가치**

그룹 관리 서비스 계정에 계정 암호를 Windows Server 2012 도메인 컨트롤러에서 관리 되 고 여러 Windows Server 2012 시스템에서 검색할 수 있으므로이 문제가 해결 되었습니다. 따라서 Windows에서 이러한 계정에 대한 암호 관리를 처리할 수 있어 서비스 계정의 관리 오버헤드가 최소화됩니다.

**달라진 기능**

컴퓨터에서 Windows Server 2012 또는 Windows 8 그룹 MSA를 작성 및 서비스의 다양 한 인스턴스는 같은 서버 팜에 배포 되도록 서비스 제어 관리자를 통해 관리 되는 실행 관리할 수 있습니다 서버. 이전에 관리 서비스 계정을 관리하기 위해 사용했던 IIS 응용 프로그램 풀 관리자 등의 도구 및 유틸리티를 그룹 관리 서비스 계정에도 사용할 수 있습니다. 도메인 관리자는 서비스 관리를 서비스 관리자에게 위임할 수 있으며, 서비스 관리자는 관리 서비스 계정 또는 그룹 관리 서비스 계정의 전체 수명 주기를 관리할 수 있습니다. 기존 클라이언트 컴퓨터는 인증 대상 서비스 인스턴스를 몰라도 해당 서비스에 대해 인증할 수 있습니다.

### <a name="interoperability"></a>제거 되었거나 사용 되지 않는 기능
Windows Server 2012, Windows PowerShell cmdlet 기본값은 서버 관리 서비스 계정이 아닌 그룹 관리 서비스 계정을 관리 합니다.

## <a name="see-also"></a>참조

-   [그룹 관리 서비스 계정 개요](group-managed-service-accounts-overview.md)

-   [Active Directory Domain Services 개요](active-directory-domain-services-overview.md)

-   [관리 서비스 계정: 이해, 구현, 모범 사례 및 문제 해결](http://blogs.technet.com/b/askds/archive/20../managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)


