# testrail-mocha-integration

Another custom mocha reporter for use with javascript framework, [mocha](https://mochajs.org/).

Inspired by [mochawesome](https://github.com/adamgruber/mochawesome) project.

## Installation

### yarn

```Bash
yarn add -D testrail-mocha-reporter
```

## Usage

### Mocha

```bash
mocha test --reporter testrail-mocha-reporter --reporter-options domain=domain.testrail.com,username=test@test.com,password=12345678,...
```

### Possible options

You can choose between three options.

1. send **planId** - then it will fetch all the suites and cases associated with that plan

2. send **runId** - then the results are send to that run with defined ID and the run is not closed
   1. suiteId required

3. send **createRun** - then it will create a new run with defined suite (suiteId) and close it after end of the suite.
   1. runName required
   2. suiteId required

**domain**: *string* domain name of your Testrail instance (e.g. for a hosted instance instance.testrail.net)

**username**: *string* user under which the test run will be created (e.g. jenkins or ci)

**password**: *string* password or API token for user

**projectId**: *number* project number with which the tests are associated

**milestoneId**: *number* (*optional*) milestone number with which the tests are associated

**planId**: *number* (*optional*) planId - if the planId is set then the results are posted to this run. Ii will fetch all the runId's and cases within that plan.

**runId**: *number* (*optional*) runId number which tests are associated.

**createRun**: *boolean* (*required*) if runId is NOT set. It will creates a new run with defined runName.

**suiteId**: *number* (*required*) with the set runId or createRun. Suite number with which the tests are associated

**runName**: *string* (*required*) with the createRun set to true.

**ci**: *string* (*optional*) add to run (createNew must be true) ci build number. Possible options are (`"circle" | "travis | jenkins`)

### Cypress integration

Reporter working well with [Cypress.io](https://www.cypress.io/).

To integrate reporter please read the Cypress [documentation](https://docs.cypress.io/guides/tooling/reporters.html) for adding custom reporters.

### Add reporter to jsou cypress.json

```json
{
  ...,
  "reporter": "testrail-mocha-reporter",
  "reporterOptions": {
    "domain": "domain.testrail.com",
    "username": "test@test.com",
    "password": "your password",
    "projectId": 1,  
    "planId": 1,
    "milestoneId": 1
  },
  ...
}
```

If you are using a `multi-custom-reporter` then you will need to add it like this: 

```json
{
  ...,
  "reporterOptions": {
    "reporterEnabled": "testrail-mocha-reporter,html",
    "testrailMochaReporterReporterOptions": {
      "domain": "domain.testrail.com",
      "username": "test@test.com",
      "password": "your password",
      "projectId": 1,  
      "planId": 1,
      "milestoneId": 1
    }
  },
  ...
}

```

## References

* <https://github.com/adamgruber/mochawesome#readme>
* <http://mochajs.org/#mochaopts>
* <https://github.com/mochajs/mocha/wiki/Third-party-reporters>
* <http://docs.gurock.com/testrail-api2/start>
