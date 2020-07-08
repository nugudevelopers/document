---
description: 정의되지 않은 기능을 수행하기 위한 규격
---

# Extension

## Version

최신 버전은 1.1 입니다.

## Precondition

Extension interface 를 사용한 Play 를 제작하기 위해서는 제휴담당자에게 요청하여 권한을 획득해야 합니다.

Play 개발자와 Application 개발자는 Context, Directive, Event 의 data 필드에 대한 데이터 구조를 협의해야 합니다.

## SDK Interface

### Context 구성

Play 에서 알아야 하는 디바이스/Application 의 정보를 [Context](extension.md#context) 에 포함시켜 주어야 합니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/extension/ExtensionAgentInterface.kt#L42)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Extension/ExtensionAgentDelegate.swift#L35)

### Directive 수신

특정 기능의 실행이 [Action](extension.md#action) directive 로 요청될 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/extension/ExtensionAgentInterface.kt#L36)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Extension/ExtensionAgentDelegate.swift#L44)

### Event 전송

특정 기능 실행을 [CommandIssued](extension.md#commandissued) event 로 요청할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/extension/ExtensionAgentInterface.kt#L69)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Extension/ExtensionAgentProtocol.swift#L39)

## Context

```text
{
  "Extension": {
    "version": "1.1",
    "data": {}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| data | object | N | 임의의 JSON object |

## Directive

### Action

```text
{
  "header": {
    "namespace": "Extension",
    "name": "Action",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "data": {}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| data | object | Y | 임의의 JSON object |

## Event

### CommandIssued

```text
{
  "header": {
    "namespace": "Extension",
    "name": "CommandIssued",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "data": {}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| data | object | Y | 임의의 JSON object |

