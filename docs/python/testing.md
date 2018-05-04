# Testing with Python

## Resources
* [PyTest](https://docs.pytest.org/en/latest/)
* [Tavern](https://taverntesting.github.io/) - API testing


## Tavern
* Uses a YAML file for test setup.
* Talks directly to the API
* Can use pytest to run the test.
### Notes
1. `pipenv install --dev tavern[pytest]`
1. Create YAML test file in *tests* directory.
    * *test_server.tavern.yaml* - all test should be *test_{name}.tavern.yaml*
1. Run `pytest` in top directory
* Notes
    * Can create *common.yaml* file with shared parameters
    * Be sure to include it in every individual test
