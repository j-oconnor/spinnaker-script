# Spinnaker Script Stage Configuration.

Right now, the Spinnaker script stage consists of a jenkins script that calls a remote git repository. This directory helps you set up the script stage in Spinnaker.

## Script Repository

You will need to set up a git repository to keep track of your files. This directory contains a sample directory of scripts.

The groovy directory contains an example of how to interact with Spinnaker pipelines to retrieve a property from a stage.

*J's Note:  Make sure any shell scripts are set with chmod +x permissions*

## Jenkins Job Import

The directory contains a jenkins job definition that you can import via:

`curl -X POST 'http://NEW_JENKINS/createItem?name=JOBNAME' -H "Content-Type: application/xml" --data-binary @scriptJobConfig.xml`

*J's Note:  If may need to add a --user "user:pass" depending on your Jenkins Global security settings*

Once you have imported the script, modify the job to point to the script repository.

*J's Note:  I also had to modify the restriction to only run the job on "Spinnaker"*

## Orca Configuration

To enable the script stage, you need to set the following properties in orca's orca.yml

```
script:
   master: [igor alias for your jenkins master]
   job: SPINNAKER-TASKS
```

*J's Note:  I used an orca-local.yml in /opt/spinnaker/config with just this one block in it.  You can find the igor alias in your spinnaker-local.yml (assuming you have already configured one).  Job should match the JOBNAME you set in the curl to import the job to Jenkins.
