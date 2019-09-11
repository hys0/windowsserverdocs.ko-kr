> [!Note] 
> 보호된 패브릭 진단 도구(Get-HgsTrace-RunDiagnostics)를 실행할 때 HTTPS 구성이 사실은 손상되지 않았거나 사용되고 있지 않은데도 HTTPS 구성이 손상되었다는 잘못된 상태가 반환될 수 있습니다. 이 오류는 HGS 증명 모드에 관계 없이 반환 될 수 있습니다. 가능한 근본 원인은 다음과 같습니다.
>
> - HTTPS가 실제로 잘못 구성되었거나 손상됨<br>
> - 관리자가 신뢰할 수 있는 증명을 사용 하 고 있고 트러스트 관계가 중단 되었습니다.<br>
> &nbsp;&nbsp;&nbsp;&nbsp;-이는 HTTPS가 올바르게 구성 되었는지, 부적절 하거나, 사용 중이 아닌 경우에 관계 없이 사용 됩니다.<br>
>
> 진단 대상이 Hyper-V 호스트인 경우에만 잘못된 상태가 반환됩니다. 진단 대상이 호스트 보호 서비스인 경우에는 올바른 상태가 반환됩니다.

<!-- Appears in guarded-fabric-setting-up-the-host-guardian-service-hgs.md and guarded-fabric-troubleshoot-diagnostics.md
-->
