# Part-c.-314768268
January 2023 (version 1.75)

Show release notes after an update

Update 1.75.1: The update addresses these issues.

Welcome to the January 2023 release of Visual Studio Code. There are many updates in this version that we hope you'll like, some of the key highlights include:

Profiles - Create and share profiles to configure extensions, settings, shortcuts, and more.
VS Marketplace signing - Published extensions now code signed by default.
Accessibility improvements - Terminal screen reader mode, new keyboard shortcuts.
Easier multi-view resizing - Drag layout corners to resize multiple views at once.
Tree view search history - Quickly rerun previous searches in tree views.
Better Terminal link detection - Detect links containing spaces, brackets, line and column formats.
New Git commands - Stash staged changes and delete remote tags from within VS Code.
Dark+ and Light+ V2 themes - Try the experimental color themes and let us know what you think.
Jupyter Notebook topics - Using notebooks on the web, how to manage Jupyter kernels.
AI Tools in VS Code - Learn about AI-powered completions with GitHub Copilot.
If you'd like to read these release notes online, go to Updates on code.visualstudio.com.

Insiders: Want to try new features as soon as possible? You can download the nightly Insiders build and try the latest updates as soon as they are available.

Housekeeping
In previous release notes, the team reported on our housekeeping efforts and we wanted to do the same here.

As we had announced back in November 2022, we used December for housekeeping our GitHub issues and pull requests (see our issue cleanup guide). Across all of our repositories, we achieved a net reduction of 3637 open issues and pull requests. Unsurprisingly, the lion share of the reduction happened in our top 5 repositories: microsoft/vscode (2520), microsoft/vscode-jupyter (374), microsoft/vscode-remote-release (278), microsoft/vscode-python (220), and microsoft/vscode-pull-request-github (160).

Accessibility
Diff navigation improvements
Go to Next/Previous Change now has audio cues to indicate if a line was inserted, deleted, or modified. Additionally, the line of the change is selected so that it can read by a screen reader.

Terminal Accessibility Mode
The Terminal: Enter Accessibility Mode (Shift+Tab) command allows screen readers to navigate through the terminal buffer via keyboard.

Terminal accessibility help
Similar to the Show Accessibility Help command in the editor, the Terminal: Show Terminal Accessibility Help (Alt+F1) command provides important information for screen reader users.

Terminal accessibility help is presented on top of the terminal

Workspace Trust editor shortcuts
To improve the keyboard accessibility of the Workspace Trust editor, which can be opened via Workspaces: Manage Workspace Trust, you can now toggle trust for the current workspace with the keyboard using Ctrl/Cmd+Enter or for the parent folder with Ctrl/Cmd+Shift+Enter.

Workspace Trust Editor showing the trust buttons with their keyboard shortcuts

Improved keyboard navigation on Settings editor indicators
For settings with multiple indicators, such as a "Modified Elsewhere" indicator and a "Default value changed" indicator, the left and right arrow keys are now used to navigate between the indicators. This change allows users to tab out of the indicators with a single press of the Tab key.

Profiles
We are happy to announce that the Profiles feature is now generally available in VS Code. A Profile can include extensions, settings, keyboard shortcuts, UI state, tasks, and user snippets. You can customize VS Code for different development scenarios like data science, documentation writing, or for multiple programming languages like Python or Java. If you have different VS Code setups based on workflow such as "Work" or "Demo", you can also save those as different profiles. You can open multiple workspaces (folders) with different profiles applied simultaneously.

The following image demonstrates a folder opened with a Work profile that is customized for a work setup.

Folder opened in Work profile

You can also export and import profiles to share them with your colleagues, friends, or students to help them get started with VS Code.

The following video demonstrates how to export a profile using a GitHub gist in order to share it with someone. Users that receive the profile link can preview the shared profile in VS Code for the Web and import it to their local VS Code instance.

Export and share profile

Note: Profiles currently do not work in remote scenarios like GitHub Codespaces, but we are working on enabling this. You can track progress in issue #165247.

Workbench
Improved multi-view resizing support
You can now resize multiple views at the same time by dragging the corners of the views.

Improved grid layout
If an editor is minimized, the grid will now preserve that state when resizing the entire workbench or sidebars. In the short video below, the width of the minimized editor on the right remains constant as the overall editor region is expanded.

Restore defaults from the Customize Layout command
When working the custom Customize Layout command either via triggering the command or using the layout controls in the custom title bar, you can Restore Defaults using the revert arrow button in the top right of the layout control.

Customize layout control showing the new Restore Defaults button

Manage panel alignment from panel
You can now adjust panel alignment directly from the panel context menu just like panel position.

Panel context menu showing the panel alignment submenu

Simplified Preferences menu
We have simplified the Preferences menu for your global settings and organized the options into a more logical order and grouping.

Global settings menu showing expanded Themes flyout

Tree Find history
The Find control inside tree views now supports history navigation. You can use the Up/Down arrow keys to navigate through the history of your previous searches.

Tree Find contiguous matching
The tree view Find control now supports contiguous matching along with the existing "fuzzy" matching. In the video below, initially searching for "src" has matches such as "resource". When "fuzzy" matching is disabled via the Fuzzy Match toggle button, only text with the contiguous text "src" is highlighted.

List scroll by page
A new setting, workbench.list.scrollByPage, lets you configure whether the list should scroll by page when clicking directly on the scroll bar.

List type navigation mode
The new workbench.list.typeNavigationMode setting allows you to configure the type navigation mode for lists. By default (setting value automatic), navigation occurs in list and trees as you type. If you prefer to only enable navigation at certain times, you can set typeNavigationMode to trigger and the list will only go into type navigation mode once the list.triggerTypeNavigation command is run.

The command list.triggerTypeNavigation does not have a keybinding by default but you can add your own. For example, if you'd like to enter type navigation mode after you press the / key, you can add a keybinding such as:

{
  "key": "/",
  "command": "list.toggleKeyboardNavigation",
  "when": "listFocus"
}

New confirmation to open large files
To prevent accidental opening of very large files, especially in remote environments where there might be an actual cost due to network transfer, a confirmation is shown before opening the file. The limit can be modified via the new workbench.editorLargeFileConfirmation setting and has different defaults based on opening local files versus remote files.

Large file confirmation shown for a 2GB package.json file

File watcher supports files.watcherExclude glob patterns
The files.watcherExclude setting supports glob patterns for powerful exclusion rules of the file watcher. However, glob patterns had not been supported natively by the library used for file watching. In this milestone, we contributed support for glob patterns for exclusions for more efficient resource usage, especially on Linux.

For Linux, refer to this FAQ entry for more information if you see file watching issues.

Keyboard Shortcuts editor improvements
Show extensions contributing keybindings
The Keyboard Shortcuts editor now shows the extension that contributes a keybinding in the Source column. You can select the extension name to open the extension's details page.

Source column shows extensions contributing keybindings

You can also search for any keybindings contributed by an extension using the Extension Keyboard Shortcuts action available in the extension context menu.

Extension keyboard shortcuts action

Show context key suggestions for when clause property
The keyboard shortcuts editor now shows context key suggestions for the when property. You can use the Ctrl+Space shortcut to trigger suggestions.

Context key suggestions for when clause property

Search for keybindings with chords
Keyboard shortcuts editor now supports searching for keybindings with chords. For example, "Ctrl+K" will also show all keybindings with Ctrl+K as the first chord.

Setting to configure shell environment resolution timeout
A new setting application.shellEnvironmentResolutionTimeout (macOS and Linux only) allows you to increase the timeout for resolving the shell environment when that is required. By default, VS Code will wait up to 10 seconds for the environment to resolve, but in certain cases with more complex shell setups that may not be enough time.

Refer to this FAQ entry for more information on how VS Code resolves shell environments.

New VSCODE_RESOLVING_ENVIRONMENT environment variable
When VS Code is resolving the user shell environment, it will now set a new environment variable VSCODE_RESOLVING_ENVIRONMENT to 1. This is useful for user scripts (for example, in .bashrc) that need to know whether they are being run in the context of resolving the shell environment.

Easier opt-out of release notes after update
You can now opt out of reading the release notes after every update, directly from the release notes editor. This will reflect and update the update.showReleaseNotes setting.

There's a checkbox inside the release notes editor that allows the user to opt out reading release notes after every update

Editor
Suggest selection mode
There is a new setting (editor.suggest.selectionMode) that allows you to configure if suggestions are selected automatically as you type or via trigger characters.

The default is to always select the best suggestion so that hitting Enter or Tab inserts it. If you prefer to not have a suggestion selected, set the value to never, whenQuickSuggestion, or whenTriggerCharacter. When using those setting values, suggestions will still show but are not selected automatically and you can use the arrow keys to select one.

Note that this setting only applies to automatic suggestions, not to suggestions that are shown when you explicitly trigger them via Ctrl+Space.

Code Action list is now scrollable
Some extensions generate long lists of Code Actions. If there is not space to render all Code Actions, you can now scroll through the list:

Color decorators limit
The number of color decorators that are shown in the editor is limited to 500. This is to prevent performance issues when opening a file containing a large number of colors. This limit can now be configured via the editor.colorDecoratorsLimit setting.

CSS decorators shown in the editor

Editor Find Go To Match
The new Go To Match... command allows you to jump to a specific match in a file based on the count when the Find control is open. This is useful when you have a large number of matches and want to jump to a specific one.

Go To Match... command

Redesigned inline suggestions toolbar
In this milestone, we redesigned the inline suggestions toolbar to make it more compact and easier to use. It features buttons to quickly cycle through alternative suggestions and to accept a suggestion fully or word by word.

In the video below, the user reviews both suggestions provided by GitHub Copilot, triggered on the comment prompt, and then incrementally accepts first console and the next word for console.log.

The toolbar features buttons to quickly cycle through alternative suggestions and to accept a suggestion fully or word by word.

The setting "editor.inlineSuggest.showToolbar": "always" can be used to always show the toolbar when inline suggestions are available.

We also added default keybindings for accepting/undoing a suggestion word by word (Ctrl+Arrow Left/Arrow Right).

Terminal
New default keybindings
The following default keybindings have been added to improve discoverability of advanced terminal features:

Open Detected Link - Ctrl/Cmd+Shift+O
The Open Detected Link command (Ctrl+Shift+O) is the keyboard-accessible way of opening terminal links. The command opens a Quick Pick with all available links in the terminal's viewport.

Ctrl+Shift+O will open a Quick Pick with a categorized list of links found

The Ctrl+Shift+O keybinding was chosen as it's a similar action to Go to Symbol in Editor but for the terminal.

Go to Recent Directory - Ctrl/Cmd+G
Go to Recent Directory (Ctrl+G) opens a Quick Pick with recent directories, picked up by shell integration. It supports pinning and fuzzy matching.

Directories are presented in a Quick Pick, split up by the current and previous sessions.

This keybinding was chosen because Ctrl+G is a relatively low-usage shell keybinding.

Send Ctrl+G to the shell - Ctrl+Alt+G
Since Ctrl+G is now used to Go to Recent Directory, using Ctrl+Alt+G is the new way to send Ctrl+G directly to the shell.

Run Recent Command - Ctrl+Alt+R
Run Recent Command (Ctrl+Alt+R) opens a Quick Pick with recent commands that have been run, modeled after most shell's reverse index search (Ctrl+R) but in a more accessible and more functional package. It supports pinning and fuzzy matching.

Commands previously run are split up by current and previous sessions and also pulled in from the shell's history file

The keybinding Ctrl+Alt+R was chosen because it's an alternative behavior to Ctrl+R, but that keybinding is too important to overwrite its default behavior.

Accessibility mode overrides
Because reverse index search isn't very accessible to screen readers, when accessibility mode is on Ctrl+R will trigger Run Recent Command and Ctrl+Alt+R will send Ctrl+R to the shell.

Link improvements
There have been many improvements to link detection in the terminal this release:

Links containing spaces are detected under certain circumstances:

When the entire line is a link.
Python-style stack trace links: File "<path>", line <line>
Some compiler errors: <path>(<line>,<col>) : ...
Independently styled sections of text are all detected independently, so if a path is underlined, it should be detected even if it has spaces.
Links containing [ and ] characters now work, they even support detection in difficult edge cases like this:

Links that end in the ] character will be detected, even when the whole link is wrapped in [ and ]

vscode:// protocol links are now detected.

/mnt/, \\wsl$\ and \\wsl.localhost\ links are now detected on Windows.

OSC hyperlink support was added in v1.72, the common file:// protocol often used in these links are now supported (for example ls --hyperlink).

The terminal.integrated.enableFileLinks setting now features a "notRemote" option, allowing it to be conditionally disabled only on remotes where the file existence checks can cause performance problems.

Most link formats also consistently support the following line and column formats:

<file>:<line>
<file>:<line>:<column>
<file> <line>
<file> <line>:<column>
<file>(<line>)
<file>(<line>,<column>)
<file>(<line>, <column>)
<file> (<line>)
<file> (<line>,<column>)
<file> (<line>, <column>)
Single quotes or no quotes also work for these:
"<file>",<line>
"<file>",<line>:<column>
"<file>", line <line>
"<file>", line <line>, col <column>
"<file>", line <line>, column <column>
"<file>":line <line>
"<file>":line <line>, col <column>
"<file>":line <line>, column <column>
"<file>": line <line>
"<file>": line <line>, col <column>
"<file>": line <line>, column <column>
"<file>" on line <line>
"<file>" on line <line>, col <column>
"<file>" on line <line>, column <column>
Terminal editor file drag and drop support
Terminal editors now support drag and drop while holding Shift to write files to the terminal instead of opening an editor.

Dragging a file into a terminal editor will show 'Hold Shift to drop into editor'

"Unsafe" profile detection
Detection of the Cygwin shell on Windows was recently removed due to a security vulnerability. This release we bring this back in a safer form and also detect more shell profiles, including Cygwin, Cmder and MSYS2. To mitigate the security problem, before one of these profiles is used, it must be configured via the Select Default Profile command:

Select Default Profile is available via the terminal view dropdown or the Command Palette

The newly detected profiles appear in a "detected" section at the bottom of the Quick Pick

When selected, a warning will appear before being added to your settings.json file and acting like a regular profile:

The notification explains the path is potentially unsafe as it could be modified by another user

This warning can safely be ignored if the computer isn't used by multiple users, for example in a corporate environment.

Toggle commands in the terminal view
A long-time request has been to add the Clear Terminal command to the terminal view actions but we have always been concerned about bloat in the UI. Thanks to a new internal feature, we have new hidden-by-default actions that appear in an overflow menu but can be toggled to show via right-click:

Clear terminal, Run Active File, and Run Selected Text commands are now available in the terminal view's overflow menu

Right-click one of the view actions to toggle which ones are visible and which go into the overflow menu

Ctrl+C drops selection on Windows
Windows shares Ctrl+C between copying a selection and sending SIGINT to the shell, depending on whether there is a selection. A common annoyance was that if you had accidentally made a selection, Ctrl+C may not send SIGINT. To help mitigate this, Ctrl+C to copy the selection will now also clear the selection, so pressing Ctrl+C twice will reliably send SIGINT either 1 or 2 times.

Add a terminal tab stop size setting
There is a new setting terminal.integrated.tabStopWidth that configures the tab stop width of the terminal. This is useful when programs output the \t character instead of configuring the tab size in their configuration.

Powerline triangle and diagonal line custom glyphs
GPU-accelerated terminals now get pixel-perfect custom glyphs for the triangle and diagonal line Powerline extra symbols glyphs (U+E0B8-U+E0BF). These characters are ambiguous as to whether they are single or double width characters and differ depending on the font used, so we chose to render them as single width.

Before:

Triangles and diagonal line previously could display with bad anti-aliasing and odd borders

After:

Triangles and diagonal line glyphs are drawn pixel perfect

Bracketed paste mode used in "Run Selected Text In Active Terminal"
The Run Selected Text In Active Terminal command will now run the text using "bracketed paste mode" in supporting shells, so a multi-line selection will be treated as a single input, rather than multiple commands. This makes running actual scripts much more intuitive with fewer errors occurring.

Before:

Previously, running two echo statements would be run one after the one with 2 separate prompts

After:

Running two echo statements will now run in a single prompt

Quick fixes for Pwsh Preview feedback providers
PowerShell Preview recently implemented a new pluggable feedback provider system that allows printing suggestions when commands fail:

Running 'gcc' in pwsh preview will present 3 suggestions, which VS Code will present as Quick Fixes

The terminal now pulls Quick Fixes from the [General] and [cmd-not-found] feedback providers. The Quick Fix dialog can be opened by clicking on the light bulb or via Ctrl/Cmd+..

Source Control
New commands
Git 2.35 introduced a new --staged mode for the git stash command. This new mode allows you to easily stash only the changes that are staged. If you have a version of Git that supports this new mode, you can take advantage of it using the new Git: Stash Staged command.

VS Code already had support for deleting a local tag using the Git: Delete Tag command. This milestone we enabled the deletion of remote tags using the new Git: Delete Remote Tag command.

Git repositories in parent folders
VS Code uses git rev-parse --show-toplevel to determine the root of a Git repository. In most cases, the root of the Git repository is inside the workspace, but there are scenarios in which the root of the Git repository is in the parent folders of the workspace or the open file(s). While opening Git repositories in parent folders of workspaces or open files is a great feature for advanced users, it can be confusing for new users. We have seen cases in which this confusion resulted in discarding changes from these Git repositories causing data loss.

To avoid confusion, and to reduce the risk of data loss, starting this milestone, VS Code will display a notification and a new welcome view in the Source Control view, and will not automatically open Git repositories from the parent folders of workspaces and open files.

Notification that there is a Git repository in parent folders

Theme: Dark+ V2 with MacOS Modern product icons

The Open Repository button will open a Quick Pick with a list of all Git repositories that were discovered in the parent folders of the workspace or the open file(s). The choice to open a Git repository from the parent folders is remembered.

Users can control how Git repositories from parent folders are being handled using the git.openRepositoryInParentFolders setting. Users who would like to restore the old behavior can set the git.openRepositoryInParentFolders setting to always.

Command disablement
Based on the size of a Git repository or the presence of various Git hooks, some Git operations can take a long time to complete. We have seen in the past that initiating commands while a previous command is still in progress can lead to unexpected results (for example, discarding changes on a file while the commit operation is in progress).

To prevent this, we are disabling most Git commands while the following operations are in progress: Checkout, Commit, Push, and Pull. This means that while these operations are running, most Git commands will not appear in the Command Palette, and will be disabled in the Source Control view and the Status bar.

User interface improvements
This milestone we have polished some of the Source Control user interface elements:

The tooltip of the Commit and Publish Branch action buttons in the Source Control view now includes the branch name.
The Checkout Status bar item now uses a different icon depending of the type of ref that is checked out (branch, tag, or commit).
The Checkout Status bar item now shows a spinning progress icon while the checkout operation is in progress.
Notebooks
Kernel picker improvements
We continued to improve the MRU (Most Recently Used) kernel picker. It can be enabled by setting notebook.kernelPicker.type to mru. Kernels that are not used are moved into a secondary picker Select Another Kernel.... This picker will group all kernels by their source (for example: Jupyter Kernel, Python Environment, etc.) when you have latest Jupyter and Python extensions installed.

Notebook Kernel Picker

Join Selected Cells
There is a new command Join Selected Cells (kb(notebook.cell.joinSelected)`) to merge multiple selected cells into one cell.

Join Selected Cells command

Fallback rendering of output to a supported mimetype
Rich outputs in Jupyter Notebooks such as IPyWidgets are visible only during the lifetime of the kernel. This means that when the notebook is closed and reopened again, the outputs are no longer visible. However, in a number of these cases, the output can be rendered using a fallback mechanism. For example, an IPyWidget can in some cases (depending on the widget used) be rendered as a static image or HTML content.

As a result, users opening existing notebooks with matplotlib widgets (or similar widgets) can now see the output without having to re-execute the code.

Notebook Renderer fallback

New documentation
There are two new topics to help you work with Jupyter Notebooks in VS Code.

Jupyter Notebooks on the web - Run notebooks on vscode.dev or in GitHub Codespaces.
Manage Jupyter Kernels - Learn how to connect your notebook to various Jupyter kernels.
Debugging
JavaScript debugging
Improved Node.js Startup Performance
The 'breakpoint predictor' used for Node.js debugging has been rewritten and improved to dramatically increase speed for large projects. For example, startup time overhead when debugging unit tests in the TypeScript repo was reduced by 62%, and the overhead to debug and start a build in the VS Code repo was reduced by 80%.

If you run into problems such as breakpoints not being hit, please file an issue. You can disable the new behavior by setting "enableTurboSourcemaps": false in your launch.json, however this option will eventually be removed as we gain confidence.

Languages
JavaScript React language label is now JavaScript JSX
The JavaScript React language mode has been renamed to JavaScript JSX to reflect that JSX syntax is used by more than just React. TypeScript React has also been renamed to TypeScript JSX.

Note that only the language names shown in the UI have been changed. The internal language IDs (javascriptreact and typescriptreact) remain unchanged for compatibility reasons.

New shellscript grammar
VS Code now uses a new grammar from better-shell-syntax for shellscript syntax highlighting.

Extensions
VS Marketplace extension signing
Every extension uploaded to the Visual Studio Marketplace starting from November 2022 is code signed by the VS Marketplace. When a user installs a signed extension through VS Code's Extensions view, VS Code will verify the signature, and thus prove that the extension is indeed coming from the VS Marketplace and that the extension package has not been modified. If the signature verification fails, VS Code will not install the extension.

VS Marketplace is in the process of signing all existing extensions (including extensions that have not been updated since November). Once this process is done, in a couple of months, VS Code will require that all extensions coming from the VS Marketplace are signed by the VS Marketplace. This requirement will guarantee the integrity of every package coming from the VS Marketplace, thus improving the overall security of our extension ecosystem.

Note: Extension authors do not have to do anything to opt-in to Marketplace signing. In addition to Marketplace signing, we are currently working on publisher signing. More about publisher signing can be found in discussion #137.

Pin an extension version from CLI
When you install a specific version of an extension from the CLI (code --install-extension {publisher}.{name}@{version}), it will now be pinned to that version. This means that the extension will not be updated automatically when you have automatic updates enabled.

Sync pinned extension versions
Settings Sync will now sync pinned extension versions. This means that when you install a specific version of an extension on one machine, it will be pinned to that version on all other machines that you sync to.

Contributions to extensions
Python
Auto-select environment when VS Code is launched from an activated terminal
If a user launches VS Code via a terminal with a conda or virtual environment already activated, the Python extension now detects that and then either auto-selects the environment itself, or asks the user if they would like to make that environment their selected one; depending on the environment.

Select requirements files when creating environment
When creating a virtual environment using the Python: Create Environment command, the Python extension now finds requirement files in the workspace folder, and allows users to multi-select any number of requirements to install.

Select optional dependencies from pyproject.toml
The Python extension detects and loads the optional dependencies provided in the [project.optional-dependencies] part of the pyproject.toml file. We use the pip editable install command if we detect that the workspace contains a pyproject.toml along with any selected optional dependencies.

Auto indentation with Pylance
When the editor.formatOnType setting is enabled for Python files, Pylance will automatically indent the code as it's typed in, allowing you to focus more on the logic of your code and less on formatting.

To try it out, enable formatOnType for Python files by adding the following to your user settings.json file:

 "[python]": {
        "editor.formatOnType": true,
    },

Live Preview
Setting for external browser preview
The Live Preview extension now lets you open the external browser preview in browsers other than your default browser. Using the livePreview.customExternalBrowser setting, you can set the external preview to open in:

Microsoft Edge
Google Chrome
Mozilla Firefox
Your default browser
Live Preview Custom External Browser setting 

Setting for the server root
You can now set the server's root path to a sub-folder in your workspace. For example, you can ask Live Preview to serve files from your src folder in your workspace by setting livePreview.serverRoot to "src".

ESLint
The ESLint extension has been updated to version 2.4.0. Major new features are:

Support for the new experimental flat config files. You need to enable the support separately in VS Code using the setting eslint.experimental.useFlatConfig. ESLint version 8.21 or greater is required.

The ESLint status indicator moved into VS Code's Language status area. As a result, the setting eslint.alwaysShowStatus was removed. Use VS Code's pin feature instead.

ESLint language status

The language status item will now inform you of slow validation times and long ESLint runs when computing code fixes during save. The time budget available (in milliseconds) can be control via the two settings eslint.timeBudget.onValidation and eslint.timeBudget.onFixes.

Long problem squiggles can be shortened to a single line using the new settings eslint.problems.shortenToSingleLine.

GitHub Pull Requests and Issues
There has been more progress on the GitHub Pull Requests and Issues extension, which allows you to work on, create, and manage pull requests and issues. Highlights include:

Support for suggesting and accepting changes.
GitHub handles in comments are now linkified.
Labels can be added to PRs at creation time.
An experimental setting githubPullRequests.experimental.quickDiff will show a quick diff view in the editor gutter for changed lines in a checked out PR.
Check out the changelog for the 0.58.0 release of the extension to see the other highlights.

GitHub Copilot
The GitHub Copilot extension is an AI-powered code completion tool that helps you write code faster and smarter. You can use the Copilot extension in VS Code to generate code, or to learn from the code it generates.

GitHub Copilot integrates into the VS Code editor through the inline suggestions UI, which lets you review various suggestions and easily accept all or part of the generated code.

GitHub Copilot is now generally available for businesses, with features like license management, organization-wide policy controls, and privacy protections. You can learn more in the GitHub Copilot for Business announcement.

To get started, you can sign up for a free trial on the GitHub Copilot website.

We've also added a new AI Tools in VS Code topic to the VS Code documentation that will help you get started with Copilot.

Remote Development
The Remote Development extensions, allow you to use a container, remote machine, or the Windows Subsystem for Linux (WSL) as a full-featured development environment. Highlights of this release include:

Dev Container support for multiple devcontainers.json files.
Docker credential forwarding.
X11 & Wayland Forwarding
You can learn about new extension features and bug fixes in the Remote Development release notes.

Remote Tunnels
Sleep inhibition
Remote Tunnels can now prevent the computer from going to sleep on Windows, macOS, and systemd-based Linux systems. This is useful if you leave your desktop to work remotely and want to make sure the tunnel stays accessible. To use this feature:

When turning on Remote Tunnel Access from the VS Code UI, update the setting remote.tunnels.access.preventSleep to true.
When using code tunnel on the CLI, pass in a --no-sleep flag.
Reliability Improvements
Several connection-related issues in Remote Tunnels have been fixed, which should improve reliability.

Continue Working On
The Continue Working On feature supports starting in a Git repository in a local window and continuing in a remote window like a GitHub Codespace. If you are on a branch that has not yet been published to the remote, you will now automatically be prompted to publish your current branch when you choose to continue working in a different development environment, so that you can access your full branch context elsewhere.

Additionally, when you're on a Git repository in a remote window, you can now continue working in a new local Git clone on VS Code Desktop using the Continue Working in New Local Clone command.

Finally, all options for continuing your work in a local, remote, or web window are now conveniently surfaced in the remote indicator. These options are also available in the Command Palette.

Continue Working On actions now available in the remote indicator

Preview features
Dark+ V2 and Light+ V2 experimental themes
Two new color themes, Dark+ V2 and Light+ V2, are now available for use. These themes are an evolution of the existing Dark+ and Light+ themes, and are designed to be more accessible and make VS Code look better than ever! These themes are still marked as experimental, and we are looking for early feedback.

Dark+ V2 and Light+ V2 experimental themes

You can find the new themes listed as Light+ V2 (Experimental) and Dark+ V2 (Experimental) in the Color Theme picker (Preferences: Color Theme Ctrl+K Ctrl+T).

TypeScript 5.0 support
This update includes support for the upcoming TypeScript 5.0 release. See the TypeScript 5.0 iteration plan for more details on what the TypeScript team is currently working on. Some editor tooling highlights:

New switch and case completions help you fill in both sections of switch statements more quickly.
Work on enabling project wide IntelliSense on github.dev and vscode.dev.
To start using the TypeScript 5.0 nightly builds, install the TypeScript Nightly extension.

"commonly used" section in the Command Palette
This milestone, we have added a new "commonly used" section to the Command Palette. The goal of this section is help new users have a better understanding of what the Command Palette is for and what it can do.

commonly used section in the Command Palette

Theme: Panda Theme (preview on vscode.dev)

This section will show up underneath the "recently used" section so to not break muscle memory and as you run more and more commands and get familiar with VS Code, either the section disappears (because the "commonly used" commands move up to "recently used") or the section is below the fold and out of sight.

commonly used section with recently used commands

Theme: Panda Theme (preview on vscode.dev)

For now, we have put this new experience behind the setting workbench.commandPalette.experimental.suggestCommands but we plan to make this the default behavior in the near future. Let us know what you think!

Extension authoring
Comment thread state
The CommentThread state API has been finalized. This API controls whether a comment renders as resolved or unresolved and can affect filtering in the Comments view. You can learn more about how to use the API in issue #127473.

Ignore a setting to sync
You can now hide a setting from Setting Sync by default using the ignoreSync property while registering a setting. This is useful for settings that are not meant to be synced across machines.

Telemetry
The new TelemetryLogger API has been finalized. This API aims to make using telemetry easier for extension authors and safer for the end user. The API enables things such as built-in secret cleaning, a telemetry output channel, error handlers, and automatic telemetry level management. This should result in a more cohesive telemetry experience that is guaranteed to follow our requirements.

Proposed APIs
Every milestone comes with new proposed APIs and extension authors can try them out. As always, we want your feedback. Here are the steps to try out a proposed API:

Find a proposal that you want to try and add its name to package.json#enabledApiProposals.
Use the latest vscode-dts and run vscode-dts dev. It will download the corresponding d.ts files into your workspace.
You can now program against the proposal.
You cannot publish an extension that uses a proposed API. There may be breaking changes in the next release and we never want to break existing extensions.

Let notebook renderer fallback to a different mimetype
Sometimes when rendering content, a notebook render may realize that it cannot render the item properly. For example, perhaps the renderer requires that the kernel be in a certain state.

Previously for cases like this, the renderer's only option was to render an error message. We've added a new proposed API that lets a renderer throw a specially named error that causes VS Code to silently fallback to rendering the other data stored on the notebook output item. For example, an interactive chart renderer could throw this error to make VS Code fallback and render the image data also stored on the current output item.

To trigger this fallback, throw an error with the name vscode.fallbackToNextRenderer in renderOutputItem:

throw new class extends Error {
    override name = 'vscode.fallbackToNextRenderer';
}();

This special error is only meant for cases where rendering is expected to fail in certain situations. If your renderer runs into an unexpected error, it should continue to show an error message.

Quick diff
The quick diff, which is the gutter decoration that shows on added, changed, and deleted lines in the editor, is currently only usable by SCM providers. The proposed quick diff API allows the quick diff to be used outside of SCM providers. The following example is from the GitHub Pull Request extension, which uses the quick diff API to show a quick diff for lines changed in a PR:

vscode.window.registerQuickDiffProvider({ scheme: 'file' }, {
    provideOriginalResource: (uri: vscode.Uri) => {
        const changeNode = this.reviewModel.localFileChanges.find(changeNode => changeNode.changeModel.filePath.toString() === uri.toString());
        if (changeNode) {
            return changeNode.changeModel.parentFilePath;
        }
    }
}, 'GitHub Pull Request', this.repository.rootUri);

The full proposal is in quickDiffProvider.d.ts.

Continuous test runs
Continuous test runs allow test extensions to indicate that they're able to watch and rerun tests when changes happen. Supporting this API is a matter of indicating support on your test run profile...

const profile = controller.createRunProfile('Run', TestRunProfileKind.Run, runHandler);
+profile.supportsContinuousRun = true;

And then checking for that in the runHandler:

const runHandler = (request: TestRunRequest, token: CancellationToken) => {
+   if (request.continuous) {
+       return watchForFileChangesThenRunTests(request, token);
+   }
}

The full proposal is in testContinuousRun.d.ts.

Engineering
Utility process for extension host
The utility process usage for extension host that is required for process sandboxing is now enabled by default. There is still a setting (extensions.experimental.useUtilityProcess), which we will remove soon.

Performance testing via command line
We introduced the following node modules to run a set of performance tests from the command line.

vscode-bisect - This module helps us measure performance regressions quickly. Run npx vscode-bisect --help for how to operate this tool.

vscode-perf - This module helps us measure the performance of VS Code. npx vscode-perf --help describes how to operate this tool.

GB18030 Certification
VS Code is now GB18030-certified - this means that a certification board within the Chinese government has confirmed that VS Code can correctly represent the full range of Chinese characters. The testing covered all built-in usage scenarios. With VS Code certified, the core Visual Studio Family (including Visual Studio and Visual Studio for Mac) has been certified under GB18030.

Migrating to ESM
We have embarked on a journey to migrate our codebase to ESM. The VS Code project predates native modules (ESM) and we have been using the asynchronous module system (AMD) for the time being. AMD has served us well but it is time to move on. We have started to migrate our codebase to ESM, we are making good progress, and hope to finish this effort in the next months.

EOL warning for macOS 10.11 and 10.12
VS Code desktop will be updating to Electron 22 in the next couple of milestones. With the Electron 22 update, VS Code desktop will no longer run on OS X El Capitan and macOS Sierra. In this milestone, we have added deprecation notices for the users on these affected platforms to prepare them for migration. If you are a user of these aforementioned OS versions, please take a look at our FAQ for additional information.

Improved usage of system and application language variables
In a previous release, we started passing in the application language to Electron so that it can lay out some components such as the window controls overlay (WCO) correctly. Meanwhile, the language recommender relied on the system language, but app.getLocale() started fetching the application language instead of the system language, so we used a newer app.getPreferredSystemLanguages() Electron API to retrieve the system language to use for the language recommender. As a result, a regression occurred where extensions in the Extensions view could not render, because the new API returned some values that toLocaleString() could not parse.

The immediate solution, which we pushed for a recovery release, was to revert back to app.getLocale() and temporarily break language recommendation, but it turns out that many areas of the codebase should have been using the application language variable instead of the system language variable as well.

This release replaces many usages of the system language with the application language. In turn, dates should now be localized in a format more consistent to the application language rather than the system language.

Notable fixes
99878 Prepending PATH env var with environmentVariableCollection doesn't work on macOS
153786 Have a command to open either side of a diff editor
165123 Allow to open a diff editor with two untitled sides
167004 Output: Show Output Channels A command to show an output channel
167528 Log level of an extension output channel persists after reloading the window
Thank you
Last but certainly not least, a big Thank You to the contributors of VS Code.

Issue tracking
Contributions to our issue tracking:

@gjsjohnmurray (John Murray)
@IllusionMH (Andrii Dieiev)
@ArturoDent (ArturoDent)
@yume-chan (Simon Chan)
Pull requests
Contributions to vscode:

@a-stewart (Anthony Stewart): Specify window consistently with matchMedia calls in browser.ts PR #164020
@Aaaaash (?????????): Fixes standaloneTheme.defines Always return false. PR #169221
@andschwa (Andy Jordan): Fix shell integration for PowerShell 5.1 PR #170516
@antonioprudenzano (Antonio Prudenzano): Feat/155294 PR #168513
@babakks (Babak K. Shandiz)
Include tilde (~) in markdown syntax tokens PR #146417
???? Include branch name in commit button popup PR #167827
Add watch without selection PR #171449
@Balastrong (Leonardo Montini): 145458 List: Support scroll by page PR #145788
@chiefmikey (Mikl Wolfe)
Remove repository.ts default parameter types PR #155908
Update git config.followTagsWhenSync definition PR #155914
@chouzz (Chouzz): Fix incorrect description for call hierarchy and type hierarchy api PR #167718
@d1y (???????????????): feat: screencast mode move scale PR #156084
@davidwengier (David Wengier): Update Razor repo PR #171560
@dtivel (Damon Tivel)
Extensions: warn not fail on UnknownError during signature verification PR #169777
Do not block if unable to verify extension signature PR #172576
@fadeevab (Alexander Fadeev): Makefile tests for else ifeq|ifneq|... syntax PR #170888
@giannisp (Ioannis Poulakas): Improve layout of search input PR #165989
@gjsjohnmurray (John Murray)
Add history to new list/tree search/filter widget (#155578) PR #159188
Add 'Fuzzy Match' toggle to tree find widget (#116286) PR #164376
Prevent hiding unresolved tree branches PR #167047
@gpoussel (Guillaume Poussel): Add command to delete remote tag (fix #104845) PR #134327
@HKalbasi: Fix inlay hint location links problem PR #167886
@hughlilly (Hugh Lilly): Copyedit: ???Double-clicking??? -> ???Double-clicking??? PR #166758
@jakebailey (Jake Bailey): Set disableLineTextInReferences=true in TS user preferences PR #171376
@jasonwilliams (Jason Williams): Allow to open either side of a diff editor as editor (fix #153786) PR #165765
@jeanp413 (Jean Pierre)
Fixes pasting into quick outline does not reveal result PR #166835
Fixes editor-area terminals are not restored after quit PR #168887
Fixes terminals/tasks restored after reload ignore confirmOnKill and confirmOnExit settings PR #168922
Fixes createTerminal does not create a terminal at the first editor group PR #169050
@joshuaobrien: Add git stash staged only command PR #165649
@laurentlb (Laurent Le Brun): Command duration: use a higher-precision for telemetry PR #167624
@maIIady (Ilya Golovin): Fix: make git commands work with keyboard PR #159113
@markw65: Fix for not auto-starting same-named tasks in different folders PR #168742
@MarkZuber (Mark Zuber): Add high latency measurement instrumentation to the network protocol PR #168668
@meskill: fix: nushell integration PR #169861
@mkhl (Martin K??hl): expose fish integration configuration via XDG_DATA_DIRS PR #168211
@MonadChains (MonadChains)
Issue 163528/create edit breakpoint command PR #163734
Enable breakpoints view when debug has been launched at least once PR #169077
@mroch (Marshall Roch): fix anyScore firstMatchCanBeWeak PR #168266
@mueheg (Google Henrik): Do not select full contents of inputbox before selecting a range, fixes #167266. PR #167274
@N1kO23: Added ${rootNameShort} formatting PR #165744
@ohah (ohah): screencast ime bug fix (#165248) PR #165249
@ookami-kb (Kirill Bubochkin): Update shellIntegration.fish to fix an error when communicating cwd PR #168452
@PEZ (Peter Str??mberg): Enable monospaced digits for statusbar items PR #167310
@pokey (Pokey Rule): Fix bug with snippet choices escaping PR #169287
@probablykasper (Kasper): Add terminal.integrated.tabStopWidth option PR #170733
@pzhlkj6612 (Mozi): Terminal Tabs: disable dragging and clicking during renaming PR #166821
@r3m0t (Tomer Chachamu): Fix webview disappearing when extension is slow to start (#168516) PR #168569
@rezasoumi (RezCoder): issue 163803/ first pick a ref then pick a name in create-branch-from... PR #170908
@rwe (Robert Estelle): shellIntegration-bash.sh: exactly preserve DEBUG trap expression PR #165581
@samdenty (Sam Denty): fix IExtensionRecommendationReson typo PR #163889
@Sean1708 (Sean Marshallsay): Introduce VSCODE_RESOLVING_ENVIRONMENT env var. PR #168436
@ssigwart (Stephen Sigwart)
Retain maximized group size when adding and removing groups or toggling side bar PR #137962
Fix paste removing indent PR #167687
Add CamelCase Transformation PR #169512
@ste42 (Steven Tam): Add new untitled diff command PR #168533
@sumneko (????????????): update Lua-grammar PR #167692
@weartist (Han)
Fix Setting to disable loop of "next change" in diff view #163331 PR #164225
Adapter css for #165169 PR #167030
support process explorer remember it's location and dimensions PR #169090
add the snippet source when the snippet with the same name appears PR #169119
Replace applicationStorageMainService with stateMainService PR #169365
@yiliang114 (??????): fix: typos PR #158431
@zardoy (Vitaly): [typescript] fix potential [object Object] in member completions PR #171127
Contributions to vscode-css-languageservice:

@romainmenke (Romain Menke): new CSS units PR #324
Contributions to vscode-hexeditor:

@brabli (Bradley): Add octal representation of the current byte in data inspector PR #410
Contributions to vscode-json-languageservice:

@rahulbanerjee26 (Rahul Banerjee): Check schema for errorMessage property for "not" rule PR #164
Contributions to vscode-languageserver-node:

@wkillerud (William Killerud): Add defaultBehavior response to onPrepareRename PR #1161
Contributions to vscode-pull-request-github:

@eamodio (Eric Amodio): Updates TypeScript (released 4.2) and Octokit (to get fixed types), and a couple minor others PR #2525
@sravan1946 (sravan): Remove unavailable badge from readme PR #4393
@Thomas1664
Fix comment layout & use bin as delete icon PR #4285
Colorize status badge PR #4286
UI fixes for PR view PR #4368
Use correct permission to show 'assign yourself' in PR view sidebar PR #4369
Fix UI for PR draft status check entry PR #4370
Contributions to debug-adapter-protocol:

@mfussenegger (Mathias Fu??enegger): Clarify that absent canRestart on frame implies true PR #365
Contributions to monaco-editor:

@jonatanklosko (Jonatan K??osko): Update Elixir tokenizer PR #3453
@rcjsuen (Remy Suen): Fix the color provider's columns PR #3348
