---
title: "Windows 인증 기술 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 286d3e41-434f-4703-9320-706d06ebda51
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 1be96846596900c7b2eb2d9d5da93e75572aac98
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="windows-authentication-technical-overview"></a>Windows 인증 기술 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목에 대 한 Windows 인증 기술 개요 항목에 대 한 링크를 제공합니다. Windows 인증 사용자 또는 Windows에 액세스 하려고 할 때 서비스의 신뢰성 입증 하는 프로세스입니다.

이 항목을이 컬렉션 Windows 인증 아키텍처와 구성 요소 설명합니다.

디지털를 저장 하거나이 라이브러리에서 페이지를 인쇄 하려면 클릭 **내보내기** (의 오른쪽 위 모서리에서 페이지의) 한 다음 지침을 따릅니다.

-   [Windows 인증 Windows 운영 체제의 차이](https://technet.microsoft.com/library/dn169017.aspx)

    인증 아키텍처와 프로세스의 주요 차이 설명 합니다.

-   [Windows 인증 개념](https://technet.microsoft.com/library/dn169018.aspx)

    Windows 인증 기반 개념에 설명 합니다.

-   [Windows 로그온 인증 시나리오](https://technet.microsoft.com/library/dn169020.aspx)

    다양 한 로그온 시나리오 요약 되어 있습니다.

-   [Windows 인증 건축물](https://technet.microsoft.com/library/dn169024.aspx)

    인증 아키텍처와 Windows 운영 체제에 대 한 프로세스의 주요 차이 설명 합니다.

    -   [보안 지원 공급자 인터페이스 구조](https://technet.microsoft.com/library/dn169026.aspx)

        SSPI 아키텍처에 설명 합니다.

    -   [자격 증명 프로세스 Windows 인증](https://technet.microsoft.com/library/dn169014.aspx)

        다양 한 자격 증명 관리 프로세스에 설명 합니다.

-   [Windows 인증에 사용 되는 그룹 정책](https://technet.microsoft.com/library/dn169021.aspx)

    사용 및 인증 과정에서 그룹 정책을 영향에 설명 합니다.

## <a name="what-is-not-covered"></a>어떻게 적용 되지 않습니다?
이 항목을이 컬렉션 디자인을 구현 또는 모니터링 Windows 환경 내에서 여 인증 기술에 대 한 절차 적용 되지 않습니다.

-   디자인에 대 한 내용은 Windows 승인 전략, [리소스 승인 전략](https://technet.microsoft.com/library/cc783368.aspx)합니다.

-   디자인에 대 한 내용은 Windows 인증 전략, [인증 전략](https://technet.microsoft.com/library/cc758124.aspx)합니다.

-   디자인에 대 한 내용은 Windows 공개 키 인프라 구현 방법, [공개 키 Infrastructure 디자인](https://technet.microsoft.com/library/cc773138.aspx)합니다.

-   구성 하 고 모니터링 인증을 포함 하 여 Windows 환경에서 보안을 참조 하십시오.

    -   [Windows XP 보안 가이드](https://www.microsoft.com/download/details.aspx?id=962)

    -   [Windows Vista 보안 초기](https://technet.microsoft.com/library/dd450978.aspx)

    -   [Windows Server 2003 보안 기본](https://technet.microsoft.com/library/cc163140.aspx) 및 [위협과 대책 가이드](https://technet.microsoft.com/library/dd162275.aspx)

    -   [Windows Server 2008 보안 가이드](https://www.microsoft.com/download/details.aspx?id=17606)

    -   [Windows Server 2008 R2 보안 초기](https://technet.microsoft.com/library/gg236605.aspx)

-   감사 Windows에 로그온 및 인증 이벤트에 대 한 내용은 [보안 이벤트 감사](https://technet.microsoft.com/library/cc776394.aspx)합니다.


