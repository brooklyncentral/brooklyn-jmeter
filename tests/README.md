To run these tests first add the necessary entities to Brooklyn's catalog:

    br catalog add ../catalog
    br catalog add includes.bom
    br catalog add jmeter.tests.bom

Then deploy `jmeter-app-test`:

    location: <of your choosing>
    services:
    - type: jmeter-app-test

The location should provision a machine that uses a CentOS or RHEL distribution.
