---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: "모범 사례에 대 한 Active Directory 보안"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ecef0c173677d379524189b1769d4721ab0774a8
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="best-practices-for-securing-active-directory"></a>모범 사례에 대 한 Active Directory 보안

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 문서는 담당자 관점 제공 하며 IT 임원 엔터프라이즈 Active Directory 환경 보호를 위해 실질적인 기술 집합을 포함 합니다. Active Directory IT 인프라에 중요 한 역할 및 조화 및 보안 글로벌, 연결 된 환경에서 다양 한 네트워크 리소스에 설치할 수 있도록 보장 합니다. 방법에 수시로 이야기는 Microsoft IT 및 Microsoft의 글로벌 500 고객의 선택한 번호 조심 뿐만 아니라 다른 Microsoft 비즈니스 부서 자산 보호에 대 한 책임은 Microsoft의 보안 정보 및 위험 관리 (ISRM) 조직 경험을 주로 기반으로 합니다.  
  
-   [Foreword](https://technet.microsoft.com/library/dn487451.aspx)  
  
-   [승인](https://technet.microsoft.com/library/dn487445.aspx)  
  
-   [요약](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [소개](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [손상 수단](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [매력적인 계정 자격 증명 도용의](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Active Directory 공격 줄이기](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [최소 권한 관리 모델을 구현합니다.](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [안전 하 게 관리 호스트 구현](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [도메인 컨트롤러 공격 으로부터 보호합니다.](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [침입 Active Directory를 모니터링합니다.](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [정책 추천 감사 합니다.](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [손상에 대 한 계획](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [더 많은 보안 환경을 유지](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [부록](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [부록 b: 권한이 있는 계정 및 그룹 Active Directory에](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [부록 c: 보호 계정과 그룹 Active Directory에](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [부록 d: Active Directory에 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [부록 e: Active Directory에 관리자 그룹 엔터프라이즈 보안](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [부록 f: 도메인 관리자 그룹 Active Directory에 고정](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [부록 g: 관리자가 그룹 Active Directory에 고정](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [로컬 관리자 계정 및 그룹 부록 h: 보안](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [부록 i: 보호 계정과 Active Directory에 있는 그룹에 대 한 계정을 만들 관리](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [모니터에 부록 l: 이벤트](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [부록 m: 링크 문서 및 권장 읽기](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


