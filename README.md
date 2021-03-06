# PHP-EasyDB

##Easy to use MySQL and PostgreSQL database library for PHP.

Disclaimer: This is a heavily modified version of the database classes used in the PHP Beyond the the Basics Lynda tutorial. I am not trying to steal the original IP.

#### Create a database object using params:
  type, host, database name, user, password
```php
// 1 for mysql
$db = new Database(1, "localhost", "foobar", "root", "toor");
// 2 for postgres
$db = new Database(2, "localhost", "foobar", "root", "toor");
```


#### Create base class and extend DatabaseTable
```php
class Test extends DatabaseTable {
  protected static $table_name = "test";
  protected static $db_fields = array(
    'id',
    'test'
  );
  protected static $db_types = array(
    'int(11) NOT NULL',         // id
    'varchar(11) NOT NULL'     // test
  );
  
  public $id;
  public $test;
  
  public static function find_by_test($database, $test){
    $sql = "SELECT * FROM " . static::$table_name . " WHERE test=" . $test;
    $result_array = static::find_by_sql($database, $sql);
    return !empty($result_array) ? $result_array : false;
  }
}
```

#### Get row by id
```php
$row = Test::find_by_id($db, 1);
```

#### Use custom function to find row(s)
```php
$rows = Test::find_by_test($db, "foobar");
```

#### Get row(s) with specific sql
```php
$rows = Test::find_by_sql($db, "SELECT * FROM test LIMIT 3 ORDER BY ASC");
```

#### Get array of all rows
```php
$rows = Test::find_all($db);
```

#### Loop through rows
```php
foreach($rows as $row){
  // do stuff
}
```

#### Get data from row
```php
echo $row->test;
```

#### Set row data
```php
$row->test = "foobar";
```

#### Save row
```php
if($row->save()){
  echo "yeah, it worked!";
} else {
  echo "dang it";
}
```

#### Delete row
```php
if($row->delete()){
  echo "yeah, it worked!";
} else {
  echo "dang it";
}
```

