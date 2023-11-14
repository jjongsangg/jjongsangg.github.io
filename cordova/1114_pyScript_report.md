># PyScript 
- HTML 인터페이스와 Pyodide, WASM 및 최신 웹 기술을 사용하여 웹브라우저에서 동작하는 다양한 Python Application을 만들 수 있는 프레임워크.
- 웹 상에 파이썬 로직을 추가할 수 있음.
- 파이썬으로 작성된 로직을 서버사이드에서 실행하여 결과를 웹 브라우저에서 확인하는 것이아닌
클라이언트 사이드에서 직접 파이썬으로 작성된 로직을 실행하도록 하는 것이 특징

># 사용법
```html
<head>
<link rel="stylesheet" href="https://pyscript.net/latest/pyscript.css" />
<script defer src="https://pyscript.net/latest/pyscript.js"></script>
</head>
    <body>
    <py-script> 
		<!-- 내부로직 -->
		print('Hello, World!')
	</py-script>
</body>
```

># py-config 설정하기
```html
<head>
	<!-- ~~생략~~ -->
	<py-config type="json">
	{
		"autoclose_loader": true,
		"runtimes": [{
		"src": "https://cdn.jsdelivr.net/pyodide/v0.21.2/full/pyodide.js",
		"name": "pyodide-0.21.2",
		"lang": "python"
		}]
	}
	</py-config>
</head>
```
or
```html
<head>
	<!-- ~~생략~~ -->
	<py-config type="json" src="./custom.json"></py-config>
</head>
```

># py-config 에서 지원하는 선택 값 목록



| 값	| 유형 | 설명 |
|---|---|---|
|name|	string|	사용자 응용 프로그램의 이름입니다. 이 필드는 임의의 문자열일 수 있으며 응용프로그램 작성자가 사용자 정의 목적으로 사용합니다.|
|description| string	|사용자 응용 프로그램에 대한 설명입니다. 이 필드는 임의의 문자열일 수 있으며 응용프로그램 작성자가 사용자 정의 목적으로 사용합니다.
|version|	string	|사용자 응용 프로그램의 버전입니다. 이 필드는 임의의 문자열일 수 있으며 응용프로그램 작성자가 사용자 정의 목적으로 사용합니다. PyScript 버전과 관련이 없습니다.|
|schema_version|	number	|지원되는 모든 키를 결정하는 구성 스키마의 버전입니다. 이것은 사용자가 제공할 수 있으므로 PyScript는 구성에서 무엇을 기대해야 하는지 알 수 있습니다. 제공하지 않으면 스키마의 최신 버전이 자동으로 사용됩니다.|
|type|	string|	프로젝트 유형입니다. 기본값은 “앱”, 즉 사용자 애플리케이션입니다.
|author_name	|string	|저자의 이름입니다.|
|author_email	|string	|저자의 이메일.
|license	|string	|사용자 애플리케이션에 사용할 라이선스입니다.|
|autoclose_loader|	boolean	|False인 경우 PyScript는 시작 작업이 완료될 때 로딩 시작 화면을 닫지 않습니다.|
|packages	|List of Packages	|써드파티 OSS 패키지에 대한 종속성이 여기에 지정됩니다. 기본값은 빈 목록입니다.|
|paths	|List of Paths	|로컬 Python 모듈은 여기에서 지정해야 합니다. 기본값은 빈 목록입니다.|
|plugins	|List of Plugins	|플러그인 목록은 여기에서 지정해야 합니다. 기본값은 빈 목록입니다.|
|runtimes	|List of Runtimes	|아래에 설명된 런타임 구성 목록입니다. 기본값은 단일 Pyodide 기반 런타임을 포함합니다.|

># runtime 설정 구성 목록
|값 |유형|설명|
|---|---|---|
|src|	string (Required)	|런타임 소스에 대한 URL입니다.|
|name	|string	|런타임의 이름입니다. 이 필드는 임의의 문자열일 수 있으며 애플리케이션 작성자가 고유한 사용자 정의 목적으로 사용합니다.|
|lang	|string	|런타임에서 지원하는 프로그래밍 언어입니다. 이 필드는 응용 프로그램 작성자가 설명을 제공하는 데 사용할 수 있습니다. 현재 PyScript가 작동하는 방식에 영향을 미치지 않습니다.|

># py-repl 태그 사용하기
```html
<html>
  <head>
    <link rel="stylesheet" href="https://pyscript.net/latest/pyscript.css" />
    <script defer src="https://pyscript.net/latest/pyscript.js"></script>
  </head>
  <py-repl></py-repl>
</html>
```
위 소스를 실행하면 코드편집기가 렌더링 되고, 내부에 파이썬 코드를 넣어 실행해볼 수 있습니다.

># 시각적 컴포넌트 태그
|태그|설명|
|---|---|
|\<py-inputbox>|	사용자에게 입력 값을 입력하라는 메시지를 표시하는 데 사용할 수 있는 입력 상자를 추가합니다.|
|\<py-box>	|\<py-box>의 요소가 페이지에 정렬되고 표시되어야 하는 방법을 정의하는 하나 이상의 시각적 구성 요소를 호스팅하는 데 사용할 수 있는 컨테이너 개체를 만듭니다.|
|\<py-button>	|작성자가 ‘on_focus’ 또는 ‘on_click’과 같은 버튼에 대한 작업에 대한 레이블 및 이벤트 핸들러를 추가할 수 있는 버튼을 추가합니다.|
|\<py-title>|	태그 내부의 텍스트를 페이지 제목으로 스타일 지정하는 정적 텍스트 제목 구성 요소를 추가합니다.|
