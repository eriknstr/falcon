## Contributing

Hi, thanks for your interest in the project! We welcome pull requests from developers of all skill levels. To get started, simply fork the master branch on GitHub to your personal account and then clone the fork into your development environment.

Kurt Griffiths (kgriffs) is the creator and current maintainer of the Falcon framework, along with a group of talented and stylish volunteers. Please don't hesitate to reach out if you have any questions, or just need a little help getting started. You can find us on IRC in #falconframework on Freenode.

Before submitting a pull request, please ensure you have added or updated tests as appropriate, and that all existing tests still pass with your changes on both Python 2 and Python 3. Please also ensure that your coding style follows PEP 8 and doesn't cause pyflakes to complain.

You can check all this by running the following from within the falcon project directory (requires Python 2.7 and Python 3.5 to be installed on your system):

```bash
$ tox -e py27,py35,pep8
```

You may also use Python 3.3 or 3.4 if you don't have 3.5 installed on your system. This is just a quick sanity check to verify that your patch works across both Python 2 and Python 3.

### Running tests against Jython

In addition to the tests run with tox against CPython, Cython, and PyPy, Travis runs tests against Jython 2.7 outside of tox. If you need to run these tests locally, do the following:
* Install JDK 7 or better
* run `travis_scripts/install_jython2.7.sh` -- this will install jython at `~/jython`
* Install testing requirements `~/jython/bin/pip install -r tools/test-requires`
    * May need to set `export JYTHON_HOME=~/jython` first
* Run tests `~/jython/bin/nosetests`

Note: coverage does not support Jython, so the coverage tests will fail.

### Test coverage

Pull requests must maintain 100% test coverage of all code branches. This helps ensure the quality of the Falcon framework. To check coverage before submitting a pull request:

```bash
$ tox -e py26,py27,py34 && tools/combine_coverage.sh
```

It is necessary to combine test coverage from all three of these environments in order to account for branches in the code that are only taken for a given Python version.

The `combine_coverage.sh` script generates an HTML coverage report that can be viewed by simply opening `.coverage_html/index.html` in a browser. This can be helpful in tracking down specific lines or branches that are missing coverage.

### Documentation

To check documentation changes (including docstrings), before submitting a PR, ensure the tox job
builds the documentation correctly:

```bash
$ tox -e docs

# OS X
$ open doc/_build/html/index.html

# Gnome
$ gnome-open doc/_build/html/index.html

# Generic X Windows
$ xdg-open doc/_build/html/index.html
```

### Code style rules

* Docstrings are required for classes, attributes, methods, and functions.
* Docstrings should utilize the [napolean style][docstrings] in order to make them read well, regardless of whether they are viewed through `help()` or on [Read the Docs][rtd].
* Please try to be consistent with the way existing docstrings are formatted. In particular, note the use of single vs. double backticks as follows:
    * Double backticks
        * Inline code
        * Variables
        * Types
        * Decorators
    * Single backticks
        * Methods
        * Params
        * Attributes
* Format non-trivial comments using your GitHub nick and one of these prefixes:
    * TODO(riker): Damage report!
    * NOTE(riker): Well, that's certainly good to know.
    * PERF(riker): Travel time to the nearest starbase?
    * APPSEC(riker): In all trust, there is the possibility for betrayal.
* When catching exceptions, name the variable `ex`.
* Use whitespace to separate logical blocks of code and to improve readability.
* No single-character variable names except for trivial indexes when looping,
or in mathematical expressions implementing well-known formulas.
* Heavily document code that is especially complex and/or clever.
* When in doubt, optimize for readability.

### Commit Message Format

Falcon's commit message format uses [AngularJS's style guide][ajs], reproduced here for convenience, with some minor edits for clarity.

Each commit message consists of a **header**, a **body** and a **footer**. The header has a special format that includes a **type**, a **scope** and a **subject**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```

No line may exceed 100 characters. This makes it easier to read the message on GitHub as well as in various git tools.

#####  Type
Must be one of the following:

* **feat**: A new feature
* **fix**: A bug fix
* **docs**: Documentation only changes
* **style**: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
* **refactor**: A code change that neither fixes a bug or adds a feature
* **perf**: A code change that improves performance
* **test**: Adding missing tests
* **chore**: Changes to the build process or auxiliary tools and libraries such as documentation generation

##### Scope
The scope could be anything specifying place of the commit change. For example: `$location`, `$browser`, `$compile`, `$rootScope`, `ngHref`, `ngClick`, `ngView`, etc...

##### Subject
The subject contains succinct description of the change:

* use the imperative, present tense: "change" not "changed" nor "changes"
* don't capitalize first letter
* no dot (.) at the end

##### Body
Just as in the **subject**, use the imperative, present tense: "change" not "changed" nor "changes"The body should include the motivation for the change and contrast this with previous behavior.

##### Footer
The footer should contain any information about **Breaking Changes** and is also the place to reference GitHub issues that this commit **Closes**.

[ajs]: https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#commit
[docstrings]: http://sphinxcontrib-napoleon.readthedocs.org/en/latest/example_google.html#example-google-style-python-docstrings
[goog-style]: http://google-styleguide.googlecode.com/svn/trunk/pyguide.html#Comments
[rtd]: http://falcon.readthedocs.org
