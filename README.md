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

# ✅ **Nexacro 공통함수 정리표 (역할 + 예시 포함)**


## 📌 **2.1 Util 함수**

| 함수명                  | 역할(설명)                           | 사용 예시                                              |
| -------------------- | -------------------------------- | -------------------------------------------------- |
| gfn_IsNull           | 값이 null 이거나 빈 문자열인지 확인하여 true 반환 | `if (gfn_IsNull(sValue)) { ... }`                  |
| gfn_IsEmpty          | 값이 존재하는지 여부 체크                   | `if (gfn_IsEmpty(ds.getColumn(0, "USER_NM")))`     |
| gfn_IsEmail          | 이메일 형식인지 체크                      | `gfn_IsEmail("test@test.com")`                     |
| gfn_Trim             | 문자열 좌우 공백 제거                     | `var s = gfn_Trim("  AA  ");`                      |
| gfn_IsNumber         | 숫자 여부 체크                         | `gfn_IsNumber("1234")`                             |
| gfn_IsNum            | 숫자 형식에 맞는지 체크                    | `gfn_IsNum("00123")`                               |
| gfn_IsDate           | YYYYMMDD 날짜 정합성 체크               | `gfn_IsDate("20250101")`                           |
| gfn_IsTime           | HHMMSS 시간 정합성 체크                 | `gfn_IsTime("235959")`                             |
| gfn_GetCenterPos     | 팝업을 모니터 중앙 위치로                   | `gfn_GetCenterPos(500, 300)`                       |
| gfn_IsDatasetUpdate  | 데이터셋 수정 여부 체크                    | `if (!gfn_IsDatasetUpdate(ds_list)) return;`       |
| gfn_Right            | 문자열 오른쪽에서 N자리                    | `gfn_Right("ABCDEF", 2) → "EF"`                    |
| gfn_Left             | 문자열 왼쪽에서 N자리                     | `gfn_Left("ABCDEF", 3) → "ABC"`                    |
| decode               | 조건 분기 처리                         | `decode(flag, "Y", "사용", "N", "미사용")`              |
| gfn_SubStr           | 문자열 부분 추출                        | `gfn_SubStr("ABCDEFG", 2, 3)`                      |
| gfn_transNullToEmpty | null → ""                        | `gfn_transNullToEmpty(null)`                       |
| gfn_StrToArray       | 문자열을 특정 길이로 자른 배열로               | `gfn_StrToArray("ABCDEF", 2) → ["AB", "CD", "EF"]` |
| gfn_IsValidFunc      | 함수 존재 여부 체크                      | `gfn_IsValidFunc("fn_search")`                     |
| gfn_Pos              | 특정 문자의 위치 반환                     | `gfn_Pos("AAA_BBB", "_") → 3`                      |
| gfn_SetMyBuilderXml  | XML 변환                           | `gfn_SetMyBuilderXml(ds)`                          |
| gfn_ReplaceAll       | 대소문자 구분 없이 치환                    | `gfn_ReplaceAll("AAaaAA", "aa", "XX")`             |
| gfn_Date2Str3        | 20160101 → 2016-01-01            | `gfn_Date2Str3("20160101")`                        |

---

## 📌 **2.2 Common Script 함수**

| 함수명             | 역할                          | 예시                                                                        |
| --------------- | --------------------------- | ------------------------------------------------------------------------- |
| gfn_ServiceCall | 트랜잭션(callTransaction) 공통 호출 | `gfn_ServiceCall("search", "getPgm/...do", ds_in, ds_out, "fn_Callback")` |
| gfn_SetFormLoad | Form 최초 로드시 초기 설정           | `this.gfn_SetFormLoad();`                                                 |
| gfn_GetUserInfo | 로그인 사용자 정보 조회               | `var user = gfn_GetUserInfo("USER_ID");`                                  |

---

## 📌 **2.3 Date 함수**

| 함수명                  | 역할         | 예시                                          |
| -------------------- | ---------- | ------------------------------------------- |
| gfn_IsHoliday        | 휴일 여부 리턴   | `if (gfn_IsHoliday("20250101"))`            |
| gfn_GetFirstDate     | 월 첫 날짜     | `gfn_GetFirstDate("20250115") → 20250101`   |
| gfn_LastDateNum      | 월의 마지막 일자  | `gfn_LastDateNum("202501") → 31`            |
| gfn_GetQuarterFLDate | 분기 시작/종료일  | `gfn_GetQuarterFLDate("20250310")`          |
| gfn_DiffDate         | 일자 차이      | `gfn_DiffDate("20250101", "20250110") → 9`  |
| gfn_GetDiffMonth     | 월 차이       | `gfn_GetDiffMonth("202401", "202501") → 12` |
| gfn_GetDay           | 요일 반환      | `gfn_GetDay("20250101") → 3`                |
| gfn_IsLeapYear       | 윤년 체크      | `gfn_IsLeapYear(2024)`                      |
| gfn_StrToDate        | 문자열 → date | `gfn_StrToDate("20250101")`                 |
| gfn_Today            | 오늘 날짜      | `gfn_Today()`                               |
| gfn_AddDate          | 날짜 + N일    | `gfn_AddDate("20250101", 3)`                |
| gfn_AddMonth         | 날짜 + N개월   | `gfn_AddMonth("20250101", 1)`               |
| gfn_DateTime         | 현재 시각 리턴   | `gfn_DateTime()`                            |
| gfn_GetWeekNo        | 주차         | `gfn_GetWeekNo("20250103")`                 |

---

## 📌 **2.4 첨부파일 함수**

| 함수명                    | 역할         | 예시                                       |
| ---------------------- | ---------- | ---------------------------------------- |
| gfn_PopupComnAtchFiles | 첨부파일 공통 팝업 | `gfn_PopupComnAtchFiles("FILE_ID", "R")` |

---

## 📌 **2.5 Form 함수**

| 함수명                 | 역할             | 예시                                        |
| ------------------- | -------------- | ----------------------------------------- |
| gfn_DialogModeless  | 모달리스 팝업        | `gfn_DialogModeless("PP0110_POP")`        |
| gfn_DialogModal     | 모달 팝업          | `gfn_DialogModal("PP0110_POP")`           |
| gfn_ShowDialog      | 공통 Dialog      | `gfn_ShowDialog("MSG001")`                |
| gfn_Alert           | 공통 alert 비동기   | `gfn_Alert("저장되었습니다")`                    |
| gfn_Confirm         | 공통 confirm 비동기 | `gfn_Confirm("삭제하시겠습니까?", "fn_Callback")` |
| gfn_ConfirmSync     | 동기 confirm     | `if (gfn_ConfirmSync("확인?")) ...`         |
| gfn_SimpleMsg       | 하단 메시지         | `gfn_SimpleMsg("조회완료")`                   |
| gfn_CallSaveMsg     | 저장 후 결과 메시지    | `gfn_CallSaveMsg("S")`                    |
| gfn_GetMsg          | 메시지 코드 변환      | `gfn_GetMsg("MSG0001")`                   |
| gfn_GoMenu          | 메뉴 오픈          | `gfn_GoMenu("PP0110C")`                   |
| gfn_SetScreenParams | 화면 파라미터 설정     | `gfn_SetScreenParams(obj)`                |
| gfn_GetScreenParams | 화면 파라미터 조회     | `gfn_GetScreenParams("projNo")`           |
| gfn_GetShareValue   | 폼간 공유값 조회      | `gfn_GetShareValue("EMP")`                |
| gfn_SetShareValue   | 폼간 공유값 설정      | `gfn_SetShareValue("EMP", "홍길동")`         |
| gfn_PopupMultiInput | 멀티 선택 pop      | `gfn_PopupMultiInput("empPop")`           |
| gfn_GetFormSize     | 폼 크기           | `gfn_GetFormSize()`                       |
| gfn_IsValidation    | 널 체크 / 중복 체크   | `if (!gfn_IsValidation(...)) return;`     |
| gfn_PopClose        | 팝업 닫기          | `gfn_PopClose()`                          |
| gfn_CallReportPopUp | 출력 팝업 호출       | `gfn_CallReportPopUp("RPT001")`           |
| gfn_GetUniqueId     | UUID 생성        | `gfn_GetUniqueId()`                       |

---

## 📌 **2.6 Grid 함수**

가장 길기 때문에 **핵심 사용함수 중심으로 실무용 정리**해줬어.

| 함수명                  | 역할                  | 예시                                   |
| -------------------- | ------------------- | ------------------------------------ |
| gfn_GridAdd          | Grid 행 추가           | `gfn_GridAdd(grd_list)`              |
| gfn_GridInsert       | 현재 행 위에 삽입          | `gfn_GridInsert(grd_list)`           |
| gfn_GridCancel       | 수정 취소               | `gfn_GridCancel(grd_list)`           |
| gfn_GridDel          | 삭제                  | `gfn_GridDel(grd_list)`              |
| gfn_GridCUDFlag      | C/U/D 처리용 flag 세팅   | `gfn_GridCUDFlag(ds, row)`           |
| _getRowUpdate        | 해당 row 수정 여부        | `_getRowUpdate(ds, row)`             |
| gfn_SetGridCheckAll  | 전체 선택               | `gfn_SetGridCheckAll(grd_list)`      |
| gfn_GridSort         | 정렬                  | `gfn_GridSort(grd_list, "ITEM_CD")`  |
| gfn_GridSetHeadText  | Header 메시지 코드 자동 적용 | `gfn_GridSetHeadText(grd_list)`      |
| gfn_FindInGrid       | 특정 문자열 검색           | `gfn_FindInGrid(grd_list, "검색어")`    |
| gfn_Grid_onrbuttonup | 우클릭 이벤트 처리          | 이벤트 내 호출                             |
| gfn_ExportExcelEx    | 엑셀 Export           | `gfn_ExportExcelEx(grd_list)`        |
| gfn_ImportExcel      | 엑셀 Import           | `gfn_ImportExcel("sheet1", ds_list)` |
| gfn_GridSelectCheck  | 체크된 row만 반환         | `gfn_GridSelectCheck(grd_list)`      |
| gfn_GridRowArea      | 우클릭 Row 영역 팝업       | 내부 메뉴 기능                             |
| gfn_GridColArea      | Column 우클릭 팝업 메뉴    | 필터/정렬 메뉴                             |


좋아!
**Naming Rule 전체를 “표 형식 + 설명 + 예시”**로 실무에서 바로 쓸 수 있게 정리해줄게.
범위는 다음 3개 전체 포함:

✔ **Front-End (Nexacro)**
✔ **Back-End (Java / Mapper / Service / Controller)**
✔ **Dataset / Column / Component / Function Rule**

---

# ✅ **📌 Nexacro & Back-End Naming Rule — 전체 표 정리**

---

# 1️⃣ **화면(FORM) Naming Rule**

| 구분    | 규칙             | 예시                                  |
| ----- | -------------- | ----------------------------------- |
| 업무 구분 | 두자리 대문자 코드     | `CM`(공통), `PP`(구매), `HR`(인사)        |
| UI 종류 | 화면 성격을 뒤에 추가   | `C`(조회), `R`(등록), `P`(팝업), `L`(리스트) |
| 완성 규칙 | 업무 + 화면ID + 종류 | `PP0110C`, `PP0110P`, `HR0120L`     |

---

# 2️⃣ **Component Naming Rule**

## ✔ Component Prefix 규칙 표

| Component | Prefix | 예시                       |
| --------- | ------ | ------------------------ |
| Div       | `div_` | `div_search`             |
| Static    | `sta_` | `sta_title`              |
| Button    | `btn_` | `btn_search`, `btn_save` |
| Edit      | `edt_` | `edt_userNm`             |
| Combo     | `cbo_` | `cbo_orgCd`              |
| Calendar  | `cal_` | `cal_frDt`               |
| Grid      | `grd_` | `grd_list`               |
| Dataset   | `ds_`  | `ds_grdList`             |
| Tab       | `tab_` | `tab_main`               |
| CheckBox  | `chk_` | `chk_useYn`              |
| Radio     | `rdo_` | `rdo_gubun`              |

---

# 3️⃣ **Dataset & Column Naming Rule**

| 항목         | 규칙                       | 예시                              |
| ---------- | ------------------------ | ------------------------------- |
| Dataset    | `ds_업무_기능`               | `ds_grdList`, `ds_codeList`     |
| Dataset 검색 | `ds_search`              | `ds_search`                     |
| Column 이름  | DB 컬럼과 동일                | `USER_ID`, `ORG_CD`             |
| Flag 컬럼    | `_YN`, `_GB`, `_INDC` 사용 | `USE_YN`, `EDIT_INDC`, `DEL_YN` |

## ✔ Column Naming 형태별 예시

| 유형     | 예시                     |
| ------ | ---------------------- |
| 코드값    | ORG_CD, ITEM_CD        |
| 명칭     | ORG_NM, ITEM_NM        |
| 날짜     | STR_DT, END_DT, REG_DT |
| 사용자 정보 | USER_ID, REG_ID        |
| 상태값    | EDIT_INDC, DEL_YN      |

---

# 4️⃣ **Function Naming Rule**

## ✔ 함수 Prefix 규칙

| 종류             | Prefix       | 예시                        |
| -------------- | ------------ | ------------------------- |
| Event Function | `컴포넌트명_이벤트명` | `btn_search_onclick`      |
| Internal 처리함수  | `fn_`        | `fn_search`, `fn_init`    |
| 공통/전역 함수       | `gfn_`       | `gfn_IsNull`, `gfn_Alert` |

---

# 5️⃣ **Event Function Naming Rule**

| 규칙            | 설명                          | 예시                       |
| ------------- | --------------------------- | ------------------------ |
| 컴포넌트ID + 이벤트명 | 이벤트 표준                      | `btn_save_onclick()`     |
| grid 이벤트      | `grd_list_oncelldblclick()` | `grd_list_oncellclick()` |
| form 이벤트      | `form_onload()`             | Form 최초 로딩               |

---

# 6️⃣ **File Naming Rule (Front-End)**

| 파일 구분     | 규칙               | 예시                             |
| --------- | ---------------- | ------------------------------ |
| Form 파일   | 업무ID + 번호 + UI종류 | `PP0110C.xfdl`, `PP0110P.xfdl` |
| 화면 Script | Form과 동일 prefix  | `PP0110C.xfdl.js`              |

---

# 7️⃣ **Back-End Naming Rule**

---

## ✔ Controller / Service / Mapper Naming Rule

### 📌 Controller

| 규칙                       | 예시                          |
| ------------------------ | --------------------------- |
| 클래스명: `업무명 + Controller` | `PpController`              |
| 메서드명: 기능 + `Do`          | `getList.do`, `saveInfo.do` |

### 📌 Service

| 규칙                              | 예시                                  |
| ------------------------------- | ----------------------------------- |
| interface: `업무명 + Service`      | `PpService`                         |
| implements: `업무명 + ServiceImpl` | `PpServiceImpl`                     |
| method: 동사 + 명사                 | `selectPgmList()`, `saveUserInfo()` |

### 📌 Mapper

| 규칙                    | 예시                                            |
| --------------------- | --------------------------------------------- |
| XML 파일명: 업무명 + Mapper | `PpMapper.xml`                                |
| namespace = 인터페이스명    | `namespace="com.org.PpMapper"`                |
| 메서드: 동사로 시작           | `selectPgmList` / `insertUser` / `updateItem` |

---

# 8️⃣ **URL Naming Rule**

| 구분   | 규칙               | 예시                        |
| ---- | ---------------- | ------------------------- |
| Root | `/업무명/기능명/액션.do` | `/pp/pgm/getList.do`      |
| 조회   | `/getList.do`    | `/pp/user/getUserList.do` |
| 저장   | `/saveInfo.do`   | `/pp/user/saveUser.do`    |
| 삭제   | `/deleteInfo.do` | `/pp/user/deleteUser.do`  |

---

# 9️⃣ **Java 변수/메서드 Naming Rule**

| 구분  | 규칙         | 예시                         |
| --- | ---------- | -------------------------- |
| 클래스 | PascalCase | `UserServiceImpl`          |
| 메서드 | camelCase  | `getUserList()`            |
| 변수  | camelCase  | `userNm`, `orgCd`          |
| 상수  | 대문자 + 언더바  | `MAX_SIZE`, `DEFAULT_LANG` |

---

# 🔟 **SQL/Mapper Naming Rule**

| 구분            | 규칙                                | 예시                                 |
| ------------- | --------------------------------- | ---------------------------------- |
| parameterType | dto 이름                            | `parameterType="UserDto"`          |
| resultType    | dto 이름                            | `resultType="UserDto"`             |
| id            | select/insert/update/delete + 기능명 | `selectUserList`, `insertUserInfo` |




