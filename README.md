<!-- ptfgen template base Login -->
<!-- ptfgen mock -->
<!-- ptfgen test -->
<!-- ptfgen json Model -->
<!-- ptfgen api Model -->
<!-- ptfgen bind Model -->

# Code generator for Flutter apps
## Installation:
### Install using pip3:
Open Terminal and run:
```
$ brew install python
```
```
$ pip3 install ptfgen
```

### Update:

```
$ pip3 install -U ptfgen
```

### Uninstall:

```
$ pip3 uninstall ptfgen
```

## 1. Create Template:
### 1.1. Base Template:
The Base Template contains necessary files for a screen using the [Flutter Clean Architecture](xxx) pattern.

Open Terminal, navigate to your flutter project folder you want to save the files and run:

```
$ ptfgen template base <Scene_Name>
```

#### Example:

```
$ ptfgen template base LoginEmail
```

Output:

```
Successfully created files:
    ./lib/assembler.dart
    ./lib/scenes/login_email/login_email_viewmodel.dart
    ./lib/scenes/login_email/login_email_navigator.dart
    ./lib/scenes/login_email/login_email_usecase.dart
    ./lib/scenes/login_email/login_email_assembler.dart
    ./lib/scenes/login_email/login_email_view.dart
    ./lib/mock/login_email_usecase_mock.dart
    ./test/unit_test/login_email/login_email_viewmodel_test.dart
    ./test/unit_test/login_email/login_email_usecase_mock.dart
    ./test/unit_test/login_email/login_email_navigator_mock.dart
```

## 2. Create models from JSON:
Copy the json then run the command:

```
$ ptfgen json <Model_Name> [-p]
```

#### Options:

`-p`, `--print`: print the result.

#### Example:
Copy the json:

```json
{
    "employees":[  
        {"name":"Shyam", "email":"shyamjaiswal@gmail.com"},  
        {"name":"Bob", "email":"bob32@gmail.com"},  
        {"name":"Jai", "email":"jai87@gmail.com"}  
    ]
} 
```

then run:

```
$ ptfgen json Company
```

Output:

```
The result has been copied to the pasteboard.
```

Content in the pasteboard:

```dart
import 'package:pt_object_mapper/pt_object_mapper.dart'; 

/// Remember register to Mappable.factories
/// Mappable.factories[Employee] = () => Employee();

class Employee with Mappable {
  String name;
  String email;

  @override
  void mapping(Mapper map) {
    map("name", name, (v) => name = v);
    map("email", email, (v) => email = v);
  }
}

/// Remember register to Mappable.factories
/// Mappable.factories[Company] = () => Company();

class Company with Mappable {
  List<Employee> employees;

  @override
  void mapping(Mapper map) {
    map<Employee>("employees", employees, (v) => employees = v);
  }
}
```

## 3. Create a mock class for a protocol/function:
Copy the abstract/function then run:

```
$ ptfgen mock [-p]
```

#### Options:

`-p`, `--print`: print the result.

#### Example:
Copy the abstract:

```dart
abstract class SignUpEmailUseCaseType {
  Stream<User> signUpWithEmail(String email, String password);
  ValidationResult validateEmail(String email);
  ValidationResult validatePassword(String password);
}
```

then run:

```
$ ptfgen mock
```

Output:

```
The result has been copied to the pasteboard.
```

Content in the pasteboard:

```dart
class SignUpEmailUseCaseMock implements SignUpEmailUseCaseType {

    /// signUpWithEmail

    var signUpWithEmail_Called = false;
    var signUpWithEmail_ReturnValue = Stream<User>.value(null);

      Stream<User> signUpWithEmail(String email, String password) {
        signUpWithEmail_Called = true;
        return signUpWithEmail_ReturnValue;
    } 

    /// validateEmail

    var validateEmail_Called = false;
    var validateEmail_ReturnValue = ValidationResult.valid();

      ValidationResult validateEmail(String email) {
        validateEmail_Called = true;
        return validateEmail_ReturnValue;
    } 

    /// validatePassword

    var validatePassword_Called = false;
    var validatePassword_ReturnValue = ValidationResult.valid();

      ValidationResult validatePassword(String password) {
        validatePassword_Called = true;
        return validatePassword_ReturnValue;
    } 
}
```
