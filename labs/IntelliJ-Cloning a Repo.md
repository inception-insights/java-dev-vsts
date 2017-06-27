## IntelliJ - Working with Git

In this exercise, you are going to clone a Github repo into VSTS and 
then open clone it to your VM for editing in IntelliJ.
This exercise assumes you have completed Exercise 1, and have created 
a Team Project that uses Git for version control and have completed
Exercise 2 where you’ve defined some work items. This exercise uses a 
team project named **jdev**, though your team project name may differ.

> **Note**: It is not necessary to clone Github repos into VSTS. VSTS
will work just fine with Github (or other Git hoster) repos. However,
some linkages from source code to other aspects of the DevOps pipeline
(such as work items, builds or releases) work best if the code is in
VSTS.

Importing a Github Repo into VSTS
---------------------------------

In this task you will import code from a Github repo into VSTS.

1. Connect to the virtual machine with the user credentials which you specified when creating the VM in Azure.
1. Open Chrome and browse to `http://<youraccount>.visualstudio.com` (where `youraccount` is the account you created in VSTS).
1. Click on the `jdev` team project to navigate to it. Click on Code in the blue toolbar at the top to open the Code Hub.
1. Click on the repo drop-down in the upper left (in the grey toolbar) and select "New repository".

    ![Import a repository in the Code Hub](images/intellij-git/import-repo.png "Import a repository in the Code Hub")

1. Enter the following url: `https://github.com/nwcadence/MyShuttle2.git` and click Import.

    ![Enter the URL](images/intellij-git/import-repo-url.png "Enter the URL")

1. After a few moments, the code will be imported.

1. Click "Save"

Connect to VSTS from IntelliJ
-----------------------------

1. Click on the IntelliJ icon in the toolbar to open IntellJ IDEA.

![Click IntelliJ in the Toolbar](images/intellij-git/click-intellij.png "Click IntelliJ in the Toolbar")

1. The first time you run IntelliJ, it will prompt for theme settings. Click on "Skip All and Set Defaults" to use the defaults.

![Accept the default IntelliJ theme](images/intellij-git/intellij-defaults.png "Accept the default IntelliJ theme")

1. When the Welcome dialog appears, click Configure and then select Plugins.

![Click on Configure to configure Plugins](images/intellij-git/intellij-config-plugins.png "Click on Configure to configure Plugins")

1. In the search box type `visual studio team services` and click the "Search in repositories" link in the main window.

![Search for the VSTS plugin](images/intellij-git/intellij-search-vsts.png "Search for the VSTS plugin")

1. Click install to install the extension. The install button will change to a "Restart" button - click it to restart IntelliJ.

![Install the plugin and restart IntelliJ](images/intellij-git/intellij-click-install.png "Install the plugin and restart IntelliJ")

1. When IntelliJ restarts, the Welcome dialog will appear again. Click "Check out from Version Control" and select "Team Services Git".

![Checkout from Team Services Git](images/intellij-git/intellij-open-from-vsts.png "Checkout from Team Services Git")

1. Click on "Sign in..." to sign in to your VSTS account.

![Sign in to VSTS](images/intellij-git/intellij-vsts-signin.png "Sign in to VSTS")

1. Once you have authenticated, enter "MyShuttle2" into the search bar and select the MyShuttle2 repo from your team project. Click the Clone button to clone the repo to the VM.

![Select the VSTS repo](images/intellij-git/intellij-select-repo.png "Select the VSTS repo")

1. IntelliJ detects a Maven project file (pom.xml) and asks if you want to open it. Click "Yes" to open the project. You can dismiss the Tip of the Day dialog that appears.

1. Press "Alt-1" to open the Project View.
1. Expand `src\main\java\com.microsoft.example` and click on "DataAccess" to open the DataAccess class.
1. A yellow warning appears in the main editor window prompting you to "Setup SDK". Click on the link.

![Setup the JDK for the project](images/intellij-git/intellij-setup-sdk.png "Setup the JDK for the project")

1. In the Select Project SDK dialog, click "Configure..."

![Click on Configure](images/intellij-git/intellij-jdk-configure.png "Click on Configure")

1. In the upper left, click the green "+" icon to add a new SDK.

![Add an SDK](images/intellij-git/intellij-add-sdk.png "Add an SDK")

1. Select `java-8-openjdk-amd64` from the folder list and click OK. Click OK back through the rest of the dialogs.

![Select the SDK folder](images/intellij-git/intellij-select-sdk.png "Select the SDK folder")

> **Note**: The project will not currently compile, since it has a dependency on a library (MyShuttleCalc) that it cannot resolve. You will fix this in the next lab.

### OPTIONAL: Create an SSH Key for Git authentication

If you prefer to authenticate via SSH, you can do so with VSTS. You need to create an SSH key if you do not already have one, then upload the public key to VSTS. Then select the SSH URL for cloning repos.

1. On your VM, open a terminal by clicking on the Terminal Emulator icon in the toolbar.

    ![Click on the terminal icon in the Toolbar](images/intellij-git/click-terminal.png "Click on the terminal icon in the Toolbar")

1. Enter the following command:

```sh
ssh-keygen -C "jdev.com"
```

and press Enter 3 times to use the default id_rsa location as well as an empty pass phrase.

![Create an SSH key](images/intellij-git/generate-key.png "Create an SSH key")

> **Note**: the domain is not important - use any value you want. You can also enter a pass phrase if you want to, though this will cause a prompt each time you use the key.

1. Enter the following command to print out the public key in the terminal:

```sh
cat /home/vmadmin/.ssh/id_rsa.pub
```

1. Select all of the text (from `ssh-rsa` to `jdev.com`), right-click and select "Copy".

1. Go back to Chrome and click on your profile image in the upper right. In the menu, click Security.

![Click on Security under your Profile image](images/intellij-git/click-security.png "Click on Security under your Profile image")

1. Click on "SSH public keys" and click the "Add" button.
1. Enter "jdev" for the Description and then paste into the Key Data the contents of the public key (which should be in your clipboard).

![Add a new public key](images/intellij-git/add-ssh-key-to-vsts.png "Add a new public key")

> **Note**: Once you have your SSH credentials set up, remember to use the SSH URL when cloning repositories.