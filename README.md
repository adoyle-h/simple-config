# Simple-Config

A simple, zero-dependence library helps you make a configuration for your library or module.

It helps you define a set of default parameters(in `default.js`), and extend them(in `local.js` or others files) recursively.

It is highly recommended to use [lorenwest/node-config](https://github.com/lorenwest/node-config) when you are willing to build an application rather than a library. It is a pretty awesome library and provides many useful features.


## Installation

`npm install --save simple-config`

## Quick Start

1. mkdir a folder.

    ```bash
    mkdir config
    ```

2. edit the default configuration via `vim config/default.js`.

    ```js
    {
        a: {
            b: {
                c: 'hello',
                c2: 'world',
                c3: 1,
            },
            d: [1, 2, 3],
        },
        e: false,
        f: null,
        g: 1,
    }
    ```

3. edit the default configuration via `vim config/local.js`.

    ```js
    {
        a: {
            b: {
                c: 'bye',
                c3: 0,
            },
            d: [],
        },
        e: true,
        g: undefined,
        h: null,
    }
    ```

4. edit the index file to indicate the default and local files via `vim config/index.js`.

    ```js
    var Config = require('simple-config');
    // the default.js and local.js are relative path to __dirname
    var config = Config.load(__dirname, ['default.js', 'local.js']);
    ```

    and `config` will be:

    ```js
    {
        a: {
            b: {
                c: 'bye',
                c2: 'world',
                c3: 0,
            },
            d: [],
        },
        e: true,
        f: null,
        g: 1,
        h: null,
    }
    ```

## Reserved Words

the following configuration names cannot be used as config key:

- get


## API

### load(fromPath, relativePaths)

Load your config files.

You could invoke the `load` function many times. Each returned config is independent and not affected by each other.

 * @param  {String} `fromPath`  A absolute path to sub-config folder.
 * @param  {Array<String>} `relativePaths`  The paths of config files, which relative to `fromPath`. The latter item will overwrite the former recursively.
 * @return {Object}  The final config object.


## Copyright and License

Copyright 2015 ADoyle

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and limitations under the License.

See the NOTICE file distributed with this work for additional information regarding copyright ownership.