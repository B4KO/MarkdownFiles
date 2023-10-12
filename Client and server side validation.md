# Validation on the client-side(frontend) and on the server-side(backend)

There are diffrent ways of validating user input on both sides of the system. While client-side validation of user input is easily bypassed by sending data packets to the backend via. a third party app,  it is still advised to use it in conjunction with server side validation. This doc will show you how to validate input using diffrent methods.

1. jQuery is a js-library featured in all ASP.NET Core Apps

2. Bootstrap is a css/js-library featured in all ASP.NET Core Apps

3. Data annotations is a feature in ASP.NET that enables the user of setting requirements to the content that uses the model. In other words validation input on the server side. 

# jQuery validation (client-side)

### 1. **Integration**:

Firstly, you'll need to include the jQuery library and the jQuery Validation plugin in your project:

```html
<script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-validate/1.19.3/jquery.validate.min.js"></script>
```

### 2. **Basic Validation**:

With the plugin included, you can now call the `validate` method on a form element to initiate validation:

```javascript
$(document).ready(function() {
    $("#myForm").validate();
});
```

When you call `validate()` on a form, the plugin will automatically validate the form before it's submitted and prevent the submission if the validation fails.

### 3. **Defining Rules**:

By default, the plugin will look for standard HTML5 data validation attributes like `required`, `email`, `url`, etc. However, you can define custom validation rules using the `rules` option:

```javascript
$("#myForm").validate({
    rules: {
        fieldName: {
            required: true,
            minlength: 5
        }
    }
});
```

### 4. **Error Messages**:

The plugin will automatically generate error messages based on the validation rules, but you can customize them using the `messages` option:

```javascript
$("#myForm").validate({
    rules: {
        fieldName: {
            required: true,
            minlength: 5
        }
    },
    messages: {
        fieldName: {
            required: "Please enter a value",
            minlength: "Your value must be at least 5 characters long"
        }
    }
});
```

### 5. **Highlighting Errors**:

You can customize the way the plugin highlights form elements with validation errors. The `highlight` and `unhighlight` options allow you to define functions to style invalid and valid elements, respectively:

```javascript
$("#myForm").validate({
    highlight: function(element, errorClass) {
        $(element).addClass('is-invalid');
    },
    unhighlight: function(element, errorClass) {
        $(element).removeClass('is-invalid');
    }
});
```

### 6. **Additional Methods**:

The plugin provides additional validation methods beyond the standard ones. For instance, you can validate that a field matches another field (useful for password confirmations) using the `equalTo` method. There's also an extension script (`additional-methods.js`) that adds even more validation methods.

### 7. **Remote Validation**:

With jQuery Validation, you can validate a field by sending the data to the server using AJAX. This is useful for checks that can't be performed client-side, like verifying if a username is already taken.

```javascript
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            remote: "check-username.php"
        }
    }
});
```

For this to work, the server-side script (e.g., `check-username.php`) should return `true` if the input is valid and an error message (as a string) if it's not.

### Final Thoughts:

While jQuery Validation is powerful and easy to use for client-side validation, remember that client-side validation can be bypassed. Always have server-side validation in place as a backup to ensure data integrity and security.

# Bootstrap 5 validation (client-side)

Bootstrap 5 provides built-in styles for form validation feedback. The validation classes in Bootstrap 5 work alongside HTML5 form validation attributes like `required`, `pattern`, etc. Here's how to use Bootstrap 5 form validation:

### 1. **Basic Validation**:

Bootstrap's styles take advantage of the `:valid` and `:invalid` pseudo-classes applied by browsers during HTML5 validation.

For example:

```html
<input type="text" class="form-control" required>
```

If this input field is left empty (since it has the `required` attribute), the browser marks it as `:invalid` and Bootstrap will style it accordingly.

### 2. **Validation Feedback**:

Bootstrap provides classes to add custom validation feedback messages:

```html
<div class="form-group">
    <input type="text" class="form-control" id="username" required>
    <div class="invalid-feedback">
        Please choose a username.
    </div>
</div>
```

The feedback won't be shown by default when using the `invalid-feedback` class. You'd need to either utilize custom JavaScript or Bootstrap's JavaScript to handle the display based on user interactions.

### 3. **Custom Styles**:

If you don't want to rely on browser default validation (which may vary across browsers), you can manually apply `.is-valid` or `.is-invalid` classes to your form controls:

```html
<input type="text" class="form-control is-invalid">
<div class="invalid-feedback">
    Please choose a username.
</div>
```

### 4. **Server-side Validation**:

If you're providing feedback after server-side validation, you might manually set `.is-valid` or `.is-invalid` classes based on the server's response.

### 5. **Validation with Tooltips**:

Instead of block-style feedback messages, Bootstrap also supports feedback in the form of tooltips. Use the `valid-tooltip` or `invalid-tooltip` classes:

```html
<input type="text" class="form-control" id="username" required>
<div class="invalid-tooltip">
    Please choose a username.
</div>
```

### 6. **Disabling Validation Styles**:

If you want to turn off the validation styling for a particular form control, you can use the `novalidate` boolean attribute on a form:

```html
<form novalidate>
  <input type="text" class="form-control" required>
</form>
```

This will prevent the browser from applying validation and thus Bootstrap will not style the form controls based on validity.

### 7. **Bootstrap JavaScript for Validation**:

Bootstrap 5 provides JavaScript to handle form validation. This can be used to provide visual feedback (displaying the validation messages):

```javascript
// Fetch all the forms we want to apply custom Bootstrap validation styles to
var forms = document.querySelectorAll('.needs-validation');

// Loop over them and prevent submission
Array.prototype.slice.call(forms)
    .forEach(function (form) {
        form.addEventListener('submit', function (event) {
            if (!form.checkValidity()) {
                event.preventDefault()
                event.stopPropagation()
            }

            form.classList.add('was-validated')
        }, false)
    });
```

The above script ensures that when the form is submitted, it checks the validity of the form elements. If any element is invalid, it prevents form submission (`event.preventDefault()`) and applies the `was-validated` class to the form. This class combined with the Bootstrap styles displays the appropriate validation feedback.

### Remember:

Bootstrap 5 provides styles and some JavaScript utilities for form validation, but the actual logic and enforcement of validation are based on HTML5 validation features. Always combine client-side validation with server-side validation for security and robustness.

# ASP.NET MVC 7 Validation (Server-side)

Server-side validation is crucial in any web application because it is the final gatekeeper to ensuring that data being processed is valid, especially since client-side validation can be bypassed. In ASP.NET, there are multiple approaches to server-side validation, depending on the specific framework or model you're using (e.g., Web Forms, ASP.NET MVC, or ASP.NET Core). Here's a general overview:

### 1. **ASP.NET MVC**:

In ASP.NET MVC, you often validate data at the model level using Data Annotations:

```csharp
public class UserModel
{
    [Required(ErrorMessage = "Username is required")]
    public string Username { get; set; }

    [EmailAddress(ErrorMessage = "Invalid Email Address")]
    public string Email { get; set; }
}
```

When the form is posted back to an action, you can check if the model is valid:

```csharp
[HttpPost]
public ActionResult Register(UserModel model)
{
    if (ModelState.IsValid)
    {
        // Process the data...
        return RedirectToAction("Success");
    }
    else
    {
        return View(model);
    }
}
```

### 2. **ASP.NET Core**:

ASP.NET Core MVC also uses Data Annotations for model validation similar to ASP.NET MVC:

```csharp
public class UserModel
{
    [Required(ErrorMessage = "Username is required")]
    public string Username { get; set; }

    [EmailAddress(ErrorMessage = "Invalid Email Address")]
    public string Email { get; set; }
}
```

The process of checking the `ModelState` in your controller action is the same as in ASP.NET MVC.

### 4. **Custom Validation**:

Regardless of the framework, you can always perform custom validation in your code. This could be inside a Web Forms code-behind file, an MVC controller action, or an ASP.NET Core action method.

```csharp
if (string.IsNullOrEmpty(model.Username) || model.Username.Length < 5)
{
    ModelState.AddModelError("Username", "Username must be at least 5 characters long.");
}
```

### Important Points:

1. **Always Perform Server-Side Validation**: Even if you're doing client-side validation, always validate on the server side. Clients can bypass client-side checks.
2. **Sensitive Data**: Be cautious about the error messages you return to the client. Avoid revealing sensitive details about your system or database.
3. **Regularly Update**: Ensure you're using the latest versions of ASP.NET, its packages, and other dependencies to benefit from any security and validation improvements.

Overall, server-side validation in ASP.NET can be done effortlessly using built-in controls and tools, but always ensure that your validations cover all potential edge cases and security threats.
