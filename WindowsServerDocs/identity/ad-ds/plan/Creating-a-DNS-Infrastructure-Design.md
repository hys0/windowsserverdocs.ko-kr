---
ms.assetid: cd70b0aa-0a67-4966-a041-4dd3f302c98b
title: DNS 인프라 디자인 만들기
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 90c670d5f59702ce932c004a016adb855b040f77
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822806"
---
# <a name="creating-a-dns-infrastructure-design"></a>DNS 인프라 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory 포리스트와 도메인 디자인을 만든 후에는 Active Directory 논리 구조를 지원 하도록 DNS (Domain Name System) 인프라를 디자인 해야 합니다. DNS를 사용 하면 사용자가 쉽게 기억할 수 있는 친숙 한 이름을 사용 하 여 IP 네트워크의 컴퓨터 및 기타 리소스에 연결할 수 있습니다. Windows Server 2008의 Active Directory Domain Services (AD DS)에는 DNS가 필요 합니다.  
  
AD DS를 지원 하기 위해 DNS를 설계 하는 프로세스는 조직에 기존 DNS 서버 서비스가 이미 있는지, 아니면 새 DNS 서버 서비스를 배포 하는지에 따라 달라 집니다.  
  
- 기존 DNS 인프라가 이미 있는 경우 Active Directory 네임 스페이스를 해당 환경에 통합 해야 합니다. 자세한 내용은 [기존 DNS 인프라에 AD DS 통합](../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)을 참조 하세요.  
- DNS 인프라를 구축 하지 않은 경우 AD DS을 지원 하도록 새 DNS 인프라를 디자인 하 고 배포 해야 합니다. 자세한 내용은 [DNS (Domain Name System) 배포](https://go.microsoft.com/fwlink/?LinkId=93656)를 참조 하세요.  
  
조직에 기존 DNS 인프라가 있는 경우 DNS 인프라가 Active Directory 네임 스페이스와 상호 작용 하는 방식을 이해 해야 합니다. 기존 DNS 인프라 디자인을 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://go.microsoft.com/fwlink/?LinkID=102558) 에서 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고 "DNS 인벤토리" (DSSLOGI_8)를 엽니다.  
  
> [!NOTE]  
> IPv4 (IP 버전 4) 주소 외에도 Windows Server는 IPv6 (IP 버전 6) 주소도 지원 합니다. 현재 DNS 구조의 재귀 이름 확인 방법을 문서화 하는 동안 IPv6 주소를 나열 하는 데 도움이 되는 워크시트의 경우 [부록 a: DNS 인벤토리](../../ad-ds/plan/Appendix-A--DNS-Inventory.md)를 참조 하세요.
  
AD DS를 지원 하도록 DNS 인프라를 디자인 하기 전에 dns 계층, DNS 이름 확인 프로세스 및 DNS가 AD DS를 지 원하는 방법을 확인 하는 것이 도움이 될 수 있습니다. DNS 계층 구조 및 이름 확인 프로세스에 대 한 자세한 내용은 DNS 기술 참조 ([https://go.microsoft.com/fwlink/?LinkID=48145](https://go.microsoft.com/fwlink/?LinkID=48145))를 참조 하십시오. DNS에서 AD DS를 지 원하는 방법에 대 한 자세한 내용은 Active Directory 기술 참조에 대 한 DNS 지원 ([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147))을 참조 하십시오.  
  
## <a name="in-this-section"></a>단원 내용  

- [DNS 개념 검토](../../ad-ds/plan/Reviewing-DNS-Concepts.md)  
- [DNS 및 AD DS](../../ad-ds/plan/DNS-and-AD-DS.md)  
- [AD DS 소유자 역할에 대한 DNS 할당](../../ad-ds/deploy/Assigning-the-DNS-for-AD-DS-Owner-Role.md)  
- [기존 DNS 인프라에 AD DS 통합](../../ad-ds/plan/../../ad-ds/plan/Integrating-AD-DS-into-an-Existing-DNS-Infrastructure.md)  
