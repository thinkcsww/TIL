​														Spring Validation

<h2>세팅 방법</h2>

------

1. Hibernate.org에서 Hibernate Validator를 다운 받아서 잘 저장한다.
2. 다운 받은 폴더에서 dist에 들어가면 있는 3개의 jar 파일을 lib에 추가한다
3. dist/lib/required에 있는 3개의 jar 파일을 lib에 추가한다.

<h2>사용 방법</h2>

------

1. 모델 class에서 다음과 같이 변수 위에 원하는 validation을 설정한다.

2. ```
   package com.luv2code.springdemo.mvc;
   
   import javax.validation.constraints.NotNull;
   import javax.validation.constraints.Size;
   
   public class Customer {
   	private String firstName;
   	
   	@NotNull(message="is required")
   	@Size(min=1, message="is required")
   	private String lastName;
   	
   	
   }
   
   ```

   2. Controller Class에 공백 제거를 하는 InitBinder를 추가한다.

   ```
   @InitBinder
   	public void initBinder(WebDataBinder dataBinder) {
   		
   		StringTrimmerEditor stringTrimmerEditor = new StringTrimmerEditor(true);
   		
   		dataBinder.registerCustomEditor(String.class, stringTrimmerEditor);
   	}
   ```

   3. Controller Class의 특정 RequestMapping에 에러 발생 시 구현한다.

   ```
   @RequestMapping("/processForm")
   	public String processForm(@Valid @ModelAttribute("customer") Customer theCustomer, BindingResult theBindingResult) {
   		
   		if (theBindingResult.hasErrors()) {
   			return "customer-form";
   		} else {
   			return "customer-confirmation";
   		}
   		
   	}
   ```

   

