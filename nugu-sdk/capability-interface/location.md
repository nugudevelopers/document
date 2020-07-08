---
description: 디바이스 위치 정보를 Play 로 전달하기 위한 규격
---

# Location

## Version

최신 버전은 1.0 입니다.

## SDK Interface

### Context 구성

디바이스 위치 정보를 [Context](location.md#context) 에 포함시켜 주어야 합니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/location/LocationProvider.kt#L26)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Location/LocationAgentDelegate.swift#L31)

## Context

```text
{
  "Location": {
    "version": "1.0",
    "current": {
      "latitude": "{{STRING}}",
      "longitude": "{{STRING}}"
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
      <td style="text-align:left">current</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xD604;&#xC7AC; &#xC704;&#xCE58;&#xC758; &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>current.</p>
        <p>latitude</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xC704;&#xB3C4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>current.</p>
        <p>longitude</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xACBD;&#xB3C4;</td>
    </tr>
  </tbody>
</table>

