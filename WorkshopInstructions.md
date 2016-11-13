
# GoCD Workshop Instructions

These are the intructions for the presenter of the GoCD Workshop. 

Navigate to http://localhost:8153/ using your web browser

* [Instructor gives over of GoCD user interface]
  * Main landing page
  * Agents
  * Environments

* We’re going to use the wizard to create our first pipeline. Later in the workshop you’ll see other ways.
  * Create new pipeline (note: it’s not required to use these names but if you don’t you may need to edit code snippets and other settings later)
    * Pipeline Name: Application
    * Pipeline Group: Development

  * [Instructor gives an overview of material options on next page]
    * Material Type: Git
    * URL: /vagrant/application
    * Branch: master

  * [Instructor gives overview of Stage / Job / Task]
    * Stage Name: BuildApplication
    * Job Name: Build
    * Task Type: More…
    * Command: /bin/bash
      * Why bash instead of calling it directly? https://docs.go.cd/16.3.0/faq/environment_variables.html
    * Arguments: (each on own line)
      * -c
      * application/build_application.sh

  * [Instructor gives overview of pipeline editing admin screen
    * Expandable menu showing pipeline / stage / job
    * Must drill into job to see tasks
    * Project Management
    * Materials
    * Environment Variables
    * Parameters

  * Navigate to home page and unpause Application pipeline

  * [Instructor talks about polling intervals in java agents]
    * Click on stage bar to drill into Pipeline

  * [Instructor gives overview of page]
    * Job Listing
    * Tabs
    * Stage History

  * Click on job name to drill into job [Instructor gives overview of page]
    * Console
    * Other tabs

  * Click ‘ADMIN’ in top menu ,select ‘Pipelines’. 

  * Navigate back to the admin screen for the Application pipeline

  * Click on Stages tab, then Add new stage
    * Stage Name: UnitTest
    * JobName: UnitTest
    * TaskType: More…
    * Command: /bin/bash
    * Arguments: (one per line)
      * -c
      * unit_test/unit_test.sh

  * Click ‘Add new stage’
    * Stage Name: Package
    * JobName: MakePackage
    * TaskType: More…
    * Command: /bin/bash
    * Arguments: (one per line)
      * -c
      * application/package_application.sh

  * On the tree on the left, click the arrow next to ‘Package’ to expand
  * Click the ‘MakePassage’ job
  * Click on ‘Artifacts’ tab [Instructor gives overview of page]
    * Source: installer.tgz
    * Destination: <blank>
    * Type: Build Artifact

  * Navigate back to home page and run pipeline
  * Drill into Package job and look at the Artifacts tab
    * [instructor use slides to teach about linear vs parallel pipelines]
    * [instructor use slides to teach about configuration in external repo]

  * Navigate to ‘Admin’ -> ‘Config XML’
    * Type or paste code snippet below the <server /> line - then save

```
  <config-repos>
    <config-repo plugin="yaml.config.plugin">
      <git url="/vagrant/gocd-configuration" />
    </config-repo>
  </config-repos>
```

  * In the gocd-configuration directory that you cloned during setup, rename verification.gocd.yaml.start to verification.gocd.yaml
  * Commit the file, and push it to the origin repo ``` git commit -am 'some comment'; git push ```


  * Navigate to the home page (Note: if you called your first pipeline something other than ‘Application; you’re going to get an error)
  * Click ‘Admin’ -> ‘Pipelines’
    * Notice that the new pipeline shows up here, but all of the options are greyed out
    * Notice that ‘delete’ is now greyed out for ‘Application’

  * [Instructor use the Application pipeline to introduce the concept of ‘Fetch Artifact’]

  * [Instructor show the documentation for GoCD YAML plugin] - http://gofor.cd/gocd-yaml-plugin

  * Look at the yaml for the Application pipeline (whitespace matters in yaml)
      ```
       - fetch:
           pipeline: Application
           stage: Package
           job: MakePackage
           is_file: yes
           source: installer.tgz
      ```

    * Note: Why did we tar it when GoCD would have zipped it for us? Zip doesn’t maintain permissions and we have an executable script in our installer.

  * Add a task to execute the installer
    * /bin/bash -c installer/deploy_application.sh FunctionalTesting
    * Commit and push the code changes

  * Navigate to GoCD homepage, drill into console output from the job to show the artifact being fetched. Note the versioning in the path to the artifact.

(note: instructions will become increasingly vague on purpose. This is to encourage learning how to navigate the documentation and learn by example)

  * Create a new stage called FunctionalTest which executes functional_test/functional_test.sh on 3 agents simultaneously 
  * Commit and push the changes to git

  * Navigate to the GoCD homepage and execute the pipeline
    * Drill into the new stage and note the number of jobs run
    * Drill into the console for each job and note the output from the shell script

  * Create a UAT pipeline that uses the same deployment script and has a manual second stage for approval. (hint, there's nothing special about an "approval" stage, it usually just does something like "echo approved" and is marked as manual)
  * Drill into UAT and manually execute the second stage

  * Create a new pipeline called DeployStaging in a new pipeline group call Operations. Use both FunctionalTesting and UserAcceptance as materials. Fetch the installer from the Application pipeline without using it as a material.
