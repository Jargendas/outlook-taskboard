# Outlook Taskboard

Outlook Taskboard is a Kanban board style view for Outlook Tasks.

*The __Fork__ sections at the end of this README list the changes made by the respective forks since the original version by evrenvarol.*

There are 2 ways to use the taskboard:

  1. As an Outlook folder Home Page
  2. Directly from Internet Explorer
  
![Outlook Taskboard](http://evrenvarol.github.io/outlook-taskboard/img/outlook-taskboard.png)

# Features

### Move tasks between task lanes
![Moving Tasks](http://evrenvarol.github.io/outlook-taskboard/img/task-drag.gif)

### Filter tasks
![Filtering](http://evrenvarol.github.io/outlook-taskboard/img/task-filter.gif)

### Show task categories
![Category footer coloring](https://user-images.githubusercontent.com/9609820/30276617-b5c02bb0-9705-11e7-8981-66021ad66f53.png)

### View task status
![Task status](https://user-images.githubusercontent.com/9609820/55799992-f0237b80-5ad2-11e9-90a6-5ea9d9cf9c89.png)

### Display task information
![Task information](https://user-images.githubusercontent.com/9609820/55242483-9d79d200-523d-11e9-90ab-a98713cbe9a6.PNG)

### Print status reports
![Status report](https://user-images.githubusercontent.com/9609820/55243657-f2b6e300-523f-11e9-969c-dbdebf350f57.png)

### Checklists in the task excerpt
You can add a checklist to your task, which will be shown in the excerpt in the taskboard like this:

![Checklist](https://user-images.githubusercontent.com/1270412/126763301-8b464632-b8f5-458f-a8a6-9be753761070.PNG)

To add a checkbox, add a `[]/[ ]` or `[x]/[X]` for an unchecked or a checked box, respectively, at the beginning of the line, e.g. for the example above:

```
[ ] Subtask 1
[X] Subtask 2
[ ] Subtask 3
```

When checking or unchecking a box, the task's description will be updated accordingly.

### Supported platforms 
Tested with Outlook 2013 and 2016 running on Windows 7/8.1/10.

The taskboard can also be opened in Internet Explorer. Due to limitations with ActiveX controls, only Internet Explorer 9/10 and 11 are supported.

## Basic Setup

First, download the [latest release zip file](https://github.com/maltehi/outlook-taskboard/archive/master.zip) and extract it to a folder in your local hard drive or [clone this repository](https://github.com/maltehi/outlook-taskboard.git) using Git.

The further setup depends on how you want to use the taskboard. While the solution based on Outlook Folder Home Page is conveniently integrated with Outlook, new Outlook versions only support Home Pages for the root folder of each account, if at all. Additionally, performance and compatibility e.g. with high-resolution displays are suboptimal. The Internet Explorer solution handles these better. Both solutions can also be used in parallel.

### For Outlook Home page:

  * Right-click the your Outlook account's __root folder__. This should be named like the account (e.g. your email address) and be visible in Outlook's __Email view__ or __Folder view__ (not in the Tasks view). Click on **Properties** (last entry in the context menu). Select the *Home Page* tab in the Properties dialog box.

    *The feature to define home pages not only on the root folder, but on any deliberate folder was supported once, but then __removed__ from Outlook at some point. Depending on your Outlook version, and potentially your Exchange Server and Group Policy settings, this might still be enabled.*

  * In the *Address box*, browse to the folder you have just extracted the Taskboard files and select the **kanban.html** file.

  * Click to select the *Show home page by default for this folder* check box and then click **OK**.

      ![Folder Home Page Offline Warning](http://evrenvarol.github.io/outlook-taskboard/img/folder-home-page-offline-warning.png)

      *If you receive above warning, simply close it and close the Properties window using the 'X' icon.*

  * Now the taskboard should open in the main window when **clicking on the root folder**.

  * **Troubleshooting : *Home Page tab is not visible***

    In newer versions of Outlook the *Home Page* tab is usually not visible in Outlook folder properties. This feature was disabled by default to limit security vulnerabilities. To re-enable this you need to add a new `DWORD value` in your windows registry settings.

    For this please open the `Registry Editor` by
     * pressing `Windows + R`,
     * typing `regedit` and
     * clicking `OK`.

    Inside the Registry Editor
     * open `Computer\HKEY_CURRENT_USER\Software\Microsoft\Office\<VERSION>\Outlook\Security`,
     * right click to add a new `DWORD (32-bit) value`,
     * set the name `EnableRoamingFolderHomepages` and
     * the value `1`.

    ![Enable Home Tab](img/EnableHomePageTab.png)

    After this please close the Registry Editor and also close and re-open Outlook. The Home Page Tab should be available in the properties window of the folder now:

    ![Enable Home Tab](img/HomePageTab.png)

    For more information please also have a look at : https://support.microsoft.com/en-us/office/outlook-home-page-feature-is-missing-in-folder-properties-d207edb7-aa02-46c5-b608-5d9dbed9bd04

### For Internet Explorer:

  * Open Internet Explorer and go to *Tools > Internet Options > Security tab*. Select the **Local Intranet Zone** and click on the **Custom Level** button. Ensure the "Initialize and script ActiveX controls not marked as safe for scripting" option is set to **Enabled**

  ![IE Local Intranet Zone Setting](http://evrenvarol.github.io/outlook-taskboard/img/ie-localintranet-activexscript-enable.png)

  * Open the page **kanban.html** in Internet Explorer.
  
    *Pro tip: Set kanban.html as your Internet Explorer homepage. (What else are you going to use IE for anyway...)*

    Note that any other browsers than Internet Explorer are __not supported__ (not even Edge), as IE's ActiveX features are required for access to Outlook data.

## Advanced Setup

To access the configuration file, open the taskboard and click on the settings symbol in the top right next to the text box.

This is an example for the configuration of the "Next" lane:

```javascript
...
  "NEXT_FOLDER": {
    "ACTIVE": true, 
    "NAME": "",
    "TITLE": "NEXT",
    "LIMIT": 20,
    "SORT": "-priority,duedate,startdate,categoryNames",
    "RESTRICT": "",
    "DISPLAY_PROPERTIES": {
      "OWNER": false,
      "PERCENT": true, 
      "TOTALWORK": true
    },
...
```

### Task Lane Folder Names and Titles

* Folder names for each lane can be customised by changing the `Name` value. This is the folder that the tasks for the respective lane are stored in. It is recommended to set the same folder for all lanes and let the taskboard sort the tasks by status. An empty string stands for the default Outlook task folder.

  *(Do __not__ change the folder identifier - i.e. NEXT_FOLDER)*

* The `Title` value represents the title showing on the task lane.

### Task Lane Limits

![Task Lane Limits](http://evrenvarol.github.io/outlook-taskboard/img/tasklane-limits.png)

* The `Limit` value can be adapted to set limits for each task lane.

* Only InProgress, Next, and Waiting lanes accept limit settings. BackLog and Completed lanes do not support limits.

* Setting the `Limit` to `0` removes the limit.

### Task Lane Sort Order

* The `Sort` value can be updated to change the sorting criteria and their order.

* It is also possible to add multiple order criteria such as: `"SORT": "-priority,duedate,startdate,categoryNames",`

### Task Template

![Task Template](http://evrenvarol.github.io/outlook-taskboard/img/task-template.png)

When a task created using the **Add** button on task lanes, a new task created with a default template.

```javascript
    // Default task template
    "TASK_TEMPLATE": '\r\n\r\n### TODO:\r\n\r\n\r\n\r\n### STATUS:\r\n\r\n\r\n\r\n### ISSUES:\r\n\r\n\r\n\r\n### REFERENCE:\r\n\r\n\r\n\r\n'
```

This template can be customised by changing the `TASK_TEMPLATE` setting.

### Task Note Excerpt

If there are some notes entered in the task, only first 200 chars are visible by default configuration.

```javascript
"TASKNOTE_EXCERPT": 200,
```

The `TASKNOTE_EXCERPT` value can be updated to change the number of characters shown in the task board view.

*Note: If the default task template used to create the task, only the first part of the task notes are visible. (until first the '###'' section).*

### More options

Open the help text by clicking on the '?' button in the taskboard to get a description of available configuration parameters.

## Multi-project setup

To work with several independent Kanban Board configurations, change the following line in ```kanban.html```:

```<body ng-controller="taskboardController" ng-init="init('')">```

Instead of an empty string, pass a unique identifier string to the init function (e.g. ```ng-init="init('Test')```). This will cause the Kanban Board to use a config name appended
with the identifier string. In this way it is possible to create a set of several kanban.html files that each operate on independent configurations.
Each of the configurations can contain different folder paths for storage of the task objects, so that different projects can be addressed.

# Version/fork history

## Fork 1: [BillyMcSkintos](https://github.com/BillyMcSkintos/outlook-taskboard)

Credit for this fork goes entirely to @evrenvarol. I have made a few simple changes to suit my needs:
1. Removed Focus Column
2. Added CSS to color columns
3. Added Owner
4. Added Task %
5. Columns are no-longer drag and drop. Tasks move from column to column with the Outlook task status.
5.a. Must add and use a category of !Next to move a task to the appropriate column.

## Fork 2: janvv - Outlook Taskboard aka **JanBan** *(Deleted)*

I found the original Kanban board implemented by Evren Varol. I looked at the forks and liked the
changes by BillyMcSkintos, using the task status instead of folders. But he lost the drag&drop
feature.

So I decided to take my own fork and added a bunch of features, and added some options to the
configuration file.

My changes:

1. Added colours to task categories
2. Tasks folder is now the Backlog folder
3. Use new folder 'Kanban' for all the current work: Next, InProgress, Waiting and Done
4. Removed Add button at InProgress and Waiting lanes. Tasks can only be added to Backlog and Next
5. Drag and drop now sets the new status
6. Introduced date format in config file
7. Drag & Drop now also works properly when filter is active
8. Use another icon for archiving of completed icons, for better difference from the edit icon
9. Removed editing option for completed tasks
10. Display Completion Date for completed tasks instead of Due Date
11. Implemented filter on private / non-private tasks (button top right)
12. If one of the task folders in the config does not exist, then it is created
13. Optional saving of filter state via CONFIG file
14. Optional use of privacy filter via CONFIG file
15. Added configuration for what to do with completed tasks (Nothing, Archive, Hide, Delete)
16. Added "Filter on start date" configuration option to Backlog folder/column to hide tasks with start date in the future
17. Added configuration options to show/hide 'Owner' and '% complete' per column
18. Added configuration option to enable/disable auto refresh of the taskboard
19. Added configuration option to show/hide sections in the report
20. Added configuration option to make task lanes active or inactive
21. Added help screen
22. Added configuration screen (journal item)
23. Tested with recurring tasks. Works perfectly :-)
24. Added new config option: AUTO_TASK_START. When true, then tasks that have start date today or earlier will be moved to the NEXT lane automatically.
25. Added new config option: Display Total Work hours for task item

## Fork 3: [maltehi](https://github.com/maltehi/outlook-taskboard)

1. Removed lane coloring.
2. Activated category-based footer coloring by default (see image below).
3. Apply display filters on status reports, too (optional).
4. Tasks are sorted into lanes by their status (as in BillyMcSkintos' fork). Drag & Drop between lanes is enabled and alters the task status.
5. Having the tasks for all lanes in a common folder, e.g. the main Tasks folder, is possible (and recommended). Archive folder is still separate.
6. Colored footings according to task category.
7. Multi-project support.
8. Many small changes...
