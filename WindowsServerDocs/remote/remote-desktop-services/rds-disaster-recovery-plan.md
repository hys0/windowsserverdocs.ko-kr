---
title: 재해 복구 계획 만들기
description: RDS 배포에 대한 재해 복구 계획을 만드는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e4e9a9ab05e672c72925e3699900218abdf1c682
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404022"
---
# <a name="create-your-disaster-recovery-plan-for-rds"></a>RDS에 대한 재해 복구 계획 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

Azure Site Recovery에서 장애 조치(failover) 프로세스를 자동화하기 위한 재해 복구 계획을 만들 수 있습니다. 복구 계획에 모든 RDS 구성 요소 VM을 추가합니다.

Azure에서 복구 계획을 만들려면 다음 단계를 사용합니다.

1. Azure Portal에서 Azure Site Recovery 자격 증명 모음을 열고 **복구 계획**을 클릭합니다.
2. **만들기**를 클릭하고 계획의 이름을 입력합니다.
3. **원본** 및  **대상**을 선택합니다. 대상은 보조 RDS 사이트 또는 Azure입니다.
4. RDS 구성 요소를 호스트하는 VM을 선택하고 **확인**을 클릭합니다.

다음 섹션에서는 다양한 유형의 RDS 배포에 대해 복구 계획을 만드는 방법에 대한 추가 정보를 제공합니다.

## <a name="sessions-based-rds-deployment"></a>세션 기반 RDS 배포

RDS 세션 기반 배포의 경우는 다음 순서대로 표시되므로 VM을 그룹화합니다.

1. 장애 조치(failover) 그룹 1 - 세션 호스트 VM
2. 장애 조치(failover) 그룹 2 - 연결 브로커 VM
3. 장애 조치(failover) 그룹 3 - 웹 액세스 VM

해당 계획은 다음과 같이 표시됩니다. 

![세션 기반 RDS 배포에 대한 재해 복구 계획](media/rds-asr-session-drplan.png)

## <a name="pooled-desktops-rds-deployment"></a>풀링된 데스크톱 RDS 배포

풀링된 데스크톱을 사용하는 RDS 배포에서 순서대로 표시되도록 VM을 그룹화하고 수동 단계 및 스크립트를 추가합니다.

1. 장애 조치(failover) 그룹 1 - RDS 연결 브로커 VM
2. 그룹 1 수동 작업 - DNS 업데이트

   연결 브로커 VM에서 관리자 권한 모드로 PowerShell을 실행합니다. 다음 명령을 실행하고 몇 분 정도 기다렸다가 DNS가 새 값으로 업데이트되었는지 확인합니다.

   ```
   ipconfig /registerdns
   ```
3. 그룹 1 스크립트 - 가상화 호스트 추가

   클라우드의 각 가상화 호스트에 대해 실행되도록 아래 스크립트를 수정합니다. 일반적으로 연결 브로커에 가상화 호스트를 추가한 후 호스트를 다시 시작해야 합니다. 스크립트 실행 전에 호스트에 대기 중인 재부팅이 없도록 합니다. 대기 중인 재부팅이 있으면 실패합니다.

   ```
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. 장애 조치(failover) 그룹 2 - 템플릿 VM
5. 그룹 2 스크립트 1 - 템플릿 VM 끄기
   
   보조 사이트로 복구된 경우 템플릿 VM이 시작되지만, sysprep이 실행된 VM으로, 완전히 시작되지 않을 수 있습니다. 또한 RDS에서 풀링된 VM 구성을 만들려면 VM을 종료해야 합니다. 따라서 VM을 꺼야 합니다. 단일 VMM 서버를 사용하는 경우 템플릿 VM 이름은 주 서버 및 보조 서버에서 동일합니다. 따라서 아래 스크립트의 *Context* 변수로 지정된 것처럼 VM ID를 사용합니다. 여러 템플릿이 있는 경우 모두 끕니다.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. 그룹 2 스크립트 2 - 풀링된 기존 VM 제거

   보조 사이트에서 새 VM을 만들 수 있도록 연결 브로커에서 기본 사이트의 풀링된 VM을 제거해야 합니다. 이 경우 풀링된 VM을 만들 정확한 호스트를 지정해야 합니다. 이 경우 해당 컬렉션에서만 VM이 삭제됩니다.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops; 
   Foreach($vm in $desktops){
      Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   ```
7. 그룹 2 수동 작업 - 새 템플릿 할당

   복구 사이트에서 풀링된 새 VM을 만들 수 있도록 컬렉션의 연결 브로커에 새 템플릿을 할당해야 합니다. RDS 연결 브로커로 이동한 후 컬렉션을 식별합니다. 속성을 편집하고 새 VM 이미지를 해당 템플릿으로 지정합니다.
8. 그룹 2 스크립트 3 - 풀링된 모든 VM 다시 만들기

   연결 브로커를 통해 복구 사이트에서 풀링된 VM을 다시 만듭니다. 이 경우 풀링된 VM을 만들 정확한 호스트를 지정해야 합니다.

   풀링된 VM 이름은 접두사와 접미사를 사용하여 고유하게 유지해야 합니다. VM 이름을 이미 있는 경우 스크립트가 실패합니다. 또한 기본쪽 VM이 1-5부터 번호가 매겨질 경우 복구 사이트 번호 매기기는 6부터 계속됩니다.

   ```powershell
   ipmo RemoteDesktop; 
   Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1} 
   ```
9. 장애 조치(failover) 그룹 3 - 웹 액세스 및 게이트웨이 서버 VM

복구 계획은 다음과 같습니다.

![풀링된 데스크톱을 사용하는 RDS 배포에 대한 재해 복구 계획](media/rds-asr-pooled-drplan.png)

## <a name="personal-desktops-rds-deployment"></a>개인 데스크톱 RDS 배포

개인 데스크톱을 사용하는 RDS 배포에서 순서대로 표시되도록 VM을 그룹화하고 수동 단계 및 스크립트를 추가합니다.

1. 장애 조치(failover) 그룹 1 - RDS 연결 브로커 VM
2. 그룹 1 수동 작업 - DNS 업데이트

   연결 브로커 VM에서 관리자 권한 모드로 PowerShell을 실행합니다. 다음 명령을 실행하고 몇 분 정도 기다렸다가 DNS가 새 값으로 업데이트되었는지 확인합니다.

   ```
   ipconfig /registerdns
   ```
3. 그룹 1 스크립트 - 가상화 호스트 추가
      
   클라우드의 각 가상화 호스트에 대해 실행되도록 아래 스크립트를 수정합니다. 일반적으로 연결 브로커에 가상화 호스트를 추가한 후 호스트를 다시 시작해야 합니다. 스크립트 실행 전에 호스트에 대기 중인 재부팅이 없도록 합니다. 대기 중인 재부팅이 있으면 실패합니다.

   ```powershell
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. 장애 조치(failover) 그룹 2 - 템플릿 VM
5. 그룹 2 스크립트 1 - 템플릿 VM 끄기
   
   보조 사이트로 복구된 경우 템플릿 VM이 시작되지만, sysprep이 실행된 VM으로, 완전히 시작되지 않을 수 있습니다. 또한 RDS에서 풀링된 VM 구성을 만들려면 VM을 종료해야 합니다. 따라서 VM을 꺼야 합니다. 단일 VMM 서버를 사용하는 경우 템플릿 VM 이름은 주 서버 및 보조 서버에서 동일합니다. 따라서 아래 스크립트의 *Context* 변수로 지정된 것처럼 VM ID를 사용합니다. 여러 템플릿이 있는 경우 모두 끕니다.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. 장애 조치(failover) 그룹 3 - 개인 VM
7. 그룹 3 스크립트 1 - 기존 개인 VM을 제거한 후 추가

   보조 사이트에서 새 VM을 만들 수 있도록 연결 브로커에서 기본 사이트의 개인 VM을 제거합니다. VM의 할당을 추출하고 할당 해시를 사용하여 가상 머신을 연결 브로커에 다시 추가해야 합니다. 이렇게 하면 컬렉션에서 개인 VM만 제거되었다가 다시 추가됩니다. 개인 데스크톱 할당을 내보낸 후 컬렉션으로 다시 가져옵니다.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName CEODesktops; 
   Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 

   Foreach($vm in $desktops){
     Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   
   Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 
   ```
8. 장애 조치(failover) 그룹 3 - 웹 액세스 및 게이트웨이 서버 VM

해당 계획은 다음과 같이 표시됩니다. 

![개인 데스크톱 RDS 배포에 대한 재해 복구 계획](media/rds-asr-personal-desktops-drplan.png)
