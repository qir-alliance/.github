# Setting up a Contributor License Agreement

Software in open source projects is generally provided for other people to use
under a certain license. A [Contributor License Agreement
(CLA)](https://en.wikipedia.org/wiki/Contributor_License_Agreement) covers legal
matters such as who retains intellectual property rights for contributions to
the project.

For repositories under the QIR Alliance, we recommend setting up a bot that
presents a CLA to new contributors, and ask them to accept it, before the
contribution can be merged into the repository. The QIR Alliance provides a
workflow template that provides a basic setup leveraging the [CLA
Assistant](https://github.com/contributor-assistant/github-action).

To add a CLA bot to your repository, click on `Actions` > `New workflow`. Under
the section `By QIR Alliance` you should see a workflow called "QIR Alliance CLA
Bot Configuration"; click on its `Configure` button. This will open the
`cla_assistant.yml` file that contains the workflow definition, which will be
checked in under `.github/workflows/` once you commit the change. Click on the
`Start commit` button and select the option to create a pull request to add the
workflow to your repository. Please note that the bot will only start to work
once the change has been merged to the default branch of your repository.

For the bot to work correctly, a <!-- markdown-link-check-disable-next-line -->
[secret](https://docs.github.com/en/actions/security-guides/encrypted-secrets)
needs to be added to the repository to give the necessary permissions to the
bot. Please reach out to [qiralliance@mail.com](mailto:qiralliance@mail.com) to
set that up. After it has been added, you should see a repository secret called
`CLA_BOT_ACCESS_TOKEN` when you click on `Settings` > `Secrets` > `Actions`.

If you/your organization does not have a specific CLA you would like to use, you
can use the standard agreement used by the QIR Alliance available
[here](https://github.com/qir-alliance/.github/blob/main/Contributor_License_Agreement.md).
In this case, you can go ahead and merge the workflow into your repository
without further changes to the PR. If you would like to customize the CLA that a
contributor agrees to, go to the created pull request and add a `CLA.md` file in
the repository root that contains a suitable agreement. Update the value of
`path-to-document` in the `cla_assistant.yml` file to point to that file before
merging the PR.

Once the PR to add the workflow has been merged, you should see a check called
"Check that the CLA has been acknowledged" the first time you create a new PR on
your repository. This check will fail initially, and you should see a comment on
your PR that gives instructions for how to accept the CLA. Confirm that the
added check passes after you follow these instructions.

After you have confirmed that everything is working correctly, we recommend to
add the check to the status checks that are required to pass before merging in
your branch protection rules.
