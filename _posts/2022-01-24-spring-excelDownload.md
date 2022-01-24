---
title: "스프링 엑셀파일 다운로드 기능 구현하기"
date: 2022-01-24
categories: Spring
---

### 엑셀 파일 다운로드 기능 구현

---

스프링에서 엑셀 파일 다운로드 하는 기능을 간단히 구현해보자.

---

**엑셀 다운로드**

```
@RequestMapping(value="excelDownload", method = RequestMethod.POST)
      public String excelDownload(HttpServletResponse response) throws Exception {
            // 엑셀 다운로드가 필요한 DB 데이터를 불러온다
            List<User> listUser = UserDao.selectAllUser();

            Workbook wb = new HSSFWorkbook(); // 엑셀 파일 만들기
            Sheet sheet = wb.createSheet("시트이름"); // 엑셀 시트 만들기
            Row row = null; // 행
            Cell cell = null; // 셀
            int rowNo = 0;

            // 헤더 스타일 지정
            CellStyle headStyle = wb.createCellStyle();

            // 가는 경계선을 가집니다
            headStyle.setBorderTop(BorderStyle.THIN);
            headStyle.setBorderBottom(BorderStyle.THIN);
            headStyle.setBorderLeft(BorderStyle.THIN);
            headStyle.setBorderRight(BorderStyle.THIN);

            // 배경색은 노란색
            headStyle.setFillForegroundColor(HSSFColorPredefined.YELLOW.getIndex());
            headStyle.setFillPattern(FillPatternType.SOLID_FOREGROUND);

            // 가운데 정렬
            headStyle.setAlignment(HorizontalAlignment.CENTER);

            // 데이터 스타일 지정
            CellStyle bodyStyle = wb.createCellStyle();

            bodyStyle.setBorderTop(BorderStyle.THIN);
            bodyStyle.setBorderBottom(BorderStyle.THIN);
            bodyStyle.setBorderLeft(BorderStyle.THIN);
            bodyStyle.setBorderRight(BorderStyle.THIN);

            // 엑셀 헤더 생성
            row = sheet.createRow(rowNo++);
            cell = row.createCell(0);
            cell.setCellStyle(headStyle);
            cell.setCellValue("사용자 ID");
            cell = row.createCell(1);
            cell.setCellStyle(headStyle);
            cell.setCellValue("이름");
            cell = row.createCell(2);
            cell.setCellStyle(headStyle);
            cell.setCellValue("구분");
            cell = row.createCell(3);
            cell.setCellStyle(headStyle);
            cell.setCellValue("등록일");
            cell = row.createCell(4);
            cell.setCellStyle(headStyle);
            cell.setCellValue("수정일");

            for(User user : listUser) {
            row = sheet.createRow(rowNo++);

            cell = row.createCell(0);
            cell.setCellStyle(bodyStyle);
            cell.setCellValue(user.getUser_id());

            cell = row.createCell(1);
            cell.setCellStyle(bodyStyle);
            cell.setCellValue(user.getUser_name());

            cell = row.createCell(2);
            cell.setCellStyle(bodyStyle);
            cell.setCellValue(user.getUser_grant());

            cell = row.createCell(3);
            cell.setCellStyle(bodyStyle);
            cell.setCellValue(user.getUser_createdate());

            cell = row.createCell(4);
            cell.setCellStyle(bodyStyle);
            cell.setCellValue(user.getUser_updatedate());
            }

            // 컨텐츠 타입과 파일명 지정
            response.setContentType("ms-vnd/excel");
            response.setHeader("Content-Disposition", "attachment;filename=users.xls");

            // 엑셀 파일 다운
            wb.write(response.getOutputStream());
            wb.close();
            return null;
      }
```

엑셀 다운로드가 필요한 DB 데이터를 불러와 값을 지정하여 다운로드가 가능하다.
헤더로 데이터명을 지정할 수 있고 스타일 설정도 가능하다.
