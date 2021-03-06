# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## Unreleased

## [1.2.2] - 2020-09-06

### 🐛 Bug Fixes

- Fixed an issue where the `task-overdue` status would disappear if a task above it was checked off.

## [1.2.1] - 2020-09-06

### 🐛 Bug Fixes

- Fixed an issue where subtasks would cause errors with sorting.

## [1.2.0] - 2020-09-05

### ✨ Features

- Subtasks are now nested under their parent if both are included in the filter. If a subtask is captured by a filter, but the parent is not, it will be listed as a top level item. You may need to adjust your priority CSS to accommodate these changes. For example:
    ```diff
    + .todoist-p1 > input[type="checkbox"] {
    - .todoist-p1 input[type="checkbox"] {
        /* This matches against the input element rendered for a priority 1 task. */
    }
    ```
- Tasks now render dates under them by default. This can be toggled in the settings (along with some the accompanying icon). If you choose to use icons, I recommend you _at least_ add the following CSS to your own (tweaking may be required based on your theme):
    ```css
    .task-calendar-icon {
        vertical-align: middle;
        height: 17px;
        width: 17px;
    }
    ```
- Added support for controlling the ordering of the rendered tasks. This can be done by either priority or date, or a combination of them (e.g. - sort by priority, then by date). To use this feature, amend your queries:
    ``````markdown
    ```json
    {
        "name": "My Tasks",
        "filter": "today | overdue",
        "autorefresh": 30,
        "sorting": ["date", "priority"]
    }
    ```
    ``````

### ⚙ Internal

- Ported the plugin to (almost entirely) Typescript.

## [1.1.0] - 2020-08-31

### ✨ Features

- Each rendered task's CSS now contains information about the task's priority. You can use this information to style each priority differently. These classes are `todoist-p1`, `todoist-p2`, `todoist-p3`, and `todoist-p4`. For example: 
    ```css
    .todoist-p1 input[type=checkbox] {
        /* This matches against the input element rendered for a priority 1 task. */
    }
    ```
- When a task is removed or added, it now transitions with a smooth fading effect, rather than immediately being added/removed. This can be turned off in the settings.
- Added support for auto-refreshing queries. This can be set at a global level within the settings tab or overridden for each individual query. For example:
    `````markdown
    ```json
    {
        "name": "My Tasks",
        "filter": "today | overdue",
        "autorefresh": 30
    }
    ```
    `````
- Added a setting tab in the Obsidian setting menu. There are three settings included in this release:
    - "Task fade animation" - controls whether to use the fade animation
    - "Auto-refresh" - controls whether all queries should auto-refresh
    - "Auto-refresh interval" - controls the default interval for auto-refreshing queries

### 🔃 Changes

- The rendered task list now uses the ordering as defined by the Todoist API.

### 🐛 Bug Fixes

- The injected Todoist query components are correctly destroyed when removed from the DOM.

## [1.0.0] - 2020-08-29

This was the initial release of the Obsidian x Todoist plugin. It contained the basic functionality for:

- materializing tasks in an Obsidian note
- allowing you to check tasks off from an Obsidian note