# 📘 Nexacro N 핵심 함수/구조 정리

## 🗂️ Dataset 기본 함수

| 함수                               | 역할                        | 예시                                    |
| -------------------------------- | ------------------------- | ------------------------------------- |
| **addRow()**                     | 마지막에 새 행 추가               | `var r = ds.addRow();`                |
| **insertRow(row)**               | 특정 위치에 행 삽입               | `ds.insertRow(2);`                    |
| **deleteRow(row)**               | 해당 행 삭제                   | `ds.deleteRow(0);`                    |
| **clearData()**                  | 데이터 초기화(컬럼 유지)            | `ds.clearData();`                     |
| **getColumn(row, colid)**        | 셀 값 조회                    | `var name = ds.getColumn(1, "NAME");` |
| **setColumn(row, colid, value)** | 셀 값 수정                    | `ds.setColumn(0, "AGE", 30);`         |
| **rowcount**                     | 전체 행 수                    | `trace(ds.rowcount);`                 |
| **filter(expr)**                 | 조건 필터링                    | `ds.filter("AGE >= 30");`             |
| **set_keystring("S:+age")**      | 정렬 설정                     | `ds.set_keystring("S:+AGE");`         |
| **copyData(ds2)**                | 데이터 복사                    | `ds2.copyData(ds1);`                  |
| **getCaseCount("U")**            | 변경된 상태 행 수 확인             | `ds.getCaseCount("U");`               |
| **getRowType(row)**              | 행 타입 조회 (INSERT/UPDATE 등) | `ds.getRowType(0);`                   |

---

## 🧱 Dataset 상태값(RowType)

| 상태         |  코드 | 의미    | 서버전송 |
| ---------- | :-: | ----- | :--: |
| **NORMAL** |  0  | 변경 없음 |   ❌  |
| **INSERT** |  2  | 신규 생성 |   ✅  |
| **UPDATE** |  4  | 수정됨   |   ✅  |
| **DELETE** |  8  | 삭제됨   |   ✅  |

---

## 📊 Grid 함수

| 함수                              | 역할         | 예시                                |
| ------------------------------- | ---------- | --------------------------------- |
| **getCellPos()**                | 현재 셀 위치 조회 | `var pos = grd.getCellPos();`     |
| **setCellPos(col)**             | 특정 컬럼으로 이동 | `grd.setCellPos(1);`              |
| **setFocus()**                  | 그리드 포커스 설정 | `grd.setFocus();`                 |
| **showEditor(true)**            | 셀 편집 강제 오픈 | `grd.showEditor(true);`           |
| **getCellValue(row, colid)**    | 셀 값 조회     | `grd.getCellValue(0, "NAME");`    |
| **setCellValue(row, colid, v)** | 셀 값 설정     | `grd.setCellValue(1, "AGE", 20);` |
| **selectRow(row)**              | 특정 행 선택    | `grd.selectRow(3);`               |
| **isSelectRow(row)**            | 선택 여부 확인   | `grd.isSelectRow(2);`             |

---

## 🧾 컴포넌트(Edit/Combo 등) 함수

| 함수                     | 역할             | 예시                            |
| ---------------------- | -------------- | ----------------------------- |
| **set_value(value)**   | 값 설정           | `edtName.set_value("홍길동");`   |
| **value / text**       | 값 또는 표시 텍스트 조회 | `var v = edtName.value;`      |
| **setFocus()**         | 포커스 이동         | `edtName.setFocus();`         |
| **set_enable(false)**  | 비활성화           | `btnSave.set_enable(false);`  |
| **set_readonly(true)** | 읽기전용           | `edtName.set_readonly(true);` |
| **set_visible(false)** | 숨김 처리          | `btnSave.set_visible(false);` |
| **set_index(i)**       | 콤보 index 설정    | `cmbType.set_index(1);`       |
| **getText()**          | 표시 텍스트 조회      | `edtName.getText();`          |

---

## 🧩 콤보박스(Combo) 속성

| 항목               | 역할       | 예시                        |
| ---------------- | -------- | ------------------------- |
| **innerdataset** | 콤보 데이터셋  | `innerdataset="ds_grade"` |
| **codecolumn**   | 실제 저장 값  | `"GRD_CD"`                |
| **datacolumn**   | 표시되는 텍스트 | `"GRD_NM"`                |
| **value / text** | 현재 선택 결과 | `cmbGrade.value // "A"`   |

---

## 🌐 Transaction (서버 통신)

| 항목                                  | 역할                          | 예시                                                                                               |
| ----------------------------------- | --------------------------- | ------------------------------------------------------------------------------------------------ |
| **transaction()**                   | 서버 호출/데이터 송수신               | `js\nthis.transaction("getUser", "svc::user.do", "in=dsIn", "out=dsOut", "id=1", "fnCallback");` |
| **fnCallback(trId, errCd, errMsg)** | 통신 After 처리                 | `js\nif(errCd < 0) alert(errMsg);`                                                               |
| **변경된 데이터만 전송됨**                    | INSERT/UPDATE/DELETE만 서버로 감 | `ds.getCaseCount("U")`로 체크                                                                       |

---

## 🧰 전역 객체 / Application

| 함수                           | 역할         | 예시                                    |
| ---------------------------- | ---------- | ------------------------------------- |
| **nexacro.getApplication()** | 전체 앱 객체 조회 | `var app = nexacro.getApplication();` |
| **app.lookup(id)**           | 컴포넌트 조회    | `app.lookup("btn_login");`            |
| **app.exit()**               | 앱 종료       | `app.exit();`                         |

---

## ⚡ Event 함수

| 함수                                 | 역할     | 예시                                                   |
| ---------------------------------- | ------ | ---------------------------------------------------- |
| **addEventHandler(evt, fn, this)** | 이벤트 추가 | `btn.addEventHandler("onclick", this.fnSave, this);` |
| **removeEventHandler(evt, fn)**    | 이벤트 제거 | `btn.removeEventHandler("onclick", this.fnSave);`    |

---

## 📢 Alert / Debug

| 함수               | 역할     | 예시                   |
| ---------------- | ------ | -------------------- |
| **alert(msg)**   | 메시지 팝업 | `alert("완료");`       |
| **confirm(msg)** | 확인창    | `confirm("삭제할까요?");` |
| **trace(msg)**   | 콘솔 출력  | `trace("LOG");`      |

---

## 📚 문자열 / 유틸

| 함수                        | 역할       | 예시                            |
| ------------------------- | -------- | ----------------------------- |
| **nexacro.trim(str)**     | 양쪽 공백 제거 | `nexacro.trim(" a ");`        |
| **nexacro.toNumber(str)** | 숫자로 변환   | `nexacro.toNumber("00123");`  |
| **nexacro.toDate(str)**   | 날짜 변환    | `nexacro.toDate("20250101");` |

---

## 🧠 Form 기본 함수

| 함수                | 역할      | 예시                             |
| ----------------- | ------- | ------------------------------ |
| **close()**       | 창 닫기    | `this.close();`                |
| **reload()**      | 화면 새로고침 | `this.reload();`               |
| **lookup(id)**    | 컴포넌트 조회 | `this.lookup("edtName");`      |
| **setFocus(obj)** | 포커스 이동  | `this.setFocus(this.edtName);` |

---

## 🧱 Grid 구조

| 영역          | 역할       |
| ----------- | -------- |
| **Head**    | 컬럼 제목    |
| **Body**    | 데이터 셀    |
| **Summary** | 합계/요약 정보 |


---
