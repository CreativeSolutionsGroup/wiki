# Google Forms ➡️ Basecamp

## Overview

This project started out as a simple idea that we could use the "onsubmit" action on a Google form to trigger an update in Basecamp that would create a card detailing what needed to be done. Originally Westin had the idea for a few forms that the team was manually transferring information from Forms to Basecamp for, but the project became more complex than that in the end.

We now have the capability to create both todo list items and cards on the card table, and will soon have a feature to allow the connector to assign people to a card by default.

## Creating Connectors

### Setting up the environment

Thankfully the Google Apps Script environment has everything that you would need for making a device like this.
There aren't too many things you have to do to set up the new project. The most important thing is making sure that you have edit access to the form.
Without this edit access, you will not be able to create a script that will run on form submissions.

The next thing to do is to link the library that we created to facilitate easier creation of these connectors.

![Add library button](./images/add_cloudflare_library.png)

Once the dialog opens and you see the text box, enter `1klv2AvLhl7gGeBTJjItWbnLeKS5gRcg1jWXEpmchs27gKkBxV1gvlFaG` and press add.

![Add library text box](./images/add_library_text_box.png)

The next step is to rename the function to a more informative name, such as `onSubmit` or `formSubmit`

Once the function is renamed, head over to the triggers tab, signified by the alarm clock in the left menu bar.

Click on the add trigger button in the bottom right corner.

![Add trigger button](./images/add_trigger_button.png)

A dialog similar to this one will pop up, prompting you to change some things to make sure that the function runs properly.

Change the function to run to be your newly created function and set the event type to be on form submit.

![Add trigger dialog](./images/trigger_details_dialog.png)

Press save and then you have your project all set up. You can now start to code the actual connector.

### Coding the connector

Head back to the code page and then copy and paste this code into the editor. This is a template for how to set up the connector.

```js
// The location to send the information
const postUrl = "https://forms-basecamp-link.creativesolutions.workers.dev/";
// List IDs for multiple destination forms
const locations = {
  SELECTOR_TEXT_1: "1234567890",
  SELECTOR_TEXT_2: "2345678901",
};

function onSubmit() {
  // Grabs the last form submission and all the answers from it
  const formItems = CloudflareLibrary.getFormItems(FormApp.getActiveForm());
  // Log for debugging
  console.log(formItems);
  // Choose where to send the form data
  const requestType = formItems["SECTION_SELECTOR"];
  // Content will be the HTML that we send to the Cloudflare connector
  let content = `
      <h3>Requester: ${formItems["NAME_FIELD"]}</h3>
      <h4>Cell phone: ${formItems["CELL_FIELD"]}</h4>
      <h4>Email: ${formItems["EMAIL_FIELD"]}</h4>
  `;

  // We may have different fields for the different request types
  switch (requestType) {
    // This should be the same as the first item in the locations object up above
    case "SELECTOR_TEXT_1":
      // We append any new content to the end of the content string
      content += `
        <h3>ITEM_1:</h3>
        <p>${formItems["ITEM_1"]}</p>
      `;
      break;
    // Same as above, except the second item in locations
    case "SELECTOR_TEXT_2":
      content += `
        <h3>ITEM_2</h3>
        <p>${formItems["ITEM_2"]}</p>
      `;
      break;
    default:
      // We didn't find a matching request type
      console.error("No request type selected");
      return;
  }

  const payload = {
    // The URL of the connector
    postUrl,
    // Type of item to create
    // Should be either list or card_table
    type: "list",
    // The project ID found in the URL after buckets e.g. https://3.basecamp.com/WORKSPACE_NUMBERS/buckets/PROJECT_ID
    projectId: "98765432",
    // The sub location ID which is found at the very end of the URL
    subId: locations[requestType], // or a constant value
    title: "TITLE_GOES_HERE",
    // The HTML formatted content string
    content,
    // What to set the due date to
    due_on: "", // defaults to a week in the future
  };

  // Actually send the data now
  CloudflareLibrary.sendDataToCloudflare(payload);
}
```

Take note that the formItems may have spaces after them, which need to be accounted for in the object.

This is the template for a multiple location todo list script, but can be easily modified for any other needs such as card tables or single destination forms.

Full HTML is supported so you can style using CSS and use any HTML tags that you want.

## See also

[Worker Documentation](./worker.md)