# BitMS Software | Common methods

### System methods 

```php
<?php

use bitms\Service\System\Common;

$common = new Common;

```

### Generation password 
> Create new string password and encode

```php
<?php 

use bitms\Service\System\Common;

$common = new Common;

/**
 * @var $length int, default 12
 * @var $str_upper bool, default true
 * @var $str_lower bool, default true
 * @var $str_number bool, default true
 * @var $str_char bool, defa    ult false
 */
$common->password->setConfig(12, true, true, true, false);

/**
 * This set only one parameter set type hash key
 * @var $role enum('account', 'manager')
 */
$password = $common->password->generation(ROLE::ACCOUNT);

```

> Create user string to password

```php
<?php 

use bitms\Service\System\Common;

$common = new Common;

$str_password = 'customerPasswordString';
/**
 * This set only one parameter set type hash key
 * @var $role enum('account', 'manager')
 */
$password = $common->password->generation(ROLE::ACCOUNT, $str_password);

```
