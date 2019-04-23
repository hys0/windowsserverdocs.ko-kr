---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: DNS 인프라 디자인 만들기
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 080c36f8410be4d6b1933c74730e2b55ce8d0a0b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856134"
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS 인프라 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory 포리스트 및 도메인 디자인을 만든 후 Active Directory 논리 구조를 지원 하기 위해 도메인 이름 시스템 (DNS) 인프라를 디자인 해야 합니다. DNS를 사용 하면 컴퓨터 및 IP 네트워크의 다른 리소스에 연결할 기억 하기 쉬운 친숙 한 이름을 사용할 수 있습니다. Active Directory Domain Services (AD DS) Windows Server 2008에서 DNS 있어야합니다.  
  
조직에 이미 기존 DNS 서버 서비스에 있는지 여부에 따라 달라 집니다 AD DS를 지원 하도록 DNS를 디자인 하기 위한 프로세스 또는 새 DNS 서버 서비스를 배포 하는:  
  
- 기존 DNS 인프라에 이미 있는 경우에 해당 환경에 Active Directory 네임 스페이스를 통합 해야 합니다. 자세한 내용은 [기존 DNS 인프라에 AD DS 통합](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)합니다.  
- 위치에 DNS 인프라가 없는 경우에 디자인 하 고 AD DS를 지원 하기 위해 새 DNS 인프라를 배포 해야 합니다. 자세한 내용은 [배포 도메인 이름 시스템 (DNS)](https://go.microsoft.com/fwlink/?LinkId=93656)합니다.  
  
조직에 기존 DNS 인프라를 DNS 인프라가 Active Directory 네임 스페이스와 상호 작용 하는 방법을 이해 해야 합니다. 기존 DNS 인프라 디자인을 문서화 하는 데 도움이 되는 워크시트를 다운로드에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) 및 "DNS 인벤토리" (DSSLOGI_8.doc)를 엽니다.  
  
> [!NOTE]  
> IP 버전 4 외에도, Windows Server도 지원 IP 버전 6(ipv6) 주소를 나타냅니다 (IPv4) 주소를 입력 합니다. 재귀적 이름 확인 방법의 현재 DNS 구조를 문서화 하는 동안 IPv6 주소를 나열 하는 데 도움이 되는 워크시트를 참조 하세요. [부록 a: DNS 인벤토리](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)합니다.
  
AD DS를 지원 하도록 DNS 인프라를 설계 하기 전에 DNS 계층 구조, DNS 이름 확인 프로세스 및 DNS AD DS에서 지 원하는 방법에 대해 읽어보려면 유용할 수 있습니다. DNS 계층 구조 및 이름 확인 프로세스에 대 한 자세한 내용은 참조는 DNS 기술 참조 ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145)). DNS에서 AD DS를 지 원하는 방법에 대 한 자세한 내용은 Active Directory 기술 참조에 대 한 DNS 지원 참조 ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147)).  
  
## <a name="in-this-section"></a>단원 내용  

- [DNS 개념 검토](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
- [DNS 및 AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
- [AD DS 소유자 역할에 대 한 DNS 할당](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
- [기존 DNS 인프라에 AD DS 통합](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
