---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: 가상화된 도메인 컨트롤러 기술 참조 부록
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9e3a5cc2c71455bb040f1311bdbfed1ac7e213fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832234"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>가상화된 도메인 컨트롤러 기술 참조 부록

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에는 다음 내용이 포함됩니다.  
  
-   [용어](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [FixVDCPermissions.ps1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>용어  
  
-   **스냅숏** -특정 시점에서 가상 컴퓨터의 상태입니다. 이 가상화 플랫폼에 이전 스냅숏을 하드웨어에서 체인에 따라 달라 집니다.  
  
-   **복제** -완료 하 고 가상 머신의 복사본을 구분 합니다. 가상 하드웨어 (하이퍼바이저)에서 다릅니다.  
  
-   **전체 복제** -전체 클론을 복제 작업 후 부모 가상 머신과 없는 리소스를 공유 하는 가상 컴퓨터의 독립적인 복사본입니다. 진행 중인 작업의 전체 클론을는 부모 가상 컴퓨터와 완전히 별개입니다.  
  
-   **차이점 보관용 디스크** -지속적인 방식으로 부모 가상 머신과 가상 디스크를 공유 하는 가상 머신의 복사본입니다. 이 일반적으로 디스크 공간을 절약 하며 동일한 소프트웨어 설치를 사용 하도록 여러 가상 머신이 있습니다.  
  
-   **VM 복사**-파일의 모든 관련된 파일 시스템 복사 및 가상 컴퓨터의 폴더입니다.  
  
-   **VHD 파일 복사** -가상 머신의 VHD의 복사본  
  
-   **VM 생성 ID** -하이퍼바이저에서 가상 컴퓨터를 지정 하는 128 비트 정수입니다. 이 ID는 메모리에 저장 되 고 스냅숏이 적용 될 때마다 다시 설정 합니다. 가상 컴퓨터에 있는 Vm-generation ID를 표시 하는 것에 대 한 하이퍼바이저 독립적인 메커니즘을 사용 하는 디자인 합니다. Hyper-v 구현을 가상 머신의 ACPI 테이블의 ID를 표시합니다.  
  
-   **Import/Export** -사용자에 게는 전체 가상 컴퓨터 (VM, VHD 파일과 컴퓨터 구성)를 저장할 수 있도록 하는 Hyper-v 기능입니다. 그런 다음 다시 동일한 VM (복원)와 동일한 컴퓨터에서 컴퓨터를 파일 집합을 사용 하 여 사용자가 동일한 VM (이동) 또는 새 VM (복사)을 다른 컴퓨터에서 수 있습니다.  
  
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
  


