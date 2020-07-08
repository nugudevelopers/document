---
description: 음성 합성 결과를 전달받기 위한 규격
---

# TTS

## Version

최신 버전은 1.1 입니다.

## SDK Interface

### 재생 상태 정보

재생 상태를 모니터링 할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/tts/TTSAgentInterface.kt#L48)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/TextToSpeech/TTSAgentDelegate.swift#L29)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/tts_interface.hh#L68)

## Context

```text
{
  "TTS": {
    "version": "1.1",
    "ttsActivity": "{{STRING}}",
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
      <td style="text-align:left">ttsActivity</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>TTS &#xC7AC;&#xC0DD; &#xC0C1;&#xD0DC;</p>
        <p><b>IDLE, PLAYING, PAUSED, FINISHED, STOPPED</b>
        </p>
        <ul>
          <li>IDLE&#xC778; &#xACBD;&#xC6B0;&#xB294; &#xCD5C;&#xCD08; &#xC804;&#xC6D0;&#xC744;
            &#xCF30;&#xC744; &#xB54C;&#xB9CC; &#xAC00;&#xB2A5;&#xD558;&#xACE0; &#xC774;&#xD6C4;&#xC5D0;&#xB294;
            &#xB098;&#xC62C; &#xC218; &#xC5C6;&#xC74C;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">engine</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>Device &#xC5D0;&#xC11C; &#xC0AC;&#xC6A9;&#xD558;&#xB294; &#xC74C;&#xC131;&#xD569;&#xC131;
          engine &#xC744; &#xBA85;&#xC2DC;</p>
        <p>NUGU &#xC74C;&#xC131;&#xD569;&#xC131; engine &#xC744; &#xC0AC;&#xC6A9;&#xD558;&#xB294;
          &#xACBD;&#xC6B0; &quot;skt&quot;</p>
        <p>(&#xAC12;&#xC744; &#xCC44;&#xC6B0;&#xC9C0; &#xC54A;&#xC73C;&#xBA74; default
          &quot;skt&quot;)</p>
      </td>
    </tr>
  </tbody>
</table>

## Directive

### Speak

새로운 TTS 재생 요청입니다.

```text
{
  "header": {
    "namespace": "TTS",
    "name": "Speak",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "sourceType": "{{STRING}}",
    "format": "{{STRING}}",
    "text": "{{STRING}}",
    "token": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| sourceType | string | N | URL or ATTACHMENT\(default 는 ATTACHMENT\) |
| format | string | Y | **TEXT** or **SKML** |
| text | string | Y | tts text |
| token | string | Y | 현재 TTS를 식별하기 위한 unique string |

### Stop

현재 TTS 중지 요청입니다.

```text
{
  "header": {
    "namespace": "TTS",
    "name": "Stop",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```















