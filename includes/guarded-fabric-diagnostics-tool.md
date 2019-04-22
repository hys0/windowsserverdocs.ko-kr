> [!Note] 
> 보호된 패브릭 진단 도구(Get-HgsTrace-RunDiagnostics)를 실행할 때 HTTPS 구성이 사실은 손상되지 않았거나 사용되고 있지 않은데도 HTTPS 구성이 손상되었다는 잘못된 상태가 반환될 수 있습니다. 이 오류는 HGS의 증명 모드에 관계없이 반환될 수 있습니다. 가능한 근본 원인은 다음과 같습니다.
>
> - HTTPS가 실제로 잘못 구성되었거나 손상됨<br>
> - 관리자가 신뢰할 수 있는 증명을 사용 중인데 트러스트 관계가 손상됨<br>
> &nbsp;&nbsp;&nbsp;&nbsp;-HTTPS 제대로, 제대로 구성 되어 있는지 여부에 관계 없이 또는 사용 중이 아님 전혀 않습니다.<br>
>
> 진단 대상이 Hyper-V 호스트인 경우에만 잘못된 상태가 반환됩니다. 진단 대상이 호스트 보호 서비스인 경우에는 올바른 상태가 반환됩니다.

<!-- Appears in guarded-fabric-setting-up-the-host-guardian-service-hgs.md and guarded-fabric-troubleshoot-diagnostics.md
-->
