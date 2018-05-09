Spring Boot Validation
---


# Default Validation with Spring Boot

Spring Boot provides good default implementation for validation for RESTful Services. Add validation to a REST API by using the `@Valid` and the `@RequestBody` annotations. 

## Wrong Content Type

If you use Content-Type as application/xml and this is not supported by your application, Spring Boot by default returns a response status of 415 - Unsupported Media Type

## Invalid JSON Content

If you send a invalid JSON content to a method expecting a body, you would get a 400 - Bad Request

Customizing Validations
To customize the validation, we will use Hibernate Validator, which is one of the implementations of the bean validation api.

We get Hibernate Validator for free when we use Spring Boot Starter Web.

**Implementing Validations on the Bean**

Let’s add a few validations to the Student bean. We are using `@Size` to specify the minimum length and also a message when a validation error occurs.

```java

@Entity
public class Student {
  @Id
  @GeneratedValue
  private Long id;
  
  @NotNull
  @Size(min=2, message="Name should have atleast 2 characters")
  private String name;
  
  @NotNull
  @Size(min=7, message="Passport should have atleast 2 characters")
  private String passportNumber;
  
```

**Implementing the Controller**



```java

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.*;
 
import javax.validation.Valid;
 
@Controller
public class CommentController {
 
    @RequestMapping(value = "/api/comment", method = RequestMethod.POST)
    @ResponseBody
    public CommentDTO add(@Valid @RequestBody CommentDTO comment) {
        return comment;
    }
}
```

We have now added a new method to our controller and added validation to it. When the validation fails, the `MethodArgumentNotValidException` is thrown. Add the following method in the `@ControllerAdvice` annotated class.

```java

	@Override
    @ResponseStatus(HttpStatus.BAD_REQUEST)
    @ResponseBody
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex,
			HttpHeaders headers, HttpStatus status, WebRequest request) {

    	BindingResult result = ex.getBindingResult();
        List<FieldError> fieldErrors = result.getFieldErrors();
        ValidationErrorVO validationErrorVO = new ValidationErrorVO();
        
        for (FieldError fieldError: fieldErrors) { 
        	validationErrorVO.addFieldError(fieldError.getField(), fieldError.getDefaultMessage());
        }
 
        ResponseEntity<Object> response = new ResponseEntity<Object>(validationErrorVO, HttpStatus.BAD_REQUEST);
        return response;
	}
```

---

# Custom validators

JSR 303 Validation gives a pretty broad set of validators out of the box. We can check string lengths, number max and min values, use regular expressions etc. But sometimes, we have a need for a specific kind of validation. That’s when we have to write our own validator and annotation.

For validator, we have to implement ConstraintValidator interface, we define an initialize method that is used to read parameters from annotations and isValid method that performs the validation.

**validation to check if given Integer value is in specified range:**

```java

public class InRangeValidator implements ConstraintValidator<InRange, Integer> {

    private int min;
    private int max;

    @Override
    public void initialize(InRange constraintAnnotation) {
        this.min = constraintAnnotation.min();
        this.max = constraintAnnotation.max();
    }

    @Override
    public boolean isValid(Integer value, ConstraintValidatorContext context) {
        return value == null || (value >= min && value <= max);
    }
}

```

Annotations are also really simple, we have to specify the validator class using Constraint annotation, and define available parameters, their default values, and default error message:

```java

@Target({ElementType.METHOD, ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Constraint(validatedBy = { InRangeValidator.class })
public @interface InRange {
    String message() default "Value is out of range";

    Class<?>[] groups() default {};

    Class<? extends Payload>[] payload() default {};

    int min() default Integer.MIN_VALUE;

    int max() default Integer.MAX_VALUE;
}

```





















