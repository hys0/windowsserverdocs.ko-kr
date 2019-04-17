---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: "DNS Infrastructure 디자인 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6e5093b05fd81a693cec87ddb00d39e70483df23
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS Infrastructure 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory 숲 및 도메인 디자인을 만든 후 Active Directory 논리 구조 지원 하기 위한 시스템 DNS (도메인 이름) 인프라를 디자인 해야 합니다. DNS는 사용자가 쉽게 기억 컴퓨터 및 기타 리소스 IP 네트워크에 연결할 수 있는 식별 이름을 사용할 수 있게 합니다. Active Directory Domain Services (AD DS) Windows Server 2008에서 DNS 있어야 합니다.  
  
조직에 이미 기존 DNS 서버 서비스에 있는지 여부에 따라 달라 집니다 DNS AD DS 지원 하도록 디자인 프로세스 또는 DNS 서버 하는 새 서비스를 배포 하는 경우:  
  
-   기존 DNS 인프라를 이미 있는 경우 Active Directory 네임 해당 환경으로 통합 해야 합니다. 자세한 내용은 참조 [기존 DNS 인프라에 통합 AD DS](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)합니다.  
  
-   장소에는 DNS 인프라 없는 경우에 디자인 하 고 배포 AD DS 지원 하기 위해 새로운 DNS 인프라 해야 합니다. 자세한 내용은 참조 배포 시스템 DNS (도메인 이름) ([https://go.microsoft.com/fwlink/?LinkId=93656](https://go.microsoft.com/fwlink/?LinkId=93656)).  
  
조직에는 기존 DNS 인프라를 경우 DNS 인프라가 Active Directory 네임와 상호 작용 하는 방식을 이해 하는 확인 해야 합니다. 기존 DNS infrastructure 디자인 문서화에 도움을 주고 워크시트를에 대 한 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit에서 ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) "DNS 인벤토리" (DSSLOGI_8.doc).  
  
> [!NOTE]  
> IP 버전 4 뿐 아니라 (IPv4) 주소, Windows Server 2008도 지원 IP 버전 6 (IPv6)을 해결 합니다. 현재 DNS 구조의 반복 이름 해결 방법을 문서화 하는 동안 IPv6 주소 목록에 도움을 주고 워크시트를 참조 하세요. [부록 a: DNS 인벤토리](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)합니다.  
  
DNS 인프라 AD DS 지원 하도록 디자인 하기 전에 DNS 계층, DNS 해상도 프로세스를 및 DNS AD DS 지원 하는 방법에 대해 유용할 수 있습니다. DNS 계층 및 이름을 확인 프로세스에 대 한 자세한 내용은 참조 DNS 기술 참조 ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145)). 에 대 한 Active Directory 기술 참조 DNS AD DS 지원 하는 방법에 대 한 자세한 내용은 참조 DNS 지원 ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147)).  
  
## <a name="in-this-section"></a>이 섹션에서  
  
-   [DNS 개념을 검토](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
  
-   [DNS 및 AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
  
-   [DNS AD DS 소유자 역할 지정 하는 방법](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
  
-   [AD DS 기존 DNS 인프라에 통합](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
  


