# Testing

Prefect embraces tests!

## Writing tests

Prefect's tests are stored in the top-level `tests` directory. In general, the test directory layout mimics the library layout: a test at `tests/utilities/test_collections.py` is expected to test `prefect/utilities/collections.py`.

Prefect's tests are organized as submodules, meaning each directory has an `__init__.py` file. This means that module names can be safely reused for tests. If you create a new directory, be sure to put an (empty) `__init__.py` in it to ensure it gets picked up during test discovery.

Please remember that the purpose of writing tests is not only to show what your code is expected to do, but also to make sure it doesn't inadvertently start doing something else! We'd prefer over-complete tests to too few tests, and a PR that adds more lines of test code than library code is a good PR.

Prefect has a few fixtures available for testing all available executors; see `conftest.py` for details.

## Running tests

Prefect uses `pytest` for unit testing. To run tests, run `pytest` from the root Prefect directory:

```bash
cd prefect
pytest
```

Prefect has a few flags for modifying pytest's behavior. Passing `--skip-formatting` will skip the `black` and `mypy` tests. Passing `--airflow` will run a series of Prefect/Airflow integration tests that can take a long time (and are not run unless this flag is invoked).

## CI

In CI, Prefect's unit tests are run against Python 3.5, 3.6, and 3.7. Much as we love `f-strings`, Prefect code must support all versions. A common pitfall is writing tests that implicitly depend on Python 3.6's implicitly-ordered dictionaries and sets; these tests can fail non-deterministically in Python 3.5.

Though Prefect's unit tests include tests for black and mypy (see the [style guide](style.md)), a separate "formatting" CI job is also run. Since formatting errors are common in PRs, we have found this to be a useful early-warning during development.

## Documentation

Prefect's API reference documentation is unit tested! If you don't describe an argument of any function, or use improperly formatted docstrings, you will get an error. For more details on docstrings, see the [documentation guide](documentation.md).
