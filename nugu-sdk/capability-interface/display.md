# Display

## Version

최신 버전은 1.3 입니다.

## SDK Interface

### Context 구성

Template 화면의 상태 정보를 [Context](display.md#context) 에 포함시켜 주어야 합니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/display/DisplayAggregatorInterface.kt#L77)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Display/DisplayAgentDelegate.swift#L24)

### UI 구성

Display 로 화면을 구성하기 위해 필요한 데이터는 [Template](display.md#directive-template) directive 에 포함되어 전달됩니다.

Template 화면은 [Close](display.md#close) directive 또는 SDK 내부 timer 등에 의해 종료될 수 있으며, [Update](display.md#update) directive 에 의해 변경될 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/display/DisplayAggregatorInterface.kt#L41)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Display/DisplayAgentDelegate.swift#L24)

### UI 제어

Template 의 focus 와 scroll 은 `사용자 발화` 에 따라 [ControlFocus](display.md#controlfocus), [ControlScroll](display.md#controlscroll) directive 로 제어될 수 있습니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/display/DisplayAggregatorInterface.kt#L77)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Display/DisplayAgentDelegate.swift#L24)

### 사용자 인터렉션 처리

Template 하위 항목 선택시 [ElementSelected](display.md#elementselected) event 가 전달됩니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/display/DisplayInterface.kt#L34)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Display/DisplayAgentProtocol.swift#L42)

Template 에 화면에 대한 사용자 interaction 발생시 SDK 로 notify 해주어야 내부 timer\(template 일정시간 노출 후 종료하기 위한\) 가 갱신됩니다.

[Android reference](https://github.com/nugu-developers/nugu-android/blob/master/nugu-agent/src/main/java/com/skt/nugu/sdk/agent/display/DisplayAggregatorInterface.kt#L84)

[iOS reference](https://github.com/nugu-developers/nugu-ios/blob/master/NuguAgents/Sources/CapabilityAgents/Display/DisplayAgentProtocol.swift#L45)

## Context

```text
{
  "Display": {
    "version": "1.3",
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "focusedItemToken": "{{STRING}}",
    "visibleTokenList": [
      "{{STRING}}"
    ]
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| token | string | N | 클릭하는 template을 식별하기 위한 unique identifier |
| focusedItemToken | string | N | 현재 화면에 List Template이 보여지고 있을 때, 포커스된 item을 식별하기 위한 unique identifier focusable이 true인 List Template이 보여지고 있을 때는 반드시 focusedItemToken이 존재해야 함 |
| visibleTokenList | list | N | 현재 화면에 List Template이 보여지고 있을 때, 보여지고 있는 item들을 식별하기 위한 unique identifier 목록 List Template이 보여지고 있을 때는 반드시 visibleTokenList이 존재해야 함 |

## Common Objects

Template 에 사용되는 공통 object 의 데이터 구조입니다.

### ImageObject

```text
{
  "contentDescription": "{{STRING}}",
  "sources": [
    {
      "url": "{{STRING}}",
      "size": "{{STRING}}",
      "widthPixels": {{LONG}},
      "heightPixels": {{LONG}}
    }
  ]
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
      <td style="text-align:left">contentDescription</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">sources</td>
      <td style="text-align:left">list</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xB9AC;&#xC2A4;&#xD2B8;&#xB85C; &#xC81C;&#xACF5;&#xB418;&#xBA70; &#xD074;&#xB77C;&#xC774;&#xC5B8;&#xD2B8;&#xC5D0;&#xC11C;
        &#xD654;&#xBA74; &#xD06C;&#xAE30;&#xC5D0; &#xAC00;&#xC7A5; &#xC801;&#xD569;&#xD55C;
        &#xC774;&#xBBF8;&#xC9C0;&#xB97C; &#xC0AC;&#xC6A9;&#xD574;&#xC57C; &#xD568;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>sources.</p>
        <p>url</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>sources.</p>
        <p>size</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">X_SMALL, SMALL, MEDIUM, LARGE, X_LARGE</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>sources.</p>
        <p>widthPixels</p>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>sources.</p>
        <p>heightPixels</p>
      </td>
      <td style="text-align:left">long</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

| size value | Recommended Size \(in pixels\) |
| :--- | :--- |
| X\_SMALL | 480 x 320 |
| SMALL | 720 x 480 |
| MEDIUM | 960 x 640 |
| LARGE | 1280 x 800 |
| X\_LARGE | 1920 x 1080 |

### TextObject

```text
{
  "text": "{{STRING}}",
  "color": "{{STRING}}"
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
      <td style="text-align:left">text</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">
        <p>Text &#xC911;&#xAC04;&#xC5D0; &#xAC15;&#xC870; &#xD45C;&#xD604;&#xC744;
          &#xC704;&#xD55C; &#xB9C8;&#xD06C;&#xC5C5; &#xC0AC;&#xC6A9; &#xAC00;&#xB2A5;
          &#xC2A4;&#xD399;</p>
        <ul>
          <li>&#xBCFC;&#xB4DC; :&lt;b&gt;&#xBCFC;&#xB4DC;&lt;/b&gt;</li>
          <li>&#xAE30;&#xC6B8;&#xB9BC; :&lt;i&gt;<em>&#xAE30;&#xC6B8;&#xB9BC;</em>&lt;/i&gt;</li>
          <li>&#xBC11;&#xC904; : &lt;u&gt;&#xBC11;&#xC904;&lt;/u&gt;</li>
          <li>&#xC717;&#xCCA8;&#xC790; : &lt;sup&gt;&#xC717;&#xCCA8;&#xC790;&lt;/sup&gt;</li>
          <li>&#xC544;&#xB798;&#xCCA8;&#xC790; : &lt;sub&gt;&#xC544;&#xB798;&#xCCA8;&#xC790;&lt;/sub&gt;</li>
          <li>&#xCDE8;&#xC18C;&#xC120; :&lt;s&gt;&#xCDE8;&#xC18C;&#xC120;&lt;/s&gt;</li>
          <li>&#xC0C9;&#xC0C1; : &lt;font color=&quot;red&quot;&gt;&#xBE68;&#xAC15;&lt;/font&gt;</li>
        </ul>
        <p>&#xC704;&#xC5D0; &#xC694;&#xC18C;&#xC678; &#xB2E4;&#xB978; &#xB9C8;&#xD06C;&#xC5C5;
          &#xC0AC;&#xC6A9; &#xC2DC; &#xB9C8;&#xD06C;&#xC5C5; &#xC694;&#xC18C; &#xC0AC;&#xC6A9;
          &#xBD88;&#xAC00;, &#xC6D0;&#xBCF8; &#xD45C;&#xC2DC;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">color</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>color &#xD615;&#xC2DD; (RGB)</p>
        <p>default &#xAC12;&#xC740; &#xB514;&#xBC14;&#xC774;&#xC2A4;&#xB9C8;&#xB2E4;
          &#xB2E4;&#xB984;</p>
      </td>
    </tr>
  </tbody>
</table>

### Button Object

```text
{
  "type": "{{STRING}}",
  "text": "{{STRING}}",
  "image": ImageObject,
  "token": "{{STRING}}"
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
      <td style="text-align:left">type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">text(default), image &#xC911; &#xD558;&#xB098;&#xC758; &#xAC12;&#xC744;
        &#xAC00;&#xC9C8; &#xC218; &#xC788;&#xC2B5;&#xB2C8;&#xB2E4;.</td>
    </tr>
    <tr>
      <td style="text-align:left">image</td>
      <td style="text-align:left">ImageObject</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBC84;&#xD2BC; &#xC774;&#xBBF8;&#xC9C0;</p>
        <ul>
          <li>type&#xC774; image&#xC778; &#xACBD;&#xC6B0;&#xC5D0; &#xD55C;&#xD574; &#xD544;&#xC218;&#xC774;&#xBA70;,
            &#xD574;&#xB2F9; &#xC774;&#xBBF8;&#xC9C0;&#xB97C; &#xC774;&#xC6A9;&#xD574;
            &#xBC84;&#xD2BC;&#xC744; &#xD45C;&#xD604;&#xD55C;&#xB2E4;.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">text</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBC84;&#xD2BC; &#xD14D;&#xC2A4;&#xD2B8;</p>
        <ul>
          <li>type&#xC774; text&#xC778; &#xACBD;&#xC6B0;&#xC5D0; &#xD55C;&#xD574; &#xD544;&#xC218;&#xC774;&#xBA70;,
            &#xD574;&#xB2F9; &#xD14D;&#xC2A4;&#xD2B8;&#xB97C; &#xC774;&#xC6A9;&#xD574;
            &#xBC84;&#xD2BC;&#xC744; &#xD45C;&#xD604;&#xD55C;&#xB2E4;.</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">token</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD074;&#xB9AD; &#xC2DC; &#xC804;&#xB2EC;&#xB420; &#xD1A0;&#xD070; &#xAC12;</td>
    </tr>
  </tbody>
</table>

### TitleObject

```text
{
  "logo": ImageObject,
  "text": TextObject,
  "subtext": TextObject,
  "subicon": ImageObject,
  "button": ButtonObject
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| logo | ImageObject | N | png 타입으로 투명 이미지로 제공해야 함 |
| text | TextObject | Y | 제목 |
| subtext | TextObject | N | ASR Text 등 부제목 |
| subicon | ImageObject | N | 서브 아이콘 \( 위치 : subText 왼쪽 \) |
| button | ButtonObject | N | 우측에 위치하는 버튼 |

### BackgroundObject

```text
{
  "image": ImageObject,
  "color": "{{STRING}}"
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
      <td style="text-align:left">image</td>
      <td style="text-align:left">ImageObject</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">color</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>color &#xD615;&#xC2DD; (RGB)</p>
        <p>default - #000000</p>
      </td>
    </tr>
  </tbody>
</table>

### Duration

TTS, 보이스 크롭 등이 종료된 후 template 이 화면에 남아 있어야 하는 시간입니다.

| Duration string | Duration value |
| :--- | :--- |
| SHORT | 7초 |
| MID | 15초 |
| LONG | 30초 |
| LONGEST | 10분 |

### GrammarGuide

발화가이드 입니다.

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
      <td style="text-align:left">grammarGuide</td>
      <td style="text-align:left">array of string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xD654;&#xBA74;&#xC5D0; &#xD45C;&#xC2DC;&#xD560; &#xBB38;&#xC790;&#xC5F4;&#xB4E4;&#xC744;
          &#xC815;&#xC758;&#xD569;&#xB2C8;&#xB2E4;.</p>
        <p>
          <br />&#xC0AC;&#xC6A9;&#xC608;.
          <br />[&quot;&#xD648; &#xD654;&#xBA74;&#xC73C;&#xB85C; &#xC774;&#xB3D9;&#xD574;&#xC918;&quot;,
          &quot;&#xC120;&#xD638;&#xCC44;&#xB110; &#xCC3E;&#xC544;&#xC918;&quot;]</p>
      </td>
    </tr>
  </tbody>
</table>

### ToggleButtonObject

```text
{
  "status": "{{STRING}}",
  "token": "{{STRING}}"
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| status | string | Y | on, off  |
| token | string | Y | 클릭 시 전달될 토큰 값 |

### ContextLayer

Template 의 종류를 구분하기 위한 속성입니다.

| contextLayer | description |
| :--- | :--- |
| INFO | 기본값. 정보성 |
| MEDIA | 미디어 재생 |
| ALERT | 알람/타이머 |
| CALL | 전화 수신/발신/통화중 |

## Directive

### Close

화면 종료 요청입니다.

```text
{
  "header": {
    "namespace": "Display",
    "name": "Close",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}"
  }
}
```

### ControlFocus

List item 의 포커스 이동 요청입니다.

```text
{
  "header": {
    "namespace": "Display",
    "name": "ControlFocus",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "direction": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| direction | string | Y | PREVIOUS, NEXT |

### ControlScroll

List 의 스크롤 이동 요청입니다.

```text
{
  "header": {
    "namespace": "Display",
    "name": "ControlScroll",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "direction": "{{STRING}}"
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| direction | string | Y | PREVIOUS, NEXT |

### Update

화면 갱신 요청입니다.

```text
{
  "header": {
    "namespace": "Display",
    "name": "Update",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    ...
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| token | string | Y | 변경된 template 의 token |
|  |  | Y | template payload 중 변경된 부분 |

## Directive - Template

### FullText1/2/3, ImageText1/2/3/4

```text
{
  "header": {
    "namespace": "Display",
    "name": "FullText1" | "FullText2" | "FullText2" | "FullText3" | "ImageText1" | "ImageText2" | "ImageText3" | "ImageText4",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "contextLayer": "{{STRING}}",
    "duration": "{{STRING}}",
    "title": TitleObject,
    "background": BackgroundObject,
    "content": {
      "image": ImageObject,
      "imageAlign": "{{STRING}}"
      "header": TextObject,
      "body": TextObject,
      "footer": TextObject
    },
    "grammarGuide": GrammarGuide
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
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">template&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xAE30; &#xC704;&#xD55C; unique
        identifier</td>
    </tr>
    <tr>
      <td style="text-align:left">contextLayer</td>
      <td style="text-align:left"><a href="display.md#contextlayer">ContextLayer</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">duration</td>
      <td style="text-align:left"><a href="display.md#duration">Duration</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">title</td>
      <td style="text-align:left"><a href="display.md#titleobject">TitleObject</a>
      </td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">background</td>
      <td style="text-align:left"><a href="display.md#backgroundobject">BackgroundObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">content</td>
      <td style="text-align:left">object</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>image</p>
      </td>
      <td style="text-align:left"><a href="display.md#imageobject">ImageObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>imageAlign</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">LEFT, RIGHT</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>header</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF8;&#xBB38; &#xC81C;&#xBAA9;</p>
        <ul>
          <li>&#xC904;&#xBC14;&#xAFC8; &#xAC00;&#xB2A5; (&apos;\n&apos;)</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>body</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF8;&#xBB38; &#xB0B4;&#xC6A9;</p>
        <ul>
          <li>&#xC904;&#xBC14;&#xAFC8; &#xAC00;&#xB2A5; (&apos;\n&apos;)</li>
          <li>Scrollable</li>
        </ul>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>footer</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xBCF4;&#xC870; &#xC124;&#xBA85;</td>
    </tr>
    <tr>
      <td style="text-align:left">grammarGuide</td>
      <td style="text-align:left"><a href="display.md#grammarguide">GrammarGuide</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### TextList1/2, ImageList1/2/3

```text
{
  "header": {
    "namespace": "Display",
    "name": "TextList1" | "TextList2" | "ImageList1" | "ImageList2" | "ImageList3",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.2"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "contextLayer": "{{STRING}}",
    "duration": "{{STRING}}",
    "title": TitleObject,
    "background": BackgroundObject,
    "badgeNumber": {{BOOLEAN}},
    "badgeNumberMode": "{{STRING}}",
    "focusable": {{BOOLEAN}},
    "anchorItemToken": "{{STRING}}",
    "listItems": [
      {
        "token": "{{STRING}}",
        "image": ImageObject,
        "icon": ImageObject,
        "header": TextObject,
        "body": TextObject,
        "footer": TextObject,
        "type": "{{STRING}}",
        "toggle": ToggleButtonObject
      }
    ]
    "grammarGuide": GrammarGuide
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
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">template&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xAE30; &#xC704;&#xD55C; unique
        identifier</td>
    </tr>
    <tr>
      <td style="text-align:left">contextLayer</td>
      <td style="text-align:left"><a href="display.md#contextlayer">ContextLayer</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">duration</td>
      <td style="text-align:left"><a href="display.md#duration">Duration</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">title</td>
      <td style="text-align:left"><a href="display.md#titleobject">TitleObject</a>
      </td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">background</td>
      <td style="text-align:left"><a href="display.md#backgroundobject">BackgroundObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">badgeNumber</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xC22B;&#xC790;(&#xC21C;&#xC11C;)&#xB97C;
          &#xBC1C;&#xD654;&#xD558;&#xC5EC; item&#xC744; &#xC120;&#xD0DD;&#xD558;&#xB3C4;&#xB85D;
          badge&#xB97C; &#xD45C;&#xC2DC;&#xD560;&#xC9C0; &#xC5EC;&#xBD80; (true -
          &#xD45C;&#xC2DC;&#xD568;, false - &#xD45C;&#xC2DC;&#xD558;&#xC9C0; &#xC54A;&#xC74C;)</p>
        <p>default - false</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">badgeNumberMode</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">badge &#xC22B;&#xC790;&#xB97C; &#xC124;&#xC815;&#xD558;&#xB294; &#xBC29;&#xBC95;
        IMMUTABILITY(item&#xC758; &#xC704;&#xCE58;&#xAC00; &#xBCC0;&#xACBD;&#xB418;&#xC5B4;&#xB3C4;
        badge &#xC22B;&#xC790;&#xB294; &#xC720;&#xC9C0;&#xB428;) PAGE(item&#xC758;
        &#xC704;&#xCE58;&#xAC00; &#xBCC0;&#xACBD;&#xB418;&#xC5C8;&#xC744; &#xB54C;
        &#xCCAB; &#xBC88;&#xC9F8; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294; item&#xC758;
        badge &#xC22B;&#xC790;&#xAC00; 1&#xBD80;&#xD130; &#xC2DC;&#xC791;&#xB428;)
        default - IMMUTABILITY</td>
    </tr>
    <tr>
      <td style="text-align:left">focusable</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">List Template&#xC758; item&#xB4E4;&#xC774; focus &#xAC00;&#xB2A5;&#xD55C;&#xC9C0;
        &#xC5EC;&#xBD80; default - true</td>
    </tr>
    <tr>
      <td style="text-align:left">anchorItemToken</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">display &#xB420; &#xB54C; &#xCCAB; &#xBC88;&#xC9F8;&#xB85C; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294;
        &#xC544;&#xC774;&#xD15C;&#xC758; &#xD1A0;&#xD070;</td>
    </tr>
    <tr>
      <td style="text-align:left">listItems</td>
      <td style="text-align:left">array</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Scrollable</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>token</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD074;&#xB9AD;&#xC740; &#xD55C; item &#xC804;&#xCCB4;&#xC5D0;&#xC11C;
        &#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>image</p>
      </td>
      <td style="text-align:left"><a href="display.md#imageobject">ImageObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>icon</p>
      </td>
      <td style="text-align:left"><a href="display.md#imageobject">ImageObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>header</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF8;&#xBB38; &#xC81C;&#xBAA9;</p>
        <p>&#xCD5C;&#xB300; 1&#xC904;&#xAE4C;&#xC9C0; &#xD45C;&#xD604; (&#xB118;&#xB294;
          &#xBB38;&#xC790;&#xB294; ... &#xCC98;&#xB9AC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>body</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF8;&#xBB38; &#xB0B4;&#xC6A9;</p>
        <p>&#xCD5C;&#xB300; 1&#xC904;&#xAE4C;&#xC9C0; &#xD45C;&#xD604; (&#xB118;&#xB294;
          &#xBB38;&#xC790;&#xB294; ... &#xCC98;&#xB9AC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>footer</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF4;&#xC870;&#xC124;&#xBA85;</p>
        <p>&#xCD5C;&#xB300; 1&#xC904;&#xAE4C;&#xC9C0; &#xD45C;&#xD604; (&#xB118;&#xB294;
          &#xBB38;&#xC790;&#xB294; ... &#xCC98;&#xB9AC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>type</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>list item&#xC758; type&#xC744; &#xC758;&#xBBF8;&#xD558;&#xBA70;, &#xC815;&#xC758;&#xD558;&#xC9C0;
          &#xC54A;&#xC73C;&#xBA74; &#xC704;&#xC758; &#xC608;&#xC2DC;&#xC640; &#xAC19;&#xC740;
          &#xC77C;&#xBC18;&#xD615;&#xC744; &#xC758;&#xBBF8;&#xD568;.</p>
        <p>&quot;SEPARATOR&quot;&#xB85C; &#xC815;&#xC758;&#xD560; &#xACBD;&#xC6B0;&#xC5D0;&#xB294;
          &#xC544;&#xB798;&#xC640; &#xAC19;&#xC740; header&#xB9CC;&#xC774; &#xC720;&#xD6A8;&#xD55C;
          &#xAD6C;&#xBD84;&#xC6A9; &#xD0C0;&#xC774;&#xD2C0; &#xD56D;&#xBAA9;&#xC774;
          &#xD45C;&#xC2DC;&#xB428;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>toggle</p>
      </td>
      <td style="text-align:left"><a href="display.md#togglebuttonobject">ToggleButtonObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xB9AC;&#xC2A4;&#xD2B8;&#xC544;&#xC774;&#xD15C;&#xC758; &#xC6B0;&#xCE21;&#xC5D0;
        &#xD45C;&#xC2DC;&#xB418;&#xB294; &#xD1A0;&#xAE00; &#xBC84;&#xD2BC;</td>
    </tr>
    <tr>
      <td style="text-align:left">grammarGuide</td>
      <td style="text-align:left"><a href="display.md#grammarguide">GrammarGuide</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### TextList3/4

```text
{
  "header": {
    "namespace": "Display",
    "name": "TextList3" | "TextList4",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.3"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "contextLayer": "{{STRING}}",
    "duration": "{{STRING}}",
    "title": TitleObject,
    "background": BackgroundObject,
    "badgeNumber": {{BOOLEAN}},
    "badgeNumberMode": "{{STRING}}",
    "focusable": {{BOOLEAN}},
    "anchorItemToken": "{{STRING}}",
    "listItems": [
      {
        "token": "{{STRING}}",
        "image": ImageObject,
        "icon": ImageObject,
        "header": TextObject,
        "body": TextObject,
        "footer": TextObject,
        "button": ToggleButtonObject
      }
    ]
    "caption": TextObject,
    "grammarGuide": GrammarGuide
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
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">template&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xAE30; &#xC704;&#xD55C; unique
        identifier</td>
    </tr>
    <tr>
      <td style="text-align:left">contextLayer</td>
      <td style="text-align:left"><a href="display.md#contextlayer">ContextLayer</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">duration</td>
      <td style="text-align:left"><a href="display.md#duration">Duration</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">title</td>
      <td style="text-align:left"><a href="display.md#titleobject">TitleObject</a>
      </td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">background</td>
      <td style="text-align:left"><a href="display.md#backgroundobject">BackgroundObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">badgeNumber</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC0AC;&#xC6A9;&#xC790;&#xAC00; &#xC22B;&#xC790;(&#xC21C;&#xC11C;)&#xB97C;
          &#xBC1C;&#xD654;&#xD558;&#xC5EC; item&#xC744; &#xC120;&#xD0DD;&#xD558;&#xB3C4;&#xB85D;
          badge&#xB97C; &#xD45C;&#xC2DC;&#xD560;&#xC9C0; &#xC5EC;&#xBD80; (true -
          &#xD45C;&#xC2DC;&#xD568;, false - &#xD45C;&#xC2DC;&#xD558;&#xC9C0; &#xC54A;&#xC74C;)</p>
        <p>default - false</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">badgeNumberMode</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">badge &#xC22B;&#xC790;&#xB97C; &#xC124;&#xC815;&#xD558;&#xB294; &#xBC29;&#xBC95;
        IMMUTABILITY(item&#xC758; &#xC704;&#xCE58;&#xAC00; &#xBCC0;&#xACBD;&#xB418;&#xC5B4;&#xB3C4;
        badge &#xC22B;&#xC790;&#xB294; &#xC720;&#xC9C0;&#xB428;) PAGE(item&#xC758;
        &#xC704;&#xCE58;&#xAC00; &#xBCC0;&#xACBD;&#xB418;&#xC5C8;&#xC744; &#xB54C;
        &#xCCAB; &#xBC88;&#xC9F8; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294; item&#xC758;
        badge &#xC22B;&#xC790;&#xAC00; 1&#xBD80;&#xD130; &#xC2DC;&#xC791;&#xB428;)
        default - IMMUTABILITY</td>
    </tr>
    <tr>
      <td style="text-align:left">focusable</td>
      <td style="text-align:left">bool</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">List Template&#xC758; item&#xB4E4;&#xC774; focus &#xAC00;&#xB2A5;&#xD55C;&#xC9C0;
        &#xC5EC;&#xBD80; default - true</td>
    </tr>
    <tr>
      <td style="text-align:left">anchorItemToken</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">display &#xB420; &#xB54C; &#xCCAB; &#xBC88;&#xC9F8;&#xB85C; &#xBCF4;&#xC5EC;&#xC9C0;&#xB294;
        &#xC544;&#xC774;&#xD15C;&#xC758; &#xD1A0;&#xD070;</td>
    </tr>
    <tr>
      <td style="text-align:left">listItems</td>
      <td style="text-align:left">array</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">Scrollable</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>token</p>
      </td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Y</td>
      <td style="text-align:left">&#xD074;&#xB9AD;&#xC740; &#xD55C; item &#xC804;&#xCCB4;&#xC5D0;&#xC11C;
        &#xAC00;&#xB2A5;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>image</p>
      </td>
      <td style="text-align:left"><a href="display.md#imageobject">ImageObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>icon</p>
      </td>
      <td style="text-align:left"><a href="display.md#imageobject">ImageObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>header</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF8;&#xBB38; &#xC81C;&#xBAA9;</p>
        <p>&#xCD5C;&#xB300; 1&#xC904;&#xAE4C;&#xC9C0; &#xD45C;&#xD604; (&#xB118;&#xB294;
          &#xBB38;&#xC790;&#xB294; ... &#xCC98;&#xB9AC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>body</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF8;&#xBB38; &#xB0B4;&#xC6A9;</p>
        <p>&#xCD5C;&#xB300; 1&#xC904;&#xAE4C;&#xC9C0; &#xD45C;&#xD604; (&#xB118;&#xB294;
          &#xBB38;&#xC790;&#xB294; ... &#xCC98;&#xB9AC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>footer</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBCF4;&#xC870;&#xC124;&#xBA85;</p>
        <p>&#xCD5C;&#xB300; 1&#xC904;&#xAE4C;&#xC9C0; &#xD45C;&#xD604; (&#xB118;&#xB294;
          &#xBB38;&#xC790;&#xB294; ... &#xCC98;&#xB9AC;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>listItems.</p>
        <p>button</p>
      </td>
      <td style="text-align:left"><a href="display.md#button-object">ButtonObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>List &#xC544;&#xC774;&#xD15C;&#xC758; &#xBC84;&#xD2BC;</p>
        <p>body&#xAC00; 2&#xC904;&#xC778; &#xACBD;&#xC6B0;&#xC5D0; &#xCD5C;&#xC801;&#xD654;
          &#xB418;&#xC5B4; &#xC788;&#xC74C;.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">caption</td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xC804;&#xCCB4; &#xB9AC;&#xC2A4;&#xD2B8; &#xC544;&#xC774;&#xD15C;&#xB4E4;&#xC5D0;
          &#xB300;&#xD55C; &#xBCF4;&#xC870;&#xC124;&#xBA85;</p>
        <p>&#xD14D;&#xC2A4;&#xD2B8; &#xAE38;&#xC774; : &#xCD5C;&#xB300; 2&#xC904;(&#xB2E8;&#xB9D0;&#xC5D0;
          &#xB530;&#xB77C; 1&#xC904;)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">grammarGuide</td>
      <td style="text-align:left"><a href="display.md#grammarguide">GrammarGuide</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Weather1/2

```text
{
  "header": {
    "namespace": "Display",
    "name": "Weather1" | "Weather2",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
    "playServiceId": "{{STRING}}",
    "token": "{{STRING}}",
    "contextLayer": "{{STRING}}",
    "duration": "{{STRING}}",
    "title": TitleObject,
    "background": BackgroundObject,
    "content": {
      "header": TextObject,
      "image": ImageObject,
      "temperature": {
        "current": TextObject,
        "max": TextObject,
        "min": TextObject
      },
      "body": TextObject,
      "footer": TextObject,
      "listItems": [
        {
          "header": TextObject,
          "image": ImageObject,
          "body": TextObject,
          "footer": TextObject
        }
      ]
    },
    "grammarGuide": GrammarGuide
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
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left">template&#xC744; &#xC2DD;&#xBCC4;&#xD558;&#xAE30; &#xC704;&#xD55C; unique
        identifier</td>
    </tr>
    <tr>
      <td style="text-align:left">contextLayer</td>
      <td style="text-align:left"><a href="display.md#contextlayer">ContextLayer</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">duration</td>
      <td style="text-align:left"><a href="display.md#duration">Duration</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">title</td>
      <td style="text-align:left"><a href="display.md#titleobject">TitleObject</a>
      </td>
      <td style="text-align:left"><b>Y</b>
      </td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">background</td>
      <td style="text-align:left"><a href="display.md#backgroundobject">BackgroundObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>header</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xB0A0;&#xC528;&#xC815;&#xBCF4;&#xB97C; &#xB098;&#xD0C0;&#xB0B4;&#xB294;
        &#xD5E4;&#xB354; &#xBB38;&#xC790;&#xC5F4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>image</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xB0A0;&#xC528;&#xC815;&#xBCF4;&#xB97C; &#xB098;&#xD0C0;&#xB0B4;&#xB294;
        &#xC774;&#xBBF8;&#xC9C0;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>temperature.</p>
        <p>current</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xD604;&#xC7AC; &#xC628;&#xB3C4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>temperature.</p>
        <p>max</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xCD5C;&#xACE0; &#xC628;&#xB3C4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>temperature.</p>
        <p>min</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xCD5C;&#xC800; &#xC628;&#xB3C4;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>body</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">
        <p>&#xBBF8;&#xC138;&#xBA3C;&#xC9C0;, &#xC624;&#xC804;, &#xAC74;&#xC870;&#xC8FC;&#xC758;&#xBCF4;
          &#xB4F1;&#xC758; &#xB0A0;&#xC528;&#xC5D0; &#xB300;&#xD55C; &#xC124;&#xBA85;</p>
        <p>HTML &#xD45C;&#xD604; &#xAC00;&#xB2A5;</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>footer</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">body &#xC544;&#xB798; &#xD45C;&#xD604;&#xB418;&#xB294; &#xD14D;&#xC2A4;&#xD2B8;(html
        &#xAC00;&#xB2A5;)</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>listItems</p>
      </td>
      <td style="text-align:left">list</td>
      <td style="text-align:left">N</td>
      <td style="text-align:left">&#xC2DC;&#xAC04;&#xBCC4; &#xB0A0;&#xC528; &#xC815;&#xBCF4; &#xD45C;&#xD604;&#xC744;
        &#xC704;&#xD55C; &#xB9AC;&#xC2A4;&#xD2B8;</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>listItems.</p>
        <p>header</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>listItems.</p>
        <p>image</p>
      </td>
      <td style="text-align:left"><a href="display.md#imageobject">ImageObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>listItems.</p>
        <p>body</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>content.</p>
        <p>listItems.</p>
        <p>footer</p>
      </td>
      <td style="text-align:left"><a href="display.md#textobject">TextObject</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">grammarGuide</td>
      <td style="text-align:left"><a href="display.md#grammarguide">GrammarGuide</a>
      </td>
      <td style="text-align:left">N</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Weather3/4

```text
{
  "header": {
    "namespace": "Display",
    "name": "Weather3" | "Weather4",
    "messageId": "{{STRING}}",
    "dialogRequestId": "{{STRING}}",
    "version": "1.1"
  },
  "payload": {
	  "playServiceId": "{{STRING}}",
	  "token": "{{STRING}}",
	  "contextLayer": "{{STRING}}",
	  "duration": "{{STRING}}",
	  "title": TextObject,
	  "background": BackgroundObject,
	  "content": {
	    "listItems": [
	      {
	        "header": TextObject,
	        "body": TextObject,
	        "image": ImageObject,
	        "temperature": {
	          "max": TextObject,
	          "min": TextObject
	        },
	        "footer": TextObject,
          "focus": {{Boolean}}
	      }
	    ]
	  },
    "grammarGuide": GrammarGuide
  }
}
```

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| token | string | **Y** | template을 식별하기 위한 unique identifier |
| contextLayer | [ContextLayer](display.md#contextlayer) | N |  |
| duration | [Duration](display.md#duration) | N |  |
| title | [TitleObject](display.md#titleobject) | **Y** |  |
| background | [BackgroundObject](display.md#backgroundobject) | N |  |
| listItems | list | N | 현재는 최대 2개의 아이템을 보여주고 있음 |
| listItems.header | [TextObject](display.md#textobject) | N | item의 최상위 텍스트 |
| listItems.body | [TextObject](display.md#textobject) | N | item의 주요내용 텍스트 |
| listItems.image | [ImageObject](display.md#imageobject) | N | item의 주 이미지 |
| listItems.temperature.max | [TextObject](display.md#textobject) | N | 최대 온도 |
| listItems.temperature.min | [TextObject](display.md#textobject) | N | 최저 온도 |
| listItems.footer | [TextObject](display.md#textobject) | N | 기타정보를 위한 텍스트 |
| listItems.focus | boolean | N | focus 여부\(bold 처리\) |
| grammarGuide | [GrammarGuide](display.md#grammarguide) | N | 4.8 Grammar Guide 참조 |

## Event

### ElementSelected

```text
{
  "header": {
    "namespace": "Display",
    "name": "ElementSelected",
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

| parameter | type | mandatory | description |
| :--- | :--- | :--- | :--- |
| token | string | **Y** |  |



