---
layout: docs
title: 브레드크럼
title_en: Breadcrumb
description: CSS로 구분자를 자동으로 추가해 내비게이션 계층 내에서 현재 페이지의 위치를 표시합니다.
group: components
toc: true
---

## 예시

순서를 가진 목록 또는 순서를 가지지 않은 목록을 사용해, 최소 스타일의 브레드크럼을 작성합니다. 유틸리티를 사용해 원하는 스타일을 추가할 수 있습니다.

{{< example >}}
<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item active" aria-current="page">Home</li>
  </ol>
</nav>

<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Library</li>
  </ol>
</nav>

<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item"><a href="#">Library</a></li>
    <li class="breadcrumb-item active" aria-current="page">Data</li>
  </ol>
</nav>
{{< /example >}}

## 구분자

구분자는 CSS의 [`::before`](https://developer.mozilla.org/en-US/docs/Web/CSS/::before)과 [`content`](https://developer.mozilla.org/en-US/docs/Web/CSS/content)를 통해 자동으로 추가됩니다. 이들은 로컬 CSS 사용자 지정 속성 `--bs-breadcrumb-divider`를 변경하거나, `$breadcrumb-divider` Sass 변수와 `$breadcrumb-divider-flipped`를 사용해 RTL에 대응하는 것으로 변경할 수 있습니다. 사용자 지정 속성의 fallback 으로 설정되어 있는 Sass 변수를 기본으로 사용하고 있습니다. 이렇게 하여, 언제든지 CSS를 다시 컴파일하지 않고 재정의할 수 있는 글로벌한 구분자를 얻을 수 있습니다.

{{< example >}}
<nav style="--bs-breadcrumb-divider: '>';" aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Library</li>
  </ol>
</nav>
{{< /example >}}

Sass 를 통해 수정할 때, 문자열의 주변에 따옴표를 만들기 위해 [quote](https://sass-lang.com/documentation/modules/string#quote) 함수가 필요합니다. 예를 들어, `>`을 구분자로 사용하려면 이렇게 사용합니다.

```scss
$breadcrumb-divider: quote(">");
```

또한 **내장된 SVG 아이콘**을 사용할 수도 있습니다. CSS 사용자 지정 속성을 통해 적용하거나 Sass 변수를 사용하세요.


{{< callout info >}}
### Using embedded SVG

Inlining SVG as data URI requires to URL escape a few characters, most notably `<`, `>` and `#`. That's why the `$breadcrumb-divider` variable is passed through our [`escape-svg()` Sass function]({{< docsref "/customize/sass#escape-svg" >}}). When using the CSS custom property, you need to URL escape your SVG on your own. Read [Kevin Weber's explanations on CodePen](https://codepen.io/kevinweber/pen/dXWoRw ) for detailed information on what to escape.
{{< /callout >}}

{{< example >}}
<nav style="--bs-breadcrumb-divider: url(&#34;data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='8' height='8'%3E%3Cpath d='M2.5 0L1 1.5 3.5 4 1 6.5 2.5 8l4-4-4-4z' fill='%236c757d'/%3E%3C/svg%3E&#34;);" aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Library</li>
  </ol>
</nav>
{{< /example >}}

```scss
$breadcrumb-divider: url("data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' width='8' height='8'><path d='M2.5 0L1 1.5 3.5 4 1 6.5 2.5 8l4-4-4-4z' fill='#{$breadcrumb-divider-color}'/></svg>");
```

또한 divider 설정인 `--bs-breadcrumb-divider: '';`을 빈 값으로 넣거나 (CSS 사용자 지정 속성의 빈 문자열은 값으로 카운터 됨), Sass 변수를 `$breadcrumb-divider: none;`으로 설정할 수도 있습니다.

{{< example >}}
<nav style="--bs-breadcrumb-divider: '';" aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="#">Home</a></li>
    <li class="breadcrumb-item active" aria-current="page">Library</li>
  </ol>
</nav>
{{< /example >}}


```scss
$breadcrumb-divider: none;
```

## 접근성

브레드크럼은 내비게이션을 제공하기 때문에, 요소에서 제공되는 내비게이션 타입을 나타내기 위해 `<nav>` 요소에 `aria-label="breadcrumb"` 과 같은 의미가 있는 라벨을 추가하고, 세트의 마지막 아이템에는 현재 페이지를 나타내는 `aria-current="page"`를 추가하는 것이 좋습니다.

자세한 내용은 [ARIA Authoring Practices Guide breadcrumb pattern](https://www.w3.org/WAI/ARIA/apg/patterns/breadcrumb/)을 확인해주세요.

## CSS

### 변수

{{< added-in "5.2.0" >}}

As part of Bootstrap's evolving CSS variables approach, breadcrumbs now use local CSS variables on `.breadcrumb` for enhanced real-time customization. Values for the CSS variables are set via Sass, so Sass customization is still supported, too.

{{< scss-docs name="breadcrumb-css-vars" file="scss/_breadcrumb.scss" >}}

### Sass 변수

{{< scss-docs name="breadcrumb-variables" file="scss/_variables.scss" >}}
