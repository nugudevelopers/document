# AudioPlayer

## Version

최신 버전은 1.2 입니다.

##  State Diagram

![](../../.gitbook/assets/image%20%285%29.png)

## SDK Interface

### 재생 상태 정보

재생 상태를 모니터링 할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/audioplayer/AudioPlayerAgentInterface.kt#L42)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AudioPlayer/AudioPlayerAgentDelegate.swift#L28)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/audio_player_interface.hh#L89)

### UI 구성

AudioPlayer 로 음원을 재생할 때 화면을 구성하기 위해 필요한 데이터는 [Play](audioplayer.md#play) directive 의 `audioItem.metadata.template` 에 포함되어 전달됩니다.

[Stop](audioplayer.md#stop) directive 또는 SDK 내부 timer 등에 의해 종료될 수 있으며, [UpdateMetadata](audioplayer.md#updatemetadata) directive 에 의해 변경될 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/display/DisplayAggregatorInterface.kt#L41)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AudioPlayer/Display/AudioPlayerDisplayDelegate.swift#L24)

### UI 제어

[AudioPlayer.Template1](audioplayer.md#audioitem-metadata-template-audioplayer-template1) 에 포함된 가사의 화면은 `사용자 발화` 에 따라 [ShowLyrics](audioplayer.md#showlyrics), [HideLyrics](audioplayer.md#hidelyrics), [ControlLyricsPage](audioplayer.md#controllyricspage) directive 로 제어될 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/audioplayer/lyrics/LyricsPresenter.kt#L18)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AudioPlayer/Display/AudioPlayerDisplayDelegate.swift#L24)

### 제어 명령

PUI, GUI 등으로 사용자가 [다음](audioplayer.md#nextcommandissued)/[이전](audioplayer.md#previouscommandissued)/[즐겨찾기](audioplayer.md#favoritecommandissued)/[반복](audioplayer.md#repeatcommandissued)/[셔플](audioplayer.md#shufflecommandissued) 요청을 event 로 전달할 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/audioplayer/AudioPlayerAgentInterface.kt#L112)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/AudioPlayer/AudioPlayerAgentProtocol.swift#L60)

[Linux reference](https://github.com/nugu-developers/nugu-linux/blob/master/include/capability/audio_player_interface.hh#L169)

## Context

```text
{
  "AudioPlayer": {
    "version": "1.2",
    "playerActivity":{{STRING}}",
    "token": "{{STRING}}",
    "offsetInMilliseconds": {{LONG}},
    "durationInMilliseconds": {{LONG}},
    "lyricsVisible": {{BOOLEAN}}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| playerActivity | string | Y | 현재 state |
| token | string | N | 현재 사용 중인 음원의 토큰 |
| offsetInMilliseconds | long | Y | 현재 사용 중인 음원의 offset |
| durationInMilliseconds | long | N | 현재 사용 중인 음원의 전체 재생시간\(알수 없으면 보내주지 않음\) |
| lyricsVisible | boolean | N | AudioPlayer에서 가사 화면이 보여지고 있는지 여부 가사를 보여줄 수 없는 Device에서는 lyricsVisible를 보내지 않음 |

## Directives

### Play

새로운 음원 또는 현재 음원 재생 요청입니다.\(Play, Resume, Seek 요청이 포함되어 있습니다.\)

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "Play",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "sourceType": "{{STRING}}",
    "cacheKey": "{{STRING}}",
    "audioItem": {
      "stream": {
        "url": "{{STRING}}",
        "offsetInMilliseconds": {{LONG}},
        "progressReport": {
          "progressReportDelayInMilliseconds": {{LONG}},
          "progressReportIntervalInMilliseconds": {{LONG}}
        },
        "token": "{{STRING}}",
        "expectedPreviousToken": "{{STRING}}"
      },
      "metadata": {
        "template": {}
      }
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
      <td style="text-align:left">sourceType</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>URL or ATTACHMENT(default &#xB294; URL)</p>
        <ul>
          <li>ATTACHMENT &#xC77C; &#xACBD;&#xC6B0; stream&#xC5D0; url&#xC774; &#xC874;&#xC7AC;
            &#xD558;&#xC9C0; &#xC54A;&#xC74C;</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">cacheKey</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">-. &#xB514;&#xBC14;&#xC774;&#xC2A4;&#xC5D0;&#xC11C; &#xBBF8;&#xB514;&#xC5B4;
        &#xCE90;&#xC2DC;&#xB97C; &#xC704;&#xD55C; unique key
        <br />(&#xB514;&#xBC14;&#xC774;&#xC2A4; &#xCE90;&#xC2DC; &#xAE30;&#xB2A5;&#xC740;
        &#xD544;&#xC218;&#xAC00; &#xC544;&#xB2D8;)
        <br />-. &#xCE90;&#xC2DC;&#xAC00; &#xBD88;&#xAC00;&#xB2A5;&#xD55C; &#xBBF8;&#xB514;&#xC5B4;
        &#xC774;&#xBA74; &#xB514;&#xBC14;&#xC774;&#xC2A4;&#xB85C; &#xB0B4;&#xB824;&#xC8FC;&#xC9C0;
        &#xC54A;&#xC74C;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream</p>
      </td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream.</p>
        <p>url</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC624;&#xB514;&#xC624; &#xCEE8;&#xD150;&#xCE20;&#xC758; URL (URL&#xC5D0;
          &#xC758;&#xD55C; streaming&#xB9CC; &#xC9C0;&#xC6D0;)</p>
        <p>sourceType &#xC774; ATTACHMENT&#xC77C; &#xACBD;&#xC6B0; &#xC5C6;&#xC74C;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream.</p>
        <p>offsetInMilliseconds</p>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xC2DC;&#xC791;&#xBD80;&#xD130; &#xC5BC;&#xB9C8;&#xB9CC;&#xD07C;&#xC758;
        offset&#xBD80;&#xD130; &#xC7AC;&#xC0DD;&#xD560;&#xC9C0; &#xC124;&#xC815;.
        0&#xC774;&#xBA74; &#xCC98;&#xC74C;&#xBD80;&#xD130; &#xC7AC;&#xC0DD;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream.</p>
        <p>progressReport.</p>
        <p>progressReportDelayInMilliseconds</p>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC7AC;&#xC0DD;&#xC744; &#xC2DC;&#xC791;&#xD574;&#xC11C; &#xC9C0;&#xC815;&#xB41C;
          &#xC2DC;&#xAC04; &#xB4A4;&#xC5D0; &#xD55C; &#xBC88; progressReportDelayElapsed
          Event&#xAC00; &#xBC1C;&#xC0DD;</p>
        <p>(offsetInMilliseconds &#xAC12;&#xACFC;&#xB294; &#xBB34;&#xAD00;&#xD558;&#xAC8C;
          &#xCEE8;&#xD150;&#xCE20; &#xC2DC;&#xC791; &#xC2DC;&#xAC04; &#xAE30;&#xC900;&#xC73C;&#xB85C;
          &#xC808;&#xB300;&#xAC12;&#xC744; &#xC758;&#xBBF8;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream.</p>
        <p>progressReport.</p>
        <p>progressReportIntervalInMilliseconds</p>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC7AC;&#xC0DD;&#xC744; &#xC2DC;&#xC791;&#xD574;&#xC11C; &#xC9C0;&#xC815;&#xB41C;
          &#xC8FC;&#xAE30;&#xB9C8;&#xB2E4; progressReportIntervalElapsed Event&#xAC00;
          &#xBC1C;&#xC0DD;</p>
        <p>(offsetInMilliseconds &#xAC12;&#xACFC;&#xB294; &#xBB34;&#xAD00;&#xD558;&#xAC8C;
          &#xCEE8;&#xD150;&#xCE20; &#xC2DC;&#xC791; &#xC2DC;&#xAC04; &#xAE30;&#xC900;&#xC73C;&#xB85C;
          &#xC808;&#xB300;&#xAC12;&#xC744; &#xC758;&#xBBF8;)
          <br />
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream.</p>
        <p>token</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD604;&#xC7AC; stream&#xC744; &#xB098;&#xD0C0;&#xB0B4;&#xB294; token</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>stream.</p>
        <p>expectedPreviousToken</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC774;&#xC804; stream&#xC744; &#xB098;&#xD0C0;&#xB0B4;&#xB294; token</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>metadata</p>
      </td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>audioItem.</p>
        <p>metadata.</p>
        <p>template</p>
      </td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xAC01; type&#xBCC4; &#xD3EC;&#xB9F7;&#xC740; &#xC544;&#xB798;&#xC5D0;
        &#xAE30;&#xC220;
        <br />template&#xC774; &#xC815;&#xC758;&#xB418;&#xC9C0; &#xC54A;&#xC740; &#xACBD;&#xC6B0;
        Display&#xB97C; &#xD3EC;&#xD568;&#xD558;&#xB294; &#xB514;&#xBC14;&#xC774;&#xC2A4;&#xB294;
        Default &#xD654;&#xBA74;&#xC744; &#xBCF4;&#xC5EC;&#xC8FC;&#xC5B4;&#xC57C;
        &#xD568;</td>
    </tr>
  </tbody>
</table>

#### audioItem.metadata.template - AudioPlayer.Template1

```text
{
  "metadata": {
    "disableTemplate": {{BOOLEAN}},
    "template": {
      "type": "AudioPlayer.Template1",
      "title": {
        "iconUrl": "{{STRING}}",
        "text": "{{{STRING}}"
      },
      "grammarGuide": ["{{STRING}}"],
      "content": {
        "title": "{{STRING}}",
        "subtitle1": "{{STRING}}",
        "subtitle2": "{{STRING}}",
        "imageUrl": "{{STRING}}",
        "durationSec": "{{STRING}}",
        "backgroundImageUrl": "{{STRING}}",
        "backgroundColor": "{{STRING}}",
        "badgeImageUrl": "{{String}}",
        "badgeMessage": "{{String}}",
        "lyrics": {
          "title": "{{String}}",
          "lyricsType": "{{String}}",
          "lyricsInfoList": [
            {
              "time": {{Integer}},
              "text": "{{String}}"
            }
          ]
        },
        "settings": {
          "favorite": {{BOOLEAN},
          "repeat": "{{String}}",
          "shuffle": {{BOOLEAN}}
        }
      }
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
      <td style="text-align:left">disableTemplate</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>true&#xBA74; &#xC2A4;&#xD06C;&#xB9B0;&#xC744; &#xAC00;&#xC9C4; &#xB514;&#xBC14;&#xC774;&#xC2A4;&#xC5D0;&#xC11C;
          AudioPlayer &#xC7AC;&#xC0DD; &#xC2DC; template&#xC744; display&#xD558;&#xC9C0;
          &#xC54A;&#xC74C;</p>
        <p>default - false</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>type</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">
        <p>AudioPlayer template type</p>
        <p>AudioPlayer.Template1</p>
        <p>AudioPlayer.Template2</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>title.</p>
        <p>iconUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">icon image url</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>title.</p>
        <p>text</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">title text</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>title</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">content &#xC601;&#xC5ED;&#xC758; title</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>subtitle1</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">subtitle1</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>subtitle2</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">subtitle2</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>imageUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">image url</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>durationSec</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">content duration in sec</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>backgroundImageUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">background image url</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>backgroundColor</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>background color</p>
        <p>default - &quot;#000&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>badgeImageUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC774;&#xBBF8;&#xC9C0;(content.imageUrl)&#xC758; &#xC624;&#xB978;&#xCABD;
        &#xC0C1;&#xB2E8;&#xC5D0; &#xD45C;&#xC2DC;&#xB420; Badge Image&#xC758; URL</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>badgeMessage</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC774;&#xBBF8;&#xC9C0;(content.imageUrl)&#xC758; &#xC67C;&#xCABD; &#xD558;&#xB2E8;&#xC5D0;
        &#xD45C;&#xC2DC;&#xB420; Badge Message</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>lyrics</p>
      </td>
      <td style="text-align:left">obejct</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xAC00;&#xC0AC; &#xD654;&#xBA74;&#xC744; &#xD45C;&#xC2DC;&#xD558;&#xAE30;
        &#xC704;&#xD55C; &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>lyrics.</p>
        <p>title</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xAC00;&#xC0AC; &#xD654;&#xBA74;&#xC5D0;&#xC11C; &#xBCF4;&#xC5EC;&#xC9C8;
        &#xC81C;&#xBAA9;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>lyrics.</p>
        <p>lyricsType</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xAC00;&#xC0AC;&#xC758; &#xC885;&#xB958;
        <br />NONE(&#xC790;&#xB9C9; &#xC5C6;&#xC74C;), SYNC(&#xC790;&#xB9C9; &#xB3D9;&#xAE30;&#xD654;),
        NON_SYNC(&#xC790;&#xB9C9; &#xB3D9;&#xAE30;&#xD654; &#xC5C6;&#xC74C;)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>lyrics.</p>
        <p>lyricsInfoList</p>
      </td>
      <td style="text-align:left">array of lyricsInfo</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xAC00;&#xC0AC; &#xB0B4;&#xC6A9;(lyricsInfo)&#xC758; &#xBAA9;&#xB85D;
        <br
        />&#xAE30;&#xBCF8; &#xAC12;&#xC740; &#xBE48; &#xBC30;&#xC5F4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>lyrics.</p>
        <p>lyricsInfoList.</p>
        <p>time</p>
      </td>
      <td style="text-align:left">integer</td>
      <td style="text-align:left">Y(lyricsType == SYNC)</td>
      <td style="text-align:left">lyricsInfo&#xAC00; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294; &#xC2DC;&#xC810;&#xC758;
        millisecond &#xB2E8;&#xC704;&#xC758; &#xC2DC;&#xAC04; &#xC815;&#xBCF4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>lyrics.</p>
        <p>lyricsInfoList.</p>
        <p>text</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">lyricsInfo&#xAC00; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294; &#xC2DC;&#xC810;&#xC758;
        &#xAC00;&#xC0AC; &#xB0B4;&#xC6A9;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>settings</p>
      </td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xC124;&#xC815;&#xD55C; &#xC815;&#xBCF4;&#xB97C;
        &#xD45C;&#xC2DC;&#xD568;
        <br />- Play&#xC5D0;&#xC11C;&#xB294; &#xD45C;&#xC2DC;&#xD560; &#xD558;&#xC704;
        field&#xB97C; &#xC124;&#xC815;&#xD560; &#xC218; &#xC788;&#xC74C;
        <br />- &#xC124;&#xC815;&#xD55C; field&#xC5D0; &#xB300;&#xD55C; Event&#xC640;
        Directive&#xB97C; &#xC0AC;&#xC6A9;&#xD560; &#xC218; &#xC788;&#xC74C;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>settings.</p>
        <p>favorite</p>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC7AC;&#xC0DD; &#xC911;&#xC778; &#xC74C;&#xC6D0;&#xC5D0; &#xB300;&#xD55C;
        &#xC88B;&#xC544;&#xC694; &#xC5EC;&#xBD80;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>settings.</p>
        <p>repeat</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC7AC;&#xC0DD; &#xBAA9;&#xB85D;&#xC5D0; &#xB300;&#xD55C; &#xBC18;&#xBCF5;
        &#xC124;&#xC815;
        <br />ALL(&#xC804;&#xACE1; &#xBC18;&#xBCF5;), ONE(&#xD55C;&#xACE1; &#xBC18;&#xBCF5;),
        NONE(&#xBC18;&#xBCF5; &#xC5C6;&#xC74C;)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>settings.</p>
        <p>shuffle</p>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC7AC;&#xC0DD; &#xBAA9;&#xB85D;&#xC758; &#xC74C;&#xC6D0;&#xC744; &#xC784;&#xC758;&#xC758;
        &#xC21C;&#xC11C;&#xB85C; &#xC7AC;&#xC0DD;&#xD560;&#xC9C0; &#xC5EC;&#xBD80;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>grammarGuide</p>
      </td>
      <td style="text-align:left">list of string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xBC1C;&#xD654; &#xB3C4;&#xC6C0;&#xB9D0;</td>
    </tr>
  </tbody>
</table>

#### audioItem.metadata.template - AudioPlayer.Template2

```text
{
  "metadata": {
    "disableTemplate": {{BOOLEAN}},
    "template": {
      "type": "AudioPlayer.Template2",
      "title": {
        "iconUrl": "{{STRING}}",
        "text": "{{STRING}}"
      },
      "grammarGuide": ["{{STRING}}"],
      "content": {
        "title": "{{STRING}}",
        "subtitle": "{{STRING}}",
        "imageUrl": "{{STRING}}",
        "durationSec": "{{STRING}}",
        "backgroundColor": "{{STRING}}"
      }
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
      <td style="text-align:left">disableTemplate</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>true&#xBA74; &#xC2A4;&#xD06C;&#xB9B0;&#xC744; &#xAC00;&#xC9C4; &#xB514;&#xBC14;&#xC774;&#xC2A4;&#xC5D0;&#xC11C;
          AudioPlayer &#xC7AC;&#xC0DD; &#xC2DC; template&#xC744; display&#xD558;&#xC9C0;
          &#xC54A;&#xC74C;</p>
        <p>default - false</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>type</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">
        <p>AudioPlayer template type</p>
        <p>AudioPlayer.Template1</p>
        <p>AudioPlayer.Template2</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>title.</p>
        <p>iconUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">icon image url</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>title.</p>
        <p>text</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">title text</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>title</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">content &#xC601;&#xC5ED;&#xC758; title</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>subtitle</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">subtitle</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>imageUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">image url</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>durationSec</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">content duration in sec</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>backgroundImageUrl</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">background image url</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>content.</p>
        <p>backgroundColor</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>background color</p>
        <p>default - &quot;#000&quot;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>template.</p>
        <p>grammarGuide</p>
      </td>
      <td style="text-align:left">list of string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xBC1C;&#xD654; &#xB3C4;&#xC6C0;&#xB9D0;</td>
    </tr>
  </tbody>
</table>

### Stop

음원 재생 중지 요청입니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "Stop",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### Pause

음원 일시정지 요청입니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "Pause",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### UpdateMetadata

음원의 Metadata UI 설정 정보를 갱신 요청입니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "UpdateMetadata",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "metadata": {
      "template": {
        "content": {
          "settings": {
            "favorite": {{BOOLEAN}},
            "repeat": "{{STRING}}",
            "shuffle": {{BOOLEAN}}
          }
        }
      }
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
      <td style="text-align:left">
        <p>metadata.</p>
        <p>template.</p>
        <p>content.</p>
        <p>settings.</p>
        <p>favorite</p>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">AudioPlayer.Template1&#xC758; settings.favorite &#xC640; &#xC5F0;&#xB3D9;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>metadata.</p>
        <p>template.</p>
        <p>content.</p>
        <p>settings.</p>
        <p>repeat</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">AudioPlayer.Template1&#xC758; settings.repeat &#xACFC; &#xC5F0;&#xB3D9;
        <br
        />ALL(&#xC804;&#xACE1; &#xBC18;&#xBCF5;), ONE(&#xD55C;&#xACE1; &#xBC18;&#xBCF5;),
        NONE(&#xBC18;&#xBCF5; &#xC5C6;&#xC74C;)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>metadata.</p>
        <p>template.</p>
        <p>content.</p>
        <p>settings.</p>
        <p>shuffle</p>
      </td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">AudioPlayer.Template1&#xC758; settings.shuffle &#xACFC; &#xC5F0;&#xB3D9;</td>
    </tr>
  </tbody>
</table>

### ShowLyrics

가사화면 표시 요청입니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "ShowLyrics",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### HideLyrics

가사화면 닫기 요청입니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "HideLyrics",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### ControlLyricsPage

가사화면 스크롤 위치 이동 요청입니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "ControlLyricsPage",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "direction": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| direction | string | Y | 이전과 다음 PREVIOUS, NEXT |

## Events

### NextCommandIssued

사용자가 다음 음원 재생을 요청하면 전송됩니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "NextCommandIssued",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "offsetInMilliseconds": {{LONG}}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| token | string | Y | 현재 재생 중인 stream의 token |
| offsetInMilliseconds | long | Y | 현재 재생 중은 stream의 offset 값 |

### PreviousCommandIssued

사용자가 이전 음원 재생을 요청하면 전송됩니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "PreviousCommandIssued",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.0"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "offsetInMilliseconds": {{LONG}}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| token | string | Y | 현재 재생 중인 stream의 token |
| offsetInMilliseconds | long | Y | 현재 재생 중은 stream의 offset 값 |

### FavoriteCommandIssued

사용자가 현재 음원 즐겨찾기\(좋아요 포함\)를 요청하면 전송됩니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "FavoriteCommandIssued",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "favorite": {{BOOLEAN}}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| favorite | boolean | Y | 재생 중인 음원에 대한 좋아요 여부 |

### RepeatCommandIssued

사용자가 현재 음원 반복 재생을 요청하면 전송됩니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "RepeatCommandIssued",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "repeat": {{BOOLEAN}}
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
      <td style="text-align:left">repeat</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>&#xC7AC;&#xC0DD; &#xBAA9;&#xB85D;&#xC5D0; &#xB300;&#xD55C; &#xBC18;&#xBCF5;
          &#xC124;&#xC815;</p>
        <p>ALL(&#xC804;&#xACE1; &#xBC18;&#xBCF5;), ONE(&#xD55C;&#xACE1; &#xBC18;&#xBCF5;),
          NONE(&#xBC18;&#xBCF5; &#xC5C6;&#xC74C;)</p>
      </td>
    </tr>
  </tbody>
</table>

### ShuffleCommandIssued

사용자가 셔플 재생을 요청하면 전송됩니다.

```text
{
  "header": {
    "namespace": "AudioPlayer",
    "name": "ShuffleCommandIssued",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "shuffle": {{BOOLEAN}}
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| shuffle | boolean | Y | 재생 목록의 음원을 임의의 순서로 재생할지 여부 |

