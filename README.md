# Google Workspace Automation

This repository contains a collection of Google Apps Scripts designed to automate and enhance various functionalities within Google Workspace. The scripts provide custom solutions for tasks in Google Sheets, Docs, Slides, and more, aiming to increase productivity and streamline workflows.

## Getting Started

To use these scripts, follow these general steps:

1. Open the Google Workspace product (e.g., Google Sheets) where you want to use the script.
2. Click on "Extensions" -> "Apps Script".
3. In the Apps Script editor, delete any existing code and replace it with the script you want to use.
4. Click on the disk icon or select "File" -> "Save" to save your script.
5. Close the Apps Script Editor and refresh your Google Workspace product page. You should now see the "Automation Tools" menu in the toolbar.

## Scripts

### Lock File Script

This script adds a function to the "Automation Tools" menu in Google Sheets. The function "Lock this file" locks the current file, making it read-only.

To use this script, follow the general instructions above. Then:

6. Click on "Services" -> "+ Add a service", then add "Drive API".
7. Click on "Deploy" -> "New deployment", then select "Web app" and deploy the script. You may need to give permissions to the script to access your Google Drive.

After refreshing your Google Sheets page, you should see the "Automation Tools" menu. Click on it and select "Lock this file" to lock the current file.

The script can be found in the repository under the filename `lock_file_script.js`.

Here's the script:

```javascript
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  var menu = ui.getMenu('Automation Tools');
  if (!menu) {
    ui.createMenu('Automation Tools')
      .addItem('Lock this file', 'lockFile')
      .addToUi();
  } else {
    menu.addItem('Lock this file', 'lockFile');
  }
}

function lockFile() {
  var fileId = SpreadsheetApp.getActiveSpreadsheet().getId();
  var update = {
    contentRestrictions: [
      {
        readOnly: true,
        reason: 'Finalized contract.'
      }
    ]
  };
  Drive.Files.update(update, fileId);
}
```

## Contributing

Contributions are welcome! If you have a script you'd like to add or an improvement to an existing script, feel free to create a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
