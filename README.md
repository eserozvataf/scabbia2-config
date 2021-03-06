# Scabbia2 Config Component

[This component](https://github.com/eserozvataf/scabbia2-config) is a configuration compiler which supports binding multiple configuration files.

[![Build Status](https://travis-ci.org/eserozvataf/scabbia2-config.png?branch=master)](https://travis-ci.org/eserozvataf/scabbia2-config)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/eserozvataf/scabbia2-config/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/eserozvataf/scabbia2-config/?branch=master)
[![Total Downloads](https://poser.pugx.org/eserozvataf/scabbia2-config/downloads.png)](https://packagist.org/packages/eserozvataf/scabbia2-config)
[![Latest Stable Version](https://poser.pugx.org/eserozvataf/scabbia2-config/v/stable)](https://packagist.org/packages/eserozvataf/scabbia2-config)
[![Latest Unstable Version](https://poser.pugx.org/eserozvataf/scabbia2-config/v/unstable)](https://packagist.org/packages/eserozvataf/scabbia2-config)
[![Documentation Status](https://readthedocs.org/projects/scabbia2-documentation/badge/?version=latest)](https://readthedocs.org/projects/scabbia2-documentation)

## Usage

### Merging multiple configurations

```php
use Scabbia\Config\ConfigCollection;

$confs = new ConfigCollection();

// add a yaml-parsed configuration
$yaml = new \Scabbia\Yaml\Parser();
$confs->add($yaml->parse(file_get_contents('common.yml')));

// ...and/or add a json file
$confs->add(json_decode(file_get_contents('production.json')));

// ...and/or add a configuration value manually
$confs->add([
    'env' => 'development'
]);

// output the result
$config = $confs->save();
print_r($config);
```

### Overriding an existing configuration item

```php
use Scabbia\Config\ConfigCollection;

$confs = new ConfigCollection();

$confs->add([
    'env' => 'production'
]);

// in second config you can override a value with 'important' flag
$confs->add([
    'env|important' => 'development'
]);

// output the result
$config = $confs->save();
echo $config['env'];
```

### Constructing a list in separate configurations

```php
use Scabbia\Config\ConfigCollection;

$confs = new ConfigCollection();

$confs->add([
    'items|list' => [
        'first',
        'second'
    ]
]);

// in second config you can override a value with 'important' flag
$confs->add([
    'items|list' => [
        'third'
    ]
]);

// output the result
$config = $confs->save();
print_r($config['items']);
```

### Flatten configuration value keys

```php
use Scabbia\Config\ConfigCollection;

$confs = new ConfigCollection();

$confs->add([
    'database|flat' => [
        'mongo' => [
            'username' => 'scabbia2',
            'password' => 'testing'
        ]
    ]
]);

// output the result
$config = $confs->save();
echo $config['database/mongo/username'];
echo $config['database/mongo/password'];
```

## Links
- [List of All Scabbia2 Components](https://github.com/eserozvataf/scabbia2)
- [Documentation](https://readthedocs.org/projects/scabbia2-documentation)
- [Twitter](https://twitter.com/eserozvataf)
- [Contributor List](contributors.md)
- [License Information](LICENSE)


## Contributing
It is publicly open for any contribution. Bugfixes, new features and extra modules are welcome. All contributions should be filed on the [eserozvataf/scabbia2-config](https://github.com/eserozvataf/scabbia2-config) repository.

* To contribute to code: Fork the repo, push your changes to your fork, and submit a pull request.
* To report a bug: If something does not work, please report it using GitHub issues.
* To support: [![Donate](https://img.shields.io/gratipay/eserozvataf.svg)](https://gratipay.com/eserozvataf/)
