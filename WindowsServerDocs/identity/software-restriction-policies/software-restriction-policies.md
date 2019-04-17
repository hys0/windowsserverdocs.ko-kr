---
title: "소프트웨어 제한 정책"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c0befad-07c3-4262-b418-372d01850305
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ab44013b947d33adc12c54b527415bf16c46a4c6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="software-restriction-policies"></a>소프트웨어 제한 정책

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

IT 전문가 위한이 항목에서 Windows 8 및 Windows Server 2012 소프트웨어 제한 정책 (소매가)에 대해 설명 하 고 소매가 부터는 Windows Server 2003에 대 한 기술 정보 링크를 제공 합니다.

절차 및 문제 해결 정보를 보려면 [소프트웨어 제한 정책을 관리](administer-software-restriction-policies.md) 및 [소프트웨어 문제를 해결 제한 정책](troubleshoot-software-restriction-policies.md)합니다.

## <a name="BKMK_OVER"></a>소프트웨어 제한 정책을 설명
소프트웨어 제한 정책 (소매가)은 도메인에 있는 컴퓨터에서 실행 중인 소프트웨어 프로그램으로 식별 하 고 이러한 프로그램을 실행 하는 기능을 제어 하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책은 Microsoft 보안 및 안정성, 무결성 및 컴퓨터 관리를 향상 시키는 기업 지원 하기 위해 관리 전략 포함 됩니다.

또한 매우 제한적 구성을 식별된 응용 프로그램을 실행 하면 컴퓨터에 대 한 제한 정책을 소프트웨어를 사용할 수 있습니다. 그룹 정책 및 Microsoft Active Directory를 제한 정책이 소프트웨어 통합 되어 있습니다. 또한 소프트웨어 제한 정책 독립 실행형 컴퓨터에 만들 수 있습니다. 소프트웨어 제한 정책은 규정 스크립트와 완벽 하 게 실행에서 신뢰할 수 없는 다른 코드를 제한 하려면 관리자 권한으로 설정 되는 보안 정책이 합니다.

로컬 그룹 정책 편집기 또는 보안 정책이 로컬 스냅인 소프트웨어 제한 정책을 확장을 통해 이러한 정책은 Microsoft Management Console MMC ()를 정의할 수 있습니다.

소매가 대 한 자세한 내용은 참조는 [소프트웨어 제한 정책 Technical 개요](software-restriction-policies-technical-overview.md)합니다.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
관리자 다음 작업에 대 한 제한 정책을 소프트웨어를 사용할 수 있습니다.

-   신뢰할 수 있는 코드를 정의합니다

-   스크립트 실행 파일, ActiveX 컨트롤을 조정 유연한 그룹 정책을 디자인합니다

소프트웨어 제한 정책을 준수 하는 응용 프로그램 (예: 스크립팅 응용 프로그램) 및 운영 체제 소프트웨어 제한 정책이 적용 됩니다.

특히, 관리자 다음 목적을 위해 제한 정책을 소프트웨어를 사용할 수 있습니다.

-   지정 하는 클라이언트에서 실행할 수 있는 소프트웨어 (실행 파일)

-   사용자 공유 컴퓨터에서 특정 프로그램을 실행 하는 것을 방지합니다

-   신뢰할 수 있는 게시자 클라이언트에 추가할 수 있는 사용자 지정

-   (정책은 모든 사용자에 게 영향을 지 여부 또는 클라이언트에서 사용자의 하위 집합 지정) 소프트웨어 제한 정책 범위 설정

-   실행 파일 로컬 컴퓨터, 조직 단위, 사이트 또는 도메인에서 실행 되지 않도록 합니다. 게 되는 경우에서 사용자가 악성 소프트웨어 제한 정책을 잠재적 문제를 해결 하려면 사용 하지 않는 경우 합니다.

## <a name="BKMK_NEW"></a>새로운 기능과 변경 된 기능
기능이 제한 정책 소프트웨어에 대 한 없습니다 변경 사항이 있습니다.

## <a name="BKMK_DEP"></a>제거 하거나 사용 하지 않는 기능
소프트웨어 제한 정책에 대 한 없는 제거 하거나 사용 하지 않는 기능이 있습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
로컬 그룹 정책 편집기 소프트웨어 제한 정책 확장 MMC를 통해 액세스할 수 있습니다.

다음과 같은 기능을 만들고 관리할 소프트웨어 제한 정책이 로컬 컴퓨터에 필요 합니다.

-   로컬 그룹 정책 편집기

-   Windows Installer

-   Authenticode 및 WinVerifyTrust

디자인 도메인 배포 위 목록 뿐만 아니라 이러한 정책에 대 한 호출 다음과 같은 기능 사항은 다음과 같습니다.

-   Active Directory Domain Services

-   그룹 정책

## <a name="BKMK_INSTALL"></a>서버 관리자 정보
소프트웨어 제한 로컬 그룹 정책 편집기의 확장 정책과 서버 관리자, 역할 추가 기능을 통해 설치 되어 있지 않습니다.

## <a name="BKMK_LINKS"></a>참조 하십시오
다음 표에서 이해 하 고 사용 하 여 소매가 관련 리소스에 대 한 링크를 제공 합니다.

|콘텐츠 종류|참조|
|--------|-------|
|**제품 평가**|[소프트웨어 제한 정책 응용 프로그램 잠금](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|
|**계획**|[소프트웨어 제한 정책 Technical 개요](software-restriction-policies-technical-overview.md) (Windows Server 2012)<br /><br />[소프트웨어 제한 정책 기술 참조](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx) (Windows Server 2003)|
|**배포**|리소스를 사용할 수 없습니다.|
|**작업**|[소프트웨어 제한 정책을 관리](administer-software-restriction-policies.md) (Windows Server 2012)<br /><br />[소프트웨어 제한 정책은 제품 지원](https://technet.microsoft.com/library/cc779607(v=WS.10).aspx) (Windows Server 2003)|
|**문제 해결**|[제한 정책이 소프트웨어 문제를 해결](troubleshoot-software-restriction-policies.md) (Windows Server 2012)<br /><br />[문제 해결 소프트웨어 제한 정책](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx) (Windows Server 2003)|
|**보안**|[위협과 대책 소프트웨어 제한에 대 한 정책을](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx) (Windows Server 2008)<br /><br />[위협과 대책 소프트웨어 제한에 대 한 정책을](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx) (Windows Server 2008 R2)|
|**도구 및 설정**|[소프트웨어 제한 정책을 도구 및 설정](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx) (Windows Server 2003)|
|**커뮤니티 리소스**|[소프트웨어 제한 정책 응용 프로그램 잠금](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|



