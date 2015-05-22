_[To Documentation Index](https://github.com/JeremySkinner/FluentValidation/wiki/Index)_

## Example

```csharp
using FluentValidation;

public class CustomerValidator: AbstractValidator<Customer> {
  public CustomerValidator() {
    RuleFor(customer => customer.Surname).NotEmpty();
    RuleFor(customer => customer.Forename).NotEmpty().WithMessage("Please specify a first name");
    RuleFor(customer => customer.Discount).NotEqual(0).When(customer => customer.HasDiscount);
    RuleFor(customer => customer.Address).Length(20, 250);
    RuleFor(customer => customer.Postcode).Must(BeAValidPostcode).WithMessage("Please specify a valid postcode");
  }

  private bool BeAValidPostcode(string postcode) {
    // custom postcode validating logic goes here
  }
}

Customer customer = new Customer();
CustomerValidator validator = new CustomerValidator();
ValidationResult results = validator.Validate(customer);

bool validationSucceeded = results.IsValid;
IList<ValidationFailure> failures = results.Errors;
```

## Documentation table of contents
See [[Index|a. Index]]
- [[FAQ - Frequently Asked Questions|z. FAQ]]
- [[Creating a Validator Class|b. Creating a Validator]] || [[Chaining Validators|b. Creating a Validator#chaining-validators-for-the-same-property]]  
  * [[Validation Results|b. Creating a Validator#validation-results]] || [[Throwing Exceptions|b. Creating a Validator#throwing-exceptions]]
  * **Re-using Validators**: [[on Complex Properties|b. Creating a Validator#complex-properties]] || and [[on Nested Collections|b. Creating a Validator#collections]]
  * [[Rule Sets|b. Creating a Validator#rulesets]]
- [[Built in Validators|c. Built In Validators]]
  * [[NotNull Validator|c. Built In Validators#notnull-validator]] || [[NotEmpty Validator|c. Built In Validators#notempty-validator]]
  * [[NotEqual Validator|c. Built In Validators#notequal-validator]] || [[Equal Validator|c. Built In Validators#equal-validator]] || [[Length Validator|c. Built In Validators#length-validator]]
  * [[Less Than Validator|c. Built In Validators#less-than-validator]] || [[Less Than Or Equal Validator|c. Built In Validators#less-than-or-equal-validator]] || [[Greater Than Validator|c. Built In Validators#greater-than-validator]] || [[GreaterThan Or Equal Validator|c. Built In Validators#greater-than-or-equal-validator]]
  * [[Predicate Validator (aka Must)|c. Built In Validators#predicate-validator]] || [[RegEx Validator|c. Built In Validators#regular-expression-validator]]
  * [[Email Validator|c. Built In Validators#email-validator]] 
- [[Configuring/Customising a validator|d. Configuring a Validator]]
  * [[When to stop validating: Specifying the cascade mode|d. Configuring a Validator#setting-the-cascade-mode]]
  * Overriding: [[the default error message|d. Configuring a Validator#overriding-the-default-error]] || [[the default property name|d. Configuring a Validator#overriding-the-default-property-name]]
  * [[Specifying a condition with When/Unless|d. Configuring a Validator#user-content-specifying-a-condition-with-whenunless]]
- [[Custom Validators|e. Custom Validators]]
  * [[Writing a custom Property Validator|e. Custom Validators#writing-a-custom-property-validator]]
  * [[Using AbstractValidator.Custom|e. Custom Validators#using-abstractvalidatorcustom]]
- [[Localization|f. Localization]]
- [[Testing Validators|g. Testing]]
- [[Integrating with ASP.NET MVC|h. MVC]]
- [[Using a Validator Factory with an IoC container|i. IoC]]
- [[Installation via NuGet|j. Nuget]]

