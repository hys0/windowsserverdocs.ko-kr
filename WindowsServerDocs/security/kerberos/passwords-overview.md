---
title: 암호 개요
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: cce76e006272104033e1437e0ccf6cad5bc47f3f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950301"
---
# <a name="passwords-overview"></a>암호 개요

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 항목에서는 Windows 운영 체제에서 사용 되는 암호에 대해 설명 하 고 자격 증명 관리 전략에서 암호 사용에 대 한 설명서 및 토론 링크를 제공 합니다.

## <a name="BKMK_OVER"></a>기능 설명
현재 운영 체제 및 응용 프로그램은 암호를 중심으로 설계 되 고 스마트 카드나 생체 인식 시스템을 사용 하는 경우에도 모든 계정에 여전히 암호가 있으며 일부 환경에서 계속 사용할 수 있습니다. 서비스를 실행 하는 데 사용 되는 계정을 비롯 한 일부 계정에는 스마트 카드 및 생체 인식 토큰을 사용할 수 없으므로 인증 하려면 암호를 사용 해야 합니다. Windows는 암호화 해시를 사용 하 여 암호를 보호 합니다.

Windows 암호에 대 한 자세한 내용은 [암호 기술 개요](https://technet.microsoft.com/library/hh994558(WS.10).aspx)를 참조 하세요.

## <a name="BKMK_APP"></a>실용적인 응용 프로그램
Windows 및 기타 다양 한 운영 체제에서 사용자의 id를 인증 하는 가장 일반적인 방법은 암호 암호 또는 암호를 사용 하는 것입니다. 네트워크 환경을 보호 하려면 모든 사용자가 강력한 암호를 사용 해야 합니다. 이를 통해 악의적인 사용자가 수동 메서드를 통하거나 도구를 사용 하 여 손상 된 사용자 계정의 자격 증명을 획득 하는 경우와 상관 없이 약한 암호를 추측 하지 않도록 방지할 수 있습니다. 이는 특히 관리 계정에 적용 됩니다. 복잡 한 암호를 정기적으로 변경 하면 암호 공격이 해당 계정을 손상 시킬 가능성이 줄어듭니다.

## <a name="BKMK_NEW"></a>새로운 기능 및 변경 된 기능
Windows Server 2012 및 Windows 8에서 그림 암호는 새로 만들기입니다. 그림 암호는 일련의 제스처와 연결 된 사용자가 선택한 이미지의 조합입니다. 도메인\-연결 된 컴퓨터에서 그림 암호 기능이 사용 하지 않도록 설정 되어 있습니다. 그림 암호에 대 한 자세한 정보에 대 한 링크는 아래 [참고 항목](#BKMK_LINKS) 에 나와 있습니다.

Windows Server 2012 및 Windows 8에서는 암호 기능이 변경 되지 않았습니다. 새 그룹 정책 설정이 추가 되지 않았습니다. 그러나 자격 증명 \(및 암호\) 관리 (예: 사진 암호, 자격 증명 보관 및 windows Microsoft 계정 8에 로그인 하 고 이전에는 Windows Live ID로 알려짐)에서 향상 된 기능이 향상 되었습니다.

## <a name="BKMK_DEP"></a>사용 되지 않는 기능
Windows Server 2012 및 Windows 8에서는 암호 기능이 더 이상 사용 되지 않습니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
엔터프라이즈 환경에서는 일반적으로 Active Directory Domain Services를 사용 하 여 암호를 관리 합니다. 로컬 보안 설정, 계정 정책, 암호 정책의 설정을 사용 하 여 로컬 컴퓨터에서 암호를 관리할 수도 있습니다.

## <a name="BKMK_LINKS"></a>참고 항목
이 표에는 암호 기능, 기술 및 자격 증명 관리에 대 한 추가 리소스가 나와 있습니다.

|콘텐츠 형식|참조|
|--------|-------|
|**시나리오 설명서**|[디지털 id 보호](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)|
|**작업**|[사용자 및 컴퓨터 Active Directory](https://technet.microsoft.com/library/cc754217.aspx)|
|**문제 해결**|[Active Directory PowerShell 블로그 \- 암호가 만료 되는 경우를 확인 합니다.](https://blogs.msdn.com/b/adpowershell/archive/2010/08/09/9970198.aspx)|
|**보안**| Windows Server 2008 R2 및 Windows 7 [위협 요소 및 대책 가이드: 계정 정책](https://technet.microsoft.com/library/hh125920(v=ws.10).aspx)<br /><br />[강력한 암호를 변경 하 고 만들기](https://www.microsoft.com/security/online-privacy/passwords-create.aspx) 위한 지침|
|**도구 및 설정**|[Microsoft 다운로드 센터의 Windows 및 Windows Server에 대 한 그룹 정책 설정 참조](https://www.microsoft.com/download/en/details.aspx?amp;displaylang=en&displaylang=en&id=25250)|
|**커뮤니티 리소스**|[디지털 id 보호](https://blogs.msdn.com/b/b8/archive/2011/12/14/protecting-your-digital-identity.aspx)<br /><br />[Windows Live ID를 사용 하 여 Windows 8에 로그인](https://blogs.msdn.com/b/b8/archive/2011/09/26/signing-in-to-windows-8-with-a-windows-live-id.aspx)<br /><br />[그림 암호를 사용 하 여 로그인](https://blogs.msdn.com/b/b8/archive/2011/12/16/signing-in-with-a-picture-password.aspx)<br /><br />[그림 암호 보안 최적화](https://blogs.msdn.com/b/b8/archive/2011/12/19/optimizing-picture-password-security.aspx)|


