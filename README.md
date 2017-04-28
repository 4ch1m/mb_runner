# mb_runner
> A helper-script to enable ConnectIQ-development on UNIX-systems

Due to the lack of a dedicated CIQ-SDK for Linux, this script aims to provide some basic automated tasks to make developing CIQ-apps on UNIX-systems possible nevertheless.  

Currently these tasks/features are available:
* compiling (re)sources and building a PRG-file for testing
* run unit-tests (requires a running simulator)
* creating a signed IQ-file package for publishing
* cleaning up previously built files
* starting the ConnectIQ-simulator (using wine)
* pushing the generated PRG-file to the running simulator

There are two ways to utilize this script:

* Manually copy the **mb_runner.sh**-file plus your customized **mb_runner.cfg**-file into your project root.

  Your directory should then look similar to this:

  ```
   .
   ├── manifest.xml
   ├── mb_runner.sh
   ├── mb_runner.cfg
   ├── resources
   │   ├── strings.xml
   │   └── ...
   ├── resources-deu
   │   ├── strings.xml
   │   └── ...
   └── source
       ├── main.mc
       └── ...  
  ```
 
* Or use this repository as a git-submodule of your project/repository.

  Simply execute ...

  ```
  git submodule add https://github.com/4ch1m/mb_runner.git
  ```

  ... to get the **mb_runner.sh**-file in a `mb_runner`-subfolder.

  You still will have to create a customized **mb_runner.cfg**-file in your project.

  Then your directory structure should look similar to this:

  ```
   .
   ├── manifest.xml
   ├── mb_runner
   │   ├── mb_runner.cfg.sample
   │   ├── mb_runner.sh
   │   └── README.md
   ├── mb_runner.cfg
   ├── resources
   │   ├── strings.xml
   │   └── ...
   ├── resources-deu
   │   ├── strings.xml
   │   └── ...
   └── source
       ├── main.mc
       └── ...  
  ```
  
  The benefit of this approach is a way more convenient way to update the *mb_runner*-script by using ...
   
  ```
  git submodule update --remote --merge
  ``` 

  ... once updates are available.

For more details please see the comments in the script itself: [mb_runner.sh](mb_runner.sh).

#### Additional Notes
The script should be run with your project's root-directory as current working directory.
Also the script expects your source-files to be in a folder called `source`, and your resources in folders named `resources*`.

However this can be customized by passing your full project-root-path, the resources-folder-name and the source-folder-name as 2nd, 3rd, and 4th parameter respectively.

#### Technical Side Note
* How to determine all available devices (listed in `mb_runner.cfg.sample`):
  ```
  grep "device id=" ${MB_HOME}/bin/devices.xml | sort
  ```
* How to determine target-SDK versions (listed in `mb_runner.cfg.sample`):
  ```
  grep "<version>" ${MB_HOME}/bin/compilerInfo.xml | tail -n +2
  ```

Have fun! :smile:
