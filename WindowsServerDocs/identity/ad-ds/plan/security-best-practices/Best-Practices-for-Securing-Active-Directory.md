---
ms.assetid: e2651dc8-4b31-4cd8-a400-3b8123890210
title: Active Directory 보안에 대한 모범 사례
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 0d6f4abbf5dd071a2e229acbda2057c1f81851e6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408623"
---
# <a name="best-practices-for-securing-active-directory"></a>Active Directory 보안에 대한 모범 사례

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 문서에서는 전문가의 관점을 제공 하며 IT 담당자가 엔터프라이즈 Active Directory 환경을 보호 하는 데 도움이 되는 실용적인 기술 집합을 제공 합니다. Active Directory는 IT 인프라에서 중요한 역할을 담당하며, 상호 연결된 글로벌 환경에서 다양한 네트워크 리소스의 보안 및 조화를 보장합니다. 설명 된 방법은 microsoft IT 및 기타 Microsoft 사업부의 자산을 보호 하는 것 외에도 microsoft의 ISRM (정보 보안 및 위험 관리) 조직의 경험을 기반으로 합니다. 선택한 수의 Microsoft Global 500 고객 수입니다.  
  
-   [요약](../../../ad-ds/manage/component-updates/Executive-Summary.md)  
  
-   [소개](../../../ad-ds/manage/component-updates/Introduction.md)  
  
-   [손상될 작업 환경](../../../ad-ds/plan/security-best-practices/Avenues-to-Compromise.md)  
  
-   [자격 증명 도난에 취약한 계정](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md)  
  
-   [Active Directory 공격 노출 영역 축소](../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md)  
  
-   [최소 권한 관리 모델 구현](../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md)  
  
-   [보안 관리 호스트 구현](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)  
  
-   [공격 으로부터 도메인 컨트롤러 보안](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md)  
  
-   [손상의 징후가 Active Directory 모니터링](../../../ad-ds/plan/security-best-practices/Monitoring-Active-Directory-for-Signs-of-Compromise.md)  
  
-   [감사 정책 권장 사항](../../../ad-ds/plan/security-best-practices/Audit-Policy-Recommendations.md)  
  
-   [손상 계획](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)  
  
-   [보다 안전한 환경 유지 관리](../../../ad-ds/plan/security-best-practices/Maintaining-a-More-Secure-Environment.md)  
  
-   [부록](../../../ad-ds/plan/security-best-practices/Appendices.md)  
   
-   [부록 B: Active Directory의 권한 있는 계정 및 그룹](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [부록 C: Active Directory의 보호된 계정 및 그룹](../../../ad-ds/plan/security-best-practices/Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md)  
  
-   [부록 D: Active Directory의 기본 제공 관리자 계정 보안](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md)  
  
-   [부록 E: Active Directory의 Enterprise Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md)  
  
-   [부록 F: Active Directory의 Domain Admins 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md)  
  
-   [부록 G: Active Directory에서 관리자 그룹의 보안 설정](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md)  
  
-   [부록 H: 로컬 관리자 계정 및 그룹 보안](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md)  
  
-   [부록 I: Active Directory의 보호된 계정 및 그룹에 대한 관리 계정 만들기](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md)   
  
-   [부록 L: 모니터링할 이벤트](../../../ad-ds/plan/Appendix-L--Events-to-Monitor.md)  
  
-   [부록 M: 문서 링크 및 권장 자료](../../../ad-ds/manage/Appendix-M--Document-Links-and-Recommended-Reading.md)  
  


