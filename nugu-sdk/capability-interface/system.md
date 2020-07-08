# System

## Version

최신 버전은 1.1 입니다.

## SDK Interface

### 디바이스 전원 제어

`사용자 발화` 에 따라 [TurnOff](system.md#turnoff) directive 로 디바이스 전원을 제어할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/system/SystemAgentInterface.kt#L39)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/system_interface.hh#L73)

### 에러처리

NUGU 서버에서 에러가 발생할 경우 [Exception](system.md#exception) directive 로 error code가 전달됩니다.

사용자가 에러 상황을 인지할 수 있도록 Toast, Local TTS 등으로 안내해야합니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/system/SystemAgentInterface.kt#L46)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/System/SystemAgentDelegate.swift#L25)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/system_interface.hh#L68)

### 디바이스 등록 해제

누구 서버에서 디바이스가 등록 해제되면 [Revoke](system.md#revoke) directive 로 reason 이 전달됩니다.

Application 의 상황에 따라 NUGU 로그인 화면으로 이동하거나 NUGU Button 을 비활성화 해야합니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/system/SystemAgentInterface.kt#L51)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/System/SystemAgentDelegate.swift#L26)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/system_interface.hh#L79)

## Context

```text
{
  "System": {
    "version": "1.1"
  }
}
```

## Directive

### TurnOff

디바이스 전원 끄기 요청입니다.

```text
{
  "header": {
    "namespace": "System",
    "name": "TurnOff",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### Exception

누구 서버에서 에러가 발생하면 전달됩니다.

```text
{
  "header": {
    "namespace": "System",
    "name": "Exception",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "code": "{{STRING}}",
    "description": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| code | string | Y | 서버에서 발생 |
| description | string | N | 에러에 대한 설명 |

| code | description |
| :--- | :--- |
| UNAUTHORIZED\_REQUEST\_EXCEPTION | 접속 시 인증 에러 |
| ASR\_RECOGNIZING\_EXCEPTION | 음성 인식 에러 |
| PLAY\_ROUTER\_PROCESSING\_EXCEPTION | Play router 에러 |
| TTS\_SPEAKING\_EXCEPTION | 음성 합성 에러 |
| INTERNAL\_SERVICE\_EXCEPTION | 기타 알 수 없는 에러 |

### Revoke

NUGU 서버에서 디바이스가 등록 해제되면 전달됩니다.

```text
{
  "header": {
    "namespace": "System",
    "name": "Revoke",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "reson": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| reason | string | Y | 디바이스가 등록 해제된 원인 |

| reason | description |
| :--- | :--- |
|  REVOKED\_DEVICE | NUGU 모바일 앱에서 디바이스 연결 해제 |



