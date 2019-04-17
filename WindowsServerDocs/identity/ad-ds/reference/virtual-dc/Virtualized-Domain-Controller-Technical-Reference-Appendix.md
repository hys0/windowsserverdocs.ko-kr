---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: "가상화 도메인 컨트롤러 기술 참조 부록"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2e7f264a098b6f67d98c9aa47ec5794374b8920d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>가상화 도메인 컨트롤러 기술 참조 부록

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에 설명 합니다.  
  
-   [용어](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>용어  
  
-   **스냅숏을** -특정 시점에서 가상 컴퓨터의 상태입니다. 이전 스냅샷이의 하드웨어, 체인 켜고 virtualization 플랫폼에 따라 달라 집니다.  
  
-   **복제** -을 완료 하 고 가상 컴퓨터의 복사본을 분리 합니다. (하이퍼바이저) 가상 하드웨어에 따라 달라 집니다.  
  
-   **전체 복제** -전체 복제본 한 별도 복제 작업 후 리소스가 부모 가상 컴퓨터를 공유 하 여 가상 컴퓨터의 복사본입니다. 전체 복제본의 진행 중인 작업은 전적으로 부모 가상 컴퓨터 다릅니다.  
  
-   **보관용 디스크** -지속적인 방식으로 가상 디스크 부모 가상 컴퓨터를 공유 하 여 가상 컴퓨터의 복사본입니다. 이 일반적으로 디스크 공간을 절약와 동일한 소프트웨어 설치를 사용 하 여 여러 가상 컴퓨터 수 있게 합니다.  
  
-   **VM 복사**-한 파일 관련 된 모든 파일의 시스템 복사 및 폴더 가상 컴퓨터의 합니다.  
  
-   **VHD 파일 복사** -가상 컴퓨터의 VHD의 복사본을  
  
-   **VM 세대 ID** -하이퍼바이저 가상 컴퓨터에 제공한 128-bit 정수 합니다. 이 ID 메모리에 저장 되 고 스냅숏을 적용 될 때마다 다시 설정 합니다. 디자인 가상 컴퓨터에서 VM 세대 ID 나타나는 하이퍼바이저를 알 수 없는 장치를 사용 합니다. Hyper-v 구현 가상 컴퓨터의 ACPI 표에 ID를 제공합니다.  
  
-   **내보내기** -사용자에 게 전체 가상 컴퓨터 (VM 파일, VHD 및 컴퓨터 구성)를 저장할 수 있도록 해 주는 A Hyper-v 기능입니다. 동일한 VM (이동) 또는 새 VM (복사)와 다른 컴퓨터에서 시스템 동일한 VM (복원)와 동일한 컴퓨터에 다시 가져올 수 해당 파일의 집합을 사용 하 여 사용자가 다음 허용  
  
## <a name="BKMK_FixPDCPerms"></a>FixVDCPermissions.ps1  
  
```  
# Unsigned script, requires use of set-executionpolicy remotesigned -force  
# You must run the Windows PowerShell console as an elevated administrator  
  
# Load Active Directory Windows PowerShell Module and switch to AD DS drive  
import-module activedirectory  
cd ad:  
  
## Get Domain NC  
$domainNC = get-addomain  
  
## Get groups and obtain their SIDs   
$dcgroup = get-adgroup "Cloneable Domain Controllers"  
  
$sid1 = (get-adgroup $dcgroup).sid  
  
## Get the DACL of the domain  
$acl = get-acl $domainNC  
  
## The following object specific ACE grants extended right 'Allow a DC to create a clone of itself' for the CDC group to the Domain NC  
## 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e is the schemaIDGuid for 'DS-Clone-Domain-Controller"  
  
$objectguid = new-object Guid 3e0f7e18-2c7a-4c10-ba82-4d926db99a3e  
$ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid1,"ExtendedRight","Allow",$objectguid  
  
## Add the ACE in the ACL and set the ACL on the object   
  
$acl.AddAccessRule($ace1)  
set-acl -aclobject $acl $domainNC  
write-host "Done writing new VDC permissions."  
cd c:   
```  
  


