---
description: 음성인식 결과를 Play 로 전달하기 위한 규격
---

# ASR

## Version

최신 버전은 1.2 입니다.

## State Diagram

![](../../.gitbook/assets/image%20%284%29.png)

## SDK Interface

### 음성 인식 요청

1. `아리아` 발화 또는 NUGU Button 선택 시 [Recognize](asr.md#recognize) event 를 전달하여 음성인식을 시작할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/asr/ASRAgentInterface.kt#L189)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AutomaticSpeechRecognition/ASRAgentProtocol.swift#L45)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/asr_interface.hh#L152)

2. 음성인식 진행 상태를 모니터링 할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/asr/ASRAgentInterface.kt#L120)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AutomaticSpeechRecognition/ASRAgentDelegate.swift#L28)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/asr_interface.hh#L84)

3. 음성인식 STT\(SpeechToText\) 결과로 [NotifyResult](asr.md#notifyresult) directive 가 전달됩니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/asr/ASRAgentInterface.kt#L131)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AutomaticSpeechRecognition/ASRAgentDelegate.swift#L32)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/asr_interface.hh#L84)

4. 음성인식 결과 Play 에서 [ExpectSpeech](asr.md#expectspeech) directive 로 음성인식을 재요청 할 수 있습니다.

### 음성 인식 중단

사용자가 음성 인식 중단 요청을 [StopRecognize](asr.md#stoprecognize) event 로 전달할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/asr/ASRAgentInterface.kt#L200)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AutomaticSpeechRecognition/ASRAgentProtocol.swift#L53)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/asr_interface.hh#L163)

## Context

```text
{
  "ASR": {
    "version": "1.2",
    "engine": "{{STRING}}"
  }
}
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">parameter</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">mandatory</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">engine</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>Device &#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xC74C;&#xC131;&#xC778;&#xC2DD;
          engine &#xC744; &#xBA85;&#xC2DC;</p>
        <p>NUGU &#xC74C;&#xC131;&#xC778;&#xC2DD; engine &#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
          &#xACBD;&#xC6B0; &quot;skt&quot;</p>
        <p>(&#xAC12;&#xC744; &#xCC44;&#xC6B0;&#xC9C0; &#xC54A;&#xC73C;&#xBA74; default
          &quot;skt&quot;)</p>
      </td>
    </tr>
  </tbody>
</table>

## Directives

### ExpectSpeech

```text
{
  "header": {
    "namespace": "ASR",
    "name": "ExpectSpeech",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "domainTypes": ["{{STRING}}"],
    "asrContext": {
      "task": "{{STRING}}",
      "sceneId": "{{STRING}}",
      "sceneText": [
        "{{STRING}}"
      ]
    }
  }
}
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">parameter</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">mandatory</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">playServiceId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Y: &#xD68C;&#xC2E0;&#xBC1B;&#xC544;&#xC57C; &#xD558;&#xB294; &#xACBD;&#xC6B0;,
        N: &#xB9C8;&#xC774;&#xD06C;&#xB9CC; &#xC5F4;&#xACE0; &#xC2F6;&#xC740;&#xACBD;&#xC6B0;
        <br
        />default: N</td>
    </tr>
    <tr>
      <td style="text-align:left">property</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p><b>NORMAL</b> - &#xC77C;&#xBC18; &#xBC1C;&#xD654;&#xB97C; &#xC785;&#xB825;&#xC73C;&#xB85C;
          &#xBC1B;&#xC74C;</p>
        <p><b>DICTATION</b> - dictation &#xC11C;&#xBC84;&#xB85C; &#xB77C;&#xC6B0;&#xD305;&#xD558;&#xC5EC;
          &#xCC98;&#xB9AC;</p>
        <p>&#xD544;&#xB4DC;&#xAC00; &#xC5C6;&#xB294; &#xACBD;&#xC6B0; default &#xAC12;&#xC740;
          NORMAL</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">domainTypes</td>
      <td style="text-align:left">Array&lt;String&gt;</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">ExpectSpeech &#xC758;&#xD55C; &#xBC1C;&#xD654;&#xC2DC;&#xC5D0; NLU&#xC5D0;&#xC11C;
        &#xC0AC;&#xC6A9;&#xD560; domainType &#xC14B;&#xD305; &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext.task</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext.sceneId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext.sceneText</td>
      <td style="text-align:left">Array&lt;String&gt;</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### NotifyResult

```text
{
  "header": {
    "namespace": "ASR",
    "name": "NotifyResult",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "token": "{{STRING}}",
    "result": "{{STRING}}",
    "state": "{{STRING}}"
  }
}
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">parameter</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">mandatory</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">token</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Recognize Event&#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;&#xD55C; token &#xAC12;
        (&#xC5B4;&#xB5A4; &#xBC1C;&#xD654;&#xC5D0; &#xB300;&#xD55C; &#xBD84;&#xC11D;
        &#xACB0;&#xACFC;&#xC778;&#xC9C0; &#xC2DD;&#xBCC4;&#xD558;&#xAE30; &#xC704;&#xD55C;
        &#xC6A9;&#xB3C4;)</td>
    </tr>
    <tr>
      <td style="text-align:left">result</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC778;&#xC2DD; &#xACB0;&#xACFC;&#xB97C; &#xC804;&#xC1A1;</td>
    </tr>
    <tr>
      <td style="text-align:left">state</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p><b>PARTIAL</b> : &#xC0AC;&#xC6A9;&#xC790; &#xBC1C;&#xD654;&#xC758; &#xC77C;&#xBD80;&#xBD84;</p>
        <p><b>COMPLETE</b> : &#xC0AC;&#xC6A9;&#xC790; &#xBC1C;&#xD654;&#xC758; &#xC804;&#xCCB4;
          &#xBB38;&#xC7A5;</p>
        <p><b>NONE</b> : &#xC74C;&#xC131; &#xC778;&#xC2DD; &#xACB0;&#xACFC; &#xC5C6;&#xC74C;</p>
        <p><b>ERROR</b> : Error &#xBC1C;&#xC0DD;</p>
        <p><b>SOS</b> : SOS(Start of Speech)</p>
        <p><b>EOS</b> : EOS(End of Speech)</p>
        <p><b>FA</b> : Wakeup False Acceptance</p>
      </td>
    </tr>
  </tbody>
</table>

### CancelRecognize

```text
{
  "header": {
    "namespace": "ASR",
    "name": "CancelRecognize",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "cause": "{{STRING}}"
  }
}
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">parameter</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">mandatory</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">cause</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <ul>
          <li>WAKEUP_POWER: &#xB2E4;&#xB978; wakeup&#xBCF4;&#xB2E4; power&#xAC00; &#xC801;&#xC5B4;&#xC11C;
            &#xCDE8;&#xC18C;&#xB428;</li>
        </ul>
      </td>
    </tr>
  </tbody>
</table>

## Events

### Recognize

```text
{
  "header": {
    "namespace": "ASR",
    "name": "Recognize",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "codec": "{{STRING}}",
    "playServiceId": "{{STRING}}",
    "domainTypes": ["{{STRING}}"],
    "language": "{{STRING}}",
    "endpointing": "{{STRING}}",
    "encoding": "{{STRING}}",
    "wakeup": {
      "word": "{{STRING}}",
      "boundary": {
        "start": {{LONG}},
        "end": {{LONG}},
        "detection": {{LONG}}
      },
      "power": {
        "noise": {{LONG}},
        "speech": {{LONG}}
      }
    },
    "asrContext": {
      "task": "{{STRING}}",
      "sceneId": "{{STRING}}",
      "sceneText": [
        "{{STRING}}"
      ]
    },
    "timeout": {
      "listen": {{LONG}},
      "maxSpeech": {{LONG}},
      "response": {{LONG}}
    }
  }
}
```

<table>
  <thead>
    <tr>
      <th style="text-align:left">parameter</th>
      <th style="text-align:left">type</th>
      <th style="text-align:left">mandatory</th>
      <th style="text-align:left">description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">codec</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left"><b>SPEEX</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">playServiceId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">ExpectSpeech&#xC5D0; &#xC758;&#xD55C; &#xBC1C;&#xD654;&#xC778; &#xACBD;&#xC6B0;&#xC5D0;&#xB9CC;
        ExpectSpeech&#xC5D0;&#xC11C; &#xBC1B;&#xC740; playServiceId&#xB97C; &#xC801;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left">property</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">ExpectSpeech&#xC5D0; &#xC758;&#xD55C; &#xBC1C;&#xD654;&#xC778; &#xACBD;&#xC6B0;&#xC5D0;&#xB9CC;
        ExpectSpeech&#xC5D0;&#xC11C; &#xBC1B;&#xC740; property&#xB97C; &#xC801;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left">domainTypes</td>
      <td style="text-align:left">Array&lt;String&gt;</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">ExpectSpeech&#xC5D0; &#xC758;&#xD55C; &#xBC1C;&#xD654;&#xC778; &#xACBD;&#xC6B0;&#xC5D0;&#xB9CC;
        ExpectSpeech&#xC5D0;&#xC11C; &#xBC1B;&#xC740; domainTypes&#xB97C; &#xC801;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left">language</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p><b>KOR, ENG, JPN, CHN, ...</b>
        </p>
        <p>default &#xAC12;&#xC740; KOR</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">endpointing</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p><b>CLIENT</b> - &#xD074;&#xB77C;&#xC774;&#xC5B8;&#xD2B8; EPD(EndPointDetector)
          &#xC0AC;&#xC6A9;</p>
        <p><b>SERVER</b> - &#xC11C;&#xBC84; EPD &#xC0AC;&#xC6A9;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">encoding</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p><b>PARTIAL</b> - &#xC0AC;&#xC6A9;&#xC790; &#xBC1C;&#xD654;&#xC758; &#xC77C;&#xBD80;&#xBD84;</p>
        <p><b>COMPLETE</b> - &#xC0AC;&#xC6A9;&#xC790; &#xBC1C;&#xD654;&#xC758; &#xC804;&#xCCB4;
          &#xBB38;&#xC7A5; (default)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC11C;&#xBC84; EPD &#xC0AC;&#xC6A9;&#xC2DC; &#xD544;&#xC218; &#xAC12;.</p>
        <p>wakeup&#xC744; &#xD3EC;&#xD568;&#xD574;&#xC11C; &#xC11C;&#xBC84;&#xC5D0;
          &#xC804;&#xB2EC;&#xD558;&#xB294; &#xACBD;&#xC6B0; &#xD3EC;&#xD568;</p>
        <p>wakeup &#xC815;&#xBCF4;&#xB97C; &#xC804;&#xB2EC;&#xD558;&#xB294; &#xACBD;&#xC6B0;
          &#xD3EC;&#xD568; (&#xC804;&#xB2EC;&#xD558;&#xB294; pcm&#xC5D0; wakeup&#xC774;
          &#xD3EC;&#xD568;&#xB418;&#xC9C0; &#xC54A;&#xB354;&#xB77C;&#xB3C4; &#xD544;&#xC694;&#xD55C;
          &#xACBD;&#xC6B0; &#xC804;&#xB2EC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.word</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xC804;&#xC1A1;&#xD558;&#xB294; stream&#xC5D0; &#xD3EC;&#xD568;&#xB41C;
        wakeup word( ex &quot;&#xC544;&#xB9AC;&#xC544;&quot;)</td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.boundary</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC804;&#xC1A1;&#xD558;&#xB294; stream&#xC5D0;&#xC11C; wakeup word&#xC5D0;
        &#xB300;&#xD55C; boundary &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.boundary.start</td>
      <td style="text-align:left">LONG</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>wakeup module &#xC5D0;&#xC11C; &#xC5BB;&#xC740; milliseconds &#xB97C;
          sample count &#xB85C; &#xBCC0;&#xD658;&#xD574;&#xC11C; &#xC804;&#xC1A1;&#xD574;&#xC57C;
          &#xD568;.</p>
        <p>sample count for start time</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.boundary.end</td>
      <td style="text-align:left">LONG</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>wakeup module &#xC5D0;&#xC11C; &#xC5BB;&#xC740; milliseconds &#xB97C;
          sample count &#xB85C; &#xBCC0;&#xD658;&#xD574;&#xC11C; &#xC804;&#xC1A1;&#xD574;&#xC57C;
          &#xD568;.</p>
        <p>sample count for end time</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.boundary.detection</td>
      <td style="text-align:left">LONG</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>wakeup module &#xC5D0;&#xC11C; &#xC5BB;&#xC740; milliseconds &#xB97C;
          sample count &#xB85C; &#xBCC0;&#xD658;&#xD574;&#xC11C; &#xC804;&#xC1A1;&#xD574;&#xC57C;
          &#xD568;.</p>
        <p>sample count for detection time</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.boundary.metric</td>
      <td style="text-align:left">STRING</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p><b>sample(default) / byte / frame / time</b>
        </p>
        <p>&#xD604;&#xC7AC; sample &#xB9CC; &#xC9C0;&#xC6D0;&#xB418;&#xBA70;, &#xCD94;&#xD6C4;
          byte / frame / time &#xC18D;&#xC131; &#xC9C0;&#xC6D0; &#xC608;&#xC815;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.power</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC804;&#xC1A1;&#xD558;&#xB294; stream&#xC5D0; &#xD3EC;&#xD568;&#xB41C;
        wakeup pcm&#xC758; power&#xAC12;</td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.power.noise</td>
      <td style="text-align:left">Float</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">wakeup pcm&#xC758; power&#xC911; noise&#xB97C; &#xC758;&#xBBF8;&#xD558;&#xB294;
        &#xAC12; (&#xC8FC;&#xB85C; min&#xAC12;)</td>
    </tr>
    <tr>
      <td style="text-align:left">wakeup.power.speech</td>
      <td style="text-align:left">Float</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">wakeup pcm&#xC758; power&#xC911; speech&#xB97C; &#xC758;&#xBBF8;&#xD558;&#xB294;
        &#xAC12; (&#xC8FC;&#xB85C; max&#xAC12;)</td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">ExpectSpeech&#xC5D0; &#xC758;&#xD55C; &#xBC1C;&#xD654;&#xC778; &#xACBD;&#xC6B0;&#xC5D0;&#xB9CC;
        ExpectSpeech&#xC5D0;&#xC11C; &#xBC1B;&#xC740; asrContext&#xB97C; &#xC801;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext.task</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext.sceneId</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">asrContext.sceneText</td>
      <td style="text-align:left">Array&lt;String&gt;</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">timeout</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">Server EPD &#xC0AC;&#xC6A9;&#xC2DC; &#xD544;&#xC218; &#xAC12;.</td>
    </tr>
    <tr>
      <td style="text-align:left">timeout.listen</td>
      <td style="text-align:left">LONG</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>SOS &#xB97C; &#xAE30;&#xB2E4;&#xB9AC;&#xB294; &#xC2DC;&#xAC04;</p>
        <p>milliseconds</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout.maxSpeech</td>
      <td style="text-align:left">LONG</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>SOS&#xC774;&#xD6C4; EOS&#xB97C; &#xAE30;&#xB2E4;&#xB9AC;&#xB294; &#xC2DC;&#xAC04;</p>
        <p>milliseconds</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">timeout.response</td>
      <td style="text-align:left">LONG</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>EOS &#xC774;&#xD6C4; &#xC751;&#xB2F5;&#xC744; &#xAE30;&#xB2E4;&#xB9AC;&#xB294;
          &#xC2DC;&#xAC04;</p>
        <p>milliseconds</p>
      </td>
    </tr>
  </tbody>
</table>

### StopRecognize

```text
{
  "header": {
    "namespace": "ASR",
    "name": "StopRecognize",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

