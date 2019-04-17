---
title: "관리 서비스 계정에 대 한 새로운 기능"
description: "Windows Server 보안"
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
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="what39s-new-for-managed-service-accounts"></a>작업 & #39; 관리 서비스 계정에 대 한 새로운 s

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목에 설명 변경 내용을 기능에서 관리 서비스 계정 그룹 관리 서비스 계정 (gMSA) Windows 8 및 Windows Server 2012에서 도입 합니다.

관리 서비스 계정 서비스 및 Windows 서비스 및 IIS 응용 프로그램 풀 수동으로 해당이 계정에 대 한 암호를 관리 하려면 관리자에 대 한 필요성을 제거 하는 동안 자신의 도메인 계정 공유 하는 등의 작업을 제공 하도록 설계 되었습니다. 관리 되는 도메인 계정 암호 자동 관리 기능을 제공 하는 것이 있습니다.

## <a name="versions"></a>Windows 8 및 Windows Server 2012에서 관리 서비스 계정에 대 한 새로운 기능
다음 기능에 변경 내용을 Windows 8 및 Windows Server 2012에서 MSA에 설명 합니다.

### <a name="group-managed-service-accounts"></a>그룹 관리 서비스 계정
도메인 계정인 도메인에 있는 서버에 대 한 구성 되어 클라이언트 컴퓨터 인증할 하 고 해당 서비스에 연결할 수 있습니다. 이전에 두 계정 유형이 신원을 암호 관리를 않고도 제공 합니다. 하지만 이러한 계정 유형이 제한:

-   계정을 하나 도메인 서버에 제한 되며 컴퓨터에서 암호 관리

-   컴퓨터에서 암호 관리 및 관리 서비스 계정 한 도메인 서버에 제한 됩니다.

이러한 계정은 여러 시스템 공유할 수 없습니다. 따라서 원하지 않는 암호 만료 되지 않도록 하려면 각 시스템에서 각 서비스에 대 한 계정을 정기적으로 유지 해야 합니다.

**이 변경에 추가 어떤 값 되나요?**

그룹 관리 서비스 계정 계정 암호 Windows Server 2012 도메인 컨트롤러에서 관리 되 고 여러 Windows Server 2012 시스템 하 여 검색할 수 때문에이 문제가 해결 되었습니다. 이 해당 계정에 대 한 암호 관리 처리 하기 위한 작업이 Windows 수 있도록 하 여 서비스 계정의 관리 오버를 최소화 합니다.

**다르게 작동 무엇 인가요?**

컴퓨터에 MSA를 작성 하 고 여러 개 서비스와 같은 서버 팜을 통해 배포할 수 있도록 서비스를 제어 관리자 관리할 수 그룹 Windows 8 또는 Windows Server 2012를 실행에서 관리할 수 한 서버 합니다. 도구 및 관리 서비스 계정, IIS 응용 프로그램 풀 관리 등을 관리 하는 데 사용 되는 유틸리티 그룹 관리 서비스 계정으로 사용할 수 있습니다. 도메인 관리자 서비스 관리 서비스 계정 관리 또는 그룹 관리 서비스 계정의 전체 수명 주기를 관리할 수 있는 서비스 관리자에 위임 수 있습니다. 기존 클라이언트 컴퓨터를 인증 하는 어떤 서비스 인스턴스 모르는 이러한 서비스를 인증 수 있습니다.

### <a name="interoperability"></a>제거 하거나 사용 하지 않는 기능
Windows Server 2012를 Windows PowerShell cmdlet 기본 대신 서버 관리 서비스 계정 그룹 관리 서비스 계정 관리 합니다.

## <a name="see-also"></a>참조 하십시오

-   [그룹 관리 서비스 계정 개요](group-managed-service-accounts-overview.md)

-   [Active Directory Domain Services 개요](active-directory-domain-services-overview.md)

-   [이해: 관리 서비스 계정, 구현 모범 사례 및 문제 해결](http://blogs.technet.com/b/askds/archive/20../managed-service-accounts-understanding-implementing-best-practices-and-troubleshooting.aspx)


