# Testing with Python

## Resources
* [Python Testing](http://pythontesting.net/)
* [PyTest](https://docs.pytest.org/en/latest/)
* [Tavern](https://taverntesting.github.io/) - API testing

## Tavern

### Notes
1. `pipenv install --dev tavern[pytest]`
1. Create YAML test file in **tests** directory.
    * **test_server.tavern.yaml** - all test should be **test_{name}.tavern.yaml**
* Pytest
  * Run `pytest` in top directory - will find **tests/** directory
  * Run selected tests - `pytest -k fake` to run all tests with **fake** in the name.
  * Minimize debug info - `pytest --tb=short`
  * Run one test - `pytest tests\test_register_service.py::test_random_code_generator`
  * Show print output in pytest - `pytest -s tests\test`
  * Continuous watching changes
    * `pipenv install --dev pytest-testmon pytest-watch` 
    * [Pytest Watch](https://github.com/joeyespo/pytest-watch)
    * [Pytest Testmon](http://testmon.org/)
* Tavern
  * Uses a YAML file for test setup.
  * Talks directly to the API
  * Can use pytest to run the test.
  * Can create **common.yaml** file with shared parameters
    * Be sure to include it in every individual test - every test is individual
