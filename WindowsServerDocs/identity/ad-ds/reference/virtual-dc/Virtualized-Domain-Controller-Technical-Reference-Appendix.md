---
ms.assetid: 73a4deba-7da6-4eae-8fdd-2a4d369f9cbb
title: 가상화된 도메인 컨트롤러 기술 참조 부록
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e1018d5bbff5922df5a696e5c4fad12dc9f6ec3d
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323135"
---
# <a name="virtualized-domain-controller-technical-reference-appendix"></a>가상화된 도메인 컨트롤러 기술 참조 부록

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에는 다음 내용이 포함됩니다.  
  
-   [용어](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_Terms)  
  
-   [FixVDCPermissions. p s 1](../../../ad-ds/reference/virtual-dc/../../../ad-ds/reference/virtual-dc/Virtualized-Domain-Controller-Technical-Reference-Appendix.md#BKMK_FixPDCPerms)  
  
## <a name="BKMK_Terms"></a>기술  
  
-   **스냅숏** -특정 시점에 있는 가상 컴퓨터의 상태입니다. 이는 사용 된 이전 스냅숏의 체인, 하드웨어 및 가상화 플랫폼에 따라 달라 집니다.  
  
-   **복제** -가상 컴퓨터의 전체 및 개별 복사본입니다. 가상 하드웨어 (하이퍼바이저)에 따라 달라 집니다.  
  
-   **전체 복제** -전체 클론은 복제 작업 후에 부모 가상 머신과 리소스를 공유 하지 않는 가상 머신의 독립적인 복사본입니다. 전체 클론의 진행 중인 작업은 부모 가상 머신과 완전히 분리 됩니다.  
  
-   **차이점 보관용 디스크** -가상 디스크를 부모 가상 머신과 지속적으로 공유 하는 가상 머신의 복사본입니다. 일반적으로 디스크 공간을 절약 하 고 여러 가상 컴퓨터에서 동일한 소프트웨어 설치를 사용할 수 있습니다.  
  
-   **VM 복사**-가상 컴퓨터의 모든 관련 파일 및 폴더에 대 한 파일 시스템 복사본입니다.  
  
-   **Vhd 파일 복사** -가상 컴퓨터의 vhd 복사본  
  
-   **VM 생성 ID** -하이퍼바이저에 의해 가상 머신에 지정 된 128 비트 정수입니다. 이 ID는 메모리에 저장 되며 스냅숏이 적용 될 때마다 다시 설정 됩니다. 이 디자인에서는 가상 머신에서 VM 생성 ID를 인식 하기 위해 하이퍼바이저와 무관 한 메커니즘을 사용 합니다. Hyper-v 구현은 가상 컴퓨터의 ACPI 테이블에 ID를 제공 합니다.  
  
-   **가져오기/내보내기** -사용자가 전체 가상 컴퓨터 (VM 파일, VHD 및 컴퓨터 구성)를 저장할 수 있도록 하는 hyper-v 기능입니다. 그런 다음 사용자가 해당 파일 집합을 사용 하 여 동일한 VM (복원)과 동일한 컴퓨터에서 동일한 VM (이동) 또는 새 VM (복사)로 컴퓨터를 다시 가져올 수 있습니다.  
  
## <a name="BKMK_FixPDCPerms"></a>FixVDCPermissions. p s 1  
  
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
  


