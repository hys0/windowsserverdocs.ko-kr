---
title: 재해 복구 계획 만들기
description: RDS 배포에 대 한 재해 복구 계획을 만드는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 8ad759a73e4a0ce1dc28f2b8e8d80f4365895430
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879504"
---
# <a name="create-your-disaster-recovery-plan-for-rds"></a>RDS에 대 한 재해 복구 계획 만들기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

장애 조치 프로세스를 자동화 하려면 Azure Site Recovery에서 재해 복구 계획을 만들 수 있습니다. 복구 계획에 모든 RDS 구성 요소 Vm을 추가 합니다.

Azure에서 복구 계획을 만들려면 다음 단계를 사용 합니다.

1. Azure portal에서 Azure Site Recovery 자격 증명 모음을 열고 클릭 **복구 계획**합니다.
2. 클릭 **만들기** 계획에 대 한 이름을 입력 합니다.
3. 선택 하면 **원본** 하 고 **대상**합니다. 대상이 보조 RDS 사이트 또는 Azure입니다.
4. Vm에 RDS 구성 요소를 호스트 하 고 클릭을 선택 **확인**합니다.

다음 섹션에서는 다양 한 유형의 RDS 배포에 대 한 복구 계획 만들기에 대 한 추가 정보를 제공 합니다.

## <a name="sessions-based-rds-deployment"></a>세션 기반 RDS 배포

RDS 세션 기반 배포의 경우는 순서 대로 표시 되므로 Vm 그룹:

1. 장애 조치 그룹 1-세션 호스트 VM
2. 장애 조치 그룹 2-연결 브로커 VM
3. 장애 조치 그룹 3-웹 액세스 VM

계획은 다음과 같이 표시 됩니다. 

![세션 기반 RDS 배포에 대 한 재해 복구 계획](media/rds-asr-session-drplan.png)

## <a name="pooled-desktops-rds-deployment"></a>풀링된 데스크톱 RDS 배포

풀링된 데스크톱을 사용 하 여 RDS 배포를 스크립트 및 수동 단계를 추가 하는 시퀀스에서 있도록 Vm을 그룹화 합니다.

1. 장애 조치 그룹 1-RDS 연결 브로커 VM
2. 수동 작업 1-업데이트 DNS 그룹

   연결 브로커 VM에서 관리자 권한 모드에서 PowerShell을 실행 합니다. 다음 명령을 실행 하 고 몇 분 DNS가 새 값으로 업데이트 되었는지 확인 될 때까지 기다립니다.

   ```
   ipconfig /registerdns
   ```
3. 가상화 호스트를 추가 1 스크립트-그룹

   클라우드의 각 가상화 호스트에 대해 실행 하도록 아래 스크립트를 수정 합니다. 일반적으로 연결 브로커에 가상화 호스트를 추가한 후 호스트를 다시 시작 해야 합니다. 호스트 스크립트 실행 되기 전에 대기 중인 재부팅이 없는 합니다. 그러지 않으면 실패를 확인 합니다.

   ```
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. 장애 조치 그룹 2-템플릿 VM
5. 템플릿 VM 해제 그룹 2 스크립트 1-설정
   
   템플릿 VM을 보조 사이트로 복구 하는 경우, 시작 되지만 VM sysprep가 적용 된 되 고 완전히 시작할 수 없습니다. 또한 RDS VM에서 풀링된 VM 구성을 만들려면 종료 되도록 필요 합니다. 따라서 해제 해야 합니다. 단일 VMM 서버를 사용 하는 경우 템플릿 VM 이름은 주 서버에서 동일 하 고 보조 복제본입니다. 따라서 지정 된 대로 VM ID를 사용 합니다 *상황에 맞는* 아래 스크립트에서 변수입니다. 여러 서식 파일에 있는 경우 설정을 모두 해제 합니다.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. 2 스크립트 2 그룹-기존 풀링된 Vm 제거

   보조 사이트에서 새 Vm을 만들 수 있도록 연결 브로커에서 기본 사이트에서 풀링된 Vm을 제거 해야 합니다. 이 경우 풀링된 VM을 만드는 정확한 호스트를 지정 해야 합니다. Vm만 컬렉션에서 삭제 됩니다는 note 합니다.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName Win8Desktops; 
   Foreach($vm in $desktops){
      Remove-RDVirtualDesktopFromCollection -CollectionName Win8Desktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   ```
7. 새 템플릿 할당-그룹 2 수동 작업

   복구 사이트에서 새 풀링된 Vm을 만들 수 있도록 새 템플릿 컬렉션에 대 한 연결 브로커에 할당 해야 합니다. RDS 연결 브로커 이동한 컬렉션을 식별 합니다. 속성을 편집 하 고 해당 템플릿으로 새 VM 이미지를 지정 합니다.
8. 2 스크립트 3 그룹-모든 풀링된 Vm를 다시 만듭니다.

   풀링된 Vm을 연결 브로커를 통해 복구 사이트에서 다시 만듭니다. 이 경우 풀링된 VM을 만드는 정확한 호스트를 지정 해야 합니다.

   풀링된 VM 이름 접두사와 접미사를 사용 하 여 고유 해야 합니다. VM 이름을 이미 있는 경우에 스크립트가 실패 합니다. 또한 기본 측 Vm 1-5에서 매깁니다 복구 사이트 번호 매기기 계속 6에서 됩니다.

   ```powershell
   ipmo RemoteDesktop; 
   Add-RDVirtualDesktopToCollection -CollectionName Win8Desktops -VirtualDesktopAllocation @{"RDVH1.contoso.com" = 1} 
   ```
9. 장애 조치 그룹 3-웹 액세스 및 게이트웨이 서버 VM

복구 계획은 다음과 같습니다.

![풀링된 데스크톱을 사용 하 여 RDS 배포에 대 한 재해 복구 계획](media/rds-asr-pooled-drplan.png)

## <a name="personal-desktops-rds-deployment"></a>개인 데스크톱 RDS 배포

개인 데스크톱을 사용 하 여 RDS 배포를 스크립트 및 수동 단계를 추가 하는 시퀀스에서 있도록 Vm을 그룹화 합니다.

1. 장애 조치 그룹 1-RDS 연결 브로커 VM
2. 수동 작업 1-업데이트 DNS 그룹

   연결 브로커 VM에서 관리자 권한 모드에서 PowerShell을 실행 합니다. 다음 명령을 실행 하 고 몇 분 DNS가 새 값으로 업데이트 되었는지 확인 될 때까지 기다립니다.

   ```
   ipconfig /registerdns
   ```
3. 가상화 호스트를 추가 1 스크립트-그룹
      
   클라우드의 각 가상화 호스트에 대해 실행 하도록 아래 스크립트를 수정 합니다. 일반적으로 연결 브로커에 가상화 호스트를 추가한 후 호스트를 다시 시작 해야 합니다. 호스트 스크립트 실행 되기 전에 대기 중인 재부팅이 없는 합니다. 그러지 않으면 실패를 확인 합니다.

   ```powershell
   Broker - broker.contoso.com
   Virtualization host - VH1.contoso.com

   ipmo RemoteDesktop; 
   add-rdserver –ConnectionBroker broker.contoso.com –Role RDS-VIRTUALIZATION –Server VH1.contoso.com 
   ```
4. 장애 조치 그룹 2-템플릿 VM
5. 템플릿 VM 해제 그룹 2 스크립트 1-설정
   
   템플릿 VM을 보조 사이트로 복구 하는 경우, 시작 되지만 VM sysprep가 적용 된 되 고 완전히 시작할 수 없습니다. 또한 RDS VM에서 풀링된 VM 구성을 만들려면 종료 되도록 필요 합니다. 따라서 해제 해야 합니다. 단일 VMM 서버를 사용 하는 경우 템플릿 VM 이름은 주 서버에서 동일 하 고 보조 복제본입니다. 따라서 지정 된 대로 VM ID를 사용 합니다 *상황에 맞는* 아래 스크립트에서 변수입니다. 여러 서식 파일에 있는 경우 설정을 모두 해제 합니다.

   ```powershell
   ipmo virtualmachinemanager; 
   Foreach($vm in $VMsAsTemplate)
   {
      Get-SCVirtualMachine -ID $vm | Stop-SCVirtualMachine –Force
   } 
   ```
6. 장애 조치 그룹 3-개인 Vm
7. 3 스크립트 1를 그룹화-기존 개인 Vm을 제거 하 고, 이러한 추가

   보조 사이트에서 새 Vm을 만들 수 있도록 연결 브로커에서 기본 사이트의 개인 Vm을 제거 합니다. Vm의 할당을 추출 하 고 가상 머신을 할당의 해시를 사용 하 여 연결 브로커에 다시 추가 해야 합니다. 이 개인 Vm 컬렉션에서 제거를 다시 추가 합니다. 개인 데스크톱 할당을 내보내고 컬렉션으로 다시 가져올 수 됩니다.

   ```powershell
   ipmo RemoteDesktop
   $desktops = Get-RDVirtualDesktop -CollectionName CEODesktops; 
   Export-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 

   Foreach($vm in $desktops){
     Remove-RDVirtualDesktopFromCollection -CollectionName CEODesktops -VirtualDesktopName $vm.VirtualDesktopName –Force
   }
   
   Import-RDPersonalVirtualDesktopAssignment -CollectionName CEODesktops -Path ./Desktopallocations.txt -ConnectionBroker broker.contoso.com 
   ```
8. 장애 조치 그룹 3-웹 액세스 및 게이트웨이 서버 VM

계획은 다음과 같이 표시 됩니다. 

![개인 데스크톱 RDS 배포에 대 한 재해 복구 계획](media/rds-asr-personal-desktops-drplan.png)
