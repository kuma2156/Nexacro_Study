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

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `addRow()` | 새 행 추가 | ```javascript<br>this.ds_user.addRow();``` |
| `deleteRow(nRow)` | 특정 행 삭제 | ```javascript<br>this.ds_user.deleteRow(0);``` |
| `getColumn(nRow, "컬럼명")` | 특정 행의 컬럼값 가져오기 | ```javascript<br>var name = this.ds_user.getColumn(0, "name");``` |
| `setColumn(nRow, "컬럼명", value)` | 특정 행의 컬럼값 설정 | ```javascript<br>this.ds_user.setColumn(0, "age", 25);``` |
| `getRowCount()` | 전체 행 수 반환 | ```javascript<br>trace("행 개수: " + this.ds_user.getRowCount());``` |
| `findRow("컬럼명", value)` | 조건에 맞는 행 인덱스 찾기 | ```javascript<br>var row = this.ds_user.findRow("user_id", "kim123");``` |
| `clearData()` | 모든 데이터 초기화 | ```javascript<br>this.ds_user.clearData();``` |

---

## 🌐 Transaction (서버 통신)

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `transaction()` | 서버와 데이터 통신 수행 | ```javascript<br>this.transaction("getUserList", "/user/getList.do", "ds_input=ds_in", "ds_output=ds_out", "param1=123", "fnCallback");``` |
| `fnCallback(trId, errCd, errMsg)` | 통신 완료 후 콜백 함수 | ```javascript<br>this.fnCallback = function(trId, errCd, errMsg){<br> if (errCd < 0) alert("오류: " + errMsg);<br> else alert("데이터 수신 완료!");<br>};``` |

---

## 🧩 Form 관련 함수

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `close()` | 현재 폼 닫기 | ```javascript<br>this.close();``` |
| `reload()` | 폼 새로고침 | ```javascript<br>this.reload();``` |
| `setFocus(obj)` | 특정 컴포넌트에 포커스 설정 | ```javascript<br>this.setFocus(this.edt_name);``` |
| `lookup("컴포넌트ID")` | 컴포넌트 찾기 | ```javascript<br>var btn = this.lookup("btn_save");``` |

---

## 🏠 Application (전역 제어)

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `nexacro.getApplication()` | 현재 실행 중인 앱 객체 가져오기 | ```javascript<br>var app = nexacro.getApplication();``` |
| `app.lookup("컴포넌트ID")` | 다른 폼의 컴포넌트 접근 | ```javascript<br>var loginForm = app.mainframe.VFrameSet.HFrameSet.form;<br>loginForm.btn_login.set_enable(false);``` |
| `app.exit()` | 애플리케이션 종료 | ```javascript<br>app.exit();``` |

---

## 🎨 컴포넌트 제어 함수

| 함수 | 설명 | 예시 코드 |
|:---|:---|:---|
| `set_visible(true/false)` | 표시/숨김 제어 | ```javascript<br>this.btn_submit.set_visible(true);``` |
| `set_enable(true/false)` | 활성/비활성 제어 | ```javascript<br>this.btn_submit.set_enable(false);``` |
| `set_text("텍스트")` | 텍스트 변경 | ```javascript<br>this.st_title.set_text("회원 정보");``` |
| `set_value(value)` | 값 설정 | ```javascript<br>this.edt_name.set_value("김명규");``` |
| `get_value()` | 현재 값 가져오기 | ```javascript<br>var name = this.edt_name.get_value();``` |

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
