---
title: "Kerberos 위임 개요를 제한"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 51923b0a-0c1a-47b2-93a0-d36f8e295589
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: e90aa5e395fa43a3f94cccb13444fd6991ac1074
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-constrained-delegation-overview"></a>Kerberos 위임 개요를 제한

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한 개요 여기서 Windows Server 2012 R2 및 Windows Server 2012에서 위임 Kerberos 제한에 대 한 새로운 기능에 설명 합니다.

## <a name="feature-description"></a>기능 설명
안전 하 게 형태의 서비스에서 사용할 수 있는 위임 제공 하기 위해 Windows Server 2003에 위임 Kerberos 제한 도입 되었습니다. 구성 된 경우 제한 위임을 지정된 서버 사용자를 대신 하 여 작동할 수 있는 서비스를 제한 합니다. 이 도메인을 서비스에 대 한 도메인 계정을 구성 하려면 관리자 권한이 필요 하며 계정을 단일 도메인에 대 한 제한 됩니다. 오늘 기업에서 프런트 서비스 도메인에만 서비스와의 통합 제한 될 수 없도록 됩니다.

이전 운영 체제를 도메인 관리자 구성 서비스를 서비스 관리자 소유 하 고 자녀가 리소스 서비스에 위임 프런트 서비스 알 수 있는 유용한 방법이 했습니다. 및 리소스 서비스에 위임 수 있는 모든 프런트 서비스 잠재적 공격 포인트를 표시 합니다. 서버 프런트 서비스 호스트 하는 손상 된 리소스 서비스에 위임 하도록 구성 된 경우 리소스 서비스 또한 손상 될 수 있습니다.

Windows Server 2012 R2 및 Windows Server 2012에서 서비스에 대 한 제한 위임 구성 하는 기능에 도메인 관리자 로부터 서비스 관리자에 게 전송 되었습니다. 이러한 방식으로 서비스 백 엔드 관리자 허용 하거나 프런트 서비스 거부 수 있습니다.

Windows Server 2003에서 도입 참조 제한 위임에 대 한 자세한 내용은 [Kerberos 프로토콜 전환 하 고 제한 위임](https://technet.microsoft.com/library/cc739587(v=ws.10))합니다.

Windows Server 2012 R2 및 Windows Server 2012 구현 Kerberos 프로토콜 제한 위임 용으로 특별히 확장 포함 되어 있습니다.  프록시 (S4U2Proxy)를 사용자에 대 한 서비스를 서비스를를 사용 하 여 사용자의 Kerberos 서비스 티켓 백 엔드 서비스를 서비스 티켓 키 메일 센터 (KDC)에서 가져올 수 있습니다. 이러한 확장 사용 제한 위임 다른 도메인에 될 수 있는 백 엔드 서비스의 계정에서 구성할 수 있습니다. 해당 확장이 프로그램에 대 한 자세한 내용은 참조 [\[MS-SFU\]: Kerberos 프로토콜 확장: 사용자와 위임 프로토콜 사양 제한에 대 한 서비스](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx) MSDN 라이브러리에 있습니다.

## <a name="practical-applications"></a>실용적인 응용 프로그램
제한 된 위임 서비스 관리자 지정 하 고 사용자를 대신 하 여 응용 프로그램 서비스 작동할 수 있는 범위를 제한 하 여 응용 프로그램 신뢰 경계를 적용 하는 기능을 제공 합니다. 서비스 관리자 프런트 서비스 계정을 자신의 백 엔드 서비스에 위임 하는 구성할 수 있습니다.

도메인 Windows Server 2012 R2 및 Windows Server 2012에서 제한 된 위임을 지원 하 여 제한 된 위임 다른 도메인에 있는 서버 인증을 사용 하 여 Microsoft Internet Security 및 라우터 서버, Microsoft Forefront 위협 관리 게이트웨이, Microsoft Exchange Outlook OWA Web Access (), Microsoft SharePoint Server 등 프런트 서비스를 구성할 수 있습니다. 이 대 한 지원을 도메인 서비스 솔루션 제공 기존 Kerberos 인프라를 사용 하 여 합니다. Kerberos 제한 위임 도메인 관리자 또는 서비스 관리자가 관리할 수 있습니다.

## <a name="new-and-changed-functionality"></a>새로운 기능과 변경 된 기능
**도메인에서 제한 된 위임 리소스 기반**

Kerberos 제한 위임 제한 위임 프런트 서비스 및 리소스 서비스 같은 도메인에 없는 경우 제공 하기 위해 사용할 수 있습니다. 서비스 관리자 계정 개체 리소스 서비스에 사용자가 가장 수 있는 프런트 서비스의 도메인 계정을 지정 하 여 새 위임 구성할 수 있습니다.

**이 변경에 추가 어떤 값 되나요?**

도메인에서 제한 된 위임을 지원 하 여 제한 위임 무제한 위임 사용 하지 않고 다른 도메인 서버 인증을 사용 하 여 서비스를 구성할 수 있습니다. 이 대 한 지원을 인증 서비스에 위임 하 프런트 서비스를 신뢰할 수 없어도 기존 Kerberos 인프라를 사용 하 여 도메인 서비스 솔루션에서 제공 합니다.

**다르게 작동 무엇 인가요?**

기본 프로토콜 변경 도메인 제한 위임 수 있게합니다. Windows Server 2012 R2 및 Windows Server 2012 구현 Kerberos 프로토콜 (S4U2Proxy) 프록시 프로토콜을 사용자에 대 한 서비스에 대 한 확장 포함 되어 있습니다. 서비스를 사용 하 여 사용자의 Kerberos 서비스 티켓 백 엔드 서비스를 서비스 티켓 키 메일 센터 (KDC)에서 가져올 수 있도록 해 주는 Kerberos 프로토콜에 대 한 확장 집합입니다.

구현 이러한 확장에 대 한 정보를 참조 하세요. [\[MS-SFU\]: Kerberos 프로토콜 확장: 사용자와 위임 프로토콜 사양 제한에 대 한 서비스](https://msdn.microsoft.com/library/cc246071(PROT.10).aspx) MSDN에 있습니다.

기본적인 메시지 순서를 전달된 허용 티켓 (TGT) 서비스와 비교 하 여 사용자 (S4U) 확장 된 Kerberos 위임에 대 한 자세한 내용은 섹션 참조 [1.3.3 프로토콜 개요](https://msdn.microsoft.com/library/cc246080(v=prot.10).aspx) [MS SFU]에: Kerberos 프로토콜 확장: 사용자와 위임 프로토콜 사양 제한에 대 한 서비스입니다.

리소스 서비스에서 사용자를 대신 프런트 서비스 액세스를 허용 하도록 구성를 Windows PowerShell cmdlet을 사용 합니다.

-   주체 목록의 검색 하려면는 **Get ADComputer**, **Get ADServiceAccount**, 및 **Get ADUser** 으로 cmdlet는 **속성 PrincipalsAllowedToDelegateToAccount** 매개 합니다.

-   리소스 서비스를 사용 하는 **새로 ADComputer**, **새로 ADServiceAccount**, **새로 ADUser**, **설정 ADComputer**, **설정 ADServiceAccount**, 및 **설정 ADUser** 으로 cmdlet는 **PrincipalsAllowedToDelegateToAccount** 매개 합니다.

## <a name="BKMK_SOFT"></a>소프트웨어 요구 사항
제한 위임 리소스 기반 Windows Server 2012 R2 및 Windows Server 2012를 실행 하는 도메인 컨트롤러에만 구성할 수 있지만 혼합 숲 내 적용 될 수 있습니다.

Windows Server 2012에서에서 실행 사용자 계정 도메인 추천 길에 이전 Windows Server 운영 체제를 실행 하는 프런트 및 백 엔드 도메인 간에 모든 도메인 컨트롤러에 다음과 같은 핫픽스 적용 해야: 리소스 기반 제한 위임 Windows Server 2008 R2 기반 도메인 컨트롤러 있는 환경에서 KDC_ERR_POLICY 실패 합니다.
