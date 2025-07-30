# 'End to End' Integration tests
Not technically end-to-end, but the idea is that we can compose our services sufficiently to integration test each service in the CI/CD pipeline. Rather than mocking each individual service.

See also: The Quality Engineering chapter writeup - https://www.notion.so/dojo-/NET-Services-Integration-Testing-18bf2b241bff800e8c18eb0693a36351

We decided to follow the settlement approach of creating a different directory structure to distinguish between pre-existing per project 'integration' tests that use mongo mocks etc. It also makes it much easier for developers to unload integration testing projects if they decide they don't want them running constantly. A similar rationale applies for not copying the 'integrations tests under the Common projects' approach from safeguarding.



## Gotchas
- In order to assert the existence of a PubSub message, that particular topic needs registering in the publishing service's `WebApplicationFactory` class.
- Before each test, MongoDB databases, PubSub queues, and API requests can be cleared. Unfortunately the Eventstore database cannot be cleared - bear this in mind when writing tests that rely on the Eventstore (and eg. use random IDs).

## Note on running tests locally
Some tests require running the Dojo Seeder to set up test customers. This has a quirk where tests may fail locally due to authorisation issues. If you encounter this, run the following commands: 
`gcloud auth  configure-docker eu.gcr.io` to ensure that your local docker is authenticated with GCP.
`docker pull eu.gcr.io/firefly-devops-2018/dojo-seeder:latest` to pull the latest Dojo Seeder image.

If you have made a change to the Dojo Seeder, you will need to pull the latest image in order to run this version locally. This is done automatically in the CI/CD pipeline.

## Note on running tests in CI
This should usually work as expected, but due to the differences in the environment you may see unexpected failures.

In the unlikely event that you need to see the logs from the test run on CI, perform the following configuration steps:
Add `tests_verbosity: 'detailed'` to the `build-branch.yaml` workflow file. This will output logs for the tests.
Add `ACTIONS_STEP_DEBUG`:`true` to the repository secrets. This will output additional debug information for the test run, enabling these new logs to appear
