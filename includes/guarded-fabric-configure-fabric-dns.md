Fabric 도메인에 대 한 이름 확인을 구성 하는 방법은 여러 가지가 있습니다. 한 가지 간단한 방법은 패브릭에 대 한 dns에서 조건부 전달자 영역을 설정 하는 합니다. 이 영역을 설정 하려면 fabric DNS 서버에서 관리자 권한 Windows PowerShell 콘솔에서 다음 명령을 실행 합니다. 이름 및 사용자 환경에 대 한 필요에 따라 아래 Windows PowerShell 구문에서 주소를 대체 합니다. 추가 HGS 노드에 대 한 마스터 서버를 추가 합니다.

```
Add-DnsServerConditionalForwarderZone -Name 'bastion.local' -ReplicationScope "Forest" -MasterServers <IP addresses of HGS server>
```

<!-- Appears in guarded-fabric-configuring-fabric-dns-ad.md and guarded-fabric-configuring-fabric-dns.md and set-up-hgs-for-always-encrypted-in-sql-server.md
-->    