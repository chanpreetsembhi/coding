1. Simple Function
   - `validator.php` file

```php
<?php

class Validator
{
    public function string($value, $min = 1, $max = INF)
    {
        $value = trim($value);
        return strlen($value) >= $min && strlen($value) <= $max;
    }
}
```

   - `note-create.php` file
   
```php
require "validator.php";

$validator = new Validator();
    if (!$validator->string($_POST['body'], 1, 1000)) {
        $errors['body'] = "A body of no more than 1,000 characters is required";
    }
```

2. Static Function
   - `validator.php` file
```php
<?php

class Validator
{
    public static function string($value, $min = 1, $max = INF)
    {
        $value = trim($value);
        return strlen($value) >= $min && strlen($value) <= $max;
    }
}
```

- `note-create.php` file

```php
if (!Validator::string($_POST['body'], 1, 1000)) {
        $errors['body'] = "A body of no more than 1,000 characters is required";
    }
```