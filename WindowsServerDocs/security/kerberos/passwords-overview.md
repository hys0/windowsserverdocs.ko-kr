---
title: "암호 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f608960e-2039-4c91-9c8c-9b81053c675e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6c1b8d56b5c0da738e7dae5c0072be81040f90d8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="passwords-overview"></a>암호 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 항목에서는 Windows 운영 체제와 설명서에서 자격 증명 관리 전략 암호의 사용에 대 한 토론에 대 한 링크에서 사용 되는 암호 설명 합니다.

## <a name="BKMK_OVER"></a>기능 설명
운영 체제 및 응용 프로그램을 현재 암호 주위 설계 고 스마트 카드 또는 생체 인식 시스템을 사용 하는 경우 모든 계정이 아직 암호 경우에 따라에서 계속 사용할 수 있습니다. 서비스를 실행 하는 데 사용 하는 계정 특히 일부 계정에서는 스마트 카드 및 생체 인식 토큰도 사용할 수 없는 인증을 암호를 사용 해야 합니다. Windows 암호를 사용 하 여 암호화 해시 보호 합니다.

For more information about Windows passwords, see [Passwords Technical Overview](https://technet.microsoft.com/library/hh994558(WS.10).aspx).

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
Windows 및 기타 많이 운영 체제에는 사용자의 id를 인증에 대 한 가장 일반적인 방법 비밀 암호 또는 암호를 사용 하 여입니다. 네트워크 환경 보안 강력한 암호 모든 사용자가 사용 해야 합니다. 이 악의적인 사용자가 수동 메서드를 통해 지 여부 또는 손상 된 사용자 계정의 자격 증명을 얻기 위해 도구를 사용 하 여 약한 암호 추측 위협 방지할 수 있습니다. 관리자 계정에 그렇습니다. 복잡 한 암호를 정기적으로 변경 하면 해당 계정에 영향을 미치지 암호 공격 가능성 줄일 수 있습니다.

## <a name="BKMK_NEW"></a>새로운 기능과 변경 된 기능
사진 암호는 Windows Server 2012 및 Windows 8에서 새 합니다. 사진 암호는 일련의 제스처와 결합 되어 사용자 선택한 이미지의 조합입니다. 사진 암호 기능 domain\ 가입 컴퓨터에서 사용 되지 않습니다. 사진 암호에 대 한 자세한 정보 링크를에 나열 된 [참고 항목](#BKMK_LINKS) 아래 합니다.

Windows 8 및 Windows Server 2012에서 암호 기능 변경이 했습니다. 새 그룹 정책 설정이 추가 되었습니다. 그러나 향상 된 기능 및 향상 된 기능의에서 내용을 자격 증명 \(and password\) 관리, 사진 암호, 자격 증명 잠금 및 Windows 8으로 Microsoft 계정으로 로그인 이전의 Windows Live ID와 같은 합니다.

## <a name="BKMK_DEP"></a>사용 하지 않는 기능
Windows 8 및 Windows Server 2012에서 되지 암호 기능이 없습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
엔터프라이즈 환경에서 Active Directory Domain Services 된 암호 관리 일반적으로 합니다. 암호에서 설정을 사용 하 여 로컬 계정 정책을 보안 설정을 암호 정책에서 로컬 컴퓨터에서 관리할 수 있습니다.

## <a name="BKMK_LINKS"></a>참조 하십시오
이 표에 암호 기능에 대 한 추가 리소스 기술 및 자격 증명 관리 합니다.

|콘텐츠 종류|참조|
|--------|-------|
|**시나리오 설명서**|[디지털 사용자의 신원을 보호](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**작업**|[Active Directory 사용자와 컴퓨터](https://technet.microsoft.com/library/cc754217.aspx)|
|**문제 해결**|[암호 만료 되는 시기에 대해 알아봅니다 \-Active Directory PowerShell 블로그](http://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**보안**| Windows Server 2008 R2  and  Windows 7 [Threats and Countermeasures Guide: Account Policies](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />Guidance to [change and create strong passwords](https://www.microsoft.com/security/online-privacy/passwords-create.aspx)|
|**도구 및 설정**|[Windows 및 Microsoft 다운로드 센터에서 Windows Server에 대 한 그룹 정책 설정 참조](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**커뮤니티 리소스**|[디지털 사용자의 신원을 보호](http://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Windows Live ID를 가진 Windows 8 로그인](http://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[사진 암호를 사용 하 여 로그인](http://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[사진 암호 보안 최적화](http://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


