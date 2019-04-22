---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Active Directory 보안에 대한 모범 사례
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 972def668634e794908a3ff2933d038ae38be5d6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817084"
---
# <a name="best-practices-for-securing-active-directory"></a>Active Directory 보안에 대한 모범 사례

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 문서는 전문가 관점을 제공 하 고 IT 임원이 엔터프라이즈 Active Directory 환경을 보호 하는 데 도움이 되는 실용적인 기술 집합을 포함 합니다. Active Directory는 IT 인프라에서 중요한 역할을 담당하며, 상호 연결된 글로벌 환경에서 다양한 네트워크 리소스의 보안 및 조화를 보장합니다. 설명 하는 방법을 기반으로 주로 Microsoft IT 및 기타 Microsoft 사업부, 조언 하는 것 외에도 자산을 보호 하는 것에 대 한 책임은 Microsoft 정보 보안 및 위험 관리 (ISRM) 조직의 경험을 Microsoft 글로벌 500 고객이 선택한 횟수입니다.  
  
-   [요약](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [소개](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [손상될 작업 환경](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [자격 증명 도난에 대 한 매력적인 계정](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Active Directory 공격 노출 영역 감소](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [최소 권한 관리 모델 구현](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [보안 관리 호스트 구현](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [공격 으로부터 도메인 컨트롤러 보호](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [손상 징후에 대 한 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [감사 정책 권장 사항](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [더 안전한 환경 유지 관리](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [부록](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [부록 b: 권한 있는 계정 및 Active Directory의 그룹](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [부록 c: 보호 된 계정 및 Active Directory의 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [부록 d: Active Directory에서 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [부록 e: Active Directory의 Enterprise Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [부록 f: Active Directory에서 Domain Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [부록 g: Active Directory에서 관리자 그룹의 보안 설정](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [부록 h: 로컬 관리자 계정 및 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [부록 i: 보호 된 계정 및 Active Directory에서 그룹에 대 한 계정 관리](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [부록 l: 모니터링할 이벤트](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [부록 m: 문서 링크 및 읽어보면 좋은 자료](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


