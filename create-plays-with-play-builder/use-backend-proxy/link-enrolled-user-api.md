# Enrolled user 정보 수신 연동 개발

Private Play에 한하여 [사용자 그룹 관리](https://github.com/nugudevelopers/document/tree/4bfc96ea5fdd94bb5026a858efa51eda75782cc2/work-with-nugu-biz/manage-enrolled-user.html#manage-enrolled-user)를 통해 추가한 사용자 정보를 Backend proxy에서 받을 수 있습니다. 연동규격에서 제공하는 사용자 정보는 다음과 같습니다.

```bash
POST /action.name
Host: backend.proxy.host.domain
Accept: application/json
Content-Length: 85
Content-Type: application/json

{
  "version": "2.0",
  "action": {
    ...
  },
  "context": {
    ...
  }
  "profile": {
    "privatePlay": {
      "deviceUniqueId": "NU200_XXXXXX",
      "userKey": "user.0.A3JFAD5YQ59L4WYJ146BMJG5Q49I1QAFU22HZSJV9MEDP46KNFDF05YNPAY1P22G",
      "deviceKey": "device.0.6L273EAELW0EK2ZY4C2Z47Z2SD9VM8CTS6CFVR1DQD355W6ZUD92L01ZIQXPRRSD",
      "enrolledUser": {
        "name": "홍길동",
        "phoneNo": "01011112222",
        "email": "gilodng@email-domain.com",
        "tag": "율도국"
      }
    }
  }
}
```

| Parameter | Type | Mandatory | 설명 |
| :--- | :--- | :--- | :--- |
| profile.privatePlay | json | N | Private Play인 경우에만 추가 |
| profile.privatePlay.deviceUniqueId | string | N | 스피커 하단에 표기된 등록번호 |
| profile.privatePlay.userKey | string | Y | 익명 처리한 user id |
| profile.privatePlay.deviceKey | string | Y | 익명 처리한 device id |
| profile.privatePlay.enrolledUser | json | N | 초대 사용자\(enrolled user\)인 경우 정보 추가   [전용 Device](https://github.com/nugudevelopers/document/tree/4bfc96ea5fdd94bb5026a858efa51eda75782cc2/work-with-nugu-biz/manage-shared-device.html#manage-shared-device)는 deviceUniqueId, userKey, deviceKey만 수신할 수 있습니다. |
| profile.privatePlay.enrolledUser.name | string | Y | 초대 사용자 이름 |
| profile.privatePlay.enrolledUser.phoneNo | string | Y | 초대 사용자 전화번호 |
| profile.privatePlay.enrolledUser.email | string | Y | 초대 사용자 이메일 |
| profile.privatePlay.enrolledUser.tag | string | N | 초대 사용자 추가 정보 \(대리점 코드, 사번, 인트라넷 사용자 아이디 등 필요한 정보를 넣어서 이용\) |

{% hint style="danger" %}
연동 규격에 사용자 개인 정보를 포함하고 있으므로 Private Play의 Backend proxy server는 HTTPS를 사용해야 합니다. Private Play에서 HTTP를 이용해 Backend proxy server를 개발할 경우 심사 반려됩니다.
{% endhint %}

