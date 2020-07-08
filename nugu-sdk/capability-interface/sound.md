---
description: 디바이스의 음원 파일 재생을 위한 규격
---

# Sound

## Version

최신 버전은 1.2 입니다.

## SDK Interface

### 재생

디바이스 음원 재생이 [Beep](sound.md#beep) directive 로 요청될 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/sound/SoundProvider.kt#L22)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Sound/SoundAgentDataSource.swift#L24)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/sound_interface.hh#L57)

## Context

```text
{
  "Sound": {
    "version": "1.0"
  }
}
```

## Directives

### Beep

Beep 유형의 음원 재생 요청입니다.

```text
{
  "header": {
    "namespace": "Sound",
    "name": "Beep",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "beepName": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| beepName | string | Y | RESPONSE\_FAIL: Play 응답 실패 |

