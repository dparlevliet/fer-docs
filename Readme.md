Fer
===

You are now Fer's bitch. Bow before her or DIE.


Getting started
---------------

Great section to have, but WAY too early.


How it works
------------

Great section to have, but WAY too early.

Modules
-------

Great section to have, but WAY too early.

### Package Managers

#### Apt

Control settings for apt-get

``` javascript
{
  apt: {
    run_at: 801,
    always_update: false,
    always_upgrade: false,
    deb_options: [
      "mariadb-server-5.5 mysql-server/root_password password asdf",
    ],
    packages: [
      'mariadb-server-5.5',
    ],
    purge: [
      'mariadb-server-5.1',
    ],
  }
}
```

### File Installer

Install files options overview

``` javascript
{
  file_install: {
    run_at: 500,
    '/tmp/test.txt': {
      group: 'root',
      owner: 'root',
      mode: '0740',
      source: 'fer://test_file.txt',
      text => 'Done.',
      modify => [
        {
          search: /<[^>]+>/g,
          replace: '[\\1]'
        }
      ],
      command: function() {
        return fer.do(function(deferred) {
          fer.command('ls -al').then(function() {
            deferred.resolve();
          });
        });
      },
    },
}
```

Real example #1

``` javascript
{
  file_install: {
    '/tmp/test_source.txt': {
      source: 'fer://test_source.txt',
      modify: function() {
        return [
          {
            search: /test/g,
            replace: 'NYPD'
          }
        ];
      },
    },
  },
}
```

Real example #2

``` javascript
{
  file_install: {
    '/tmp/fer_test.tmp': {
      text: 'test test test',
      modify: [
        {
          search: /test/g,
          replace: 'NYPD'
        }
      ],
    },
  }
}
```

Real example #3

``` javascript
{
  file_install: {
    '/tmp/suzie.tmp': {
      source: 'https://raw.githubusercontent.com/dparlevliet/suzie/master/install.sh',
      command: 'bash /tmp/suzie.tmp',
    }
  }
}
```

Real example #4

``` javascript
{
  file_install: {
    '/tmp/fer_test.tmp': {
      text: 'test test test',
      mode: '0540',
      modify: [
        {
          search: /test/g,
          replace: 'NYPD'
        }
      ],
    },
    '/tmp/suzie.tmp': {
      source: 'https://raw.githubusercontent.com/dparlevliet/suzie/master/install.sh',
      mode: '0440',
      command: 'bash /tmp/suzie.tmp',
    }
  }
}
```