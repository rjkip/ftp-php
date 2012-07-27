FTP for PHP (c) David Grudl, 2008 (http://davidgrudl.com)

Introduction
------------
FTP for PHP is a very small and easy-to-use library for accessing FTP servers.

David Grudl's project at GoogleCode: http://ftp-php.googlecode.com  
David Grudl's PHP blog: http://phpfashion.com

Requirements
------------
 * PHP 5.3+

Usage
-----
Opens an FTP connection to the specified host:

```php
<?php
$ftp = new FtpPhp\FtpClient;
$ftp->connect($host);
```

Login with username and password
```php
<?php
$ftp->login($username, $password);
```

Upload the file
```php
<?php
$ftp->put($destination_file, $source_file, FTP_BINARY);
```

Close the FTP stream
```php
<?php
$ftp->close();
```

Ftp throws exception if operation failed. So you can simply do following:
```php
<?php
try {
	$ftp = new FtpPhp\FtpClient;
	$ftp->connect($host);
	$ftp->login($username, $password);
	$ftp->put($destination_file, $source_file, FTP_BINARY);

} catch (FtpPhp\FtpException $e) {
	echo 'Error: ', $e->getMessage();
}
```

On the other hand, if you'd like the possible exception quietly catch, call methods with the prefix 'try':
```php
<?php
$ftp->tryDelete($destination_file);
```

When the connection is accidentally interrupted, you can re-establish it using method `$ftp->reconnect()`.