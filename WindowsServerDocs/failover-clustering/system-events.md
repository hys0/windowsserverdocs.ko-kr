---
title: 장애 조치 (Failover) 클러스터링 시스템 로그 이벤트
description: Windows Server 시스템 로그의 장애 조치 (Failover) 클러스터링 이벤트 목록입니다. 이러한 이벤트를 사용 하 여 클러스터 문제를 해결할 수 있습니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 01/14/2020
ms.openlocfilehash: 24be2b39c8130b97d22ee182c0064986b3378549
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472980"
---
# <a name="failover-clustering-system-log-events"></a>장애 조치 (Failover) 클러스터링 시스템 로그 이벤트

> 적용 대상: Windows Server 2019, Windows Server 2016

이 항목에서는 Windows Server 시스템 로그 (이벤트 뷰어에서 볼 수 있음)의 장애 조치 (Failover) 클러스터링 이벤트를 나열 합니다. 이러한 이벤트는 모두 **FailoverClustering** 의 이벤트 원본을 공유 하며 클러스터 문제를 해결할 때 유용할 수 있습니다.

## <a name="critical-events"></a>중요 이벤트

### <a name="event-1000-unexpected_fatal_error"></a>이벤트 1000: UNEXPECTED_FATAL_ERROR

원본 모듈 %2의 줄 %1에서 예기치 않은 오류가 발생 했습니다. 클러스터 서비스 오류 코드는 %3입니다.

### <a name="event-1001-assertion_failure"></a>이벤트 1001: ASSERTION_FAILURE

클러스터 서비스 원본 모듈 %2의 줄 %1에 대 한 유효성 검사에 실패 했습니다. ' %3 '

### <a name="event-1006-nm_event_membership_halt"></a>이벤트 1006: NM_EVENT_MEMBERSHIP_HALT

다른 클러스터 노드와의 불완전 한 연결로 인해 클러스터 서비스 중단 되었습니다.

### <a name="event-1057-dm_database_corrupt_or_missing"></a>이벤트 1057: DM_DATABASE_CORRUPT_OR_MISSING

클러스터 데이터베이스를 로드할 수 없습니다. 파일이 없거나 손상 되었을 수 있습니다.
자동 복구를 시도할 수 있습니다.

### <a name="event-1070-nm_event_begin_join_failed"></a>이벤트 1070: NM_EVENT_BEGIN_JOIN_FAILED

노드는 오류 코드 ' %2 ' (으)로 인해 장애 조치 (failover) 클러스터 ' %1 '에 가입 하지 못했습니다.

### <a name="event-1073-cs_event_inconsistency_halt"></a>이벤트 1073: CS_EVENT_INCONSISTENCY_HALT

장애 조치 (failover) 클러스터 내에서 불일치를 방지 하기 위해 클러스터 서비스 중단 되었습니다. 오류 코드는 ' %1 '입니다.

### <a name="event-1080-cs_diskwrite_failure"></a>이벤트 1080: CS_DISKWRITE_FAILURE

클러스터 서비스에서 클러스터 데이터베이스를 업데이트 하지 못했습니다 (오류 코드 ' %1 ').
디스크 공간이 부족 하거나 파일 시스템 손상이 원인일 수 있습니다.

### <a name="event-1090-cs_event_reg_operation_failed"></a>이벤트 1090: CS_EVENT_REG_OPERATION_FAILED

클러스터 서비스를 시작할 수 없습니다. 오류 ' %1 ' (으)로 인해 Windows 레지스트리에서 구성 데이터를 읽지 못했습니다. 장애 조치 (Failover) 클러스터 관리 스냅인을 사용 하 여이 컴퓨터가 클러스터의 구성원 인지 확인 하세요.
기존 클러스터에이 컴퓨터를 추가 하려면 노드 추가 마법사를 사용 합니다. 또는이 컴퓨터가 클러스터의 멤버로 구성 된 경우 클러스터 서비스가 클러스터의 구성원 임을 식별 하는 데 필요한 누락 된 구성 데이터를 복원 해야 합니다.
구성 데이터를 복원 하기 위해이 컴퓨터의 시스템 상태 복원을 수행 합니다.

### <a name="event-1092-nm_event_mm_form_failed"></a>이벤트 1092: NM_EVENT_MM_FORM_FAILED

클러스터 ' %1 '을 (를) 구성 하지 못했습니다 (오류 코드 ' %2 '). 장애 조치 (Failover) 클러스터를 사용할 수 없습니다.

### <a name="event-1093-nm_event_node_not_member"></a>이벤트 1093: NM_EVENT_NODE_NOT_MEMBER

클러스터 서비스 ' %1 ' 노드를 ' %2 ' 장애 조치 (failover) 클러스터의 멤버로 식별할 수 없습니다. 이 노드의 컴퓨터 이름이 최근에 변경 된 경우 이전 이름으로 되돌리는 것이 좋습니다. 또는 장애 조치 (failover) 클러스터에 노드를 추가 하 고 필요한 경우 클러스터형 응용 프로그램을 다시 설치 합니다.

### <a name="event-1105-cs_event_rpc_init_failed"></a>이벤트 1105: CS_EVENT_RPC_INIT_FAILED

RPC 서비스에 인터페이스를 등록할 수 없어 클러스터 서비스를 시작 하지 못했습니다. 오류 코드는 ' %1 '입니다.

### <a name="event-1135-event_node_down"></a>이벤트 1135: EVENT_NODE_DOWN

클러스터 노드 ' %1 '이 (가) 활성 장애 조치 (failover) 클러스터 멤버 자격에서 제거 되었습니다. 이 노드의 클러스터 서비스 중지 되었을 수 있습니다. 이는 노드가 장애 조치 (failover) 클러스터의 다른 활성 노드와 통신이 끊어진 경우에도 발생할 수 있습니다.
구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면이 노드의 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1146-rcm_event_resmon_died"></a>이벤트 1146: RCM_EVENT_RESMON_DIED

클러스터 RHS(Resource Hosting Subsystem) (RHS) 프로세스가 종료 되었으며 다시 시작 됩니다. 이는 일반적으로 리소스의 클러스터 상태 검색 및 복구와 관련 되어 있습니다. 시스템 이벤트 로그를 참조 하 여 문제의 원인이 되는 리소스 및 리소스 DLL을 확인 하십시오.

### <a name="event-1177-mm_event_arbitration_failed"></a>이벤트 1177: MM_EVENT_ARBITRATION_FAILED

쿼럼이 손실 되어 클러스터 서비스를 종료 하 고 있습니다. 이는 클러스터의 일부 또는 모든 노드 또는 미러링 모니터 디스크의 장애 조치 (failover) 간 네트워크 연결이 끊어진 것일 수 있습니다.

구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1181-netres_resource_start_error"></a>이벤트 1181: NETRES_RESOURCE_START_ERROR

연결 된 서비스를 시작 하지 못했기 때문에 클러스터 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 서비스 반환 코드는 ' %2 '입니다. 서비스와 연결 된 추가 이벤트를 확인 하 고 서비스가 올바르게 시작 되는지 확인 하세요.

### <a name="event-1247-cluster_event_invalid_service_sid_type"></a>이벤트 1247: CLUSTER_EVENT_INVALID_SERVICE_SID_TYPE

클러스터 서비스에 대 한 SID (보안 식별자) 유형이 ' %1 ' (으)로 구성 되어 있지만 필요한 SID 유형은 ' 제한 없음 '입니다. 클러스터 서비스는 SCM (서비스 제어 관리자)을 사용 하 여 SID 유형 구성을 자동으로 수정 하 고이 변경 내용을 적용 하기 위해 다시 시작 됩니다.

### <a name="event-1248-cluster_event_service_sid_missing"></a>이벤트 1248: CLUSTER_EVENT_SERVICE_SID_MISSING

클러스터 서비스와 연결 된 보안 식별자 (SID) ' %1 '이 (가) 프로세스 토큰에 없습니다. 클러스터 서비스에서 자동으로이 문제를 해결 하 고 다시 시작 합니다.

### <a name="event-1282-sm_event_handshake_timeout"></a>이벤트 1282: SM_EVENT_HANDSHAKE_TIMEOUT

로컬 끝점과 원격 끝점 ' %2 ' 간의 보안 핸드셰이크가 ' %1 ' 초 내에 완료 되지 않았습니다. 노드가 연결을 종료 합니다.

### <a name="event-1542-service_prerestore_failed"></a>이벤트 1542: SERVICE_PRERESTORE_FAILED

클러스터 구성 데이터에 대 한 복원 요청이 실패 했습니다. 이 복원은 일반적으로 클러스터를 구성 하는 일부 노드가 현재 작동 하지 않음을 나타내는 ' 사전 복원 ' 단계 중에 실패 했습니다. 이 클러스터를 구성 하는 모든 노드에서 클러스터 서비스가 성공적으로 실행 되 고 있는지 확인 합니다.

### <a name="event-1543-service_postrestore_failed"></a>이벤트 1543: SERVICE_POSTRESTORE_FAILED

클러스터 구성 데이터의 복원 작업에 실패 했습니다. 이 복원은 일반적으로 클러스터를 구성 하는 일부 노드가 현재 작동 하지 않음을 나타내는 ' 복원 후 ' 단계 중에 실패 했습니다. 현재 클러스터 구성 데이터 파일 (ClusDB)을 ' %1 ' (으)로 바꾸는 것이 좋습니다.

### <a name="event-1546-service_form_version_incompatible"></a>이벤트 1546: SERVICE_FORM_VERSION_INCOMPATIBLE

노드 ' %1 '이 (가) 장애 조치 (failover) 클러스터를 형성 하지 못했습니다. 클러스터 서비스 소프트웨어의 호환 되지 않는 버전을 실행 하는 하나 이상의 노드가 원인일 수 있습니다. 클러스터의 노드 ' %1 ' 또는 다른 노드가 최근에 업그레이드 된 경우 모든 노드에서 호환 되는 클러스터 서비스 소프트웨어 버전을 실행 하 고 있는지 다시 확인 하세요.

### <a name="event-1547-service_connect_version_incompatible"></a>이벤트 1547: SERVICE_CONNECT_VERSION_INCOMPATIBLE

노드 ' %1 '이 (가) 장애 조치 (failover) 클러스터에 조인 하려고 했지만 클러스터 서비스 소프트웨어 버전 간의 비 호환성으로 인해 실패 했습니다. 클러스터의 노드 ' %1 ' 또는 다른 노드가 최근에 업그레이드 된 경우 다른 버전의 클러스터 서비스 소프트웨어로 변경 된 클러스터 배포가 지원 되는지 확인 하세요.

### <a name="event-1553-service_no_network_connectivity"></a>이벤트 1553: SERVICE_NO_NETWORK_CONNECTIVITY

이 클러스터 노드는 네트워크에 연결 되어 있지 않습니다. 연결이 복원 될 때까지 클러스터에 참여할 수 없습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1554-service_network_connectivity_lost"></a>이벤트 1554: SERVICE_NETWORK_CONNECTIVITY_LOST

이 클러스터 노드가 모든 네트워크 연결을 손실 했습니다. 연결이 복원 될 때까지 클러스터에 참여할 수 없습니다. 이 노드의 클러스터 서비스가 종료 됩니다.

### <a name="event-1556-service_unhandled_exception_in_worker_thread"></a>이벤트 1556: SERVICE_UNHANDLED_EXCEPTION_IN_WORKER_THREAD

클러스터 서비스에서 예기치 않은 문제가 발생 하 여 종료 됩니다. 오류 코드는 ' %2 '입니다.

### <a name="event-1561-service_nonstorage_witness_better_tag"></a>이벤트 1561: SERVICE_NONSTORAGE_WITNESS_BETTER_TAG

이 노드가 클러스터 구성 데이터의 최신 복사본을 포함 하지 않음을 감지 했으므로 클러스터 서비스를 시작 하지 못했습니다. 이 노드가 구성원 자격에 있지 않고 구성 데이터 업데이트를 받을 수 없어 클러스터에 대 한 변경 내용이 발생 했습니다.

#### <a name="guidance"></a>지침

클러스터의 모든 노드에서 클러스터 서비스를 시작 하 여 클러스터 구성 데이터의 최신 복사본을 포함 하는 노드가 먼저 클러스터를 구성할 수 있도록 합니다. 그러면이 노드는 클러스터에 가입할 수 있으며 업데이트 된 클러스터 구성 데이터를 자동으로 가져옵니다. 클러스터 구성 데이터의 최신 복사본에 사용할 수 있는 노드가 없으면 ' Start-clusternode-FQ ' Windows PowerShell cmdlet을 실행 합니다. FQ (클러스터가 forcequorum) 매개 변수를 사용 하 여 클러스터 서비스를 시작 하 고이 노드의 클러스터 구성 데이터 복사본을 신뢰할 수 있는 것으로 표시 합니다. 클러스터 데이터베이스의 오래 된 복사본을 사용 하 여 노드에 쿼럼을 강제 적용 하면 노드가 클러스터에 참가 하지 않는 동안 클러스터 구성 변경이 발생할 수 있습니다.

### <a name="event-1564-res_fsw_arbitratefailure"></a>이벤트 1564: RES_FSW_ARBITRATEFAILURE

파일 공유 감시 리소스 ' %1 '이 (가) 파일 공유 ' %2 '에 대해 중재 하지 못했습니다.
파일 공유 ' %2 '이 (가) 있고 클러스터에서 액세스할 수 있는지 확인 하세요.

### <a name="event-1570-service_connect_authentication_failure"></a>이벤트 1570: SERVICE_CONNECT_AUTHENTICATION_FAILURE

클러스터를 조인 하는 동안 ' %1 ' 노드에서 통신 세션을 설정 하지 못했습니다.
이는 인증 오류로 인 한 것입니다. 노드가 호환 되는 클러스터 서비스 소프트웨어 버전을 실행 하 고 있는지 확인 하세요.

### <a name="event-1571-service_connect_authorizaion_failure"></a>이벤트 1571: SERVICE_CONNECT_AUTHORIZAION_FAILURE

클러스터를 조인 하는 동안 ' %1 ' 노드에서 통신 세션을 설정 하지 못했습니다.
이것은 권한 부여 오류로 인 한 것입니다. 노드가 호환 되는 클러스터 서비스 소프트웨어 버전을 실행 하 고 있는지 확인 하세요.

### <a name="event-1572-service_netft_route_initial_failure"></a>이벤트 1572: SERVICE_NETFT_ROUTE_INITIAL_FAILURE

노드 ' %1 '이 (가) 다른 클러스터 노드와 함께 오류 검색 네트워크 메시지를 보내고 받을 수 없어서 클러스터에 참가 하지 못했습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 설정을 확인 하세요. 또한 Windows 방화벽의 장애 조치 (Failover) 클러스터 규칙을 확인 합니다.

### <a name="event-1574-dm_database_unload_failed"></a>이벤트 1574: DM_DATABASE_UNLOAD_FAILED

장애 조치 (failover) 클러스터 데이터베이스를 언로드할 수 없습니다. 클러스터 서비스를 다시 시작 해도 문제가 해결 되지 않으면 컴퓨터를 다시 시작 하십시오.

### <a name="event-1575-dm_database_corrupt_or_missing_fixquorum"></a>이벤트 1575: DM_DATABASE_CORRUPT_OR_MISSING_FIXQUORUM

이 노드의 클러스터 구성 데이터가 없거나 손상 되어 클러스터 서비스를 강제로 시작 하지 못했습니다. 클러스터 구성 데이터를 그대로 유지 하 고 유효한 복사본을 포함 하는 다른 노드에서 클러스터 서비스를 먼저 시작 하세요. 그런 다음이 노드에서 시작 작업을 다시 시도 합니다 (업데이트 된 유효한 구성 정보를 자동으로 가져오려고 함). 다른 노드를 사용할 수 없는 경우에는 WBAdmin을 사용 하 여 구성 데이터를 복원 하기 위해이 노드의 시스템 상태 복원을 수행 하십시오.

### <a name="event-1593-dm_could_not_discard_changes"></a>이벤트 1593: DM_COULD_NOT_DISCARD_CHANGES

장애 조치 (failover) 클러스터 데이터베이스를 언로드할 수 없으며 잠재적으로 잘못 된 메모리 변경을 삭제할 수 없습니다. 클러스터 서비스는 다른 클러스터 노드에서 데이터베이스를 검색 하 여 복구를 시도 합니다. 클러스터 서비스가 온라인 상태가 아닌 경우이 노드에서 클러스터 서비스를 다시 시작 합니다. 클러스터 서비스를 다시 시작 해도 문제가 해결 되지 않으면 컴퓨터를 다시 시작 하십시오. 다시 부팅 한 후 클러스터 서비스를 온라인 상태로 만들지 못한 경우 마지막 백업에서 클러스터 데이터베이스를 복원 하세요. 현재 데이터베이스가 ' %1 ' (으)로 복사 되었습니다. 사용할 수 있는 백업이 없으면 ' %1 '을 (를) ' %2 ' (으)로 복사 하 고 클러스터 서비스를 시작 해 보세요. 클러스터 서비스가이 노드에서 온라인 상태가 되 면 일부 클러스터 구성 변경 내용이 손실 되 고 클러스터가 제대로 작동 하지 않을 수 있습니다. 구성 유효성 검사 마법사를 실행 하 여 클러스터 구성을 확인 하 고 호스팅된 서비스 및 응용 프로그램이 온라인 상태이 고 제대로 작동 하는지 확인 합니다.

### <a name="event-1672-event_node_quarantined"></a>이벤트 1672: EVENT_NODE_QUARANTINED

클러스터 노드 ' %1 '이 (가) 격리 되었습니다. 노드에 짧은 시간 내에 ' %2 ' 개의 연속 오류가 발생 하 여 추가 중단을 방지 하기 위해 클러스터에서 제거 되었습니다. 노드가 ' %3 '까지 격리 된 후 노드가 자동으로 클러스터를 다시 조인 하려고 시도 합니다.

이 노드의 문제를 확인 하려면 시스템 및 응용 프로그램 이벤트 로그를 참조 하십시오. 문제가 해결 되 면 격리를 수동으로 지우면 노드가 ' Start-clusternode – ClearQuarantine ' Windows PowerShell cmdlet과 다시 가입할 수 있습니다.

노드 이름: %1

연속 된 클러스터 구성원 자격 수 손실: %2

시간 격리가 자동으로 지워집니다. %3

## <a name="error-events"></a>오류 이벤트

### <a name="event-1024-cp_reg_ckpt_restore_failed"></a>이벤트 1024: CP_REG_CKPT_RESTORE_FAILED

클러스터 리소스 ' %1 '에 대 한 레지스트리 검사점을 레지스트리 키 HKEY_LOCAL_MACHINE %2 (으)로 복원할 수 없습니다 \\ . 리소스가 제대로 작동 하지 않을 수 있습니다.
이 레지스트리 하위 트리에서 레지스트리 키에 대 한 열린 핸들이 있는 다른 프로세스가 없는지 확인 합니다.

### <a name="event-1034-res_disk_missing"></a>이벤트 1034: RES_DISK_MISSING

연결 된 디스크를 찾을 수 없어 클러스터 실제 디스크 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 필요한 디스크 시그니처는 ' %2 '입니다.
디스크가 교체 되거나 복원 된 경우 장애 조치(Failover) 클러스터 관리자 스냅인에서 디스크의 속성 시트에 있는 Repair 함수를 사용 하 여 새 디스크 또는 복원 된 디스크를 복구할 수 있습니다. 디스크가 교체 되지 않으면 연결 된 디스크 리소스를 삭제 합니다.

### <a name="event-1035-res_disk_mount_failed"></a>이벤트 1035: RES_DISK_MOUNT_FAILED

디스크 리소스 ' %1 '을 (를) 온라인 상태로 전환 하는 동안 ' %2 ' 오류로 인해 하나 이상의 볼륨에 액세스할 수 없습니다. 구성 유효성 검사 마법사를 실행 하 여 저장소 구성을 확인 합니다. 필요에 따라 Chkdsk를 실행 하 여이 디스크에 있는 모든 볼륨의 무결성을 확인할 수 있습니다.

### <a name="event-1037-res_disk_filesystem_failed"></a>이벤트 1037: RES_DISK_FILESYSTEM_FAILED

' %1 ' 리소스에 대 한 디스크에 있는 하나 이상의 파티션에 대 한 파일 시스템이 손상 되었을 수 있습니다. 구성 유효성 검사 마법사를 실행 하 여 저장소 구성을 확인 합니다. 필요에 따라 Chkdsk를 실행 하 여이 디스크에 있는 모든 볼륨의 무결성을 확인할 수 있습니다.

### <a name="event-1038-res_disk_reservation_lost"></a>이벤트 1038: RES_DISK_RESERVATION_LOST

이 노드에서 클러스터 디스크 ' %1 '의 소유권이 예기치 않게 손실 되었습니다. 구성 유효성 검사 마법사를 실행 하 여 저장소 구성을 확인 합니다.

### <a name="event-1039-res_genapp_create_failed"></a>이벤트 1039: RES_GENAPP_CREATE_FAILED

프로세스를 만드는 동안 제네릭 응용 프로그램 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다 (오류 ' %2 '). 가능한 원인은 다음과 같습니다 .이 노드에 응용 프로그램이 없을 때 경로 이름을 잘못 지정 했을 수 있습니다. 이진 이름을 잘못 지정 했을 수 있습니다.

### <a name="event-1040-res_gensvc_open_failed"></a>이벤트 1040: RES_GENSVC_OPEN_FAILED

서비스를 열려고 시도 하는 동안 제네릭 서비스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다 (오류 ' %2 '). 가능한 원인은 다음과 같습니다. 서비스가 설치 되지 않았거나 지정 된 서비스 이름이 잘못 되었습니다.

### <a name="event-1041-res_gensvc_start_failed"></a>이벤트 1041: RES_GENSVC_START_FAILED

서비스를 시작 하는 동안 제네릭 서비스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다 (오류 ' %2 '). 가능한 원인: 지정 된 서비스 매개 변수가 잘못 되었을 수 있습니다.

### <a name="event-1042-res_gensvc_failed_after_start"></a>이벤트 1042: RES_GENSVC_FAILED_AFTER_START

' %2 ' 오류로 인해 제네릭 서비스 ' %1 '이 (가) 실패 했습니다. 응용 프로그램 이벤트 로그를 확인 하십시오.

### <a name="event-1044-res_ipaddr_nbt_interface_create_failed"></a>이벤트 1044: RES_IPADDR_NBT_INTERFACE_CREATE_FAILED

' %1 ' 리소스를 온라인 상태로 전환 하는 동안 새 NetBIOS 인터페이스를 만들려고 할 때 오류가 발생 했습니다 (오류 코드 ' %2 '). 최대 NetBIOS 이름 수를 초과 했을 수 있습니다.

### <a name="event-1046-res_ipaddr_invalid_subnet"></a>이벤트 1046: RES_IPADDR_INVALID_SUBNET

서브넷 마스크 값이 잘못 되었기 때문에 클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. IP 주소 리소스 속성을 확인 하세요.

### <a name="event-1047-res_ipaddr_invalid_address"></a>이벤트 1047: RES_IPADDR_INVALID_ADDRESS

주소 값이 잘못 되었기 때문에 클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. IP 주소 리소스 속성을 확인 하세요.

### <a name="event-1048-res_ipaddr_invalid_adapter"></a>이벤트 1048: RES_IPADDR_INVALID_ADAPTER

클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 클러스터 네트워크 인터페이스 ' %2 '에 해당 하는 네트워크 어댑터에 대 한 구성 데이터를 확인할 수 없습니다 (오류 코드는 ' %3 '). IP 주소 리소스가 올바른 주소 및 네트워크 속성으로 구성 되어 있는지 확인 하세요.

### <a name="event-1049-res_ipaddr_in_use"></a>이벤트 1049: RES_IPADDR_IN_USE

네트워크에서 중복 IP 주소 ' %2 '이 (가) 검색 되어 클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 모든 IP 주소가 고유한 지 확인 하세요.

### <a name="event-1050-res_netname_duplicate"></a>이벤트 1050: RES_NETNAME_DUPLICATE

이름 ' %2 '이 (가)이 클러스터 노드 이름과 일치 하므로 클러스터 네트워크 이름 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 네트워크 이름이 고유한 지 확인 합니다.

### <a name="event-1051-res_netname_no_ip_address"></a>이벤트 1051: RES_NETNAME_NO_IP_ADDRESS

클러스터 네트워크 이름 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 종속 IP 주소 리소스에 대 한 네트워크 어댑터에 하나 이상의 DNS 서버에 대 한 액세스 권한이 있는지 확인 하십시오. 또는 종속 IP 주소에 대해 NetBIOS를 사용 하도록 설정 합니다.

### <a name="event-1052-res_netname_cant_add_name_status"></a>이벤트 1052: RES_NETNAME_CANT_ADD_NAME_STATUS

시스템에 이름을 추가할 수 없기 때문에 클러스터 네트워크 이름 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 관련 오류 코드는 데이터 섹션에 저장 됩니다.

### <a name="event-1053-res_smb_cant_create_share"></a>이벤트 1053: RES_SMB_CANT_CREATE_SHARE

공유를 만들 수 없으므로 클러스터 파일 공유 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다.

### <a name="event-1054-res_smb_share_not_found"></a>이벤트 1054: RES_SMB_SHARE_NOT_FOUND

파일 공유 리소스 ' %1 '에 대 한 상태 검사에 실패 했습니다. 네트워크 이름 %3 (으)로 범위가 지정 된 공유 ' %2 '에 대 한 정보를 검색 하는 중 오류 코드 ' %4 '이 (가) 공유가 존재 하며 액세스할 수 있는지 확인 하십시오.

### <a name="event-1055-res_smb_share_failed"></a>이벤트 1055: RES_SMB_SHARE_FAILED

파일 공유 리소스 ' %1 '에 대 한 상태 검사에 실패 했습니다. 네트워크 이름 %3 (으)로 범위가 지정 된 공유 ' %2 '에 대 한 정보를 검색 하는 동안 공유가 존재 하지 않습니다 (오류 코드 ' %4 '). 공유가 존재 하며 액세스할 수 있는지 확인 하세요.

### <a name="event-1069-rcm_resource_failure"></a>이벤트 1069: RCM_RESOURCE_FAILURE

클러스터 된 역할 ' %2 '의 클러스터 리소스 ' %1 '이 (가) 실패 했습니다.

### <a name="event-1069-rcm_resource_failure_with_typename"></a>이벤트 1069: RCM_RESOURCE_FAILURE_WITH_TYPENAME

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '이 (가) 실패 했습니다.<br><br>리소스 및 역할에 대 한 오류 정책에 따라 클러스터 서비스는이 노드에서 리소스를 온라인 상태로 전환 하거나 그룹을 클러스터의 다른 노드로 이동한 후 다시 시작할 수 있습니다. 장애 조치(Failover) 클러스터 관리자 또는 Get-clusterresource Windows PowerShell cmdlet을 사용 하 여 리소스 및 그룹 상태를 확인 합니다.

### <a name="event-1069-rcm_resource_failure_with_cause"></a>이벤트 1069: RCM_RESOURCE_FAILURE_WITH_CAUSE

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '이 (가) 실패 했습니다. 오류 코드는 ' %5 ' (' %4 ')입니다.<br><br>리소스 및 역할에 대 한 오류 정책에 따라 클러스터 서비스는이 노드에서 리소스를 온라인 상태로 전환 하거나 그룹을 클러스터의 다른 노드로 이동한 후 다시 시작할 수 있습니다. 장애 조치(Failover) 클러스터 관리자 또는 Get-clusterresource Windows PowerShell cmdlet을 사용 하 여 리소스 및 그룹 상태를 확인 합니다.

### <a name="event-1069-rcm_resource_failure_with_error_code"></a>이벤트 1069: RCM_RESOURCE_FAILURE_WITH_ERROR_CODE

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '이 (가) 실패 했습니다. 오류 코드는 ' %4 '입니다.<br><br>리소스 및 역할에 대 한 오류 정책에 따라 클러스터 서비스는이 노드에서 리소스를 온라인 상태로 전환 하거나 그룹을 클러스터의 다른 노드로 이동한 후 다시 시작할 수 있습니다. 장애 조치(Failover) 클러스터 관리자 또는 Get-clusterresource Windows PowerShell cmdlet을 사용 하 여 리소스 및 그룹 상태를 확인 합니다.

### <a name="event-1069-rcm_resource_failure_due_to_veto"></a>이벤트 1069: RCM_RESOURCE_FAILURE_DUE_TO_VETO

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '이 (가) 클러스터 리소스에서 필요한 상태 변경을 차단 하려고 했기 때문에 실패 했습니다.

### <a name="event-1077-res_ipaddr_ipv4_address_interface_failed"></a>이벤트 1077: RES_IPADDR_IPV4_ADDRESS_INTERFACE_FAILED

IP 인터페이스 ' %1 ' (주소 ' %2 ')에 대 한 상태 검사에 실패 했습니다 (상태는 ' %3 '). 구성 유효성 검사 마법사를 실행 하 여 네트워크 어댑터가 제대로 작동 하는지 확인 합니다.

### <a name="event-1078-res_ipaddr_wins_address_failed"></a>이벤트 1078: RES_IPADDR_WINS_ADDRESS_FAILED

' %3 ' 오류로 인해 ' %2 ' 인터페이스에서 WINS 등록에 실패 했으므로 클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 액세스 가능한 올바른 WINS 서버가 지정 되어 있는지 확인 하십시오.

### <a name="event-1121-cp_crypto_ckpt_restore_failed"></a>이벤트 1121: CP_CRYPTO_CKPT_RESTORE_FAILED

클러스터 리소스 ' %1 '에 대 한 암호화 된 설정을이 노드의 컨테이너 이름 ' %2 '에 적용 하지 못했습니다.

### <a name="event-1127-tm_event_cluster_netinterface_failed"></a>이벤트 1127: TM_EVENT_CLUSTER_NETINTERFACE_FAILED

네트워크 ' %3 '의 클러스터 노드 ' %2 '에 대 한 클러스터 네트워크 인터페이스 ' %1 '이 (가) 실패 했습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1129-tm_event_cluster_network_partitioned"></a>이벤트 1129: TM_EVENT_CLUSTER_NETWORK_PARTITIONED

클러스터 네트워크 ' %1 '이 (가) 분할 되었습니다. 연결 된 일부 장애 조치 (failover) 클러스터 노드는 네트워크를 통해 서로 통신할 수 없습니다. 장애 조치 (failover) 클러스터에서 오류 위치를 확인할 수 없습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1130-tm_event_cluster_network_down"></a>이벤트 1130: TM_EVENT_CLUSTER_NETWORK_DOWN

클러스터 네트워크 ' %1 '이 (가) 종료 되었습니다. 사용 가능한 노드가이 네트워크를 사용 하 여 통신할 수 없습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1137-rcm_drain_move_failed"></a>이벤트 1137: RCM_DRAIN_MOVE_FAILED

드레이닝에 대 한 클러스터 역할 ' %1 '의 이동을 완료할 수 없습니다. 작업에 실패 했습니다 (오류 코드 %2).

### <a name="event-1138-res_smb_cant_create_dfs_root"></a>이벤트 1138: RES_SMB_CANT_CREATE_DFS_ROOT

클러스터 파일 공유 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. ' %3 ' 오류로 인해 DFS 네임 스페이스 루트를 만들지 못했습니다. ' DFS 네임 스페이스 ' 서비스를 시작 하지 못하여 ' %2 ' 공유의 DFS-N 루트를 만들지 못했기 때문일 수 있습니다.

### <a name="event-1141-res_smb_cant_init_dfs_svc"></a>이벤트 1141: RES_SMB_CANT_INIT_DFS_SVC

클러스터 파일 공유 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. ' %3 ' 오류로 인해 DFS 루트 대상 ' %2 '의 다시 동기화에 실패 했습니다.

### <a name="event-1142-res_smb_cant_online_dfs_root"></a>이벤트 1142: RES_SMB_CANT_ONLINE_DFS_ROOT

DFS 네임 스페이스에 대 한 클러스터 파일 공유 리소스 ' %1 '은 (는) 오류 ' %2 ' (으)로 인해 온라인 상태로 만들 수 없습니다.

### <a name="event-1182-netres_resource_stop_error"></a>이벤트 1182: NETRES_RESOURCE_STOP_ERROR

연결 된 서비스에서 다시 시작 하려는 시도가 실패 하 여 클러스터 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 오류 코드는 ' %2 '입니다. 매개 변수를 업데이트 하려면 서비스를 다시 시작 해야 합니다. 그러나 서비스를 중지 했다가 다시 시작 하기 전에 서비스에 오류가 발생 했습니다. 서비스와 연결 된 추가 이벤트를 확인 하 고 서비스가 올바르게 작동 하는지 확인 하십시오.

### <a name="event-1183-res_disk_invalid_mp_source_not_clustered"></a>이벤트 1183: RES_DISK_INVALID_MP_SOURCE_NOT_CLUSTERED

클러스터 디스크 리소스 ' %1 '에 잘못 된 탑재 지점이 있습니다. 탑재 지점과 연결 된 원본 및 대상 디스크는 모두 클러스터 된 디스크 여야 하며 동일한 그룹의 구성원 이어야 합니다. <br>볼륨 ' %3 '의 탑재 지점 ' %2 '이 (가) 잘못 된 원본 디스크를 참조 합니다. 원본 디스크가 클러스터 된 디스크이 고 대상 디스크와 동일한 그룹에 있어야 합니다 (탑재 지점 호스팅).

### <a name="event-1191-res_netname_delete_computer_account_failed_status"></a>이벤트 1191: RES_NETNAME_DELETE_COMPUTER_ACCOUNT_FAILED_STATUS

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 도메인 ' %2 '에서 연결 된 컴퓨터 개체를 삭제 하지 못했습니다. 오류 코드는 ' %3 '입니다. <br>도메인 관리자가 Active Directory 도메인에서 컴퓨터 개체를 수동으로 삭제 했는지 확인 하십시오.

### <a name="event-1192-res_netname_delete_computer_account_failed"></a>이벤트 1192: RES_NETNAME_DELETE_COMPUTER_ACCOUNT_FAILED

다음 이유로 인해 클러스터 네트워크 이름 리소스 ' %1 '이 (가) 도메인 ' %2 '에서 연결 된 컴퓨터 개체를 삭제 하지 못했습니다.<br>%3. <br><br>도메인 관리자가 Active Directory 도메인에서 컴퓨터 개체를 수동으로 삭제 했는지 확인 하십시오.

### <a name="event-1193-res_netname_add_computer_account_failed_status"></a>이벤트 1193: RES_NETNAME_ADD_COMPUTER_ACCOUNT_FAILED_STATUS

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 도메인 ' %2 '에 연결 된 컴퓨터 개체를 만들지 못했습니다 (원인: %3).<br><br>관련 오류 코드: %5<br><br>
다음을 확인 하려면 도메인 관리자에 게 문의 하세요.

- 클러스터 id ' %4 '이 (가) 컴퓨터 개체를 만들 수 있습니다. 기본적으로 모든 컴퓨터 개체는 ' Computers ' 컨테이너에 생성 됩니다. 이 위치가 변경 된 경우 도메인 관리자에 게 문의 하십시오.
- 컴퓨터 개체에 대 한 할당량에 도달 하지 않았습니다.
- 기존 컴퓨터 개체가 있는 경우 Active Directory 사용자 및 컴퓨터 도구를 사용 하 여 클러스터 Id ' %4 '에 해당 컴퓨터 개체에 대 한 ' 모든 권한 ' 권한이 있는지 확인 하십시오.

### <a name="event-1194-res_netname_add_computer_account_failed"></a>이벤트 1194: RES_NETNAME_ADD_COMPUTER_ACCOUNT_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) %3 동안 도메인 ' %2 '에 연결 된 컴퓨터 개체를 만들지 못했습니다.<br><br>관련 오류 코드의 텍스트는 %4입니다.

다음을 확인 하려면 도메인 관리자에 게 문의 하세요.

- 클러스터 id ' %5 '에 컴퓨터 개체 만들기 권한이 있습니다. 기본적으로 모든 컴퓨터 개체는 클러스터 id ' %5 '과 (와) 동일한 컨테이너에 생성 됩니다.
- 컴퓨터 개체에 대 한 할당량에 도달 하지 않았습니다.
- 기존 컴퓨터 개체가 있는 경우 Active Directory 사용자 및 컴퓨터 도구를 사용 하 여 클러스터 Id ' %5 '에 해당 컴퓨터 개체에 대 한 ' 모든 권한 ' 권한이 있는지 확인 하십시오.

### <a name="event-1195-res_netname_dns_registration_failed_status"></a>이벤트 1195: RES_NETNAME_DNS_REGISTRATION_FAILED_STATUS

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 하나 이상의 연결 된 DNS 이름을 등록 하지 못했습니다. 오류 코드는 ' %2 '입니다. 종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 하나 이상의 DNS 서버에 액세스할 수 있도록 구성 되어 있는지 확인 합니다.

### <a name="event-1196-res_netname_dns_registration_failed"></a>이벤트 1196: RES_NETNAME_DNS_REGISTRATION_FAILED

다음 이유로 인해 클러스터 네트워크 이름 리소스 ' %1 '에서 하나 이상의 연결 된 DNS 이름을 등록 하지 못했습니다.<br>%2.<br><br>종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 액세스 가능한 DNS 서버를 하나 이상 사용 하도록 구성 되어 있는지 확인 합니다.

### <a name="event-1205-rcm_event_group_failed_online_offline"></a>이벤트 1205: RCM_EVENT_GROUP_FAILED_ONLINE_OFFLINE

클러스터 서비스에서 클러스터 된 역할 ' %1 '을 (를) 완전히 온라인 또는 오프 라인 상태로 만들지 못했습니다. 하나 이상의 리소스가 실패 상태에 있을 수 있습니다. 이는 클러스터 된 역할의 가용성에 영향을 줄 수 있습니다.

### <a name="event-1206-res_netname_update_computer_account_failed_status"></a>이벤트 1206: RES_NETNAME_UPDATE_COMPUTER_ACCOUNT_FAILED_STATUS

클러스터 네트워크 이름 리소스 ' %1 '과 (와) 연결 된 컴퓨터 개체를 ' %2 ' 도메인에서 업데이트할 수 없습니다. 오류 코드는 ' %3 '입니다. 클러스터 id ' %4 '에 개체를 업데이트 하는 데 필요한 권한이 없을 수 있습니다. 도메인 관리자와 협력 하 여 클러스터 id가 도메인의 컴퓨터 개체를 업데이트할 수 있는지 확인 하십시오.

### <a name="event-1207-res_netname_update_computer_account_failed"></a>이벤트 1207: RES_NETNAME_UPDATE_COMPUTER_ACCOUNT_FAILED

클러스터 네트워크 이름 리소스 ' %1 '과 (와) 연결 된 컴퓨터 개체를 ' %2 ' 도메인에서 업데이트할 수 없습니다. <br>%3 작업.<br><br>관련 오류 코드의 텍스트는 %4입니다.<br> <br>클러스터 id ' %5 '에 개체를 업데이트 하는 데 필요한 권한이 없을 수 있습니다. 도메인 관리자와 협력 하 여 클러스터 id가 도메인의 컴퓨터 개체를 업데이트할 수 있는지 확인 하십시오.

### <a name="event-1208-res_disk_invalid_mp_target_not_clustered"></a>이벤트 1208: RES_DISK_INVALID_MP_TARGET_NOT_CLUSTERED

클러스터 디스크 리소스 ' %1 '에 잘못 된 탑재 지점이 있습니다. 탑재 지점과 연결 된 원본 및 대상 디스크는 모두 클러스터 된 디스크 여야 하며 동일한 그룹의 구성원 이어야 합니다. <br>볼륨 ' %3 '의 탑재 지점 ' %2 '이 (가) 잘못 된 대상 디스크를 참조 합니다. 대상 디스크가 클러스터 된 디스크이 고 원본 디스크와 동일한 그룹에 있어야 합니다 (탑재 지점 호스팅).

### <a name="event-1211-res_netname_no_writeable_dc_status"></a>이벤트 1211: RES_NETNAME_NO_WRITEABLE_DC_STATUS

클러스터 네트워크 이름 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 리소스와 연결 된 컴퓨터 개체를 만들거나 업데이트 하기 위해 쓰기 가능한 도메인 컨트롤러 (도메인 %2)를 찾지 못했습니다. 오류 코드는 ' %3 '입니다.
구성 된 도메인 내에서이 노드가 쓰기 가능한 도메인 컨트롤러에 액세스할 수 있는지 확인 합니다. 또한 도메인 컨트롤러의 이름을 확인 하기 위해 DNS 서버가 실행 중인지 확인 합니다.

### <a name="event-1212-res_netname_no_writeable_dc"></a>이벤트 1212: RES_NETNAME_NO_WRITEABLE_DC

클러스터 네트워크 이름 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 다음 이유로 인해 리소스와 연결 된 컴퓨터 개체를 만들거나 업데이트 하기 위해 쓰기 가능한 도메인 컨트롤러 (도메인 %2)를 찾으려고 시도 하지 못했습니다.<br>%3.<br><br> 오류 코드는 ' %4 '입니다. 구성 된 도메인 내에서이 노드가 쓰기 가능한 도메인 컨트롤러에 액세스할 수 있는지 확인 합니다. 또한 도메인 컨트롤러의 이름을 확인 하기 위해 DNS 서버가 실행 중인지 확인 합니다.

### <a name="event-1213-res_netname_rename_restore_failed"></a>이벤트 1213: RES_NETNAME_RENAME_RESTORE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 도메인 컨트롤러 ' %2 '에서 연결 된 컴퓨터 개체의 이름을 완전히 바꿀 수 없습니다. 새 이름 ' %3 '에서 원래 이름 ' %4 ' (으)로 컴퓨터 개체의 이름을 다시 바꾸려고 했지만 실패 했습니다. 오류 코드는 ' %5 '입니다. 네트워크 이름 및 연결 된 컴퓨터 개체 이름이 일치 해야 클라이언트 연결에 영향을 줄 수 있습니다. 컴퓨터 개체의 이름을 수동으로 바꾸려면 도메인 관리자에 게 문의 하십시오.

### <a name="event-1214-res_netname_cant_add_name2"></a>이벤트 1214: RES_NETNAME_CANT_ADD_NAME2

클러스터 네트워크 이름 리소스는 Netbios에 등록할 수 없습니다. <br><br>네트워크 이름: ' %3 ' <br>실패 이유: %2 <br>리소스 이름: ' %1 ' <br><br> 네트워크 이름에 대해 nbtstat를 실행 하 여 이름이 Netbios에 이미 등록 되지 않았는지 확인 합니다.

### <a name="event-1215-res_netname_not_registered_with_rdr"></a>이벤트 1215: RES_NETNAME_NOT_REGISTERED_WITH_RDR

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 상태 검사에 실패 했습니다. 네트워크 이름 ' %2 '이 (가)이 노드에 더 이상 등록 되어 있지 않습니다. 오류 코드는 ' %3 '입니다. 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인할 수 있습니다.

### <a name="event-1218-res_netname_online_rename_recovery_missing_account"></a>이벤트 1218: RES_NETNAME_ONLINE_RENAME_RECOVERY_MISSING_ACCOUNT

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 이름 변경 작업을 수행 하지 못했습니다 (원래 이름 ' %3 '을 (를) 이름 ' %4 ' (으)로 변경 하려고 함). ' %2 ' 도메인 컨트롤러가 생성 된 컴퓨터 개체를 찾을 수 없습니다. 다음에 리소스가 온라인 상태가 될 때 컴퓨터 개체를 다시 만드는 시도가 수행 됩니다. 또한 도메인 관리자와 협력 하 여 컴퓨터 개체가 도메인에 있는지 확인 하십시오.

### <a name="event-1219-res_netname_online_rename_dc_not_found"></a>이벤트 1219: RES_NETNAME_ONLINE_RENAME_DC_NOT_FOUND

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 이름 변경 작업을 수행 하지 못했습니다.
컴퓨터 개체 ' %3 '의 이름을 바꾼 도메인 컨트롤러 ' %2 '에 연결할 수 없습니다. 오류 코드는 ' %4 '입니다. 쓰기 가능한 도메인 컨트롤러에 액세스할 수 있는지 확인 하 고 연결 문제가 있는지 확인 하십시오.

### <a name="event-1220-res_netname_online_rename_recovery_failed"></a>이벤트 1220: RES_NETNAME_ONLINE_RENAME_RECOVERY_FAILED

도메인 컨트롤러 %4을 (를) 사용 하 여 ' %1 ' 리소스의 컴퓨터 계정을 %2에서 %3 (으)로 이름을 바꾸지 못했습니다. 관련 오류 코드는 데이터 섹션에 저장 됩니다.<br>
<br>이 리소스의 컴퓨터 계정이 이름을 바꿔서 완료 되지 않았습니다. 이 리소스의 온라인 프로세스 중에 검색 되었습니다.
복구 하려면 컴퓨터 계정의 이름을 이름 속성의 현재 값 (예: 네트워크에 표시 되는 이름)으로 바꿔야 합니다.<br> <br>이름을 바꾼 도메인 컨트롤러를 사용 하지 못할 수 있습니다. 이 경우 도메인 컨트롤러를 다시 사용할 수 있을 때까지 기다립니다. 도메인 컨트롤러에서 계정에 대 한 액세스를 거부할 수 있습니다. 액세스를 확인 한 후 이름을 다시 온라인으로 전환 하십시오.<br> <br>가능 하지 않은 경우 Kerberos 인증을 사용 하지 않도록 설정 했다가 다시 사용 하도록 설정 하면 다른 DC에서 컴퓨터 계정을 찾으려고 시도 합니다. 기존 컴퓨터 계정을 사용 하려면 이름 속성을 %2 (으)로 변경 해야 합니다.

### <a name="event-1223-res_ipaddr_invalid_network_role"></a>이벤트 1223: RES_IPADDR_INVALID_NETWORK_ROLE

클러스터 네트워크 ' %2 '이 (가) 클라이언트 액세스를 허용 하도록 구성 되어 있지 않으므로 클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 클러스터 네트워크의 구성 된 속성을 확인 하려면 장애 조치(Failover) 클러스터 관리자 스냅인를 사용 하세요.

### <a name="event-1226-res_netname_tcb_not_held"></a>이벤트 1226: RES_NETNAME_TCB_NOT_HELD

네트워크 이름 리소스 ' %1 ' (연결 된 네트워크 이름 ' %2 ')이 (가) Kerberos 인증 지원을 사용 하도록 설정 되어 있습니다. 필수 자격 증명을 LSA에 추가 하지 못했습니다. 관련 오류 코드 ' %3 '이 (가) 일반적으로이 작업에 필요한 권한이 부족 함을 나타냅니다. 필요한 권한은 ' 신뢰할 수 있는 컴퓨팅 기반 ' 이며 클러스터를 구성 하는 각 노드에서 로컬에서 사용 하도록 설정 해야 합니다.

### <a name="event-1227-res_netname_lsa_error"></a>이벤트 1227: RES_NETNAME_LSA_ERROR

네트워크 이름 리소스 ' %1 ' (연결 된 네트워크 이름 ' %2 ')이 (가) Kerberos 인증 지원을 사용 하도록 설정 되어 있습니다. 필수 자격 증명을 LSA에 추가 하지 못했습니다. 관련 오류 코드는 ' %3 '입니다.

### <a name="event-1228-res_netname_clone_failure"></a>이벤트 1228: RES_NETNAME_CLONE_FAILURE

클러스터 네트워크 이름 리소스 ' %1 '이 (가)이 노드에서 네트워크 이름을 사용 하도록 설정 하는 동안 오류가 발생 했습니다. 실패 이유는 다음과 같습니다. <br> ' %2 '.<br><br> 오류 코드는 ' %3 '입니다. <br><br> 네트워크 이름 리소스를 오프 라인 상태로 전환 하 여 다시 온라인 상태로 전환할 수 있습니다.

### <a name="event-1229-res_netname_no_ips_for_dns"></a>이벤트 1229: RES_NETNAME_NO_IPS_FOR_DNS

클러스터 네트워크 이름 리소스 ' %1 '이 (가) DNS 서버에 등록할 IP 주소를 식별할 수 없습니다. ' 클라이언트가이 네트워크를 통해 연결할 수 있도록 허용 ' 설정을 사용 하 여 클러스터에서 사용할 수 있는 네트워크가 하나 이상 있고 각 노드에 네트워크에 대해 구성 된 유효한 IP 주소가 있는지 확인 합니다.

### <a name="event-1230-rcm_deadlock_or_crash_detected"></a>이벤트 1230: RCM_DEADLOCK_OR_CRASH_DETECTED

서버의 구성 요소가 적시에 응답 하지 않았습니다. 이로 인해 클러스터 리소스 ' %1 ' (리소스 유형 ' %2 ', DLL ' %3 ')이 (가) 제한 시간 임계값을 초과 했습니다. 클러스터 상태 검색의 일부로 복구 작업이 수행 됩니다.
클러스터는이 리소스를 실행 하는 RHS(Resource Hosting Subsystem) (RHS) 프로세스를 종료 하 고 다시 시작 하 여 자동으로 복구를 시도 합니다. 리소스와 연결 된 기본 인프라 (예: 저장소, 네트워킹 또는 서비스)가 제대로 작동 하는지 확인 합니다.

### <a name="event-1230-rcm_resource_control_deadlock_detected"></a>이벤트 1230: RCM_RESOURCE_CONTROL_DEADLOCK_DETECTED

서버의 구성 요소가 적시에 응답 하지 않았습니다. 이로 인해 제어 코드 ' %4; '을 (를) 처리 하는 동안 클러스터 리소스 ' %1 ' (리소스 유형 ' %2 ', DLL ' %3 ')이 (가) 제한 시간 임계값을 초과 했습니다. 클러스터 상태 검색의 일부로 복구 작업이 수행 됩니다. 클러스터는이 리소스를 실행 하는 RHS(Resource Hosting Subsystem) (RHS) 프로세스를 종료 하 고 다시 시작 하 여 자동으로 복구를 시도 합니다. 리소스와 연결 된 기본 인프라 (예: 저장소, 네트워킹 또는 서비스)가 제대로 작동 하는지 확인 합니다.

### <a name="event-1231-res_netname_logon_failure"></a>이벤트 1231: RES_NETNAME_LOGON_FAILURE

클러스터 네트워크 이름 리소스 ' %1 '에 도메인에 로그온 하는 동안 오류가 발생 했습니다. 실패 이유는 다음과 같습니다. <br> ' %2 '.<br><br> 오류 코드는 ' %3 '입니다.
<br><br> 구성 된 도메인 내에서이 노드에 도메인 컨트롤러에 액세스할 수 있는지 확인 합니다.

### <a name="event-1232-res_genscript_timeout"></a>이벤트 1232: RES_GENSCRIPT_TIMEOUT

클러스터 일반 스크립트 리소스 ' %1 '의 진입점 ' %2 '이 (가) 적시에 실행을 완료 하지 못했습니다. 무한 루프 또는 무한 대기를 발생 시킬 수 있는 다른 문제가 원인일 수 있습니다. 또는이 리소스에 대해 지정 된 보류 제한 시간 값이 너무 짧을 수도 있습니다. ' %2 ' 스크립트 진입점을 검토 하 여 스크립트 코드에서 가능한 모든 무한 대기를 수정 했는지 확인 하십시오. 그런 다음 필요한 경우 보류 제한 시간 값을 늘립니다.

### <a name="event-1233-res_genscript_hangmode"></a>이벤트 1233: RES_GENSCRIPT_HANGMODE

클러스터 일반 스크립트 리소스 ' %1 ': ' %2 ' 작업을 수행 하는 요청이 처리 되지 않습니다. 이는 이전에 ' %3 ' 진입점을 적시에 실행 하려고 했지만 실패 했기 때문입니다. 무한 루프 또는 무한 대기를 일으킬 수 있는 다른 문제가 없는지 확인 하려면이 진입점에 대 한 스크립트 코드를 검토 하십시오. 그런 다음 필요 하다 고 판단 되 면 리소스 보류 제한 시간 값을 늘립니다.

### <a name="event-1234-cluster_event_account_missing_privs"></a>이벤트 1234: CLUSTER_EVENT_ACCOUNT_MISSING_PRIVS

클러스터 서비스 서비스 계정에 필요한 권한이 하나 이상 누락 된 것을 발견 했습니다. 누락 된 권한 목록은 ' %1 '이 고 현재 서비스 계정에 부여 되지 않았습니다. ' sc.exe qprivs clussvc '를 사용 하 여 클러스터 서비스 (ClusSvc)의 권한을 확인 합니다. 또한 기본 권한을 변경 했을 수 있는 Active Directory Domain Services의 보안 정책 또는 그룹 정책을 확인 합니다. 다음 명령을 입력 하 여 올바르게 작동 하는 데 필요한 권한을 클러스터 서비스에 부여 합니다.

```
sc.exe privs
clussvc
SeBackupPrivilege/SeRestorePrivilege/SeIncreaseQuotaPrivilege/SeIncreaseBasePriorityPrivilege/SeTcbPrivilege/SeDebugPrivilege/SeSecurityPrivilege/SeAuditPrivilege/SeImpersonatePrivilege/SeChangeNotifyPrivilege/SeIncreaseWorkingSetPrivilege/SeManageVolumePrivilege/SeCreateSymbolicLinkPrivilege/SeLoadDriverPrivilege
```

### <a name="event-1242-res_ipaddr_lease_expired"></a>이벤트 1242: RES_IPADDR_LEASE_EXPIRED

클러스터 IP 주소 리소스 ' %1 '과 (와) 연결 된 IP 주소 ' %2 '의 임대가 만료 되었거나 곧 만료 됩니다. 현재 갱신할 수 없습니다. 연결 된 DHCP 서버가 액세스할 수 있고이 IP 주소에 대 한 임대를 갱신 하도록 제대로 구성 되어 있는지 확인 합니다.

### <a name="event-1245-res_ipaddr_lease_renewal_failed"></a>이벤트 1245: RES_IPADDR_LEASE_RENEWAL_FAILED

클러스터 IP 주소 리소스 ' %1 '이 (가) IP 주소 ' %2 '에 대 한 임대를 갱신 하지 못했습니다.
DHCP 서버가 액세스할 수 있고이 IP 주소에 대 한 임대를 갱신 하도록 제대로 구성 되어 있는지 확인 합니다.

### <a name="event-1250-rcm_resource_embedded_failure"></a>이벤트 1250: RCM_RESOURCE_EMBEDDED_FAILURE

클러스터 된 역할 ' %2 '의 클러스터 리소스 ' %1 '이 (가) 위험 상태 알림을 받았습니다. 가상 컴퓨터의 경우 가상 컴퓨터 내의 응용 프로그램 또는 서비스가 비정상 상태임을 나타냅니다. 가상 컴퓨터 내에서 모니터링 되는 서비스 또는 응용 프로그램의 기능을 확인 합니다.

### <a name="event-1254-rcm_group_terminal_failure"></a>이벤트 1254: RCM_GROUP_TERMINAL_FAILURE

클러스터 된 역할 ' %1 '이 (가) 장애 조치 (failover) 임계값을 초과 했습니다. 장애 조치 (failover) 기간 내에 구성 된 장애 조치 (failover) 시도 횟수를 모두 사용 하 여 실패 한 상태로 유지 됩니다. 역할을 온라인으로 전환 하거나 클러스터의 다른 노드로 장애 조치 (failover) 하는 추가 시도는 수행 되지 않습니다.
실패와 관련 된 이벤트를 확인 하십시오. 오류가 발생 하는 문제를 해결 한 후에는 수동으로 역할을 온라인 상태로 만들 수 있으며, 다시 시작 지연 기간 후 클러스터가 다시 온라인 상태로 전환 하려고 할 수도 있습니다.

### <a name="event-1255-rcm_resource_network_failure"></a>이벤트 1255: RCM_RESOURCE_NETWORK_FAILURE

클러스터 된 역할 ' %2 '의 클러스터 리소스 ' %1 '이 (가) 위험 상태 알림을 받았습니다. 가상 컴퓨터의 경우 가상 컴퓨터의 중요 한 네트워크가 비정상 상태임을 나타냅니다. 가상 컴퓨터 및 가상 컴퓨터에서 사용 하도록 구성 된 가상 네트워크의 네트워크 연결을 확인 합니다.

### <a name="event-1256-res_netname_dns_registration_failed_dynamic_dns_zone"></a>이벤트 1256: RES_NETNAME_DNS_REGISTRATION_FAILED_DYNAMIC_DNS_ZONE

해당 DNS 영역에서 동적 업데이트를 받아들이지 않으므로 클러스터 네트워크 이름 리소스에서 하나 이상의 연결 된 DNS 이름을 등록 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>DNS 영역: ' %2 '

#### <a name="guidance"></a>지침

DNS가 동적 DNS 영역으로 구성 되어 있는지 확인 합니다. DNS 서버에서 동적 업데이트를 허용 하지 않는 경우 네트워크 어댑터의 속성에서 ' DNS에이 연결의 주소를 등록 하십시오 '를 선택 취소 합니다.

### <a name="event-1257-res_netname_dns_registration_failed_secure_dns_zone"></a>이벤트 1257: RES_NETNAME_DNS_REGISTRATION_FAILED_SECURE_DNS_ZONE

보안 DNS 영역 업데이트에 대 한 액세스가 거부 되었기 때문에 클러스터 네트워크 이름 리소스에서 하나 이상의 연결 된 DNS 이름을 등록 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>DNS 영역: ' %2 '<br><br>CNO (클러스터 이름 개체)에 보안 DNS 영역에 대 한 권한이 부여 되어 있는지 확인 하십시오.

### <a name="event-1258-res_netname_dns_registration_failed_timeout"></a>이벤트 1258: RES_NETNAME_DNS_REGISTRATION_FAILED_TIMEOUT

DNS 서버에 연결할 수 없기 때문에 클러스터 네트워크 이름 리소스에서 하나 이상의 연결 된 DNS 이름을 등록 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>DNS 영역: ' %2 '<br>DNS 서버: ' %3 '<br><br>종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 액세스 가능한 DNS 서버를 하나 이상 사용 하도록 구성 되어 있는지 확인 합니다.

### <a name="event-1259-res_netname_dns_registration_failed_cleanup"></a>이벤트 1259: RES_NETNAME_DNS_REGISTRATION_FAILED_CLEANUP

클러스터 서비스가 네트워크 이름에 해당 하는 기존 레코드를 정리 하지 못했으므로 클러스터 네트워크 이름 리소스에서 하나 이상의 연결 된 DNS 이름을 등록 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>DNS 영역: ' %2 '<br><br>CNO (클러스터 이름 개체)에 보안 DNS 영역에 대 한 권한이 부여 되어 있는지 확인 하십시오.

### <a name="event-1260-res_netname_dns_registration_modify_failed"></a>이벤트 1260: RES_NETNAME_DNS_REGISTRATION_MODIFY_FAILED

클러스터 네트워크 이름 리소스가 DNS 등록을 수정 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>오류 코드: ' %2 '

#### <a name="guidance"></a>지침

종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 하나 이상의 DNS 서버에 액세스할 수 있도록 구성 되어 있는지 확인 합니다.

### <a name="event-1261-res_netname_dns_registration_modify_failed_status"></a>이벤트 1261: RES_NETNAME_DNS_REGISTRATION_MODIFY_FAILED_STATUS

클러스터 네트워크 이름 리소스가 DNS 등록을 수정 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>이유: ' %2 '

#### <a name="guidance"></a>지침

종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 하나 이상의 DNS 서버에 액세스할 수 있도록 구성 되어 있는지 확인 합니다.

### <a name="event-1262-res_netname_dns_registration_publish_ptr_failed"></a>이벤트 1262: RES_NETNAME_DNS_REGISTRATION_PUBLISH_PTR_FAILED

클러스터 네트워크 이름 리소스가 DNS 역방향 조회 영역에서 PTR 레코드를 게시 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>오류 코드: ' %2 '

#### <a name="guidance"></a>지침

종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 하나 이상의 DNS 서버에 대 한 액세스로 구성 되어 있고 DNS 역방향 조회 영역이 있는지 확인 하십시오.

### <a name="event-1264-res_netname_dns_registration_publish_ptr_failed_status"></a>이벤트 1264: RES_NETNAME_DNS_REGISTRATION_PUBLISH_PTR_FAILED_STATUS

클러스터 네트워크 이름 리소스가 DNS 역방향 조회 영역에서 PTR 레코드를 게시 하지 못했습니다.<br><br>클러스터 네트워크 이름: ' %1 '<br>이유: ' %2 '

#### <a name="guidance"></a>지침

종속 IP 주소 리소스와 연결 된 네트워크 어댑터가 하나 이상의 DNS 서버에 대 한 액세스로 구성 되어 있고 DNS 역방향 조회 영역이 있는지 확인 하십시오.

### <a name="event-1265-res_type_control_timed_out"></a>이벤트 1265: RES_TYPE_CONTROL_TIMED_OUT

제어 코드 %2을 (를) 처리 하는 동안 클러스터 리소스 유형 ' %1 '이 (가) 시간 초과 되었습니다. 클러스터는 호출을 처리 하는 RHS (RHS(Resource Hosting Subsystem)) 프로세스를 종료 하 고 다시 시작 하 여 자동으로 복구를 시도 합니다.

### <a name="event-1289-netft_adapter_not_found"></a>이벤트 1289: NETFT_ADAPTER_NOT_FOUND

클러스터 서비스가 네트워크 어댑터 ' %1 '에 액세스할 수 없습니다. 다른 네트워크 어댑터가 제대로 작동 하는지 확인 하 고 장치 관리자에서 ' %1 ' 어댑터와 관련 된 오류를 확인 하십시오. ' %1 ' 어댑터의 구성이 변경 된 경우이 컴퓨터에 장애 조치 (failover) 클러스터링 기능을 다시 설치 해야 할 수 있습니다.

### <a name="event-1360-res_ipaddr_invalid_network"></a>이벤트 1360: RES_IPADDR_INVALID_NETWORK

클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 네트워크 속성 ' %2 '이 (가) 클러스터 네트워크 이름과 일치 하는지 또는 주소 속성 ' %3 '이 (가) 클러스터 네트워크의 서브넷 중 하 나와 일치 하는지 확인 하십시오. IPv6 주소 유형인 경우이 리소스와 일치 하는 클러스터 네트워크에 링크 로컬 또는 터널이 아닌 IPv6 접두사가 하나 이상 있는지 확인 하세요.

### <a name="event-1361-res_ipaddr_missing_dependant"></a>이벤트 1361: RES_IPADDR_MISSING_DEPENDANT

IPv6 터널 주소 리소스 ' %1 '이 (가) IP 주소 (IPv4) 리소스에 종속 되지 않으므로 온라인 상태로 전환 하지 못했습니다. 하나 이상의 IP 주소 (IPv4) 리소스에 대 한 종속성이 필요 합니다.

### <a name="event-1362-res_ipaddr_missing_data"></a>이벤트 1362: RES_IPADDR_MISSING_DATA

' %2 ' 속성을 읽을 수 없기 때문에 클러스터 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 리소스가 올바르게 구성 되었는지 확인 하세요.

### <a name="event-1363-res_ipaddr_no_isatap_support"></a>이벤트 1363: RES_IPADDR_NO_ISATAP_SUPPORT

IPv6 터널 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 종속 IP 주소 (IPv4) 리소스 ' %3 '과 (와) 연결 된 클러스터 네트워크 ' %2 '은 (는) ISATAP 터널링을 지원 하지 않습니다. 클러스터 네트워크가 ISATAP 터널링을 지원 하는지 확인 하세요.

### <a name="event-1540-service_backup_noquorum"></a>이벤트 1540: SERVICE_BACKUP_NOQUORUM

클러스터에 대 한 쿼럼이 아직 달성 되지 않았기 때문에 클러스터 구성 데이터에 대 한 백업 작업이 중단 되었습니다. 클러스터가 쿼럼을 달성 한 후에이 백업 작업을 다시 시도 하세요.

### <a name="event-1554-service_restore_invaliduser"></a>이벤트 1554: SERVICE_RESTORE_INVALIDUSER

클러스터 구성 데이터에 대 한 복원 작업이 실패 했습니다. 복원을 수행 하는 사용자 계정과 연결 된 권한이 부족 하기 때문입니다. 사용자 계정에 로컬 관리자 권한이 있는지 확인 하십시오.

### <a name="event-1557-service_witness_attach_failed"></a>이벤트 1557: SERVICE_WITNESS_ATTACH_FAILED

클러스터 서비스에서 감시 리소스의 클러스터 구성 데이터를 업데이트 하지 못했습니다. 감시 리소스가 온라인 상태이 고 액세스 가능한 지 확인 하세요.

### <a name="event-1559-res_witness_new_node_conflict"></a>이벤트 1559: RES_WITNESS_NEW_NODE_CONFLICT

파일 공유 감시 리소스와 연결 된 파일 공유 ' %1 '이 (가) 현재 서버 ' %2 '에서 호스트 되 고 있습니다. 이 서버 ' %2 '이 (가) 장애 조치 (failover) 클러스터 내의 새 노드로 추가 되었습니다. 동일한 클러스터를 구성 하는 노드에의 한 파일 공유 감시를 호스트 하는 것은 권장 되지 않습니다. 동일한 클러스터 내의 노드에서 호스팅되지 않는 파일 공유 감시를 선택 하 고 그에 따라 파일 공유 감시 리소스의 설정을 수정 하십시오.

### <a name="event-1560-res_smb_share_conflict"></a>이벤트 1560: RES_SMB_SHARE_CONFLICT

클러스터 파일 공유 리소스 ' %1 '이 (가) 공유 폴더 충돌을 검색 했습니다. 따라서 이러한 공유 폴더 중 일부에 액세스 하지 못할 수 있습니다. 이러한 상황을 해결 하려면 여러 공유 폴더에 동일한 공유 이름이 없도록 해야 합니다.

### <a name="event-1563-res_fsw_onlinefailure"></a>이벤트 1563: RES_FSW_ONLINEFAILURE

파일 공유 감시 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 파일 공유 ' %2 '이 (가) 있고 클러스터에서 액세스할 수 있는지 확인 하세요.

### <a name="event-1566-res_netname_timedout"></a>이벤트 1566: RES_NETNAME_TIMEDOUT

클러스터 네트워크 이름 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 네트워크 이름 리소스가 허용 가능한 시간 내에 작업을 완료 하지 못해 리소스 호스트 하위 시스템에 의해 종료 되었습니다. 작업을 수행 하는 동안 작업 시간이 초과 되었습니다.<br> ' %2 '

### <a name="event-1567-service_failed_to_change_log_size"></a>이벤트 1567: SERVICE_FAILED_TO_CHANGE_LOG_SIZE

클러스터 서비스에서 추적 로그 크기를 변경 하지 못했습니다. ' Get-Cluster \| Format-List ' PowerShell cmdlet을 사용 하 여 ClusterLogSize 설정을 확인 하세요 \* . 또한 성능 모니터 스냅인을 사용 하 여 FailoverClustering에 대 한 이벤트 추적 세션 설정을 확인 합니다.

### <a name="event-1567-res_vipaddr_address_interface_failed"></a>이벤트 1567: RES_VIPADDR_ADDRESS_INTERFACE_FAILED

IP 인터페이스 ' %1 ' (주소 ' %2 ')에 대 한 상태 검사에 실패 했습니다 (상태는 ' %3 '). 실제 또는 가상 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다.

### <a name="event-1568-res_cloud_witness_cant_communicate_to_azure"></a>이벤트 1568: RES_CLOUD_WITNESS_CANT_COMMUNICATE_TO_AZURE

클라우드 감시 리소스가 Microsoft Azure storage 서비스에 연결할 수 없습니다.<br><br>클러스터 리소스: %1 <br>클러스터 노드: %2

#### <a name="guidance"></a>지침

이는 클러스터 노드와 차단 중인 Microsoft Azure 서비스 간의 네트워크 통신 때문에 발생할 수 있습니다. Microsoft Azure에 대 한 노드의 인터넷 연결을 확인 합니다. Microsoft Azure portal에 연결 하 여 저장소 계정이 있는지 확인 합니다.

### <a name="event-1569-service_using_restricted_network"></a>이벤트 1569: SERVICE_USING_RESTRICTED_NETWORK

장애 조치 (failover) 클러스터에 사용 하지 않도록 설정 된 네트워크 ' %1 '은 (는) 현재 노드 ' %2 '이 (가) 클러스터의 다른 노드와 통신 하는 데 사용할 수 있는 유일한 네트워크로 검색 되었습니다. 이는 클러스터에 참여 하는 노드의 기능에 영향을 줄 수 있습니다. 노드 ' %2 '의 네트워크 연결을 확인 하 고 클러스터 통신용 네트워크를 하나 이상 사용 하도록 설정 하세요. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다.

### <a name="event-1569-res_cloud_witness_token_expired"></a>이벤트 1569: RES_CLOUD_WITNESS_TOKEN_EXPIRED

클라우드 감시 리소스에서 Microsoft Azure 저장소 서비스로 인증 하지 못했습니다. Microsoft Azure 저장소 계정에 연결 하는 동안 액세스 거부 오류가 반환 되었습니다. <br><br>클러스터 리소스: %1

#### <a name="guidance"></a>지침

저장소 계정의 액세스 키가 더 이상 유효 하지 않을 수 있습니다. 장애 조치(Failover) 클러스터 관리자 또는 집합-ClusterQuorum Windows PowerShell cmdlet의 클러스터 쿼럼 구성 마법사를 사용 하 여 업데이트 된 저장소 계정 액세스 키로 클라우드 감시 리소스를 구성 합니다.

### <a name="event-1573-service_form_witness_failed"></a>이벤트 1573: SERVICE_FORM_WITNESS_FAILED

노드 ' %1 '이 (가) 클러스터를 형성 하지 못했습니다. 미러링 모니터 서버에 액세스할 수 없기 때문입니다. 감시 리소스가 온라인 상태이 고 사용 가능한 상태 인지 확인 하세요.

### <a name="event-1580-res_netname_dns_registration_secure_zone_failed"></a>이벤트 1580: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 보안 DNS 영역에서 ' %4 ' 어댑터를 통해 이름 ' %2 '을 (를) 등록 하지 못했습니다. 이는이 이름의 기존 레코드와 클러스터 id에 해당 레코드를 업데이트할 수 있는 권한이 없기 때문입니다. 오류 코드는 ' %3 '입니다. Dns 서버 관리자에 게 문의 하 여 클러스터 id에 DNS 레코드 ' %2 '에 대 한 권한이 있는지 확인 하십시오.

### <a name="event-1580-res_netname_dns_registration_secure_zone_failed"></a>이벤트 1580: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 보안 DNS 영역에서 ' %4 ' 어댑터를 통해 이름 ' %2 '을 (를) 등록 하지 못했습니다. 이는이 이름의 기존 레코드와 클러스터 id에 해당 레코드를 업데이트할 수 있는 권한이 없기 때문입니다. 오류 코드는 ' %3 '입니다. Dns 서버 관리자에 게 문의 하 여 클러스터 id에 DNS 레코드 ' %2 '에 대 한 권한이 있는지 확인 하십시오.

### <a name="event-1585-res_fileserver_fscheck_srvsvc_stopped"></a>이벤트 1585: RES_FILESERVER_FSCHECK_SRVSVC_STOPPED

클러스터 파일 서버 리소스 ' %1 '이 (가) 상태 검사에 실패 했습니다. 서버 서비스가 시작 되지 않았기 때문입니다. 서버 관리자를 사용 하 여이 클러스터 노드에 있는 서버 서비스의 상태를 확인 하십시오.

### <a name="event-1586-res_fileserver_fscheck_scoped_name_not_registered"></a>이벤트 1586: RES_FILESERVER_FSCHECK_SCOPED_NAME_NOT_REGISTERED

클러스터 파일 서버 리소스 ' %1 '이 (가) 상태 검사에 실패 했습니다. 공유 폴더 중 일부에 액세스할 수 없기 때문입니다. 클라이언트에서 폴더에 액세스할 수 있는지 확인 합니다. 또한 서버 관리자를 사용 하 여이 클러스터 노드에서 서버 서비스의 상태를 확인 하 고이 클러스터 노드의 서버 서비스와 관련 된 다른 이벤트를 찾아보십시오. 이 클러스터 된 역할에서 네트워크 이름 리소스 ' %2 '을 (를) 다시 시작 해야 할 수 있습니다.

### <a name="event-1587-res_fileserver_fscheck_failed"></a>이벤트 1587: RES_FILESERVER_FSCHECK_FAILED

클러스터 파일 서버 리소스 ' %1 '이 (가) 상태 검사에 실패 했습니다. 공유 폴더 중 일부에 액세스할 수 없기 때문입니다. 클라이언트에서 폴더에 액세스할 수 있는지 확인 합니다. 또한 서버 관리자를 사용 하 여이 클러스터 노드에서 서버 서비스의 상태를 확인 하 고이 클러스터 노드의 서버 서비스와 관련 된 다른 이벤트를 찾아보십시오.

### <a name="event-1588-res_fileserver_share_cant_add"></a>이벤트 1588: RES_FILESERVER_SHARE_CANT_ADD

클러스터 파일 서버 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 리소스가 네트워크 이름 ' %3 '과 (와) 연결 된 파일 공유 ' %2 '을 (를) 만들지 못했습니다. 오류 코드는 ' %4 '입니다. 폴더가 존재 하며 액세스할 수 있는지 확인 하십시오. 또한 서버 관리자를 사용 하 여이 클러스터 노드에서 서버 서비스의 상태를 확인 하 고이 클러스터 노드에서 다른 관련 이벤트를 찾아보십시오. 이 클러스터 된 역할에서 네트워크 이름 리소스 ' %3 '을 (를) 다시 시작 해야 할 수 있습니다.

### <a name="event-1600-clusapi_create_cannot_set_ad_dacl"></a>이벤트 1600: CLUSAPI_CREATE_CANNOT_SET_AD_DACL

클러스터 서비스에서 ' %1 ' 클러스터 컴퓨터 개체에 대 한 사용 권한을 설정 하지 못했습니다. 네트워크 관리자에 게 문의 하 여 Active Directory 컴퓨터 개체의 클러스터 보안 설명자를 확인 하 고, DACL이 너무 크지 않은지 확인 하 고, 필요한 경우 개체에서 불필요 한 추가 ACE를 제거 하십시오.

### <a name="event-1603-res_fileserver_clone_failed"></a>이벤트 1603: RES_FILESERVER_CLONE_FAILED

' 네트워크 이름 ' 리소스에 대 한 예상 종속성이 없거나 제대로 구성 되지 않았으므로 파일 서버를 시작할 수 없습니다. 오류 = 0x %2.

### <a name="event-1606-res_disk_cno_check_failed"></a>이벤트 1606: RES_DISK_CNO_CHECK_FAILED

클러스터 디스크 리소스 ' %1 '에 BitLocker로 보호 된 볼륨 ' %2 '이 (가) 포함 되어 있지만이 볼륨의 Active Directory 클러스터 이름 계정 (클러스터 이름 개체 또는 CNO 라고도 함)이 볼륨에 대 한 BitLocker 보호기가 아닙니다. BitLocker로 보호 되는 볼륨에 필요 합니다. 이를 해결 하려면 먼저 클러스터에서 디스크를 제거 합니다. 그런 다음 Manage-bde.exe 명령줄 도구를 사용 하 여 클러스터 이름에 대 한 도메인 ClusterName 형식을 사용 하 여 클러스터 이름을 ADAccountOrGroup 보호기로 추가 \\ \$ 합니다. 그런 다음 클러스터에 디스크를 다시 추가 합니다. 자세한 내용은 Manage-bde.exe에 대 한 설명서를 참조 하세요.

### <a name="event-1607-res_disk_cno_unlock_failed"></a>이벤트 1607: RES_DISK_CNO_UNLOCK_FAILED

클러스터 디스크 리소스 ' %1 '이 (가) BitLocker로 보호 되는 볼륨 ' %2 '의 잠금을 해제할 수 없습니다. 클러스터 이름 개체 (CNO)가이 볼륨의 유효한 BitLocker 보호기로 설정 되어 있지 않습니다. 이를 해결 하려면 클러스터에서 디스크를 제거 합니다. 그런 다음 Manage-bde.exe 명령줄 도구를 사용 하 여 도메인 ClusterName 형식을 사용 하 여 클러스터 이름을 ADAccountOrGroup 보호기로 추가 하 \\ \$ 고 디스크를 클러스터에 다시 추가 합니다. 자세한 내용은 Manage-bde.exe에 대 한 설명서를 참조 하세요.

### <a name="event-1608-res_fileserver_leader_failed"></a>이벤트 1608: RES_FILESERVER_LEADER_FAILED

' 네트워크 이름 ' 리소스에 대 한 예상 종속성이 없거나 제대로 구성 되지 않았으므로 파일 서버를 시작할 수 없습니다. 오류 = 0x %2.

### <a name="event-1609-res_soda_fileserver_leader_failed"></a>이벤트 1609: RES_SODA_FILESERVER_LEADER_FAILED

' 분산 네트워크 이름 ' 리소스에 대 한 예상 종속성이 없거나 제대로 구성 되지 않았기 때문에 Scale Out 파일 서버를 시작할 수 없습니다. 오류 = 0x %2.

### <a name="event-1632-clusapi_create_mismatched_ou"></a>이벤트 1632: CLUSAPI_CREATE_MISMATCHED_OU

클러스터를 만들지 못했습니다. Active directory 조직 구성 단위 ' %2 '에서 클러스터 이름 개체 ' %1 '을 (를) 만들 수 없습니다. ' %3 ' 조직 구성 단위에 개체가 이미 있습니다. 지정 된 고유 이름 경로 및 클러스터 이름 개체가 올바른지 확인 합니다. 고유 이름 경로를 지정 하지 않으면 기존 컴퓨터 개체 ' %1 '이 (가) 사용 됩니다.

### <a name="event-1652-service_tcp_connection_failure"></a>이벤트 1652: SERVICE_TCP_CONNECTION_FAILURE

클러스터 노드 ' %1 '이 (가) 클러스터에 연결 하지 못했습니다. 노드 ' %2 '에 대 한 TCP 연결을 설정할 수 없습니다. 네트워크 연결 및 네트워크 방화벽의 구성을 확인 합니다.

### <a name="event-1652-service_udp_connection_failure"></a>이벤트 1652: SERVICE_UDP_CONNECTION_FAILURE

클러스터 노드 ' %1 '이 (가) 클러스터에 연결 하지 못했습니다. ' %2 ' 노드에 대 한 UDP 연결을 설정할 수 없습니다. 네트워크 연결 및 네트워크 방화벽의 구성을 확인 합니다.

### <a name="event-1652-service_virtual_tcp_connection_failure"></a>이벤트 1652: SERVICE_VIRTUAL_TCP_CONNECTION_FAILURE

클러스터 노드 ' %1 '이 (가) 클러스터에 연결 하지 못했습니다. Microsoft 장애 조치 (Failover) 클러스터 가상 어댑터를 사용 하는 TCP 연결을 ' %2 ' 노드에 설정할 수 없습니다. 네트워크 연결 및 네트워크 방화벽의 구성을 확인 합니다.

### <a name="event-1653-service_no_connectivity"></a>이벤트 1653: SERVICE_NO_CONNECTIVITY

클러스터 노드 ' %1 '은 (는) 네트워크를 통해 클러스터의 다른 노드와 통신할 수 없으므로 클러스터에 참가 하지 못했습니다. 네트워크 연결 및 네트워크 방화벽의 구성을 확인 합니다.

### <a name="event-1654-res_vipaddr_invalid_adaptername"></a>이벤트 1654: RES_VIPADDR_INVALID_ADAPTERNAME

클러스터 비연속 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 네트워크 어댑터 ' %2 '에 해당 하는 네트워크 어댑터에 대 한 구성 데이터를 확인할 수 없습니다 (오류 코드는 ' %3 '). IP 주소 리소스가 올바른 주소 및 네트워크 속성으로 구성 되어 있는지 확인 하십시오.

### <a name="event-1655-res_vipaddr_invalid_vsid"></a>이벤트 1655: RES_VIPADDR_INVALID_VSID

클러스터 비연속 IP 주소 리소스 ' %1 '을 (를) 온라인 상태로 만들지 못했습니다. 가상 서브넷 Id ' %2 ' 및 라우팅 도메인 Id ' %3 '에 해당 하는 네트워크 어댑터에 대 한 구성 데이터를 확인할 수 없습니다 (오류 코드는 ' %4 '). IP 주소 리소스가 올바른 주소 및 네트워크 속성으로 구성 되어 있는지 확인 하십시오.

### <a name="event-1656-res_vipaddr_address_create_failed"></a>이벤트 1656: RES_VIPADDR_ADDRESS_CREATE_FAILED

비연속 IP 주소 리소스 ' %1 '에 대 한 IP 주소 ' %2 '을 (를) 추가 하지 못했습니다 (오류 코드는 ' %3 '). 실제 또는 가상 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다.

### <a name="event-1664-cluster_upgrade_incomplete"></a>이벤트 1664: CLUSTER_UPGRADE_INCOMPLETE

클러스터의 기능 수준을 업그레이드 하지 못했습니다. 클러스터의 모든 노드가 현재 실행 중이 고 동일한 버전의 Windows Server 인지 확인 한 다음 ClusterFunctionalLevel Windows PowerShell cmdlet을 다시 실행 합니다.

### <a name="event-1676-event_local_node_quarantined"></a>이벤트 1676: EVENT_LOCAL_NODE_QUARANTINED

로컬 클러스터 노드가 ' %1 ' (으)로 격리 되었습니다. 노드가 ' %2 '까지 격리 된 후 노드가 자동으로 클러스터를 다시 조인 하려고 시도 합니다.
<br><br>이 노드의 문제를 확인 하려면 시스템 및 응용 프로그램 이벤트 로그를 참조 하십시오. 문제가 해결 되 면 격리를 수동으로 지우면 노드가 ' Start-clusternode – ClearQuarantine ' Windows PowerShell cmdlet과 다시 가입할 수 있습니다.<br><br>QuarantineType: %1에 의해 격리 됨<br>시간 격리가 자동으로 지워집니다. %2

### <a name="event-1677-event_node_drain_failed"></a>이벤트 1677: EVENT_NODE_DRAIN_FAILED

노드 드레이닝이 클러스터 노드 %1에 실패 했습니다. <br><br>노드의 시스템 및 응용 프로그램 이벤트 로그와 클러스터 로그를 참조 하 여 드레이닝 오류의 원인을 조사 합니다. 문제가 해결 되 면 드레이닝 작업을 다시 시도할 수 있습니다.

### <a name="event-1683-res_netname_computer_account_no_dc"></a>이벤트 1683: RES_NETNAME_COMPUTER_ACCOUNT_NO_DC

클러스터 서비스가 도메인에서 사용 가능한 도메인 컨트롤러에 연결할 수 없습니다. 이는 클러스터 네트워크 이름 인증에 따라 달라 지는 기능에 영향을 줄 수 있습니다.<br><br>DC 서버: %1

#### <a name="guidance"></a>지침

네트워크에서 클러스터 노드에 대해 도메인 컨트롤러에 액세스할 수 있는지 확인 합니다.

### <a name="event-1684-res_netname_computer_object_vco_not_found"></a>이벤트 1684: RES_NETNAME_COMPUTER_OBJECT_VCO_NOT_FOUND

클러스터 네트워크 이름 리소스가 Active Directory에서 연결 된 컴퓨터 개체를 찾지 못했습니다. 이는 클러스터 네트워크 이름 인증에 따라 달라 지는 기능에 영향을 줄 수 있습니다.<br><br>네트워크 이름: %1<br>조직 구성 단위: %2

#### <a name="guidance"></a>지침

Active Directory 휴지통에서 네트워크 이름에 대 한 컴퓨터 개체를 복원 합니다. 또는 클러스터 네트워크 이름 리소스를 오프 라인으로 전환 하 고 복구 작업을 실행 하 여 Active Directory에 컴퓨터 개체를 다시 만듭니다.

### <a name="event-1685-res_netname_computer_object_cno_not_found"></a>이벤트 1685: RES_NETNAME_COMPUTER_OBJECT_CNO_NOT_FOUND

클러스터 네트워크 이름 리소스가 Active Directory에서 연결 된 컴퓨터 개체를 찾지 못했습니다. 이는 클러스터 네트워크 이름 인증에 따라 달라 지는 기능에 영향을 줄 수 있습니다.<br><br>네트워크 이름: %1<br>조직 구성 단위: %2
#### <a name="guidance"></a>지침

Active Directory 휴지통에서 네트워크 이름에 대 한 컴퓨터 개체를 복원 합니다.

### <a name="event-1686-res_netname_computer_object_vco_disabled"></a>이벤트 1686: RES_NETNAME_COMPUTER_OBJECT_VCO_DISABLED

클러스터 네트워크 이름 리소스가 사용 하지 않도록 설정 된 Active Directory에서 연결 된 컴퓨터 개체를 찾았습니다. 이는 클러스터 네트워크 이름 인증에 따라 달라 지는 기능에 영향을 줄 수 있습니다.<br><br>네트워크 이름: %1<br>조직 구성 단위: %2

#### <a name="guidance"></a>지침

Active Directory에서 네트워크 이름에 대 한 컴퓨터 개체를 사용 하도록 설정 합니다.

### <a name="event-1687-res_netname_computer_object_cno_disabled"></a>이벤트 1687: RES_NETNAME_COMPUTER_OBJECT_CNO_DISABLED

클러스터 네트워크 이름 리소스가 사용 하지 않도록 설정 된 Active Directory에서 연결 된 컴퓨터 개체를 찾았습니다. 이는 클러스터 네트워크 이름 인증에 따라 달라 지는 기능에 영향을 줄 수 있습니다.<br><br>네트워크 이름: %1<br>조직 구성 단위: %2

#### <a name="guidance"></a>지침

Active Directory에서 네트워크 이름에 대 한 컴퓨터 개체를 사용 하도록 설정 합니다. 또는 클러스터 네트워크 이름 리소스를 오프 라인으로 전환 하 고 복구 작업을 실행 하 여 Active Directory에서 컴퓨터 개체를 사용 하도록 설정 합니다.

### <a name="event-1688-res_netname_computer_object_failed"></a>이벤트 1688: RES_NETNAME_COMPUTER_OBJECT_FAILED

클러스터 네트워크 이름 리소스가 Active Directory의 연결 된 컴퓨터 개체를 사용 하지 않도록 설정 하 고 사용 하도록 설정 하지 못했음을 검색 했습니다. 이는 클러스터 네트워크 이름 인증에 따라 달라 지는 기능에 영향을 줄 수 있습니다.<br><br>네트워크 이름: %1<br>조직 구성 단위: %2

#### <a name="guidance"></a>지침

Active Directory에서 네트워크 이름에 대 한 컴퓨터 개체를 사용 하도록 설정 합니다.

### <a name="event-4608-nodecleanup_get_clustered_disks_failed"></a>이벤트 4608: NODECLEANUP_GET_CLUSTERED_DISKS_FAILED

클러스터를 삭제 하는 동안 클러스터 된 디스크 목록을 검색 하지 못했습니다 클러스터 서비스. 오류 코드는 ' %1 '입니다. 이러한 디스크에 액세스할 수 없는 경우 ' Clear-ClusterDiskReservation ' PowerShell cmdlet을 실행 합니다.

### <a name="event-4611-nodecleanup_release_clustered_disks_from_partmgr_failed"></a>이벤트 4611: NODECLEANUP_RELEASE_CLUSTERED_DISKS_FROM_PARTMGR_FAILED

클러스터를 삭제 하는 동안 ID가 ' %2 ' 인 클러스터 된 디스크를 파티션 관리자에서 해제 하지 않았습니다. 오류 코드는 ' %1 '입니다. 컴퓨터를 다시 시작 하면 파티션 관리자가 디스크를 해제 하 게 됩니다.

### <a name="event-4613-nodecleanup_clear_clusdisk_database_failed"></a>이벤트 4613: NODECLEANUP_CLEAR_CLUSDISK_DATABASE_FAILED

클러스터를 삭제 하는 동안 클러스터 서비스에서 ID가 ' %2 ' 인 클러스터 된 디스크를 제대로 정리 하지 못했습니다. 오류 코드는 ' %1 '입니다. 정리가 성공적으로 완료 될 때까지이 디스크에 액세스할 수 없습니다. 수동 정리의 경우 \\ Windows 레지스트리에서 ' HKEY_LOCAL_MACHINE SYSTEM \\ CurrentControlSet \\ Services \\ ClusDisk \\ Parameters ' 키의 ' AttachedDisks ' 값을 삭제 합니다.

### <a name="event-4615-nodecleanup_disable_cluster_service_failed"></a>이벤트 4615: NODECLEANUP_DISABLE_CLUSTER_SERVICE_FAILED

클러스터 서비스가 중지 되었으며 클러스터 노드 정리의 일부로 비활성으로 설정 되었습니다.

### <a name="event-4616-nodecleanup_disable_cluster_service_timeout"></a>이벤트 4616: NODECLEANUP_DISABLE_CLUSTER_SERVICE_TIMEOUT

클러스터 노드 정리 중 클러스터 서비스가 예상 된 기간 내에 완료 되지 않았습니다. 클러스터 서비스가 더 이상 실행 되 고 있지 않은지 확인 하려면이 컴퓨터를 다시 시작 하세요.

### <a name="event-4618-nodecleanup_reset_cluster_registry_entries_failed"></a>이벤트 4618: NODECLEANUP_RESET_CLUSTER_REGISTRY_ENTRIES_FAILED

클러스터 노드를 정리 하는 동안 클러스터 서비스 레지스트리 항목을 다시 설정 하지 못했습니다.
오류 코드는 ' %1 '입니다. 정리가 성공적으로 완료 될 때까지이 컴퓨터에서 클러스터를 만들거나 조인할 수 없습니다. 수동 정리의 경우이 컴퓨터에서 ' Start-clusternode ' PowerShell cmdlet을 실행 합니다.

### <a name="event-4620-nodecleanup_unload_cluster_hive_failed"></a>이벤트 4620: NODECLEANUP_UNLOAD_CLUSTER_HIVE_FAILED

클러스터 노드를 정리 하는 동안 클러스터 서비스 레지스트리 하이브를 언로드하지 못했습니다.
오류 코드는 ' %1 '입니다. 정리가 성공적으로 완료 될 때까지이 컴퓨터에서 클러스터를 만들거나 조인할 수 없습니다. 수동 정리의 경우이 컴퓨터에서 ' Start-clusternode ' PowerShell cmdlet을 실행 합니다.

### <a name="event-4622-nodecleanup_errors"></a>이벤트 4622: NODECLEANUP_ERRORS

노드 정리 중에 클러스터 서비스 오류가 발생 했습니다. 정리가 성공적으로 완료 될 때까지이 컴퓨터에서 클러스터를 만들거나 조인할 수 없습니다. 이 노드에서 ' Start-clusternode ' PowerShell cmdlet을 사용 합니다.

### <a name="event-4624-nodecleanup_reset_nlbsflags_failed"></a>이벤트 4624: NODECLEANUP_RESET_NLBSFLAGS_FAILED

클러스터 노드를 정리 하는 동안 IPSec 보안 연결 시간 제한 레지스트리 값을 다시 설정 하지 못했습니다. 오류 코드는 ' %1 '입니다. 수동 정리의 경우이 컴퓨터에서 ' Start-clusternode ' PowerShell cmdlet을 실행 합니다. 또는 Windows 레지스트리의 HKEY_LOCAL_MACHINE에서 ' %2 ' 값 및 ' %3 ' 값을 삭제 하 여 IPSec 보안 연결 시간 제한을 다시 설정할 수 있습니다.

### <a name="event-4627-nodecleanup_delete_cluster_tasks_failed"></a>이벤트 4627: NODECLEANUP_DELETE_CLUSTER_TASKS_FAILED

노드 정리 중 클러스터형 태스크를 삭제 하지 못했습니다. 오류 코드는 ' %1 '입니다.
Windows 작업 스케줄러를 사용 하 여 나머지 클러스터 된 작업을 삭제 합니다.

### <a name="event-4629-nodecleanup_delete_local_account_failed"></a>이벤트 4629: NODECLEANUP_DELETE_LOCAL_ACCOUNT_FAILED

노드 정리 중에는 클러스터에서 관리 하는 로컬 사용자 계정이 삭제 되지 않습니다. 오류 코드는 ' %1 '입니다. 로컬 사용자 및 그룹 (lusrmgr.msc)을 열어 계정을 삭제 합니다.

### <a name="event-4864-res_vsstask_open_failed"></a>이벤트 4864: RES_VSSTASK_OPEN_FAILED

볼륨 섀도 복사본 서비스 작업 리소스 ' %1 '을 (를) 만들지 못했습니다. 오류 코드는 ' %2 '입니다.

### <a name="event-4865-res_vsstask_terminate_task_failed"></a>이벤트 4865: RES_VSSTASK_TERMINATE_TASK_FAILED

볼륨 섀도 복사본 서비스 작업 리소스 ' %1 '이 (가) 실패 했습니다. 오류 코드는 ' %2 '입니다.
이는 연결 된 작업을 오프 라인 작업의 일부로 중지할 수 없기 때문입니다. 작업 스케줄러 스냅인을 사용 하 여 수동으로 중지 해야 할 수도 있습니다.

### <a name="event-4866-res_vsstask_delete_task_failed"></a>이벤트 4866: RES_VSSTASK_DELETE_TASK_FAILED

볼륨 섀도 복사본 서비스 작업 리소스 ' %1 '이 (가) 실패 했습니다. 오류 코드는 ' %2 '입니다.
오프 라인 작업의 일부로 연결 된 작업을 삭제할 수 없기 때문입니다. 작업 스케줄러 스냅인을 사용 하 여 수동으로 삭제 해야 할 수도 있습니다.

### <a name="event-4867-res_vsstask_online_failed"></a>이벤트 4867: RES_VSSTASK_ONLINE_FAILED

볼륨 섀도 복사본 서비스 작업 리소스 ' %1 '이 (가) 실패 했습니다. 오류 코드는 ' %2 '입니다.
온라인 작업의 일부로 연결 된 작업을 추가할 수 없기 때문입니다. 작업 스케줄러 스냅인을 사용 하 여 작업이 올바르게 구성 되었는지 확인 하십시오.

### <a name="event-4868-unable_to_start_autologger"></a>이벤트 4868: UNABLE_TO_START_AUTOLOGGER

클러스터 서비스에서 클러스터 로그 추적 세션을 시작 하지 못했습니다. 오류 코드는 ' %2 '입니다. 클러스터가 제대로 작동 하지만 보완 로깅 정보가 누락 됩니다. 성능 모니터 스냅인을 사용 하 여 ' %1 '에 대 한 이벤트 채널 설정을 확인 하십시오.

### <a name="event-4869-netft_watchdog_process_hung"></a>이벤트 4869: NETFT_WATCHDOG_PROCESS_HUNG

사용자 모드 상태 모니터링에서 시스템이 응답 하지 않음을 감지 했습니다. 장애 조치 (Failover) 클러스터 가상 어댑터가 ' %3 ' 초 동안 프로세스 ID가 ' %2 ' 인 ' %1 ' 프로세스와의 연결이 끊어졌습니다. 성능 모니터를 사용 하 여 시스템 상태를 평가 하 고 시스템에 부정적인 영향을 미칠 수 있는 프로세스를 확인 하세요.

### <a name="event-4870-netft_watchdog_process_terminated"></a>이벤트 4870: NETFT_WATCHDOG_PROCESS_TERMINATED

사용자 모드 상태 모니터링에서 시스템이 응답 하지 않음을 감지 했습니다. 장애 조치 (Failover) 클러스터 가상 어댑터가 ' %3 ' 초 동안 프로세스 ID가 ' %2 ' 인 ' %1 ' 프로세스와의 연결이 끊어졌습니다. 복구 작업이 수행 됩니다.

### <a name="event-4871-netft_miniport_initialization_failure"></a>이벤트 4871: NETFT_MINIPORT_INITIALIZATION_FAILURE

클러스터 서비스를 시작 하지 못했습니다. 장애 조치 (failover) 클러스터 가상 어댑터가 미니 포트 어댑터를 초기화 하지 못했기 때문입니다. 오류 코드는 ' %1 '입니다. 다른 네트워크 어댑터가 제대로 작동 하는지 확인 하 고 장치 관리자에서 오류를 확인 하십시오. 구성이 변경 된 경우이 컴퓨터에 장애 조치 (failover) 클러스터링 기능을 다시 설치 해야 할 수 있습니다.

### <a name="event-4872-netft_missing_datalink_address"></a>이벤트 4872: NETFT_MISSING_DATALINK_ADDRESS

장애 조치 (failover) 클러스터 가상 어댑터가 고유 MAC 주소를 생성 하지 못했습니다.
고유 주소를 생성할 실제 이더넷 어댑터를 찾지 못했습니다. 또는 생성 된 주소가이 컴퓨터의 다른 어댑터와 충돌 합니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 하세요.

### <a name="event-5122-dcm_event_root_creation_failed"></a>이벤트 5122: DCM_EVENT_ROOT_CREATION_FAILED

클러스터 서비스에서 클러스터 공유 볼륨 루트 디렉터리 ' %2 '을 (를) 만들지 못했습니다.
오류 메시지는 ' %1 '입니다.

### <a name="event-5142-dcm_volume_no_access"></a>이벤트 5142: DCM_VOLUME_NO_ACCESS

오류 ' %3 ' (으)로 인해이 클러스터 노드에서 클러스터 공유 볼륨 ' %1 ' (' %2 ')에 더 이상 액세스할 수 없습니다. 저장소 장치 및 네트워크 연결에 대 한이 노드의 연결 문제를 해결 하세요.

### <a name="event-5143-dcm_veto_resource_move_due_to_cc"></a>이벤트 5143: DCM_VETO_RESOURCE_MOVE_DUE_TO_CC

잠재적인 교착 상태를 방지 하기 위해 노드 ' %1 '에 대 한 캐시 관리자의 현재 상태에 따라 디스크 이동 (' %2 ')이 거부 되었습니다. ' Cache Manager 더티 페이지 ' is %3, ' Cache Manager 더티 페이지 '는 %4입니다. ' Cache Manager 더티 페이지 '가 ' Cache Manager 더티 페이지 '의 70% 미만이 고 ' Cache Manager 더티 페이지가 ' 빼기 ' 캐시 관리자 더티 페이지 '가 128000 페이지 보다 큰 경우에는 이동이 허용 됩니다 (페이지 크기가 4096 바이트인 경우 500MB).
이 디스크의 클러스터 공유 볼륨을 일시 중지 하는 동안 캐시 관리자에서 버퍼링 된 쓰기를 제한 하기 때문에 잠재적인 교착 상태를 방지 하기 위해 클러스터에서 리소스 이동을 거부 했습니다.

### <a name="event-5144-dcm_snapshot_diff_area_failure"></a>이벤트 5144: DCM_SNAPSHOT_DIFF_AREA_FAILURE

디스크 (' %1 ')를 클러스터 공유 볼륨에 추가 하는 동안 ' %3 ' 오류로 인해 볼륨 (' %2 ')에 대 한 명시적 스냅숏 diff 영역 연결을 설정 하지 못했습니다. 클러스터 공유 볼륨에 대해 유일 하 게 지원 되는 소프트웨어 스냅숏 diff 영역 연결은 자체입니다.

### <a name="event-5145-dcm_snapshot_diff_area_delete_failure"></a>이벤트 5145: DCM_SNAPSHOT_DIFF_AREA_DELETE_FAILURE

클러스터 디스크 리소스 ' %1 '이 (가) 소프트웨어 스냅숏을 삭제 하지 못했습니다. 볼륨 ' %3 '의 diff 영역을 ' %2 ' 볼륨에서 분리 하지 못했습니다. 이는 활성 스냅숏으로 인 한 것일 수 있습니다. 클러스터 공유 볼륨을 사용 하려면 소프트웨어 스냅숏이 동일한 디스크에 위치 해야 합니다.

### <a name="event-5146-dcm_veto_resource_move_due_to_dismount"></a>이벤트 5146: DCM_VETO_RESOURCE_MOVE_DUE_TO_DISMOUNT

리소스에 속하는 볼륨 중 하나가 분리 된 상태 여 서 클러스터 공유 볼륨 리소스 ' %1 '의 이동이 거부 되었습니다. 분리 작업이 완료 된 후 작업을 다시 시도 하세요.

### <a name="event-5147-dcm_veto_resource_move_due_to_snapshot"></a>이벤트 5147: DCM_VETO_RESOURCE_MOVE_DUE_TO_SNAPSHOT

리소스에 속하는 볼륨 중 하나가 분리 된 상태 여 서 클러스터 공유 볼륨 리소스 ' %1 '의 이동이 거부 되었습니다. 분리 작업이 완료 된 후 작업을 다시 시도 하세요.

### <a name="event-5148-dcm_veto_resource_move_due_to_io_mode_change"></a>이벤트 5148: DCM_VETO_RESOURCE_MOVE_DUE_TO_IO_MODE_CHANGE

리소스에 속하는 볼륨 중 하나에서 IO 모드 변경 작업 (직접 IO를 리디렉션된 IO로 또는 그 반대로)이 진행 중 이므로 클러스터 공유 볼륨 리소스 ' %1 '의 이동이 거부 되었습니다. 작업이 완료 된 후 작업을 다시 시도 하세요.

### <a name="event-5150-dcm_set_resource_in_failed_state"></a>이벤트 5150: DCM_SET_RESOURCE_IN_FAILED_STATE

클러스터 물리적 디스크 리소스 ' %1 '이 (가) 실패 했습니다. ' %2 ' 오류가 발생 하 여 클러스터 공유 볼륨 실패 상태로 전환 되었습니다.

### <a name="event-5200-cam_cannot_create_cno_token"></a>이벤트 5200: CAM_CANNOT_CREATE_CNO_TOKEN

클러스터 서비스 클러스터 공유 볼륨에 대 한 클러스터 id 토큰을 만들지 못했습니다. 오류 코드는 ' %1 '입니다. 도메인 컨트롤러에 액세스할 수 있는지 확인 하 고 연결 문제가 있는지 확인 하십시오. 도메인 컨트롤러에 대 한 연결이 복구 될 때까지 클러스터 공유 볼륨에 대해이 노드에 대 한 일부 작업이 실패할 수 있습니다.

### <a name="event-5216-csv_sw_snapshot_failed"></a>이벤트 5216: CSV_SW_SNAPSHOT_FAILED

%3 오류로 인해 클러스터 공유 볼륨 ' %1 ' (' %2 ')에서 소프트웨어 스냅숏을 만들지 못했습니다. 스냅숏 생성을 지원 하려면 리소스가 온라인 상태 여야 합니다. 리소스의 상태를 확인 하세요.

### <a name="event-5217-csv_sw_snapshot_set_failed"></a>이벤트 5217: CSV_SW_SNAPSHOT_SET_FAILED

' %3 ' 오류로 인해 스냅숏 집합 id가 ' %2 ' 인 클러스터 공유 볼륨 (' %1 ')에 대 한 소프트웨어 스냅숏을 만들지 못했습니다. CSV 리소스의 상태와 리소스 소유자 노드의 시스템 이벤트를 확인 하십시오.

### <a name="event-5219-csv_register_snapshot_prov_with_vss_failed"></a>이벤트 5219: CSV_REGISTER_SNAPSHOT_PROV_WITH_VSS_FAILED

클러스터 서비스에서 VSS (볼륨 섀도 서비스)를 사용 하 여 클러스터 공유 볼륨 스냅숏 공급자를 등록 하지 못했습니다. 이 문제는 VSS 서비스가 종료 되었거나 VSS 서비스에서 들어오는 요청을 허용 하지 않는 문제가 발생 한 경우에 발생할 수 있습니다. <br>오류: %1

### <a name="event-5377-operation_exceeded_timeout"></a>이벤트 5377: OPERATION_EXCEEDED_TIMEOUT

내부 클러스터 서비스 작업에서 정의 된 임계값 ' %2 ' 초를 초과 했습니다. 클러스터 서비스 복구 하기 위해 종료 되었습니다. 서비스 제어 관리자는 클러스터 서비스를 다시 시작 하 고 노드는 클러스터에 다시 가입 됩니다.

### <a name="event-5396-two_partitions_have_quorum"></a>이벤트 5396: TWO_PARTITIONS_HAVE_QUORUM

쿼럼이 있는 다른 클러스터 노드가 있음을 감지 했으므로이 노드의 클러스터 서비스을 종료 하 고 있습니다. 이는 클러스터 서비스 쿼럼 강제 스위치 (/fq)로 시작 된 다른 노드를 검색 한 경우에 발생 합니다. 강제 쿼럼 스위치를 사용 하 여 시작 된 노드는 계속 실행 됩니다. 클러스터 서비스가 다시 시작 될 때이 노드가 자동으로 클러스터에 조인 되었는지 확인 하려면 장애 조치(Failover) 클러스터 관리자을 사용 합니다.

### <a name="event-5397-rlua_account_failed"></a>이벤트 5397: RLUA_ACCOUNT_FAILED

클러스터 리소스 ' %1 '이 (가)이 노드에서 복제 된 로컬 사용자 계정 ' %2 '을 (를) 만들거나 수정할 수 없습니다. 자세한 내용은 클러스터 로그를 확인 하십시오.

### <a name="event-5398-nm_event_cluster_failed_to_form"></a>이벤트 5398: NM_EVENT_CLUSTER_FAILED_TO_FORM

클러스터를 시작 하지 못했습니다. 클러스터를 시작 하려는 노드 집합 내에서 클러스터 구성 데이터의 최신 복사본을 사용할 수 없습니다. 노드 집합이 멤버 자격에 있지 않고 구성 데이터 업데이트를 받을 수 없어 클러스터에 대 한 변경 내용이 발생 했습니다. .<br><br>클러스터를 시작 하는 데 필요한 응답: %1<br>사용 가능한 투표: %2<br>응답이 있는 노드: %3

#### <a name="guidance"></a>지침

클러스터의 모든 노드에서 클러스터 서비스를 시작 하 여 클러스터 구성 데이터의 최신 복사본을 포함 하는 노드가 먼저 클러스터를 구성할 수 있도록 합니다. 클러스터를 시작할 수 있으며 노드에서 업데이트 된 클러스터 구성 데이터를 자동으로 가져옵니다. 클러스터 구성 데이터의 최신 복사본에 사용할 수 있는 노드가 없으면 ' Start-clusternode-FQ ' Windows PowerShell cmdlet을 실행 합니다. FQ (클러스터가 forcequorum) 매개 변수를 사용 하 여 클러스터 서비스를 시작 하 고이 노드의 클러스터 구성 데이터 복사본을 신뢰할 수 있는 것으로 표시 합니다. 클러스터 데이터베이스의 오래 된 복사본을 사용 하 여 노드에 쿼럼을 강제 적용 하면 노드가 클러스터에 참가 하지 않는 동안 클러스터 구성 변경이 발생할 수 있습니다.

## <a name="warning-events"></a>경고 이벤트

### <a name="event-1011-nm_node_evicted"></a>이벤트 1011: NM_NODE_EVICTED

클러스터 노드 %1이 (가) 장애 조치 (failover) 클러스터에서 제거 되었습니다.

### <a name="event-1045-res_ipaddr_ipv4_address_create_failed"></a>이벤트 1045: RES_IPADDR_IPV4_ADDRESS_CREATE_FAILED

리소스 ' %1 '의 IP 주소 ' %2 '에 대해 일치 하는 네트워크 인터페이스를 찾을 수 없습니다 (반환 코드는 ' %3 '). 클러스터 노드가 다른 서브넷에 걸쳐 있는 경우이는 정상적인 것일 수 있습니다.

### <a name="event-1066-res_disk_corrupt_disk"></a>이벤트 1066: RES_DISK_CORRUPT_DISK

클러스터 디스크 리소스 ' %1 '이 (가) 볼륨 ' %2 '에 대 한 손상을 나타냅니다. Chkdsk를 실행 하 여 문제를 복구 합니다. Chkdsk가 완료 될 때까지 디스크를 사용할 수 없습니다.
Chkdsk 출력이 ' %3 ' 파일에 기록 됩니다.<br> Chkdsk는 응용 프로그램 이벤트 로그에 정보를 기록할 수도 있습니다.

### <a name="event-1068-res_smb_share_cant_add"></a>이벤트 1068: RES_SMB_SHARE_CANT_ADD

클러스터 파일 공유 리소스 ' %1 '을 (를) 온라인 상태로 만들 수 없습니다. 오류 ' %4 ' (으)로 인해 파일 공유 ' %2 ' (네트워크 이름 %3)을 (를) 만들지 못했습니다. 이 작업은 자동으로 다시 시도 됩니다.

### <a name="event-1071-rcm_resource_online_blocked_by_locked_mode"></a>이벤트 1071: RCM_RESOURCE_ONLINE_BLOCKED_BY_LOCKED_MODE

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '에 대해 시도 된 작업을 완료 하지 못했습니다. 리소스 또는 해당 공급자 중 하나가 잠금 상태입니다.

### <a name="event-1071-rcm_resource_offline_blocked_by_locked_mode"></a>이벤트 1071: RCM_RESOURCE_OFFLINE_BLOCKED_BY_LOCKED_MODE

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '에 대해 시도 된 작업을 완료 하지 못했습니다. 리소스 또는 해당 종속 항목 중 하나가 잠긴 상태입니다.

### <a name="event-1094-sm_invalid_security_level"></a>이벤트 1094: SM_INVALID_SECURITY_LEVEL

이 클러스터에서 클러스터 공용 속성 SecurityLevel을 변경할 수 없습니다. 클러스터가 인증 모드로 현재 구성 되어 있지 않으므로 클러스터 보안 수준을 변경할 수 없습니다.

### <a name="event-1119-res_netname_dns_registration_missing"></a>이벤트 1119: RES_NETNAME_DNS_REGISTRATION_MISSING

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 다음 이유로 인해 ' %4 ' 어댑터에 대 한 ' %2 ' DNS 이름을 등록 하지 못했습니다. <br><br>' %3 '

### <a name="event-1125-tm_event_cluster_netinterface_unreachable"></a>이벤트 1125: TM_EVENT_CLUSTER_NETINTERFACE_UNREACHABLE

네트워크 ' %3 '의 클러스터 노드 ' %2 '에 대 한 클러스터 네트워크 인터페이스 ' %1 '은 (는) 네트워크에 연결 된 하나 이상의 다른 클러스터 노드에서 연결할 수 없습니다. 장애 조치 (failover) 클러스터에서 오류 위치를 확인할 수 없습니다. 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 상태가 지속 되 면 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 합니다. 또한 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1149-res_netname_cant_delete_dns_records"></a>이벤트 1149: RES_NETNAME_CANT_DELETE_DNS_RECORDS

클러스터 리소스 ' %1 '과 (와) 연결 된 DNS 호스트 (A) 및 포인터 (PTR) 레코드가 리소스의 연결 된 DNS 서버에서 제거 되지 않았습니다. 필요한 경우 수동으로 삭제할 수 있습니다. 이러한 작업을 지원 하려면 DNS 관리자에 게 문의 하세요.

### <a name="event-1150-res_netname_dns_ptr_record_delete_failed"></a>이벤트 1150: RES_NETNAME_DNS_PTR_RECORD_DELETE_FAILED

' %4 ' 오류로 인해 클러스터 네트워크 이름 리소스 ' %1 '과 (와) 연결 된 ' %3 ' 호스트에 대 한 ' %2 ' DNS 포인터 (PTR) 레코드를 제거 하지 못했습니다.
필요한 경우 레코드를 수동으로 삭제할 수 있습니다. 도움이 필요 하면 DNS 관리자에 게 문의 하십시오.

### <a name="event-1151-res_netname_dns_a_record_delete_failed"></a>이벤트 1151: RES_NETNAME_DNS_A_RECORD_DELETE_FAILED

' %3 ' 오류로 인해 클러스터 네트워크 이름 리소스 ' %1 '과 (와) 연결 된 DNS 호스트 (A) 레코드 ' %2 '을 (를) 제거 하지 못했습니다. 필요한 경우 레코드를 수동으로 삭제할 수 있습니다. 도움이 필요 하면 DNS 관리자에 게 문의 하십시오.

### <a name="event-1155-rcm_event_exited_queuing"></a>이벤트 1155: RCM_EVENT_EXITED_QUEUING

' %1 ' 역할의 보류 중인 이동이 완료 되지 않았습니다.

### <a name="event-1197-res_netname_delete_disable_failed"></a>이벤트 1197: RES_NETNAME_DELETE_DISABLE_FAILED

리소스를 삭제 하는 동안 클러스터 네트워크 이름 리소스 ' %1 '에서 연결 된 컴퓨터 개체 ' %2 '을 (를) 삭제 하거나 사용 하지 않도록 설정 하지 못했습니다. 오류 코드는 ' %3 '입니다. <br>사이트가 읽기 전용인 지 확인 하세요. 클러스터 이름 개체에 Active Directory의 ' %2 ' 개체에 대 한 적절 한 권한이 있는지 확인 하십시오.

### <a name="event-1198-res_netname_delete_vco_guid_failed"></a>이벤트 1198: RES_NETNAME_DELETE_VCO_GUID_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) guid가 ' %2 ' 인 컴퓨터 개체를 삭제 하지 못했습니다. 오류 코드는 ' %3 '입니다. <br>사이트가 읽기 전용인 지 확인 하세요. 클러스터 이름 개체에 Active Directory의 ' %2 ' 개체에 대 한 적절 한 권한이 있는지 확인 하십시오.

### <a name="event-1216-service_netname_change_warning"></a>이벤트 1216: SERVICE_NETNAME_CHANGE_WARNING

클러스터 코어 netname 리소스에 대 한 이름 변경 작업이 실패 했습니다.
이름 변경 작업을 원래 이름으로 되돌리는 시도도 실패 했습니다. 오류 코드는 ' %1 '입니다. 이 상황이 수동으로 해결 될 때까지 클러스터 이름을 사용 하 여 클러스터를 원격으로 관리할 수 없습니다.

### <a name="event-1221-res_netname_rename_out_of_synch_with_compobj"></a>이벤트 1221: RES_NETNAME_RENAME_OUT_OF_SYNCH_WITH_COMPOBJ

클러스터 네트워크 이름 리소스 ' %1 '의 이름 ' %2 '이 (가) 해당 하는 컴퓨터 개체 이름 ' %3 '과 (와) 일치 하지 않습니다. 컴퓨터 개체의 이전 이름 변경이 도메인의 모든 도메인 컨트롤러에 복제 되지 않았을 수 있습니다. 이름이 일치 해야 네트워크 이름 리소스의 이름을 바꿀 수 있습니다. 컴퓨터 개체가 최근에 변경 되지 않은 경우 컴퓨터 개체의 이름을 바꾸고 일관 되도록 도메인 관리자에 게 문의 하세요. 또한 도메인 컨트롤러 간 복제가 성공적으로 완료 되었는지 확인 합니다.

### <a name="event-1222-res_netname_set_permissions_failed"></a>이벤트 1222: RES_NETNAME_SET_PERMISSIONS_FAILED

클러스터 네트워크 이름 리소스 ' %1 '과 (와) 연결 된 컴퓨터 개체를 업데이트할 수 없습니다.<br><br>관련 오류 코드의 텍스트는 %2입니다.<br> <br>클러스터 id ' %3 '에 개체를 업데이트 하는 데 필요한 권한이 없을 수 있습니다. 도메인 관리자와 협력 하 여 클러스터 id가 도메인의 컴퓨터 개체를 업데이트할 수 있는지 확인 하십시오.

### <a name="event-1240-res_ipaddr_obtain_lease_failed"></a>이벤트 1240: RES_IPADDR_OBTAIN_LEASE_FAILED

클러스터 IP 주소 리소스 ' %1 '이 (가) 임대 된 IP 주소를 가져오지 못했습니다.

### <a name="event-1243-res_ipaddr_release_lease_failed"></a>이벤트 1243: RES_IPADDR_RELEASE_LEASE_FAILED

클러스터 IP 주소 리소스 ' %1 '이 (가) IP 주소 ' %2 '에 대 한 임대를 해제 하지 못했습니다.

### <a name="event-1251-rcm_group_preempted"></a>이벤트 1251: RCM_GROUP_PREEMPTED

클러스터 된 역할 ' %2 '이 (가) 오프 라인 상태입니다. 이 역할은 우선 순위가 높은 클러스터 된 역할 ' %1 '에 의해 선점 되었습니다. 클러스터 서비스는 시스템 리소스를 사용할 수 있는 경우 클러스터 된 역할 ' %2 '을 (를) 온라인 상태로 전환 합니다.

### <a name="event-1544-service_vss_onabort"></a>이벤트 1544: SERVICE_VSS_ONABORT

클러스터 구성 데이터에 대 한 백업 작업이 취소 되었습니다. 클러스터 볼륨 섀도 복사본 서비스 (VSS) 기록기에서 중단 요청을 받았습니다.

### <a name="event-1548-service_connect_version_compatible"></a>이벤트 1548: SERVICE_CONNECT_VERSION_COMPATIBLE

노드 ' %1 '이 (가) 노드 ' %2 '과 (와) 통신을 설정 하 고 호환 되는 다른 버전의 운영 체제를 실행 하 고 있음을 검색 했습니다. 모든 노드가 동일한 버전의 운영 체제를 실행 하는 것이 좋습니다. 모든 노드를 업그레이드 한 후 ClusterFunctionalLevel Windows PowerShell cmdlet을 실행 하 여 클러스터 업그레이드를 완료 합니다.

### <a name="event-1550-service_connect_novercheck"></a>이벤트 1550: SERVICE_CONNECT_NOVERCHECK

버전 호환성 검사를 사용 하지 않도록 설정 되어 있으므로 ' %1 ' 노드에서 버전 호환성 검사를 수행 하지 않고 ' %2 ' 노드와의 통신 세션을 설정 했습니다. 버전 호환성 검사 해제는 지원 되지 않습니다.

### <a name="event-1551-service_form_novercheck"></a>이벤트 1551: SERVICE_FORM_NOVERCHECK

버전 호환성 검사를 사용 하지 않도록 설정 되어 있으므로 ' %1 ' 노드에서 버전 호환성 검사를 수행 하지 않고 장애 조치 (failover) 클러스터를 구성 했습니다. 버전 호환성 검사 해제는 지원 되지 않습니다.

### <a name="event-1555-service_netft_disable_autoconfig_failed"></a>이벤트 1555: SERVICE_NETFT_DISABLE_AUTOCONFIG_FAILED

' %1 ' 네트워크 어댑터에 대해 IPv4를 사용 하는 데 실패 했습니다. IPv4 자동 구성 및 DHCP를 사용 하지 않도록 설정 하는 데 실패 했기 때문입니다. DHCP 클라이언트 서비스가 이미 사용 하지 않도록 설정 된 경우이 문제가 발생할 수 있습니다. IPv6은 사용 하도록 설정 된 경우 사용 되며, 그렇지 않으면이 노드가 장애 조치 (failover) 클러스터에 참여 하지 못할 수 있습니다.

### <a name="event-1558-service_witness_failover_attempt"></a>이벤트 1558: SERVICE_WITNESS_FAILOVER_ATTEMPT

클러스터 서비스에서 감시 리소스에 문제가 있음을 발견 했습니다. 클러스터 구성 데이터에 대 한 액세스를 다시 설정 하려고 시도 하면 감시 리소스가 클러스터 내의 다른 노드로 장애 조치 (failover) 됩니다.

### <a name="event-1562-res_fsw_alivefailure"></a>이벤트 1562: RES_FSW_ALIVEFAILURE

파일 공유 감시 리소스 ' %1 '이 (가) 파일 공유 ' %2 '에 대 한 주기적인 상태 검사에 실패 했습니다. 파일 공유 ' %2 '이 (가) 있고 클러스터에서 액세스할 수 있는지 확인 하세요.

### <a name="event-1576-res_netname_dns_registration_secure_zone_refused"></a>이벤트 1576: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_REFUSED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 보안 DNS 영역에서 ' %4 ' 어댑터를 통해 이름 ' %2 '을 (를) 등록 하지 못했습니다. 이는이 이름의 기존 레코드와 클러스터 id에 해당 레코드를 업데이트할 수 있는 권한이 없기 때문입니다. 오류 코드는 ' %3 '입니다. Dns 서버 관리자에 게 문의 하 여 클러스터 id에 DNS 레코드 ' %2 '에 대 한 권한이 있는지 확인 하십시오.

### <a name="event-1576-res_netname_dns_registration_secure_zone_refused"></a>이벤트 1576: RES_NETNAME_DNS_REGISTRATION_SECURE_ZONE_REFUSED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 보안 DNS 영역에서 ' %4 ' 어댑터를 통해 이름 ' %2 '을 (를) 등록 하지 못했습니다. 이는이 이름의 기존 레코드와 클러스터 id에 해당 레코드를 업데이트할 수 있는 권한이 없기 때문입니다. 오류 코드는 ' %3 '입니다. Dns 서버 관리자에 게 문의 하 여 클러스터 id에 DNS 레코드 ' %2 '에 대 한 권한이 있는지 확인 하십시오.

### <a name="event-1577-res_netname_dns_server_could_not_be_contacted"></a>이벤트 1577: RES_NETNAME_DNS_SERVER_COULD_NOT_BE_CONTACTED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) ' %4 ' 어댑터를 통해 이름 ' %2 '을 (를) 등록 하지 못했습니다. DNS 서버에 연결할 수 없습니다. 오류 코드는 ' %3. '입니다. 이 클러스터 노드에서 DNS 서버에 액세스할 수 있는지 확인 하십시오. DNS 등록은 나중에 다시 시도 됩니다.

### <a name="event-1577-res_netname_dns_server_could_not_be_contacted"></a>이벤트 1577: RES_NETNAME_DNS_SERVER_COULD_NOT_BE_CONTACTED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) ' %4 ' 어댑터를 통해 이름 ' %2 '을 (를) 등록 하지 못했습니다. DNS 서버에 연결할 수 없습니다. 오류 코드는 ' %3. '입니다. 이 클러스터 노드에서 DNS 서버에 액세스할 수 있는지 확인 하십시오. DNS 등록은 나중에 다시 시도 됩니다.

### <a name="event-1578-res_netname_dns_test_for_dynamic_update_failed"></a>이벤트 1578: RES_NETNAME_DNS_TEST_FOR_DYNAMIC_UPDATE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) ' %4 ' 어댑터를 통해 이름 ' %2 '에 대 한 동적 업데이트를 등록 하지 못했습니다. DNS 서버가 동적 업데이트를 허용 하도록 구성 되어 있지 않을 수 있습니다. 오류 코드는 ' %3 '입니다. Dns 서버 관리자에 게 문의 하 여 DNS 서버를 사용할 수 있고 동적 업데이트를 구성 했는지 확인 하십시오.<br><br>또는 DNS 탭 아래의 ' %4 ' 어댑터에 대 한 고급 TCP/IP 설정에서 '이 연결의 주소를 DNS에 등록 ' 설정의 선택을 취소 하 여 동적 DNS 업데이트를 사용 하지 않도록 설정할 수 있습니다.

### <a name="event-1578-res_netname_dns_test_for_dynamic_update_failed"></a>이벤트 1578: RES_NETNAME_DNS_TEST_FOR_DYNAMIC_UPDATE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) ' %4 ' 어댑터를 통해 이름 ' %2 '에 대 한 동적 업데이트를 등록 하지 못했습니다. DNS 서버가 동적 업데이트를 허용 하도록 구성 되어 있지 않을 수 있습니다. 오류 코드는 ' %3 '입니다. Dns 서버 관리자에 게 문의 하 여 DNS 서버를 사용할 수 있고 동적 업데이트를 구성 했는지 확인 하십시오.<br><br>또는 DNS 탭 아래의 ' %4 ' 어댑터에 대 한 고급 TCP/IP 설정에서 '이 연결의 주소를 DNS에 등록 ' 설정의 선택을 취소 하 여 동적 DNS 업데이트를 사용 하지 않도록 설정할 수 있습니다.

### <a name="event-1579-res_netname_dns_record_update_failed"></a>이벤트 1579: RES_NETNAME_DNS_RECORD_UPDATE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) ' %4 ' 어댑터를 통해 이름 ' %2 '에 대 한 DNS 레코드를 업데이트 하지 못했습니다. 오류 코드는 ' %3 '입니다. 이 클러스터 노드에서 DNS 서버에 액세스할 수 있는지 확인 하 고 DNS 서버 관리자에 게 문의 하 여 클러스터 id가 DNS 레코드 ' %2 '을 (를) 업데이트할 수 있는지 확인 하십시오.

### <a name="event-1579-res_netname_dns_record_update_failed"></a>이벤트 1579: RES_NETNAME_DNS_RECORD_UPDATE_FAILED

클러스터 네트워크 이름 리소스 ' %1 '이 (가) ' %4 ' 어댑터를 통해 이름 ' %2 '에 대 한 DNS 레코드를 업데이트 하지 못했습니다. 오류 코드는 ' %3 '입니다. 이 클러스터 노드에서 DNS 서버에 액세스할 수 있는지 확인 하 고 DNS 서버 관리자에 게 문의 하 여 클러스터 id가 DNS 레코드 ' %2 '을 (를) 업데이트할 수 있는지 확인 하십시오.

### <a name="event-1581-clussvc_unable_to_move_hive_to_safe_file"></a>이벤트 1581: CLUSSVC_UNABLE_TO_MOVE_HIVE_TO_SAFE_FILE

클러스터 구성 데이터에 대 한 복원 요청에서 기존 클러스터 구성 데이터 파일 (ClusDB)의 복사본을 만들지 못했습니다. 기존 구성을 유지 하는 동안 복원 작업에서 위치 ' %1 '에 복사본을 만들 수 없습니다. 기존 구성 데이터 파일이 손상 된 경우이 문제가 발생할 수 있습니다. 복원 작업이 계속 되었으나 기존 클러스터 구성으로 되돌리는 시도는 불가능 합니다.

### <a name="event-1582-clussvc_unable_to_move_restored_hive_to_current"></a>이벤트 1582: CLUSSVC_UNABLE_TO_MOVE_RESTORED_HIVE_TO_CURRENT

클러스터 서비스가 ' %1 '에서 복원 된 클러스터 하이브를 ' %2 ' (으)로 이동 하지 못했습니다. 이로 인해 복원 작업이 성공적으로 완료 되지 못할 수 있습니다. 클러스터 구성이 제대로 복원 되지 않은 경우 복원 작업을 다시 시도 하세요.

### <a name="event-1583-clussvc_netft_disable_connectionsecurity_failed"></a>이벤트 1583: CLUSSVC_NETFT_DISABLE_CONNECTIONSECURITY_FAILED

클러스터 서비스 장애 조치 (Failover) 클러스터 가상 어댑터 ' %1 '에서 IPsec (인터넷 프로토콜 보안)을 사용 하지 않도록 설정 하지 못했습니다. 이는 클러스터 통신 성능에 부정적인 영향을 미칠 수 있습니다. 이 문제가 지속 되 면 IPSec 및 Windows 방화벽에 적용 되는 로컬 및 도메인 연결 보안 정책을 확인 하세요. 또한 기본 필터링 엔진 서비스와 관련 된 이벤트를 확인 하세요.

### <a name="event-1584-shared_volume_not_ready_for_snapshot"></a>이벤트 1584: SHARED_VOLUME_NOT_READY_FOR_SNAPSHOT

백업 응용 프로그램에서 스냅숏에 대 한 볼륨을 제대로 준비 하지 않고 클러스터 공유 볼륨 ' %1 ' (' %3 ')에서 VSS 스냅숏을 시작 했습니다. 이 스냅숏은 잘못 된 것 이며 복원 작업에 백업을 사용할 수 없습니다. 클러스터 공유 볼륨의 호환성을 확인 하려면 백업 응용 프로그램 공급 업체에 문의 하세요.

### <a name="event-1589-res_netname_dns_returning_ip_that_is_not_provider"></a>이벤트 1589: RES_NETNAME_DNS_RETURNING_IP_THAT_IS_NOT_PROVIDER

클러스터 네트워크 이름 리소스 ' %1 '이 (가) 종속 IP 주소 리소스가 아닌 DNS 이름 ' %2 '과 (와) 연결 된 IP 주소를 하나 이상 찾았습니다. 발견 된 추가 주소는 ' %3 '입니다. 이는 네트워크 이름 및 연결 된 DNS 레코드가 일치 해야 클라이언트 연결에 영향을 줄 수 있습니다. 이름 ' %2 '과 (와) 연결 된 레코드를 확인 하려면 DNS 서버 관리자에 게 문의 하세요.

### <a name="event-1604-res_disk_chkdsk_spotfix_needed"></a>이벤트 1604: RES_DISK_CHKDSK_SPOTFIX_NEEDED

클러스터 디스크 리소스 ' %1 '이 (가) 볼륨 ' %2 '에 대 한 손상을 검색 했습니다. 문제를 복구 하려면 Spotfix Chkdsk가 필요 합니다.

### <a name="event-1605-res_disk_spotfix_performed"></a>이벤트 1605: RES_DISK_SPOTFIX_PERFORMED

클러스터 디스크 리소스 ' %1 '이 (가) 볼륨 ' %2 '에서/spotfix ChkDsk.exe 실행을 완료 했습니다.
반환 코드는 ' %4 '입니다. ChkDsk의 출력이 ' %3 ' 파일에 기록 되었습니다.<br>
ChkDsk에서 추가 정보는 응용 프로그램 이벤트 로그를 확인 하십시오.

### <a name="event-1671-res_disk_online_set_attributes_completed_failure"></a>이벤트 1671: RES_DISK_ONLINE_SET_ATTRIBUTES_COMPLETED_FAILURE

클러스터 실제 디스크 리소스를 온라인 상태로 만들 수 없습니다.<br><br>실제 디스크 리소스 이름: %1<br>오류 코드: %2<br>경과 된 시간 (초): %3

#### <a name="guidance"></a>지침

구성 유효성 검사 마법사를 실행 하 여 저장소 구성을 확인 합니다. 오류 코드가 ERROR_CLUSTER_SHUTDOWN 된 경우 관리자가 온라인 보류 중 상태를 취소 했습니다. 복제 된 볼륨인 경우 디스크 특성을 설정 하는 데 실패 했을 수 있습니다. 저장소 복제 이벤트에서 추가 정보를 검토 합니다.

### <a name="event-1673-cluster_node_entered_isolated_state"></a>이벤트 1673: CLUSTER_NODE_ENTERED_ISOLATED_STATE

클러스터 노드 ' %1 '이 (가) isolated 상태를 입력 했습니다.

### <a name="event-1675-event_joining_node_quarantined"></a>이벤트 1675: EVENT_JOINING_NODE_QUARANTINED

클러스터 노드 ' %1 '이 (가) ' %2 ' (으)로 격리 되었으며 클러스터에 연결할 수 없습니다. 노드가 ' %3 '까지 격리 된 후 노드가 자동으로 클러스터를 다시 조인 하려고 시도 합니다. <br><br>이 노드의 문제를 확인 하려면 시스템 및 응용 프로그램 이벤트 로그를 참조 하십시오. 문제가 해결 되 면 격리를 수동으로 지우면 노드가 ' Start-clusternode – ClearQuarantine ' Windows PowerShell cmdlet과 다시 가입할 수 있습니다.<br><br>노드 이름: %1<br>QuarantineType: %2에의 한 격리<br>시간 격리가 자동으로 지워집니다. %3

### <a name="event-1681-cluster_groups_unmonitored_on_node"></a>이벤트 1681: CLUSTER_GROUPS_UNMONITORED_ON_NODE

' %1 ' 노드의 가상 컴퓨터에서 모니터링 되지 않는 상태가 되었습니다. 노드가 격리 된 상태에서 반환 되거나 노드가 반환 되지 않으면 장애 조치 (failover) 될 때 가상 머신 상태가 다시 모니터링 됩니다. 더 이상 모니터링 하 고 있지 않은 가상 머신은 %2입니다.

### <a name="event-1689-event_disable_and_stop_other_service"></a>이벤트 1689: EVENT_DISABLE_AND_STOP_OTHER_SERVICE

클러스터 서비스가 장애 조치 (Failover) 클러스터링과 호환 되지 않는 서비스를 검색 했습니다. 장애 조치 (Failover) 클러스터에서 발생할 수 있는 문제를 방지 하기 위해 서비스를 사용 하지 않도록 설정 했습니다.<br><br>서비스 이름: ' %1 '

### <a name="event-4625-nodecleanup_reset_nlbsflags_preserved"></a>이벤트 4625: NODECLEANUP_RESET_NLBSFLAGS_PRESERVED

클러스터 노드를 정리 하는 동안 IPSec 보안 연결 시간 제한 레지스트리 값을 다시 설정 하지 못했습니다. 이는이 컴퓨터가 클러스터의 구성원이 되도록 구성 된 후 IPSec 보안 연결 제한 시간이 수정 되었기 때문입니다. 수동 정리의 경우이 컴퓨터에서 ' Start-clusternode ' PowerShell cmdlet을 실행 합니다. 또는 Windows 레지스트리의 HKEY_LOCAL_MACHINE ' %1 ' 값 및 ' %2 ' 값을 삭제 하 여 IPSec 보안 연결 시간 제한을 다시 설정할 수 있습니다.

### <a name="event-4873-netft_clussvc_terminate_because_of_watchdog"></a>이벤트 4873: NETFT_CLUSSVC_TERMINATE_BECAUSE_OF_WATCHDOG

클러스터 서비스가 장애 조치 (failover) 클러스터 가상 어댑터가 중지 되었음을 감지 했습니다. 핫 replace CPU가이 노드에 대해 수행 되는 경우이 작업이 필요 합니다.
작업이 완료 되 면 작업이 중지 되 고 작업이 완료 된 후 자동으로 다시 시작 됩니다. 클러스터 서비스 서비스와 연결 된 추가 이벤트를 확인 하 고이 노드에서 클러스터 서비스가 다시 시작 되었는지 확인 하십시오.

### <a name="event-5120-dcm_volume_auto_pause_after_failure"></a>이벤트 5120: DCM_VOLUME_AUTO_PAUSE_AFTER_FAILURE

' %3 ' (으)로 인해 클러스터 공유 볼륨 ' %1 ' (' %2 ')이 (가) 일시 중지 된 상태로 전환 되었습니다.
볼륨에 대 한 경로를 다시 설정할 때까지 모든 i/o는 일시적으로 큐에 대기 됩니다.

### <a name="event-5123-dcm_event_root_rename_success"></a>이벤트 5123: DCM_EVENT_ROOT_RENAME_SUCCESS

클러스터 공유 볼륨 루트 디렉터리 ' %1 '이 (가) 이미 있습니다. ' %1 ' 디렉터리의 이름을 ' %2 ' (으)로 바꿨습니다. 이 위치의 데이터에 액세스 하는 응용 프로그램이 필요에 따라 업데이트 되었는지 확인 하세요.

### <a name="event-5124-dcm_unsafe_filters_found"></a>이벤트 5124: DCM_UNSAFE_FILTERS_FOUND

' %1 ' (' %3 ')이 (가)이 장치 스택에서 하나 이상의 활성 필터 드라이버를 식별 하 여 CSV 작업을 방해할 수 클러스터 공유 볼륨. I/o 액세스는 네트워크를 통해 다른 클러스터 노드를 통해 저장소 장치로 리디렉션됩니다. 이로 인해 성능이 저하 될 수 있습니다. 클러스터 공유 볼륨의 상호 운용성을 확인 하려면 필터 드라이버 공급 업체에 문의 하세요. <br><br>검색 한 활성 필터 드라이버:<br>%2

### <a name="event-5125-dcm_unsafe_volfilter_found"></a>이벤트 5125: DCM_UNSAFE_VOLFILTER_FOUND

클러스터 공유 볼륨 ' %1 ' (' %3 ')이 (가) CSV 작업을 방해할 수 있는이 장치 스택에서 하나 이상의 활성 볼륨 드라이버를 식별 했습니다. I/o 액세스는 네트워크를 통해 다른 클러스터 노드를 통해 저장소 장치로 리디렉션됩니다. 이로 인해 성능이 저하 될 수 있습니다. 볼륨 드라이버 공급 업체에 문의 하 여 클러스터 공유 볼륨의 상호 운용성을 확인 하세요. <br><br>찾은 활성 볼륨 드라이버:<br>%2

### <a name="event-5126-dcm_event_cannot_disable_short_names"></a>이벤트 5126: DCM_EVENT_CANNOT_DISABLE_SHORT_NAMES

물리적 디스크 리소스 ' %1 '에서 짧은 이름 생성을 사용 하지 않도록 설정할 수 없습니다. 이로 인해 응용 프로그램 호환성 문제가 발생할 수 있습니다. ' Fsutil 8dot3name set 2 '를 사용 하 여 짧은 이름 생성을 비활성화 한 다음 리소스를 오프 라인/온라인으로 설정 하십시오.

### <a name="event-5128-dcm_event_cannot_disable_short_names"></a>이벤트 5128: DCM_EVENT_CANNOT_DISABLE_SHORT_NAMES

물리적 디스크 리소스 ' %1 '에서 짧은 이름 생성을 사용 하지 않도록 설정할 수 없습니다. 이로 인해 응용 프로그램 호환성 문제가 발생할 수 있습니다. ' Fsutil 8dot3name set 2 '를 사용 하 여 짧은 이름 생성을 비활성화 한 다음 리소스를 오프 라인/온라인으로 설정 하십시오.

### <a name="event-5133-dcm_cannot_restore_drive_letters"></a>이벤트 5133: DCM_CANNOT_RESTORE_DRIVE_LETTERS

클러스터 디스크 ' %1 '이 (가) 제거 되어 ' 사용 가능한 저장소 ' 클러스터 그룹에 다시 배치 되었습니다. 이 과정에서 원래 드라이브 문자를 복원 하려는 시도는 이미 사용 중인 드라이브 문자 때문에 예상 보다 오래 걸렸습니다.

### <a name="event-5134-dcm_cannot_set_acl_on_root"></a>이벤트 5134: DCM_CANNOT_SET_ACL_ON_ROOT

클러스터 서비스에서 클러스터 공유 볼륨 루트 디렉터리 ' %1 '에 대 한 사용 권한 (ACL)을 설정 하지 못했습니다. 오류는 ' %2 '입니다.

### <a name="event-5135-dcm_cannot_set_acl_on_volume_folder"></a>이벤트 5135: DCM_CANNOT_SET_ACL_ON_VOLUME_FOLDER

클러스터 서비스에서 클러스터 공유 볼륨 디렉터리 ' %1 ' (' %2 ')에 대 한 사용 권한을 설정 하지 못했습니다. 오류는 ' %3 '입니다.

### <a name="event-5136-dcm_csv_into_redirected_mode"></a>이벤트 5136: DCM_CSV_INTO_REDIRECTED_MODE

클러스터 공유 볼륨 ' %1 ' (' %2 ')이 (가) 리디렉션된 액세스가 설정 되었습니다. 저장소 장치에 대 한 액세스는이 볼륨에 액세스 하는 모든 클러스터 노드에서 네트워크를 통해 리디렉션됩니다. 이로 인해 성능이 저하 될 수 있습니다. 정상적인 작업을 다시 시작 하려면이 볼륨에 대 한 리디렉션된 액세스를 해제 합니다.

### <a name="event-5149-dcm_csv_block_cache_resized"></a>이벤트 5149: DCM_CSV_BLOCK_CACHE_RESIZED

채워진 메모리에 따라 캐시 크기가 ' %1 ' (으)로 조정 되었습니다. 사용자 setsize이 너무 높습니다.

### <a name="event-5156-dcm_volume_auto_pause_after_snapshot_failure"></a>이벤트 5156: DCM_VOLUME_AUTO_PAUSE_AFTER_SNAPSHOT_FAILURE

' %3 ' (으)로 인해 클러스터 공유 볼륨 ' %1 ' (' %2 ')이 (가) 일시 중지 된 상태로 전환 되었습니다.
이 오류는 CSV 볼륨을 기반으로 하는 volsnap 스냅숏이 사용자 요청 외부에서 삭제 되는 경우에 발생 합니다. 스냅숏이 확장 될 때 스냅숏의 공간이 부족 하거나 스냅숏 데이터를 업데이트 하려고 시도 하는 동안 IO 오류가 발생 한 것 같습니다. 스냅숏 상태가 volsnap와 동기화 될 때까지 모든 i/o는 일시적으로 큐에 대기 됩니다.

### <a name="event-5157-dcm_volume_auto_pause_after_failure_expected"></a>이벤트 5157: DCM_VOLUME_AUTO_PAUSE_AFTER_FAILURE_EXPECTED

' %3 ' (으)로 인해 클러스터 공유 볼륨 ' %1 ' (' %2 ')이 (가) 일시 중지 된 상태로 전환 되었습니다.
볼륨에 대 한 경로를 다시 설정할 때까지 모든 i/o는 일시적으로 큐에 대기 됩니다.
이 오류는 일반적으로 인프라 오류로 인해 발생 합니다. 예를 들어 클러스터 공유 볼륨를 소유 하는 저장소 또는 노드에 대 한 연결이 끊어진 경우 활성 클러스터 멤버 자격에서 제거 됩니다.

### <a name="event-5394-pool_online_warnings"></a>이벤트 5394: POOL_ONLINE_WARNINGS

저장소 풀을 온라인 상태로 전환 하는 동안 클러스터 서비스에 일부 저장소 오류가 발생 했습니다. 클러스터 저장소 유효성 검사를 실행 하 여 문제를 해결 합니다.

### <a name="event-5395-rcm_group_auto_move_storage_pool"></a>이벤트 5395: RCM_GROUP_AUTO_MOVE_STORAGE_POOL

현재 노드 ' %3 '이 (가) 저장소 풀의 실제 디스크와 최적으로 연결 되어 있지 않으므로 클러스터가 저장소 풀 ' %1 '에 대 한 그룹을 이동 하는 중입니다.

## <a name="informational-events"></a>정보 이벤트

### <a name="event-1592-clussvc_tcp_reconnect_connection_reestablished"></a>이벤트 1592: CLUSSVC_TCP_RECONNECT_CONNECTION_REESTABLISHED

클러스터 노드 ' %1 '이 (가) 클러스터 노드 ' %2 '과 (와)의 통신을 끊어졌습니다. 네트워크 통신이 다시 설정 되었습니다. 이는 일시적으로 방화벽 또는 연결 보안 정책 업데이트에 의해 차단 되는 통신 때문에 발생할 수 있습니다. 문제가 지속 되 고 네트워크 통신이 다시 설정 되지 않으면 하나 이상의 노드에서 클러스터 서비스가 중지 됩니다. 이러한 경우 구성 유효성 검사 마법사를 실행 하 여 네트워크 구성을 확인 합니다. 또한이 노드의 네트워크 어댑터와 관련 된 하드웨어 또는 소프트웨어 오류를 확인 하 고 허브, 스위치 또는 브리지와 같이 노드가 연결 된 다른 모든 네트워크 구성 요소에서 오류를 확인 합니다.

### <a name="event-1594-cluster_functional_level_upgrade_complete"></a>이벤트 1594: CLUSTER_FUNCTIONAL_LEVEL_UPGRADE_COMPLETE

클러스터 서비스 클러스터 기능 수준을 업그레이드 했습니다. <br><br>
기능 수준: %1 <br> 업그레이드 버전: %2

### <a name="event-1635-rcm_resource_failure_info_with_typename"></a>이벤트 1635: RCM_RESOURCE_FAILURE_INFO_WITH_TYPENAME

클러스터 된 역할 ' %2 '에서 ' %3 ' 유형의 클러스터 리소스 ' %1 '이 (가) 실패 했습니다.

### <a name="event-1636-clussvc_password_changed"></a>이벤트 1636: CLUSSVC_PASSWORD_CHANGED

클러스터 서비스가 ' %2 ' 노드에서 ' %1 ' 계정의 암호를 변경 했습니다.

### <a name="event-1680-cluster_node_exited_isolated_state"></a>이벤트 1680: CLUSTER_NODE_EXITED_ISOLATED_STATE

클러스터 노드 ' %1 '이 (가) 격리 된 상태를 종료 했습니다.

### <a name="event-1682-cluster_group_moved_no_longer_unmonitored"></a>이벤트 1682: CLUSTER_GROUP_MOVED_NO_LONGER_UNMONITORED

격리 된 노드 ' %1 '에서 모니터링 되지 않는 가상 머신 ' %2 '이 (가) 다른 노드로 장애 조치 (failover) 되었습니다. 가상 컴퓨터의 상태가 다시 모니터링 되 고 있습니다.

### <a name="event-1682-cluster_multiple_groups_no_longer_unmonitored"></a>이벤트 1682: CLUSTER_MULTIPLE_GROUPS_NO_LONGER_UNMONITORED

노드 ' %1 '이 (가) 클러스터에 다시 가입 했으며 해당 노드에서 실행 중인 가상 컴퓨터 %2이 (가) 다시 한 번 모니터링 되 고 있습니다.

### <a name="event-4621-nodecleanup_success"></a>이벤트 4621: NODECLEANUP_SUCCESS

이 노드가 클러스터에서 성공적으로 제거 되었습니다.

### <a name="event-5121-dcm_volume_no_direct_io_due_to_failure"></a>이벤트 5121: DCM_VOLUME_NO_DIRECT_IO_DUE_TO_FAILURE

클러스터 공유 볼륨 ' %1 ' (' %2 ')은 (는)이 클러스터 노드에서 더 이상 직접 액세스할 수 없습니다. I/o 액세스는 네트워크를 통해 볼륨을 소유 하는 노드로 저장 장치로 리디렉션됩니다. 이로 인해 성능이 저하 되 면 저장소 장치에 대 한이 노드의 연결 문제를 해결 하세요. 그러면 저장소 장치에 대 한 연결이 다시 설정 되 면 i/o가 정상 상태로 다시 시작 됩니다.

### <a name="event-5218-csv_old_sw_snapshot_deleted"></a>이벤트 5218: CSV_OLD_SW_SNAPSHOT_DELETED

클러스터 물리적 디스크 리소스 ' %1 '이 (가) 소프트웨어 스냅숏을 삭제 했습니다. ' %2 ' 클러스터 공유 볼륨의 소프트웨어 스냅숏이 ' %3 ' 일 보다 오래 되어 삭제 되었습니다. 스냅숏 ID는 ' %4 ' 이며 ' %6 '의 ' %5 ' 노드에서 만들어졌습니다.
백업 작업이 완료 된 후 백업 응용 프로그램에서 스냅숏을 삭제할 것으로 예상 됩니다. 스냅숏이 존재 하는 것으로 예상 되는 시간이 초과 되었습니다. 백업 응용 프로그램에서 백업 작업이 성공적으로 완료 되는지 확인 합니다.

## <a name="additional-references"></a>추가 참조

-   [Windows Server 2008의 장애 조치 (Failover) 클러스터링 구성 요소에 대 한 자세한 이벤트 정보](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753362(v%3dws.10))
