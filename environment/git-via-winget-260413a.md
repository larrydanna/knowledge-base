# Install Git

## TL;DR

-  bn  Open a termina.
-  bn  Run `winget install --id Git.Git -e --source winget`
-  bn  Close and reopen the terminal.

---
To install Git using the Windows Package Manager (winget), follow these steps:
## 1. Run the Install Command
Open PowerShell or Command Prompt (running as Administrator is recommended to ensure proper system integration) and enter the following command: [1, 2] 

`winget install --id Git.Git -e --source winget`


* --id Git.Git: Specifically targets the official Git package.
* -e: Ensures an exact match for the package ID.
* --source winget: Specifies the official [Microsoft community repository](https://learn.microsoft.com/en-us/windows/package-manager/winget/) as the source. [1, 3, 4, 5, 6] 

## 2. Complete the Installation Wizard [6] 
Unlike some winget packages that install silently, the Git installer typically launches a standard setup window. [7, 8] 

* Follow the prompts to choose your default editor and PATH settings.
* Important: Ensure "Git from the command line and also from 3rd-party software" is selected (this is the default) so you can use it in any terminal. [6, 7, 9] 

## 3. Verify the Installation
Once the process finishes, restart your terminal and verify that Git is correctly installed by checking its version: [10, 11, 12] 

git --version

If successful, you will see a response like git version 2.x.x. [6, 13] 
------------------------------
## Additional Options

* Specific Installation Path: If you need to install Git to a custom directory (e.g., a different drive), use the --location flag:
winget install --id Git.Git -e --location "D:\Git".
* Microsoft-Specific Fork: For monorepo scenarios, Microsoft offers a specialized fork containing patches for extremely large repositories:
winget install --id Microsoft.Git -e. [14, 15, 16] 

Would you like help configuring your user name and email for Git next?

[1] [https://git-scm.com](https://git-scm.com/install/windows)
[2] [https://cloudminister.com](https://cloudminister.com/blog/how-to-upgrade-git-on-windows-version/#:~:text=To%20do%20this%2C%20right%2Dclick%20on%20Command%20Prompt,required%20changes%20to%20your%20existing%20Git%20installation.)
[3] [https://learn.microsoft.com](https://learn.microsoft.com/en-us/windows/package-manager/winget/install)
[4] [https://winstall.app](https://winstall.app/apps/Git.Git)
[5] [https://stackoverflow.com](https://stackoverflow.com/questions/62153958/how-to-install-git-on-windows-10-without-git-bash-or-gui)
[6] [https://petri.com](https://petri.com/install-git-windows/)
[7] [https://www.howtogeek.com](https://www.howtogeek.com/832083/how-to-install-git-on-windows/)
[8] [https://developercommunity.visualstudio.com](https://developercommunity.visualstudio.com/t/Install-Git-on-Windows-2019-Core/10220376?space=8&q=git+undo+2015)
[9] [https://recyclarr.dev](https://recyclarr.dev/guide/installation/tips/git-install/)
[10] [https://www.linode.com](https://www.linode.com/docs/guides/how-to-install-git-on-linux-mac-and-windows/#:~:text=When%20completed%2C%20check%20the%20Git%20version%20to%20ensure%20the%20installation%20was%20successful.)
[11] [https://blog.devgenius.io](https://blog.devgenius.io/git-basics-from-nothing-to-beginner-5c3fdab0b47d#:~:text=If%20you%20get%20a%20popup%20with%20the,move%20on%20to%20making%20your%20first%20repository!)
[12] [https://www.geeksforgeeks.org](https://www.geeksforgeeks.org/git/how-to-fix-git-is-not-recognized-as-an-internal-or-external-command/)
[13] [https://robolab.inf.tu-dresden.de](https://robolab.inf.tu-dresden.de/en/knowledge/how-to/git)
[14] [https://stackoverflow.com](https://stackoverflow.com/questions/35146260/how-do-i-install-git-for-windows-software-to-a-specific-directory)
[15] [https://winstall.app](https://winstall.app/apps/Microsoft.Git)
[16] [https://winget.run](https://winget.run/pkg/Microsoft/Git)
