# Fluent Validation Implementation

### Step-1 : Add Below `Package` into Project from `NuGet Package Manager` for Use Fluent Validation

```
- FluentValidation.AspNetCore
```

### Step-2 : Register `FluentValidation` into `Program.cs` File

```
builder.Services.AddValidatorsFromAssemblyContaining<PersonValidation>();
```

### Step-3 : Inject Below Code into `PersonController`

```
private readonly IValidator<PersonModel> _validator;

public PersonController(IValidator<PersonModel> validator)
{
    _validator = validator;
}
```

### Step-4 : Create `Validation` Folder into Project and Create `PersonValidation.cs` file and Add Below Code

```
using FluentValidation;
using WebApi_Demo.Models;

namespace WebApi_Demo.Validation
{
    public class PersonValidation : AbstractValidator<PersonModel>
    {
        public PersonValidation()
        {
            RuleFor(person => person.Name)
                .NotEmpty().WithMessage("Person Name is required")
                .Length(5, 30).WithMessage("Person Name must be between 5 to 30 characters");

            RuleFor(person => person.Contact)
                .NotEmpty().WithMessage("Contact Number is required")
                .Length(10).WithMessage("Contact Number must be exactly 10 digits")
                .Matches(@"^\d{10}$").WithMessage("Contact Number must contain only digits");

            RuleFor(person => person.Email)
                .NotEmpty().WithMessage("Email Address is required")
                .EmailAddress().WithMessage("Invalid Email Address format");
        }
    }
}
```
