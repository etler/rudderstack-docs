---
description: >-
  Step-by-step guide on the different repositories that you need to submit a PR
  to, when creating a new integration.
---

# How to Submit a Destination Integration Pull Request

When contributing to our open-source code by creating your own RudderStack integration, this guide will help you ensure that you have completed the required steps. It will also help you make sure that your integration code will fit with our pre-existing code base without any issues.

For your integration to be reviewed and considered, there are three repositories that you must contribute to:

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Repository</b>
      </th>
      <th style="text-align:left"><b>Link</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>RudderStack Transformer
          <br />
        </p>
        <p><b><code>rudder-transformer</code></b>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/rudderlabs/rudder-transformer"><b>GitHub Repo</b></a>&lt;b&gt;&lt;/b&gt;</p>
      </td>
      <td style="text-align:left">Responsible for transforming the standard RudderStack payload from the
        source into the required payload format needed for a given downstream destination.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>RudderStack Config Generator</p>
        <p></p>
        <p><b><code>config-generator</code></b>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p><a href="https://github.com/rudderlabs/config-generator"><b>GitHub Repo</b></a>&lt;b&gt;&lt;/b&gt;</p>
      </td>
      <td style="text-align:left">Responsible for gathering the required configuration details that will
        be specific to each user, i.e. API keys, event mappings, metrics, etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>RudderStack Documentation</p>
        <p></p>
        <p><b><code>rudderstack-docs</code></b>
        </p>
      </td>
      <td style="text-align:left">
        <p></p>
        <p>&lt;b&gt;&lt;/b&gt;<a href="https://github.com/rudderlabs/rudderstack-docs"><b>GitHub Repo</b></a>&lt;b&gt;&lt;/b&gt;</p>
      </td>
      <td style="text-align:left">Includes the relevant instructions on setting up, configuring, and using
        the integration you have created.</td>
    </tr>
  </tbody>
</table>

## Creating a Pull Request

For each of the three repositories listed above, it is necessary to fork each one and clone them to your local machine. Ensure that you are updating your local repositories regularly to limit any merge conflicts. It is important to create a branch with a descriptive name and ensure that your commit messages are clear. 

When you are ready to create a pull request, follow the steps below:

1. Push your changes to your remote origin.
2. Then, go to the RudderStack's repository and click on **New pull request**.
3. Click the link the says **Compare across forks**.
4. Change the **Head Repository** to be your forked repository and change **Compare** to be the associated branch name.
5. Make any necessary title or descriptions changes. Add any tags such as WIP \(work in progress\), etc. to help add clarity on what is needed.
6. Finally, click on **Create pull request**.

{% hint style="success" %}
Repeat the steps above for each of the repositories - **`rudder-transformer`**, **`config-generator`**, and **`rudderstack-docs`**`.`
{% endhint %}

## RudderStack Contributor Agreement

{% hint style="warning" %}
To contribute to this project, we need you to sign to [**Contributor License Agreement \(“CLA”\)**](https://rudderlabs.wufoo.com/forms/rudderlabs-contributor-license-agreement) for the first commit you make. By agreeing to the [**CLA**](https://rudderlabs.wufoo.com/forms/rudderlabs-contributor-license-agreement), ****we can add you to list of approved contributors and review the changes proposed by you.
{% endhint %}

## RudderStack Transformer

[**GitHub Repository Link**](https://github.com/rudderlabs/rudder-transformer)\*\*\*\*

The `rudder-transformer` repository is responsible for transforming __the source payload into the required payload for the downstream destination. This is where the bulk of the code will need to be written. Therefore, the following should be considered when contributing to this repository.

* There is a big emphasis on formatting the code to match current project structure. If there are any questions or issues regarding this, reach out to our team; see [**Contact Us**](https://docs.rudderstack.com/user-guides/how-to-guides/how-to-submit-an-integration-pull-request#contact-us) section below.
* Include any `eslint` logic in the top of the file.
* Include test cases that cover around 80% code coverage.

#### Necessary Files to Contribute To ####
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>File</b>
      </th>
      <th style="text-align:left"><b>Path</b>
      </th>
      <th style="text-align:left"><b>Responsibility</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Create <code>transform.js</code></p>
      </td>
      <td style="text-align:left">
        <p><code>v0/&lt;destination_name&gt;/transform.js</code></p>
      </td>
      <td style="text-align:left">This file will hold all the logic that will tranform a payload from RudderStack's standard format to the destination's acceptable format.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;destination_name&gt;.test.js</code></p>
      </td>
      <td style="text-align:left">
        <p><code>__tests__/&lt;destination_name&gt;.test.js</code></p>
      </td>
      <td style="text-align:left">This file will administer the test for the transformation. Please follow the format from an existing destination.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;destination_name&gt;_input.json</code></p>
      </td>
      <td style="text-align:left">
        <p><code>__tests__/data/&lt;destination_name&gt;_input.json</code></p>
      </td>
      <td style="text-align:left">This <code>JSON</code> file will hold all of the dummy testing payloads that will be inserted into the transformation when the test file is ran. Please follow the format from an existing destination.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;destination_name&gt;_output.json</code></p>
      </td>
      <td style="text-align:left">
        <p><code>__tests__/data/&lt;destination_name&gt;_output.json</code></p>
      </td>
      <td style="text-align:left">This <code>JSON</code> file will hold all of the expected outcomes after the input payloads were transformed by the transformation when the test file is ran. Please follow the format from an existing destination.</td>
    </tr>
  </tbody>
</table>

## RudderStack Config Generator

[**GitHub Repository Link**](https://github.com/rudderlabs/config-generator)\*\*\*\*

The `config-generator` repository allows the user to upload the necessary settings needed for configuring the integration. Follow the pre-existing structure to the best of your ability and please reach out to us via the [**Contact Us**](https://docs.rudderstack.com/user-guides/how-to-guides/how-to-submit-an-integration-pull-request#contact-us) ****section with any questions or concerns. 

Please note the following when creating the config generator:

* Your documentation should be in the `.md` format
* Include proper `regex` validation rules for all of the text input fields.
* The icon file must be an `svg`.

#### Necessary Files to Contribute To ####
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>File</b>
      </th>
      <th style="text-align:left"><b>Path</b>
      </th>
      <th style="text-align:left"><b>Responsibility</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;DESTINATION_NAME&gt;.json</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/components/destination/destinationList/&lt;DESTINATION_NAME&gt;.json</code></p>
      </td>
      <td style="text-align:left">This file will contain a <code>JSON</code> object that will hold all of the fields for the necessary settings that your integration will need to operate properly.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Edit <code>dst.ts</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/components/destination/destinationList/dst.ts</code></p>
      </td>
      <td style="text-align:left">This small edit will help allow the destination to appear in the destination catalogue.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Edit <code>destinations.json</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/stores/destinations.json</code></p>
      </td>
      <td style="text-align:left">Including the necessary data here will allow the destination to appear in the destination catalogue (follow pre-existing template).</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;DESTINATION_NAME&gt;.md</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/components/destinationsCatalogue/destinationsConfigure/&lt;DESTINATION_NAME&gt;.md</code></p>
      </td>
      <td style="text-align:left">This markdown file will act as a quick high level overview of what this destination is and how to find more information for it.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Edit <code>index.tsx</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/components/destinationsCatalogue/destinationsConfigure/index.tsx</code></p>
      </td>
      <td style="text-align:left">This small edit will allow the text in the markdown file to be viewed by the client.</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Edit <code>destinationIcon.tsx</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/components/icons/destinationIcon.tsx</code></p>
      </td>
      <td style="text-align:left">There are two necessary edits to be made to this file. Add an import for you icon's <code>svg</code> file (follow the pre-existing template). Then below, add another <code>case</code> to the <code>switch</code> statement (follow the pre-existing template).</td>
    </tr>
        <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;destination_name&gt;.svg</code></p>
      </td>
      <td style="text-align:left">
        <p><code>src/icons/svg/&lt;destination_name&gt;.svg</code></p>
      </td>
      <td style="text-align:left">Include the actual icon <code>svg</code> file here.</td>
    </tr>
  </tbody>
</table>

## RudderStack Documentation

[**GitHub Repository Link**](https://github.com/rudderlabs/rudderstack-docs)\*\*\*\*

The `rudderstack-docs` repository houses all the relevant documentation for instructing the users on using the integration you have created. Remember to be thorough with your documentation to avoid confusion and any errors. Although we will review the documentation and get in touch with you in case of any clarification, it will certainly be very helpful to ensure clear, concise steps on setting up, configuring, and using your integration.

{% hint style="warning" %}
Please do not include screenshots. We will include them after merging the changes.
{% endhint %}

#### Necessary Files to Contribute To ####
<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>File</b>
      </th>
      <th style="text-align:left"><b>Path</b>
      </th>
      <th style="text-align:left"><b>Responsibility</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Create <code>&lt;destination_name&gt;.md</code></p>
      </td>
      <td style="text-align:left">
        <p><code>destinations/&lt;category_folder&gt;/&lt;destination_name&gt;.md</code></p>
      </td>
      <td style="text-align:left">This markdown file will be added to the RudderStack Docs. Inform the user how to properly use this integration. Follow the pre-existing structure found with other integrations.</td>
    </tr>
  </tbody>
</table>

## Contact Us

For more information on any of the sections in this guide, feel free to [**contact us**](mailto:%20docs@rudderstack.com) ****or start a conversation on our [**Slack**](https://resources.rudderstack.com/join-rudderstack-slack) channel.

