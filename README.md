Documentation
-------------
- https://github.com/EcomDev/EcomDev_PHPUnit
- http://www.ecomdev.org/2011/02/01/phpunit-and-magento-yes-you-can.html

Installation
------------
- ensure ```packagist: false``` is not included in the project composer.json
- update project composer.json

```
#!json
{
    "require-dev": {
        "codebyjoe/ecomdev-phpunit": "dev-master"
    },
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/CodeByJoe/EcomDev_PHPUnit"
        }
    ]
}
```

Configuration
-------------
- cd MAGENTO_ROOT/shell
- php -f ecomdev-phpunit.php -- --action install
- php -f ecomdev-phpunit.php -- --action change-status
- php -f ecomdev-phpunit.php -- --action magento-config --db-name $DB_NAME --base-url http://your.magento.url/
- modify app/etc/local.xml.phpunit and set allow_same_db to 1

Usage
-----
- cd MAGENTO_ROOT
- ../vendor/phpunit/phpunit/phpunit

Example Unit Test
-----------------
### config.xml ###

```
#!xml
<?xml version="1.0"?>
<config>
    <modules>
        <MyNamespace_ModuleName>
            <version>0.1.0</version>
        </MyNamespace_ModuleName>
    </modules>
    <phpunit>
        <suite>
            <modules>
                <MyNamespace_ModuleName/>
            </modules>
        </suite>
    </phpunit>
</config>
```

### app/code/{codePool}/MyNamespace/ModuleName/Test/Model/TestModel.php ###

```
#!php
<?php
class MyNamespace_ModuleName_Test_Model_TestModel extends EcomDev_PHPUnit_Test_Case
{
    /**
     * @test
     * @author Joseph McDermott <code@josephmcdermott.co.uk>
     */
    public function testSomething()
    {
        $this->assertTrue(false, 'This is an optional description of what failed');
    }
}
```