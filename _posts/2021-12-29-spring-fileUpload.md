---
title: "스프링에서 다중 파일 업로드 구현하기"
date: 2021-12-29
categories: Spring
---

### 다중 파일 업로드 구현

---

input file로 파일 업로드를 구현할 시 여러개의 파일을 한번에 업로드 하는 방법을 알아보자.

---

**JSP**

```
<form action="fileUpload" method="post" enctype="multipart/form-data">
    <input type="file" name="file" multiple>
</form>
```

form에 enctype 속성을 추가시켜 multipart/form-data를 설정해주고 input에 multiple 속성을 추가시켜주면 여러개의 파일을 업로드 가능하게 된다.

---

**Controller**

```
@Controller
public class FileController {

	@RequestMapping("/fileUpload")
	public String fileUpload(MultipartHttpServletRequest request, Model model) {
		List<MultipartFile> fileList = request.getFiles("file");

		for(MultipartFile file : fileList) {
			String fileName = file.getOriginalFilename();
			byte[] fileData = null;
			try {
				fileData = file.getBytes();
			} catch (IOException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}

			String savedFileName = uploadFile(fileName, fileData);
		}

		return "mainPage";
	}
```

Controller에서는 다중 업로드 파일을 처리하기 위해 MultipartHttpServletRequest로 파일 데이터를 가져온다.

가져온 다중 파일 데이터는 List 형식으로 저장되며 file을 디렉토리, DB에 업로드 하는 작업을 처리한다.

---

**파일 업로드**

```
public String uploadFile(String fileName, byte[] fileData) {

    String uploadPath = "/upload/";
    File fileDirectory = new File(uploadPath);
    if(!fileDirectory.exists()) {
        fileDirectory.mkdirs();
    }

    UUID uuid = UUID.randomUUID();
    String savedFileName = uuid.toString() + fileName;

    File target = new File(uploadPath, savedFileName);
    try {
        FileCopyUtils.copy(fileData, target);
    } catch (IOException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
    }

    return savedFileName;
}
```

컨트롤러에 디렉토리에 파일 업로드를 위한 기능을 구현하는 메소드를 작성한다.
파일 이름이 중복 되더라도 고유성이 보장되는 파일 이름으로 저장하기 위해 UUID를 사용하여 파일 이름을 작성하여 저장한다.
