---
description: 문자 확인 및 전송 기능 제어를 위한 규격
---

# Message

## Version

최신 버전은 1.5 입니다.

| Version | Date       | Description                                                                  |
| ------- | ---------- | ---------------------------------------------------------------------------- |
| 1.0     | 2020.07.02 | 규격 추가                                                                        |
| 1.1     | 2020.07.13 | Context 의 template 에 info 필드 추                                               |
| 1.2     | 2020.08.13 | contact type 에 EMERGENCY 추가                                                  |
| 1.3     | 2020.11.02 | SendCandidates directive 에 searchScene 필드 추가 Context 에 searchScene 필드 추가     |
| 1.4     | 2021.01.19 | Context 에 messageToSend 필드 추가 SendCandidates directive 에 messageToSend 필드 추가 |
| 1.5     | 2021.08.24 | Contact Object > message.type을 Mandatory N으로 변경                              |

## SDK Interface

### MessageAgent 사용

MessageCall interface 규격에 따른 디바이스의 동작 제어는 MessageAgent 가 처리합니다.

{% tabs %}
{% tab title="Android" %}
NuguAndroidClient instance 를 통해 MessageAgent instance 에 접근할 수 있습니다.

```
val messageAgent = nuguAndroidClient.getAgent(MessageAgent.NAMESPACE)
```

NuguAndroidClient 생성시 MessageClient 를 추가합니다.

```
class MyMessageClient: MessageClient {
    ...
}
NuguAndroidClient().Builder()
    .enableMessage(MyMessageClient())
```
{% endtab %}

{% tab title="Linux" %}
[CapabilityFactory::makeCapability](https://nugu-developers.github.io/nugu-linux/classNuguCapability\_1\_1CapabilityFactory.html#a46d96b1bc96903f02905c92ba8794bf6) 함수로 [MessageAgent](https://nugu-developers.github.io/nugu-linux/classNuguCapability\_1\_1IMessageHandler.html) 를 생성하고 [NuguClient](https://nugu-developers.github.io/nugu-linux/classNuguClientKit\_1\_1NuguClient.html) 에 추가해 주어야합니다.

```
auto message_handler(std::shared_ptr<IMessageHandler>(
        CapabilityFactory::makeCapability<MessageAgent, IMessageHandler>()));

nugu_client->getCapabilityBuilder()
    ->add(message_handler.get())
    ->construct();
```
{% endtab %}
{% endtabs %}

### Context 구성

문자 기능과 관련된 상태 정보를 [Context](message.md#context) 에 포함시켜 주어야 합니다.

{% tabs %}
{% tab title="Android" %}
MessageClient 를 구현합니다.

```
class MyMessageClient: MessageClient {
    override fun getContext(): Context {
        ...
    }

    ...
}
```
{% endtab %}
{% endtabs %}

### 문자 전송

문자 전송이 [SendCandidates](message.md#sendcandidates), [SendMessage](message.md#sendmessage) directive 로 요청될 수 있습니다.

{% tabs %}
{% tab title="Android" %}
MessageClient 를 구현합니다.

```
class MyMessageClient: MessageClient {
    override fun sendCandidates(payload: SendCandidatesPayload, callback: Callback) {
        // 연락처 검색 기능을 구현
        ...
    }

    override fun sendMessage(payload: SendMessagePayload, callback: EventCallback) {
        // 문자 전송 기능을 구현
        ...
    }

    ...
}
```
{% endtab %}

{% tab title="Linux" %}
[IMessageListener](https://nugu-developers.github.io/nugu-linux/classNuguCapability\_1\_1IMessageListener.html) 를 추가합니다.

```
class MyMessageListener : public IMessageListener {
public:
    ...

    void processSendCandidates(const std::string& payload) override
    {
        ...
    }
    
    void processSendMessage(const std::string& payload) override
    {
        ...
    }

    ...
};
auto message_listener(std::make_shared<MyMessageListener>());
CapabilityFactory::makeCapability<MessageAgent, IMessageHandler>(message_listener.get());
```
{% endtab %}
{% endtabs %}

### 문자 읽기

문자 읽기가 [GetMessage](message.md#getmessage), [ReadMessage](message.md#readmessage) directive 로 요청될 수 있습니다.

{% tabs %}
{% tab title="Android" %}
MessageClient 를 구현합니다.

```
class MyMessageClient: MessageClient {
    override fun getMessageList(payload: GetMessagePayload, callback: Callback) {
        ...
    }

    ...
}
```

문자 재생은 SDK 에서 실행됩니다.
{% endtab %}

{% tab title="Linux" %}
[IMessageListener](https://nugu-developers.github.io/nugu-linux/classNuguCapability\_1\_1IMessageListener.html) 를 추가합니다.

```
class MyMessageListener : public IMessageListener {
public:
    ...

    void processGetMessage(const std::string& payload) override
    {
        ...
    }

    ...
};
auto message_listener(std::make_shared<MyMessageListener>());
CapabilityFactory::makeCapability<MessageAgent, IMessageHandler>(message_listener.get());
```
{% endtab %}
{% endtabs %}

### 재생 상태 모니터링

[ReadMessage](message.md#readmessage) directive 로 전달된 문자에 대한 재생 상태를 모니터링 할 수 있습니다.

{% tabs %}
{% tab title="Android" %}
MessageAgentInterface.OnPlaybackListener 를 추가합니다.

```
val listener = object: MessageAgentInterface.OnPlaybackListener {
    ...
}
messageAgent.addOnPlaybackListener(listener)
```
{% endtab %}
{% endtabs %}

## Context

```
{
  "Message": {
    "version": "1.2",
    "readActivity": "{{STRING}}",
    "token": "{{STRING}}",
    "template": {
      "info": "{{STRING}}",
      "recipientIntended": {
        "name": "{{STRING}}",
        "label": "{{STRING}}"
      },
      "searchScene": "{{STRING}}",
      "candidates": [array of Contact],
      "messageToSend": {
        "text": "{{STRING}}",
        "type": "{{STRING}}"
      }
    }
  }
}
```

| parameter                         | type                           | mandatory | description                                                                                                                                                                                                                                                    |
| --------------------------------- | ------------------------------ | --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| readActivity                      | string                         | Y         | 이전 발화가 재생 상태를 전달 **IDLE**, **PLAYING**, **PAUSED**, **FINISHED**, **STOPPED** - IDLE인 경우는 최초 전원을 켰을 때만 가능하고 이후에는 나올 수 없음                                                                                                                                       |
| token                             | string                         | N         | readActivity에서 재생 중인 prompt의 token                                                                                                                                                                                                                             |
| template                          | object                         | N         | context 유지 정책과 동일하게 관리되어야 함 → Play Stack에 현재 Play가 가장 위에 있는 동안은 보내주어야 함 - 화면에 template이 디스플레이 되는 동안 - 앱에서 화면을 그리는 경우 앱이 정확한 시점 파악 가능 - 화면이 없는 경우는 DM 및 TTS 종료 후 7초 - DM이 유지되는 동안은 SDK로부터 대화 세션 유지 상황을 피드백 받아 전달 대표적인 경우는 위의 두 경우와 같으며 자세한 구현은 context 관리 정책 참조 |
| template. info                    | string                         | N         | 현재 template에 포함된 데이터가 어떤 정보를 담고 있는지 식별하기 위한 값 - **PHONE\_BOOK** : 주소록 조회 결과를 포함 - **MESSAGE** : 수신된 Message 정보를 포함                                                                                                                                             |
| template. recipientIntended       | object                         | N         | 발화에서 분석된 recipient 정보                                                                                                                                                                                                                                          |
| template. recipientIntended.name  | string                         | N         | 검색에 요청할때 사용된 상대방 이름 (NLU 분석으로 나온 이름)                                                                                                                                                                                                                           |
| template. recipientIntended.label | string                         | N         | 집, 회사 등을 구분하기 위한 라벨                                                                                                                                                                                                                                            |
| template. searchScene             | string                         | N         | 검색 대상과 화면을 정의하기 위해 추가 - **DEFAULT** : 기본 검색 로직 - **T114DIRECT** : 긴급전화                                                                                                                                                                                         |
| template. candidates              | array of [Contact](./#contact) | N         | 화면에 검색 결과 리스트를 디스플레이하는 중에만 context에 추가                                                                                                                                                                                                                         |
| template. messageToSend           | object                         | N         | 발신용으로 사용할 메세지 SendCandidates의 같은 파라미터를 통해 전달받은 MSG\_BODY를 그대로 반환                                                                                                                                                                                               |
| template. messageToSend. text     | string                         | Y         | 본문                                                                                                                                                                                                                                                             |
| template. messageToSend. type     | string                         | N         | 메세지의 타입                                                                                                                                                                                                                                                        |

## Common Objects

### Contact

```
{
  "name": "{{STRING}}",
  "type": "{{STRING}}",
  "number": "{{STRING}}",
  "label": "{{STRING}}",
  "profileImgUrl": "{{STRING}}",
  "message": {
    "text": "{{STRING}}",
    "type": "{{STRING}}"
  },
  "time": "{{STRING}}",
  "numInMessageHistory": "{{STRING}}",
  "token": "{{STRING}}",
  "score": "{{STRING}}"
}
```

| parameter           | type   | mandatory | description                                                                                                                                                                                |
| ------------------- | ------ | --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| name                | string | N         | candidates가 존재하면 각 candidate는 최소한 이름은 포함해야 함                                                                                                                                               |
| type                | string | N         | recipient candidates의 타입 - **CONTACT** : 연락처 검색 - **EXCHANGE** : exchange 검색 - **T114** : T114 검색 - **NONE** : 특정 카테고리에 속하지 않음 - **EMERGENCY** : 긴급 재난, 안전 안내 문자의 경우 "안전 안내 문자"로 TTS 나갈 예정 |
| number              | string | N         | -                                                                                                                                                                                          |
| label               | string | N         | **MOBILE** **COMPANY** **HOME** **USER\_DEFINED**                                                                                                                                          |
| profileImgUrl       | string | N         | -                                                                                                                                                                                          |
| message             | object | N         | -                                                                                                                                                                                          |
| message.text        | string | Y         | 보내는 or 받는 메세지 내용                                                                                                                                                                           |
| message.type        | string | N         | 메세지의 타입 - **SMS** - **MMS**                                                                                                                                                                |
| time                | string | N         | 날짜, 시간 정보로 ISO 8601 포맷 (2007-12-03T10:15:30)                                                                                                                                               |
| numInMessageHistory | string | N         | 문자 수신 내역에 존재하는 건수 0, 1, 2, ... 값을 string 형태로 받음                                                                                                                                            |
| token               | string | N         | 사용자 추가 정보를 식별하기 위해 임의로 정의한 key값을 포함 unique 여부는 사용되는 용도에 의해 결정                                                                                                                              |
| score               | string | N         | 검색 결과의 신뢰도                                                                                                                                                                                 |

## Directives

### SendCandidates

```
{
  "header": {
    "namespace": "Message",
    "name": "SendCandidates",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "recipientIntended": {
      "name": "{{STRING}}",
      "label": "{{STRING}}"
    },
    "searchScene": "{{STRING}}",
    "candidates": [array of Contact],
    "messageToSend": {
      "text": "{{STRING}}",
      "type": "{{STRING}}"
    }
  }
}
```

| parameter                     | type                           | mandatory | description                                                            |
| ----------------------------- | ------------------------------ | --------- | ---------------------------------------------------------------------- |
| intent                        | string                         | N         | **SEND** : 문자보내줘 **READ** : 문자읽어줘                                      |
| recipientIntended             | object                         | N         | 발화에서 분석된 recipient 정보                                                  |
| recipientIntended. name       | string                         | N         | 검색에 요청할때 사용된 상대방 이름 (NLU 분석으로 나온 이름)                                   |
| recipientIntended. label      | string                         | N         | 집, 회사 등을 구분하기 위한 라벨                                                    |
| searchScene                   | string                         | N         | 검색 대상과 화면을 정의하기 위해 추가 - **DEFAULT** : 기본 검색 로직 - **T114DIRECT** : 긴급전화 |
| candidates                    | array of [Contact](./#contact) | N         | candidates가 없으면 이 항목이 없어야 함                                            |
| template. messageToSend       | object                         | N         | 발신용으로 사용할 메세지 SendCandidates의 같은 파라미터를 통해 전달받은 MSG\_BODY를 그대로 반환       |
| template. messageToSend. text | string                         | Y         | 본문                                                                     |
| template. messageToSend. type | string                         | N         | 메세지의 타입                                                                |

### SendMessage

```
{
  "header": {
    "namespace": "Message",
    "name": "SendMessage",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "recipient": Contact
  }
}
```

| parameter | type                          | mandatory | description |
| --------- | ----------------------------- | --------- | ----------- |
| recipient | [Contact](message.md#contact) | Y         |             |

### GetMessage

```
{
  "header": {
    "namespace": "Message",
    "name": "GetMessage",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "recipientIntended": {
      "name": "{{STRING}}",
      "label": "{{STRING}}"
    },
    "candidates": [array of Contact]
  }
}
```

| parameter                | type                           | mandatory | description                                                                                                                                                                              |
| ------------------------ | ------------------------------ | --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| recipientIntended        | object                         | N         | 발화에서 분석된 recipient 정보 optional 파라미터로 포함되지 않으면 전체 문자를 보내줘야 함 항목이 존재할 경우 SendCandidates와 동일하게 조건에 맞는 대상자의 문자리스트만 GetMessageSucceeded로 전달하고 항목이 없을 경우 전체 문자리스트를 GetMessageSucceeded로 전달해야함. |
| recipientIntended. name  | string                         | N         | 검색에 요청할때 사용된 상대방 이름 (NLU 분석으로 나온 이름)                                                                                                                                                     |
| recipientIntended. label | string                         | N         | 집, 회사 등을 구분하기 위한 라벨                                                                                                                                                                      |
| candidates               | array of [Contact](./#contact) | N         | candidates가 없으면 이 항목이 없어야 함                                                                                                                                                              |

### ReadMessage

```
{
  "header": {
    "namespace": "Message",
    "name": "ReadMessage",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "receivedTime": "{{STRING}}",
    "token": "{{STRING}}"
  }
}
```

| parameter    | type   | mandatory | description                                                                                                                                                                                                       |
| ------------ | ------ | --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| receivedTime | string | N         | Application에서 읽은 메시지를 처리하기 위한 timeStamp timeStamp 값은 디바이스에서 문자 메시지의 (수신한) 시간값(LONG)으로 GetMessageSucceeded 의 candidates (문자 메시지 리스트) 의 time 값 Application은 해당 시간값 이후에 수신된 문자 메시지를 GetMessageSucceeded 응답데이터로 전달한다. |
| token        | string | Y         | 현재 TTS를 식별하기 위한 unique string                                                                                                                                                                                     |

## Events

### CandidatesListed

* 검색 결과 리스트가 화면에 보여지는 경우 보내는 Event
* list는 context로 전송됨

```
{
  "header": {
    "namespace": "Message",
    "name": "CandidatesListed",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### SendMessageSucceeded

```
{
  "header": {
    "namespace": "Message",
    "name": "SendMessageSucceeded",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "recipient": Contact
  }
}
```

| parameter | type                          | mandatory | description |
| --------- | ----------------------------- | --------- | ----------- |
| recipient | [Contact](message.md#contact) | Y         |             |

### SendMessageFailed

```
{
  "header": {
    "namespace": "Message",
    "name": "SendMessageFailed",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "recipient": Contact,
    "errorCode": "{{STRING}}"
  }
}
```

| parameter | type           | mandatory | description |
| --------- | -------------- | --------- | ----------- |
| recipient | Contact Object | Y         |             |
| errorCode | string         | Y         |             |

### GetMessageSucceeded

```
{
  "header": {
    "namespace": "Message",
    "name": "GetMessageSucceeded",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "candidates": [array of Contact]
  }
}
```

| parameter  | type                    | mandatory | description |
| ---------- | ----------------------- | --------- | ----------- |
| candidates | array of Contact Object | N         |             |

### GetMessageFailed

```
{
  "header": {
    "namespace": "Message",
    "name": "GetMessageFailed",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "errorCode": "{{STRING}}"
  }
}
```

| parameter | type   | mandatory | description |
| --------- | ------ | --------- | ----------- |
| errorCode | string | Y         |             |

### ReadMessageFinished

```
{
  "header": {
    "namespace": "Message",
    "name": "ReadMessageFinished",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}"
  }
}
```

| parameter | type   | mandatory | description                               |
| --------- | ------ | --------- | ----------------------------------------- |
| token     | string | Y         | Message.ReadMessage Directive에서 전달한 token |
