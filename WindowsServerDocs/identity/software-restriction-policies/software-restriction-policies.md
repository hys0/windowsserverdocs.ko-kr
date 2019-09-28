---
title: 소프트웨어 제한 정책
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: b06d038e919e2f4904d60b88ad223493c4f818eb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357666"
---
# <a name="software-restriction-policies"></a>소프트웨어 제한 정책

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

IT 전문가를 위한이 항목에서는 Windows Server 2012 및 Windows 8의 SRP (소프트웨어 제한 정책)에 대해 설명 하 고 Windows Server 2003부터 SRP에 대 한 기술 정보 링크를 제공 합니다.

절차 및 문제 해결 팁은 [소프트웨어 제한 정책 관리](administer-software-restriction-policies.md) 및 [소프트웨어 제한 정책 문제 해결](troubleshoot-software-restriction-policies.md)을 참조 하세요.

## <a name="BKMK_OVER"></a>소프트웨어 제한 정책 설명
SRP(소프트웨어 제한 정책)는 도메인의 컴퓨터에서 실행 중인 소프트웨어 프로그램을 식별하고, 실행할 해당 프로그램의 기능을 제어하는 그룹 정책 기반 기능입니다. 소프트웨어 제한 정책은 Microsoft 보안 및 관리 전략의 일환으로, 기업이 자사 컴퓨터에 대한 안정성과 무결성, 관리 효율성을 향상시킬 수 있도록 지원합니다.

또한 소프트웨어 제한 정책을 사용하여 명확하게 식별된 응용 프로그램만 실행할 수 있도록 고도로 제한된 컴퓨터 구성을 만들 수 있습니다. 소프트웨어 제한 정책은 Microsoft Active Directory 및 그룹 정책에 통합되어 있습니다. 독립 실행형 컴퓨터에 소프트웨어 제한 정책을 만들 수도 있습니다. 소프트웨어 제한 정책은 완전히 신뢰할 수 없는 스크립트와 기타 코드를 실행하지 못하도록 제한하기 위해 관리자가 만든 규정으로 구성된 신뢰할 수 있는 정책입니다.

이러한 정책은 로컬 그룹 정책 편집기의 소프트웨어 제한 정책 확장이나 MMC(Microsoft Management Console)의 로컬 보안 정책 스냅인을 사용하여 정의할 수 있습니다.

SRP에 대한 자세한 내용은 [Software Restriction Policies Technical Overview](software-restriction-policies-technical-overview.md)를 참조하세요.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
관리자는 소프트웨어 제한 정책을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

-   신뢰할 수 있는 코드 정의

-   스크립트, 실행 파일 및 ActiveX 컨트롤을 규제할 수 있는 유연한 그룹 정책 설계

소프트웨어 제한 정책은 소프트웨어 제한 정책을 준수하는 응용 프로그램(예: 스크립팅 응용 프로그램) 및 운영 체제에서 강제 적용됩니다.

관리자는 특히 다음과 같은 목적으로 소프트웨어 제한 정책을 사용할 수 있습니다.

-   클라이언트에서 실행할 수 있는 소프트웨어(실행 파일) 지정

-   사용자가 공유 컴퓨터에서 특정 프로그램을 실행할 수 없도록 지정

-   클라이언트에 신뢰할 수 있는 게시자를 추가할 수 있는 사람 지정

-   소프트웨어 제한 정책의 범위 설정(정책 적용 대상을 클라이언트의 모든 사용자로 할지, 일부 사용자로 할지 지정)

-   실행 파일이 로컬 컴퓨터, OU(조직 구성 단위), 사이트 또는 도메인에서 실행될 수 없도록 방지합니다. 이는 악성 사용자의 잠재적인 문제점을 해결하는 데 소프트웨어 제한 정책을 사용하지 않는 경우에 적절합니다.

## <a name="BKMK_NEW"></a>새로운 기능 및 변경 된 기능
소프트웨어 제한 정책에는 변경된 기능이 없습니다.

## <a name="BKMK_DEP"></a>제거 되었거나 더 이상 사용 되지 않는 기능
소프트웨어 제한 정책에는 제거되었거나 더 이상 사용되지 않는 기능이 없습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
MMC를 통해 로컬 그룹 정책 편집기의 소프트웨어 제한 정책 확장을 액세스할 수 있어야 합니다.

로컬 컴퓨터에서 소프트웨어 제한 정책을 만들고 유지 관리하려면 다음과 같은 기능이 필요합니다.

-   로컬 그룹 정책 편집기

-   Windows Installer

-   Authenticode 및 WinVerifyTrust

설계 시 이러한 정책에 대한 도메인 배포가 필요한 경우 다음과 같은 기능이 추가로 필요합니다.

-   Active Directory 도메인 서비스

-   그룹 정책

## <a name="BKMK_INSTALL"></a>서버 관리자 정보
소프트웨어 제한 정책은 로컬 그룹 정책 편집기의 확장으로, 서버 관리자의 역할 및 기능 추가를 통해 설치되지 않습니다.

## <a name="BKMK_LINKS"></a>참고 항목
다음 표에는 SRP를 이해하고 사용하는 일과 관련된 리소스에 대한 링크가 포함되어 있습니다.

|콘텐츠 형식|참조|
|--------|-------|
|**제품 평가**|[소프트웨어 제한 정책을 사용 하는 응용 프로그램 잠금](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|
|**계획**|[소프트웨어 제한 정책 기술 개요](software-restriction-policies-technical-overview.md) (Windows Server 2012)<br /><br />[소프트웨어 제한 정책 기술 참조](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx) (Windows Server 2003)|
|**배포**|사용 가능한 리소스 없음|
|**작업**|[소프트웨어 제한 정책 관리](administer-software-restriction-policies.md) (Windows Server 2012)<br /><br />[소프트웨어 제한 정책 제품 도움말](https://technet.microsoft.com/library/cc779607(v=WS.10).aspx) (Windows Server 2003)|
|**문제 해결**|[소프트웨어 제한 정책 문제 해결](troubleshoot-software-restriction-policies.md) (Windows Server 2012)<br /><br />[소프트웨어 제한 정책 문제 해결](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx) (Windows Server 2003)|
|**보안**|[소프트웨어 제한 정책에 대한 위협 및 대책](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx) (Windows Server 2008)<br /><br />[소프트웨어 제한 정책에 대한 위협 및 대책](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx) (Windows Server 2008 R2)|
|**도구 및 설정**|[소프트웨어 제한 정책 도구 및 설정](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx) (Windows Server 2003)|
|**커뮤니티 리소스**|[소프트웨어 제한 정책을 사용 하는 응용 프로그램 잠금](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|



