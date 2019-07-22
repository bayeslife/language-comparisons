# Learning Python as a Javascript Developer

## Package Structure
- Python has a hierarchical package structure  package.subpackage.subpackage
```
from pkg import module //this imports just module
module.fun()


import pkg.module //this imports both pkg and module
pkg.module.function()

?? can we import just a single function from a module
?? can we hide functions in a module
```
- Javascript has a single @namespace/module structure
```
let p = require('@namespace/module') //common js
import module from '@namespace/module' //es6
```

## Installing modules
- npm or yarn install - installs modules in node_modules folder and preserves all version dependencies all the way down the dependency tree.
- pip install (or conda install)
Installing python modules from pip seems to dowload source and compile code while from conda retrieves binary.
Both npm and yarn install source (almost exclusively)

Python dependencies install out of the module in ~/.local/lib/python so the dependencies seem to be shared
Node dependencies are install for each dependency recursively.
Comment: Node allows multiple versions of any library to run so that there are no conflicts when 2 modules use different versions of a 3rd module.

## Printing to stdout
- javascript: console.log('something)
- python: print ('something')

## Defining a module
- javascript : 2 main approaches CommonJS and ES6
    - CommonJs: define file and define module.exports = <something to export>
    ```
        //file p/f.js

        module.exports = {
            fun: function(){ console.log('test')}
        }
    ```
    ```
        //file p2.js

        let p2 = require('p/f.js')
        p2.fun()
    ```
    - ES6: define file and markup all variables/functions to export with export keyword.
    ```
        //file p/f.js

        export function fun(){ consolel.log('test')}
    ```
    ```
        //file p2.js

        import { fun} from 'p/f.js'
        fun()
    ```
- python
    - Define a function (fun) in  file (f) in some pkg (p)  then import into another file
    ```
    #file p/f.py

    def fun:
        print('test')
    ```
    ```
    # file p2.py

    from p import f
    f.fun()
    ```

## Running Tests

- javascript : mocha, jest, ava, riteway - all unit test frameworks which provides ways to express sets of unit tests, with descriptions and expectations.
```
npm install riteway

//file f.test.js
import { describe } from 'riteway'

describe('Library', async (assert) => {
      assert({
        given: 'the library',
        should: 'Should do something',
        actual: 'True',
        expected: 'True'
      })
    }
)

//run
riteway
```
- python : pytest is one framework
```
#install pytest
pytest
```

## Debug Logging
- javascript : Provides a debug module which support selective logging
```
//some module mod.js
let debug = require('debug')('someContext')
debug('This is some debug')
```
```
node mod.js //will not log anything
DEBUG=someContext node mod.js //will log
```
- python : Has the logging package (which apparently designed after log4j)
```
//some module mod.py
import logging

logger = logging.getLogger('Mod')
logging.basicConfig(level=logging.DEBUG)
logger.debug('This is some logging')
print('This is some print')
```
```
python3 mod.py
```

## Destructing
