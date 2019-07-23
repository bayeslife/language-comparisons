# Learning Python as a Javascript Developer

Style
- Google Python Style Guide: https://google.github.io/styleguide/pyguide.html 
- PEP-008 Style Guide for Python Code: https://www.python.org/dev/peps/pep-0008/ 
- PEP-257 Doc String Conventions: https://www.python.org/dev/peps/pep-0257/ 
- PEP-020 The Zen of Python: https://www.python.org/dev/peps/pep-0020/ 
- Hitchhiker’s Guide to Python: https://docs.python-guide.org/writing/style/
- Documentation: https://realpython.com/documenting-python-code/ 

Tooling
- Linting: https://www.pylint.org/
- Formatting: https://github.com/python/black
- Testing: https://docs.pytest.org/en/latest/
- Dependency Management: https://poetry.eustace.io/

## Comments
- javascript: C style comments
```
// This is a single line comment
/**
* THis is a multiple line comment
**/
```
- python
```
# This is a comment
```

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

## Destructuring
- javascript
```
let foo = {
    test1: 1
    test2: 2
}
let {test2,test1} = foo
```

```
let foo = [1,2]
let [test1,test2] = foo
```
- python
```
foo = (1,2)
(test1,test2)=foo
print(test1)
```
```
>>> foo = [1,2]
>>> [head,*tail]= foo
>>> print(head)
1
>>> print(tail)
[2]
```


## Linting
- javascript: eslint and prettier are 2 options here.  Prettier is more about getting a standard automatically
```
"scripts": {
    "archetype:lint": "eslint -c node_modules/short-interval-control-archetype-lib-component/eslintrc.json --fix src test --ext .js",
```
Can be achieved through an archetype.
Code is fixed automatically on each save.
The eslintrc.json has the standard linting rules to apply

- python : pylint
```
pylint 
```
??? How to set linting rules
??? How to fix code automatically


## Archytype
The ability to define build tools in a library.
- javascript : Common pattern in large frameworks, possible through [builder](https://www.npmjs.com/package/builder)
- python : ???

