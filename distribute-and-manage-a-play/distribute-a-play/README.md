# Play 배포

Play 심사 승인이 완료된 Play는 배포 설정 기능을 통해 Play 배포일을 등록해야 NUGU 서비스 제공이 가능합니다.

## 배포 정책 <a id="distribution-policy"></a>

Play 배포는 NUGU developers의 정책에 따라 주 1회 배포가 진행됩니다. Play는 매주 수요일에 상용 배포되며, 화요일까지 심사가 완료되어 배포 신청이 접수된 Play에 한해 그 주 수요일에 적용됩니다.

## 배포 신청 <a id="distribution-request"></a>

Play의 심사 승인이 완료되면 Play 등록 현황 리스트에 `배포설정` 버튼이 생성됩니다. 이 버튼을 이용하여 배포를 신청할 수 있습니다.

1. `NUGU developers` &gt; `NUGU play kit` &gt; `관리` &gt; `Play 등록` 페이지의 등록 현황에서 배포 신청할 Play의 \[배포설정\] 버튼을 클릭합니다.

   ![](../../.gitbook/assets/ch5_512_c01.png)

2. 배포일 확인 팝업창에서 배포 일정을 확인하거나 변경한 후 `확인` 버튼을 클릭하면 배포 신청이 완료됩니다.

   ![](../../.gitbook/assets/ch5_512_c02.png)

   * 배포일은 신청일 기준으로 가장 빠른 일정으로 자동 지정됩니다. 만약, 배포일을 직접 설정하려면 `배포일 변경` 버튼을 클릭하여 원하는 일정을 지정하면 됩니다.

3. 배포 신청이 완료되면 해당 Play는 **심사완료**에서 **배포대기** 상태로 변경되며, `배포취소` 버튼이 생성됩니다.
4. 배포 신청 후 최종 배포가 완료되면 **배포대기**에서 **배포완료** 상태로 변경됩니다.

   ![](../../.gitbook/assets/ch5_512_c03.png)

{% hint style="info" %}
배포 대기는 배포 신청을 한 상태에서 배포일이 도래하지 않았을 경우를 말하며, 이 경우에는 배포 신청을 취소할 수가 있습니다. 자세한 내용은 [배포 신청 취소](./#distribution-requestcancellation)를 참고하세요.
{% endhint %}

## 배포 신청 취소 <a id="distribution-requestcancellation"></a>

Play 배포 대기 상태\(지정한 배포일이 아직 도래하지 않은 상태\)에서는 언제든지 배포 신청을 취소할 수 있습니다.

1. `NUGU developers` &gt; `NUGU play kit` &gt; `관리` &gt; `Play 등록` 페이지의 등록 현황에서 배포 신청을 취소할 Play의 `배포취소` 버튼을 클릭합니다.

   ![](../../.gitbook/assets/ch5_513_c01.png)

2. 배포 취소 확인 팝업창에서 `확인` 버튼을 클릭하면 배포 신청이 취소됩니다.

   ![](../../.gitbook/assets/ch5_513_c02.png)

3. 배포 취소가 완료되면 해당 Play는 `배포대기`에서 `심사완료` 상태로 변경되고, `배포설정` 버튼이 생성됩니다.

   ![](../../.gitbook/assets/ch5_513_c03.png)

{% hint style="info" %}
배포를 다시 신청하려면 일정을 재설정해야 합니다. 배포 신청에 대한 자세한 내용은 [배포 신청](./#distribution-request)을 참고하세요.
{% endhint %}

## 배포 프로세스 <a id="distribution-process"></a>

배포는 별다른 설정 없이 자동으로 진행되며, 지정 배포일에 해당 Play는 서버 내에 배포됩니다. 정상적으로 배포가 완료되면 사용자들은 해당 Play를 호출하여 사용할 수 있게 됩니다. 배포가 진행된 이후에는 취소할 수 없습니다.

만약, 배포된 Play에 대해서 긴급한 이슈로 배포 취소가 필요한 경우에는 `NUGU developers` &gt; `NUGU play kit` &gt; `관리` &gt; `Play 관리`에서 `Play 중지`를 실행하여 서비스를 중지시켜야 합니다.

{% hint style="info" %}
서비스 중인 Play를 중지하는 방법에 대한 자세한 내용은 [Play 상태 변경\(중지 및 서비스 재개\)](../manage-a-play/#change-play-status)를 참고하세요.
{% endhint %}

