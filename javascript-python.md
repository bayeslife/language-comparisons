# How To comparision of Python and Javascript

## Versions
nodejs is up to version 12 now. Differences between versions is not significant.
python2.7 seems a default on ubuntu...any reason.  Seem like major differences between 2 and 3.

## Comments
- javascript: C style comments
```
// This is a single line comment
```
- python
```
# This is a comment
```

## Package Structure
- Javascript has a single @namespace/module structure
```
let p = require('@namespace/module') //common js
import module from '@namespace/module' //es6
```

- Python has a hierarchical package structure  package.subpackage.subpackage
```
from pkg import module #this imports just module
module.fun()

import pkg.module #this imports both pkg and module
pkg.module.function()

?? can we import just a single function from a module
?? can we hide functions in a module
```

## Installing modules
- javascript
- installs modules in node_modules folder and preserves all version dependencies all the way down the dependency tree.
```
npm install
or
yarn install
``` 
- python
```
pip install
python3 -m pip install --index-url https://test.pypi.org/simple/ --no-deps <pkg>

conda install
```
Installing python modules from pip seems to dowload source and compiled code while from conda retrieves binary.

Both npm and yarn install source (except when the module contains binary/platform specific code)

Python dependencies install out of the module in ~/.local/lib/python so the dependencies seem to be shared
Node dependencies are install for each dependency recursively.
Comment: Node allows multiple versions of any library to run so that there are no conflicts when 2 modules use different versions of a 3rd module.

## Clean Dependencies
- javascript
```
npm clean-install (aka npm ci)
```
- python
Not sure if there is a standard way to remote the build/dist directories after a build.

## Public Repositories
- javascript
npmjs.com - This is effectively a single public repository

There is no 'test' repository.
It is a single flat namespace but anyone can purchase an '@namespace' to which only they are allowed to publish to.

- python
https://pypi.org/ - The main python repository?
https://test.pypi.org - A test python repository you can publish to initially.

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

- javascript : mocha, jest, ava, riteway - all unit test frameworks which provides ways to express sets of unit tests, with descriptions and expectations.  Some frameworks try to cater more for setup and teardown support, some are better at storing mocks or input/outputs to be used for subsequent tests.
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
```
import pytest

import src.hello

#make sure to start function name with test
def test_sum():
    assert src.hello.sum(1, 2) == 3
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

## Dependency Management
- javascript: provided through npm and yarn
```
npm init
npm install <package>

yarn init
yarn add <package>
```
All packages are installing locally to the module by default.  There is a global install option as well which is sometimes used but mainly discouraged.
Produces a package.lock.json or yarn.lock.json file which provides determinism.

- python : poetry
```
poetry init
poetry add <package>
```
??? is this different from pip in that it records dependencies for a particular project (as package.lock.json does)

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


## Archetype
The ability to define build tools in a library.
- javascript : Common pattern in large frameworks, possible through [builder](https://www.npmjs.com/package/builder)
- python : ???


## Building a library
- javascript
With javascript there is no requirement to 'build' source code.  The `npm publish` command simply zips up the package.json and all source code which then is registered as a zip file.  The package.json file contains the meta data about what is the main file (usually index.js) and what is the source.

- python
```
poetry build
```

## Publish a library
- javascript -
It is easy to publish modules to the npm (public) registry. You need an account and then get an NPM_TOKEN which you install into the npmrc file

```
echo '//registry.npmjs.org/:_authToken='$NPM_TOKEN > ~/.npmrc

npm publish
```
- python
using [setuptools](https://setuptools.readthedocs.io/en/latest/setuptools.html#developer-s-guide)
define a setup.py file
```
import setuptools

with open("README.md", "r") as fh:
    long_description = fh.read()

setuptools.setup(
    name="pylib1-ptomq1",
    version="0.1.0",
    author="ptomq1",
    author_email="ptomlinson@quartileone.com",
    description="First public library",
    long_description=long_description,
    long_description_content_type="text/markdown",
    url="https://github.com/bayeslife/pylib1_ptomq1",
    packages=setuptools.find_packages(),
    classifiers=[
        "Programming Language :: Python :: 3",
        "License :: OSI Approved :: MIT License",
        "Operating System :: OS Independent",
    ],
)
```
Then build the distribution package and publish using twine
```
 python3 setup.py sdist bdist_wheel #builds the dist
 python3 -m twine upload --repository-url https://test.pypi.org/legacy/ dist/* # uploads to the test pypi repository
```
# alternative
poetry publish
```

## Creating a Docker image


## How to run multiple versions at the same time
- javascript: use [node version managaement](https://github.com/nvm-sh/nvm)
- python: installs python2,python3.6,...
```
pyenv
````
??? not sure how separate the python configurations are


## Project Generator

-javascript
There is a project generator [here](https://gitlab.com/q1-packages/generator)
```
//After cloninig the repo, install it globally
npm install -g

//Then run it with
generate
```

- python
