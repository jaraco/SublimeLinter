Linter Settings
===============
Each linter plugin can provide its own settings. SublimeLinter already provides these for every linter:


args
----
Specifies extra arguments to pass to an external binary.

The value may be a string or an array. If it is a string,
it will be parsed as if it were passed on a command line.
For example, these values are equivalent:

.. code-block:: json

    {
        "args": "--foo=bar --bar=7 --no-baz"
    }

    {
        "args": [
            "--foo=bar",
            "--bar=7",
            "--no-baz"
        ]
    }

The default value is an empty array.


disable
-------
Disables the linter.


env
---
Set additional environment variables.

.. code-block:: json

    {
        "env": "{'GEM_HOME': '~/foo/bar'}"
    }


excludes
--------
This setting specifies a list of path patterns to exclude from linting.
If there is only a single pattern, the value may be a string.
Otherwise it must be an array of patterns.

Patterns are matched against a file's **absolute path** with all symlinks/shortcuts resolved.
This means to match a filename, you must match everything in the path before the filename.
For example, to exclude any python files whose name begins with “foo”, you would use this pattern:

.. code-block:: json

    {
        "excludes": "*/foo*.py"
    }

The default value is an empty array.
Untitled views can be ignored with ``<untitled>``,
and you can use ``!`` to negate a pattern.
Note that :ref:`Settings Expansion <settings-expansion>` can be used here as well.


executable
----------

At any time you can manually set the executable a linter should use. This can
be a string or a list.

.. code-block:: json

    {
        "executable": "${folder}/node_modules/bin/eslint",
        "executable": ["py", "-3", "-m", "flake8"],
        "executable": ["nvm", "exec", "8.9", "eslint"]
    }

See :ref:`Settings Expansion <settings-expansion>` for more info on using variables.


python
------

This should point to a python binary on your system. Alternatively
it can be set to a version, in which case we try to find a python
binary on your system matching that version (using PATH).

It then executes ``python -m script_name``
(where script_name is e.g. ``flake8``).


.. _selector:

selector
--------

.. note::

    This takes precedence over the (deprecated) `syntax` property.

This defines if when given linter is activated for specific file types.
It should be a string containing a list of comma separated selectors.

For example, by default yamllint is activated only for YAML files (``source.yaml``)
files. But we also want to activate it for ansible files, which have the
``source.ansible`` scope.

To do that, we can override the selector for this linter:

.. code-block:: json

    {
        "linters": {
            "yamllint":
            {
                "selector": "source.yaml, source.ansible"

            },
        }
    }

To find out what selector to use for given file type, use the
"Tools > Developer > Show Scope Name" menu entry.


working_dir
-----------
This setting specifies the linter working directory.
The value must be a string, corresponding to a valid directory path.

For example (this is also the default):

.. code-block:: json

    {
        "working_dir": "${folder:$file_path}"
    }

Here the linter will get invoked from the ``${folder}`` directory
or the file's directory if it is not contained within a project folder.

See :ref:`Settings Expansion <settings-expansion>` for more info on using variables.
