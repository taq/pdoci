PDOCI
=====

Wrapping on PHP OCI functions to simulate a PDO object, since PDO support for OCI is very confuse and slow.

Let's face it. Installing PHP, PDO, Oracle drivers and PDO OCI is not a pleasant
task. Is more pleasant to insert bamboo sticks under your fingernails than make
all the voodoo needed to accomplish that task. And there are two big problems
with that:

1. If you install `pdo_oci` with `pecl` you'll get a version from 2005. Even
   Christian Bale is now far from the things from 2005, and wow, he had a cool
   costume and a very nice car.

2. If you follow the official docs, you'll need to compile PHP and still get an
   *experimental* feature. Come on. We can't (yeah, we know how to do it!)
   compile PHP on every server we need and just for an experimental feature?

That's why I made `PDOOCI`.

What is needed
--------------

Just install the Oracle drivers (I like the instant client versions) and the
`oci8` package (with `pecl`, this one seems to be updated often). Then require
the `pdooci.php` file and change some existing code like

```
$pdo = new PDO("oci:dbname=mydatabase;charset=utf8", "user", "password");
```

to 

```
require_once "pdooci.php";

$pdo = new PDOOCI\PDO("mydatabase", "user", "password");
```

Yeah, the rest should work exactly the same as if you were using a PDO object. :-)

Testing
-------

There is a test suite (using `PHPUnit`) on the `test` directory. If you want to
test (you must test your code!), create a table called `people` with two
columns:

1. `name` as `varchar2(50)`
2. `email` as `varchar2(30)` 

And some environment variables:

1. `PDOOCI_user` with the database user name
2. `PDOOCI_pwd` with the database password
3. `PDOOCI_str` with the database connection string

And then go to the `test` dir and run `PHPUnit` like:

```
phpunit --colors .
```
