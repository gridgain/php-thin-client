# Tests #

PHP Client for GridGain contains [PHPUnit](https://phpunit.de/) tests to check the behavior of the client. The tests include:
- functional tests which cover all API methods of the client
- examples executors which run all examples except AuthTlsExample
- AuthTlsExample executor

## Tests Installation ##

1. Download GridGain PHP client sources to `gridgain_client_path`
2. Go to `gridgain_client_path` folder
3. Execute `composer install` command. Depending on you PHP configuration you may need to install/configure some additional PHP extensions required by PHPUnit (see Composer error messages if any).

```bash
cd gridgain_client_path
composer install
```

## Tests Running ##

1. Run GridGain server locally or remotely with default configuration.
2. Set the environment variable:
    - **GRIDGAIN_CLIENT_ENDPOINTS** - comma separated list of GridGain node endpoints.
    - **GRIDGAIN_CLIENT_DEBUG** - (optional) if *true*, tests will display additional output (default: *false*).
3. Alternatively, instead of the environment variables setting, you can directly specify the values of the corresponding variables in [gridgain_client_path/tests/TestConfig.php](./TestConfig.php) file.
4. Run the tests. 

The below commands include `--teamcity` option to generate additional output for integration with TeamCity. If you don't need this output remove that option.

### Run Functional Tests ###

Call `./vendor/bin/phpunit --teamcity tests` command from `gridgain_client_path` folder.

### Run Examples Executors ###

Call `./vendor/bin/phpunit --teamcity tests/examples/ExecuteExamples.php` command from `gridgain_client_path` folder.

### Run AuthTlsExample Executor ###

It requires running GridGain server with non-default configuration (authentication and TLS switched on).

If the server runs locally:
- setup the server to accept TLS. During the setup use `keystore.jks` and `truststore.jks` certificates from `gridgain_client_path/examples/certs/` folder. Password for the files: `123456`
- switch on the authentication on the server. Use the default username/password.

If the server runs remotely, and/or other certificates are required, and/or non-default username/password is required - see this [instruction](../examples/README.md#additional-setup-for-authtlsexample).

Call `./vendor/bin/phpunit --teamcity tests/examples/ExecuteAuthTlsExample.php` command from `gridgain_client_path` folder.