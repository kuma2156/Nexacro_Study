## 🛠️ 넥사크로 N 

| 📁 항목 (Item) | ✨ 역할 (Role) |
| :--- | :--- |
| **Environment** | 애플리케이션의 **최상위 전역 설정** 관리. |
| **ScreenDefinition** |  해상도/장치별 **화면 크기 정의** 및 설정 관리. |
| **Variables** (Screen Definition 하위) | 특정 화면 내에서 사용되는 **전역 변수** 관리. |
| **Cookies** | 애플리케이션에서 사용되는 **쿠키** 관련 설정 관리. |
| **HTTP Header** | 서버 통신 시 사용되는 **HTTP 헤더** 설정 관리. |
| **Script** | **전역 JavaScript 파일** 및 설정 관리. |
| **TypeDefinition** | 사용자 정의 타입 (Objects, Services 등) 정의. |
| **Services** | 서버 통신을 위한 **서비스 (URL, 프로토콜)** 정의. |
| **ProtocolAdaptors** | 통신 프로토콜을 처리하는 **어댑터** 정의 관리. |
| **DeviceAdaptors** | **장치별 기능** (카메라, GPS 등) 활용을 위한 어댑터 관리. |
| **CordovaPlugins** | 하이브리드 앱 개발 시 사용되는 **플러그인** 설정 관리. |
| **Application Variables** | 앱 전체에서 공유되는 **데이터셋/변수** 관리. |
| **Datasets** (App Variables 하위) | 애플리케이션 전체에서 공유되는 **공통 데이터셋** 정의. |
| **Variables** (App Variables 하위) | 애플리케이션 전체에서 공유되는 **공통 변수** 정의. |
| **Applications** | 메인 애플리케이션 (예: `Application_Desktop`) 파일 관리. |
| **Base / FrameBase** | 기본 프레임워크, 공통 모듈/폼 등의 **기반 구조** 관리. |

# 🧭 넥사크로 N 핵심 함수 정리

---

## 📘 Dataset 관련 함수

| 함수                               | 설명                | 예시                                |
| -------------------------------- | ----------------- | --------------------------------- |
| **addRow()**                     | 마지막에 행 추가         | `var nRow = ds.addRow();`         |
| **insertRow(n)**                 | n번째 위치에 행 삽입      | `ds.insertRow(0);`                |
| **deleteRow(n)**                 | n번째 행 삭제          | `ds.deleteRow(1);`                |
| **clearData()**                  | 데이터만 초기화(컬럼 유지)   | `ds.clearData();`                 |
| **getColumn(row, colid)**        | 값 읽기              | `ds.getColumn(0, "name");`        |
| **setColumn(row, colid, value)** | 값 수정              | `ds.setColumn(0, "age", 29);`     |
| **getRowCount()**                | 총 행 수             | `ds.rowcount;`                    |
| **filter(expr)**                 | 조건에 맞는 행만 표시      | `ds.filter("age >= 30");`         |
| **set_keystring()**              | 정렬 설정             | `ds.set_keystring("S:+age");`     |
| **copyData(ds2)**                | 다른 Dataset 데이터 복사 | `ds2.copyData(ds1);`              |
| **getCaseCount(type)**           | 변경된 행 수           | `ds.getCaseCount("U")` (업데이트된 행만) |

## Dataset의 “상태(STATE)” 구조

| 상태     | 의미     | 코드 | 서버전송 여부 |
| ------ | ------ | -- | ------- |
| NORMAL | 수정 없음  | 0  | ❌       |
| INSERT | 새로 추가됨 | 2  | ✅       |
| UPDATE | 수정됨    | 4  | ✅       |
| DELETE | 삭제됨    | 8  | ✅       |


---

## 🌐 Transaction (서버 통신)

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `transaction()` | 서버와 데이터 통신 수행 | ```javascript<br>this.transaction("getUserList", "/user/getList.do", "ds_input=ds_in", "ds_output=ds_out", "param1=123", "fnCallback");``` |
| `fnCallback(trId, errCd, errMsg)` | 통신 완료 후 콜백 함수 | ```javascript<br>this.fnCallback = function(trId, errCd, errMsg){<br> if (errCd < 0) alert("오류: " + errMsg);<br> else alert("데이터 수신 완료!");<br>};``` |

---

### 실무에서 자주보는 코드
```
if (this.ds_main.getCaseCount("U") > 0 || this.ds_main.getCaseCount("I") > 0)
{
    this.fnSave(); // 변경된 데이터 있을 때만 저장
}
```

## 그리드
### 그리드 내부구조
| 영역      | 의미             | 예시       |
| ------- | -------------- | -------- |
| Head    | 컬럼 제목 (필드명)    | 이름, 나이   |
| Body    | 실제 데이터 셀       | 홍길동, 28  |
| Summary | 합계, 평균 등 하단 요약 | 총합계: ... |

### 그리드의 주요속성
| 속성                 | 설명                                | 예시                             |
| ------------------ | --------------------------------- | ------------------------------ |
| **autofittype**    | 칸 자동 크기 조정                        | `"col"`, `"row"`, `"col, row"` |
| **autosizingtype** | 내용에 따라 크기 조정                      | `"both"`                       |
| **displaytype**    | 셀 표시 형식 (text, combo, checkbox 등) | `"combo"`                      |
| **edittype**       | 편집 가능 여부                          | `"text"`, `"none"`             |
| **binddataset**    | 연결할 Dataset 지정                    | `"ds_main"`                    |

### 그리드의 이벤트
| 이벤트                | 발생 시점    | 예시          |
| ------------------ | -------- | ----------- |
| **onheadclick**    | 헤더 클릭 시  | 정렬 토글 구현    |
| **oncelldblclick** | 셀 더블클릭   | 상세 팝업 열기    |
| **oncellclick**    | 셀 클릭     | 특정 로직 실행    |
| **onkeydown**      | 키보드 입력   | 엔터로 다음 행 이동 |
| **oneditclick**    | 편집 모드 진입 | 입력 유효성 검사   |

## 실무에서 꼭 외워야할 포인트
| 구분         | 꼭 외워야 할 포인트                          |
| ---------- | ------------------------------------ |
| Dataset 기본 | Row, Column, Cell 구조                 |
| 데이터 조작     | addRow, setColumn, filter, clearData |
| 상태값        | NORMAL / INSERT / UPDATE / DELETE    |
| Grid 연동    | binddataset으로 자동 연결                  |
| 양방향 바인딩    | Grid 수정 = Dataset 변경                 |
| 콤보 연동      | displaytype="combo" + combodataset   |
| 서버 전송      | 변경 상태 행만 전송됨                         |
| 데이터 갱신     | Grid ↔ Dataset 자동 동기화                |
| 실무 핵심      | 트랜잭션(gfn_ServiceCall) 구조 이해          |

---

## 🏠 Application (전역 제어)

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `nexacro.getApplication()` | 현재 실행 중인 앱 객체 가져오기 | ```javascript<br>var app = nexacro.getApplication();``` |
| `app.lookup("컴포넌트ID")` | 다른 폼의 컴포넌트 접근 | ```javascript<br>var loginForm = app.mainframe.VFrameSet.HFrameSet.form;<br>loginForm.btn_login.set_enable(false);``` |
| `app.exit()` | 애플리케이션 종료 | ```javascript<br>app.exit();``` |

---

## ⚡ 이벤트 관련 함수

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `addEventHandler("onclick", func, this)` | 이벤트 등록 | ```javascript<br>this.btn_save.addEventHandler("onclick", this.fnSave, this);``` |
| `removeEventHandler("onclick", func, this)` | 이벤트 제거 | ```javascript<br>this.btn_save.removeEventHandler("onclick", this.fnSave, this);``` |
| `fnSave(obj, e)` | 이벤트 함수 예시 | ```javascript<br>this.fnSave = function(obj, e){<br> alert("저장 버튼 클릭됨!");<br>};``` |

---

## 🧱 Alert / Debug 함수

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `alert("메시지")` | 경고창 표시 | ```javascript<br>alert("작업이 완료되었습니다!");``` |
| `confirm("메시지")` | 확인/취소 대화창 | ```javascript<br>var res = confirm("정말로 삭제하시겠습니까?");``` |
| `trace("로그")` | 콘솔 로그 출력 | ```javascript<br>trace("현재 행 수: " + this.ds_user.getRowCount());``` |

## 🧠 넥사크로 N 핵심 개념 요약

| 🧩 개념 | 💬 설명 | 💡 핵심 포인트 / 예시 |
|:--|:--|:--|
| **Form (폼)** | 실제 화면(UI)을 구성하는 기본 단위 | - `.xfdl` 파일로 저장<br>- 버튼, 그리드, 에디트박스 등 배치<br>- 자바스크립트(`.xfdl.js`)로 로직 작성 |
| **Dataset** | 화면/서버 간 데이터 교환용 구조체 (2차원 테이블) | - 엑셀처럼 행(Row), 열(Column) 구성<br>- `addRow()`, `setColumn()` 자주 사용 |
| **Bind** | UI 컴포넌트와 Dataset의 특정 컬럼을 연결 | - 데이터 변경 시 자동 반영<br>```js\nBindItem("bind_id", objInput, "value", dsUser, "name");\n``` |
| **Transaction** | 서버와 데이터 송수신을 담당하는 함수 | - 비동기 통신 지원<br>```js\ntransaction("getData", "svc::user.do", "", "dsUser=out_ds", "param=value", "fnCallback");\n``` |
| **Script (JS)** | 폼 동작 로직 작성 (이벤트, 데이터 처리 등) | - 각 폼마다 JS 파일 존재 (`.xfdl.js`)<br>- 함수/이벤트 핸들러 정의 |
| **Component (컴포넌트)** | 화면 구성요소 (Button, Grid, Combo 등) | - `Button00_onclick` 이벤트에서 자바스크립트 실행 |
| **Event** | 사용자 동작(클릭, 변경, 로드 등)을 처리 | - `onload`, `onclick`, `onchanged` 등<br>```js\nthis.alert("클릭됨!");\n``` |
| **Service (서비스)** | 서버 통신 URL, 경로, 프로토콜 설정 | - `Environment`의 Services 영역에서 관리<br>예: `svc:: = http://localhost:8080/service/` |
| **Application Variables** | 앱 전체에서 공유되는 전역 변수/데이터셋 | - `application.g_userName` 식으로 접근 |
| **Popup (팝업폼)** | 새 창을 띄워 추가 화면 표시 | ```js\nthis.open("popup01", "PopupForm.xfdl", this, null, null, 400, 300);\n``` |
| **FrameSet / ChildFrame** | 메인 프레임 구조 정의 (화면 전환용) | - TopFrame, LeftFrame, MainFrame 등 구조화 |
| **Theme / CSS** | 화면 스타일(색상, 글꼴 등)을 관리 | - `.xtheme` 파일로 디자인 일괄 변경 |
| **DeviceAdapter** | 모바일 기기 기능(GPS, 카메라 등)과 연동 | - `nexacro.Device.currentlocation` 등 사용 |
| **File Upload / Download** | 서버로 파일 업로드 또는 내려받기 기능 | - `FileUpload`, `FileDownload` 컴포넌트 사용 |
| **Grid** | 데이터셋을 표 형태로 보여주는 컴포넌트 | - `bindDataset` 속성에 Dataset 지정<br>- 정렬, 합계, 필터링 지원 |

---

## ⚙️ 넥사크로 개발 흐름 정리

| 단계 | 설명 | 예시 |
|:--|:--|:--|
| 1️⃣ Form 설계 | `.xfdl` 파일에서 UI 구성 | 버튼, 그리드, 에디트박스 배치 |
| 2️⃣ Dataset 생성 | 데이터 구조 정의 | `dsUser` (id, name, age 등) |
| 3️⃣ Script 작성 | 이벤트, 데이터 로직 구현 | `Button00_onclick → transaction 호출` |
| 4️⃣ Transaction 호출 | 서버 데이터 연동 | `svc::getUserList.do` 호출 |
| 5️⃣ Bind 연결 | Dataset ↔ UI 자동 동기화 | `BindItem` 설정 |
| 6️⃣ Application 관리 | 전역 변수/데이터 관리 | `application.g_userInfo` |
| 7️⃣ 배포/빌드 | 톰캣 등 웹 서버에 올려 실행 | `http://localhost:8080/nexa/` 접속 |


---

## 🧰 자주 쓰는 전역 객체

| 객체 | 설명 | 예시 코드 |
|:--|:--|:--|
| `application` | 전역 앱 객체 | `application.g_userId` |
| `this` | 현재 Form 객체 | `this.alert("Hi");` |
| `nexacro` | 넥사크로 전역 API | `nexacro.getApplication();` |
| `system` | OS 관련 기능 | `system.openURL("http://...");` |


## 콤보박스
| 항목           | 역할                | 예시값                   |
| ------------ | ----------------- | --------------------- |
| innerdataset | 콤보박스의 데이터 원본      | ds_grade              |
| codecolumn   | 실제 저장되는 코드값       | “A”, “B”, “C”         |
| datacolumn   | 사용자에게 표시될 값       | “관리자”, “일반사용자”        |
| Dataset 구조   | ColumnInfo + Rows | code, name            |
| value/text   | 콤보 선택 결과          | value=“A”, text=“관리자” |


## 데이터셋 기본함수
| 함수                             | 설명             | 예시                                       |
| ------------------------------ | -------------- | ---------------------------------------- |
| `setColumn(row, colid, value)` | 특정 셀 값 설정      | `ds.setColumn(0, "NAME", "홍길동");`        |
| `getColumn(row, colid)`        | 특정 셀 값 가져오기    | `var name = ds.getColumn(1, "NAME");`    |
| `addRow()`                     | 맨 뒤에 행 추가      | `var r = ds.addRow();`                   |
| `insertRow(row)`               | 특정 위치에 행 삽입    | `ds.insertRow(2);`                       |
| `deleteRow(row)`               | 해당 행 삭제        | `ds.deleteRow(0);`                       |
| `clearData()`                  | 데이터만 삭제        | `ds.clearData();`                        |
| `clear()`                      | 데이터 + 컬럼 모두 삭제 | `ds.clear();`                            |
| `rowcount`                     | 전체 행 개수        | `trace(ds.rowcount);`                    |
| `filter(expr)`                 | 조건 필터링         | `ds.filter("AGE >= 30");`                |
| `sort(expr)`                   | 정렬             | `ds.sort("NAME ASC");`                   |
| `findRow(col, value)`          | 해당 값 첫 번째 찾기   | `var r = ds.findRow("USER_ID", "1001");` |
| `findRowExpr(expr)`            | 조건식으로 찾기       | `ds.findRowExpr("AGE > 40");`            |
| `getRowType(row)`              | ROWTYPE 확인     | `ds.getRowType(0); // 2: Insert`         |


## Component(Edit/Combo/Calendar 등) 기본 함수
| 함수                         | 설명            | 예시                            |
| -------------------------- | ------------- | ----------------------------- |
| `set_value(value)`         | 값 설정          | `edtName.set_value("홍길동");`   |
| `value`                    | 값 가져오기        | `var v = edtName.value;`      |
| `text`                     | 표시 텍스트 가져오기   | `var t = edtSearch.text;`     |
| `setFocus()`               | 포커스 이동        | `edtName.setFocus();`         |
| `set_enable(true/false)`   | 활성/비활성        | `cmbType.set_enable(false);`  |
| `set_readonly(true/false)` | 읽기 전용         | `edtName.set_readonly(true);` |
| `set_visible(true/false)`  | 보이기/숨기기       | `btnSave.set_visible(false);` |
| `set_index(i)`             | 콤보박스 index 변경 | `cmbType.set_index(1);`       |
| `getText()`                | 컴포넌트 문자열      | `var s = edtName.getText();`  |

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `set_visible(true/false)` | 표시/숨김 제어 | ```javascript<br>this.btn_submit.set_visible(true);``` |
| `set_enable(true/false)` | 활성/비활성 제어 | ```javascript<br>this.btn_submit.set_enable(false);``` |
| `set_text("텍스트")` | 텍스트 변경 | ```javascript<br>this.st_title.set_text("회원 정보");``` |
| `set_value(value)` | 값 설정 | ```javascript<br>this.edt_name.set_value("김명규");``` |
| `get_value()` | 현재 값 가져오기 | ```javascript<br>var name = this.edt_name.get_value();``` |

## 그리드 기본함수
| 함수                            | 설명          | 예시                                |
| ----------------------------- | ----------- | --------------------------------- |
| `getCellPos()`                | 현재 셀 위치     | `var pos = grd.getCellPos();`     |
| `setCellPos(col)`             | 특정 컬럼으로 이동  | `grd.setCellPos(1);`              |
| `setFocus()`                  | 그리드에 포커스    | `grd.setFocus();`                 |
| `showEditor(true)`            | 셀 편집기 강제 열기 | `grd.showEditor(true);`           |
| `getCellValue(row, colid)`    | 셀 값 가져오기    | `grd.getCellValue(0, "NAME");`    |
| `setCellValue(row, colid, v)` | 셀 값 변경      | `grd.setCellValue(2, "AGE", 30);` |
| `selectRow(row)`              | 해당 row 선택   | `grd.selectRow(3);`               |
| `isSelectRow(row)`            | 선택 여부       | `grd.isSelectRow(1);`             |

## 폼 전역함수
| 함수                 | 설명       | 예시                      |
| ------------------ | -------- | ----------------------- |
| `alert(msg)`       | 알림 메시지   | `alert("저장 완료");`       |
| `confirm(msg)`     | 예/아니오    | `confirm("삭제하시겠습니까?");` |
| `trace(msg)`       | 콘솔 출력    | `trace("LOG");`         |
| `transaction(...)` | 서버 통신 실행 | *(아래 예시)*               |


| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `close()` | 현재 폼 닫기 | ```javascript<br>this.close();``` |
| `reload()` | 폼 새로고침 | ```javascript<br>this.reload();``` |
| `setFocus(obj)` | 특정 컴포넌트에 포커스 설정 | ```javascript<br>this.setFocus(this.edt_name);``` |
| `lookup("컴포넌트ID")` | 컴포넌트 찾기 | ```javascript<br>var btn = this.lookup("btn_save");``` |



## 문자열 / 유틸
| 함수                      | 설명     | 예시                            |
| ----------------------- | ------ | ----------------------------- |
| `nexacro.trim(str)`     | 공백 제거  | `nexacro.trim(" a ")`         |
| `nexacro.toNumber(str)` | 숫자로 변환 | `nexacro.toNumber("00123")`   |
| `nexacro.toDate(str)`   | 날짜형 변환 | `nexacro.toDate("20250101")`  |
| `isEmpty(str)` (직접 구현)  | 빈문자 체크 | `if (this.gfn_isEmpty(v)) {}` |


