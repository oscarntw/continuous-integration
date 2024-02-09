<header>

<!__
  <<< Author notes: Course header >>>
  Include a 1280×640 image, course title in sentence case, and a concise description in emphasis.
  In your repository settings: enable template repository, add your 1280×640 social image, auto delete head branches.
  Add your open source license, GitHub uses MIT license.
__>

# Test with Actions

_Create workflows that enable you to use Continuous Integration (CI) for your projects._

</header>

<!__
  <<< Author notes: Step 2 >>>
__>

## Step 2: Fix the test

_Great job adding the templated workflow! :tada:_

Adding that file to this branch is enough for GitHub Actions to begin running CI on your repository.

When a GitHub Actions workflow is running, you should see some checks in progress, like the screenshot below.

<img alt="checks in progress in a merge box" src=https://user_images.githubusercontent.com/16547949/66080348_ecc5f580_e533_11e9_909e_c213b08790eb.png width=400 />

You can follow along as GitHub Actions runs your job by going to the __Actions__ tab or by clicking "Details" in the merge box below.

When the tests finish, you'll see a red X :x: or a green check mark :heavy_check_mark: in the merge box. At that point, you can access the logs for the build job and its associated steps.

*By looking at the logs, can you identify which tests failed?* To find it, go to one of the failed builds and scroll through the log. Look for a section that lists all the unit tests. We're looking for the name of the test with an "x".

<img alt="screenshot of a sample build log with the names of the tests blurred out" src=https://user_images.githubusercontent.com/16547949/65922013_e740a200_e3b1_11e9_8151_faf52c30201e.png width=400 />

If the checks don't appear or if the checks are stuck in progress, there's a few things you can do to try and trigger them:

_ Refresh the page, it's possible the workflow ran and the page just hasn't been updated with that change.
_ Try making a commit on this branch. Our workflow is triggered with a `push` event, and committing to this branch will result in a new `push`.
_ Edit the workflow file on GitHub and ensure there are no red lines indicating a syntax problem.

### :keyboard: Activity: Fix the test

1. Update the contents in the `ci` branch to get the test to pass. You need to look at the logs to see what caused the test to fail.
1. __Commit changes__.
=======
## Step 3: Upload test reports

_The workflow has finished running! :sparkles:_

So what do we do when we need the work product of one job in another? We can use the built_in [artifact storage](https://docs.github.com/actions/advanced_guides/storing_workflow_data_as_artifacts) to save artifacts created from one job to be used in another job within the same workflow.

To upload artifacts to the artifact storage, we can use an action built by GitHub: [`actions/upload_artifacts`](https://github.com/actions/upload_artifact).

### :keyboard: Activity: Upload test reports

1. Edit your workflow file.
1. Update the `Run markdown lint` step in your `build` job to use `vfile_reporter_json` and output the results to `remark_lint_report.json`.
1. Add a step to your `build` job that uses the `upload_artifact` action. This step should upload the `remark_lint_report.json` file generated by the updated `Run markdown lint` step.
1. Your new `build` should look like this:

   ```yml
   build:
     runs_on: ubuntu_latest
     steps:
       _ uses: actions/checkout@v4

       _ name: Run markdown lint
         run: |
           npm install remark_cli remark_preset_lint_consistent vfile_reporter_json
           npx remark . __use remark_preset_lint_consistent __report vfile_reporter_json 2> remark_lint_report.json

       _ uses: actions/upload_artifact@v3
         with:
           name: remark_lint_report
           path: remark_lint_report.json
   ```

1. Commit your change to this branch.

Get help: [Post in our discussion board](https://github.com/orgs/skills/discussions/categories/test_with_actions) &bull; [Review the GitHub status page](https://www.githubstatus.com/)

&copy; 2023 GitHub &bull; [Code of Conduct](https://www.contributor_covenant.org/version/2/1/code_of_conduct/code_of_conduct.md) &bull; [MIT License](https://gh.io/mit)

</footer>
