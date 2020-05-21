---
layout: post
title:  "Hello, Jekyll"
date:   2020-05-20 21:03:36 +0530
---
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse

 Install afl

- My linux: CentOS Linux 7

- Use below commands to install afl:

  ```shell
  git clone https://github.com/mirrorer/afl
  cd afl
  make
  sudo make install
  ```

  

- Use command `ls -l /usr/local/bin/afl*` to check the installed files.

  ![1589878959728](C:\Users\wjq\AppData\Roaming\Typora\typora-user-images\1589878959728.png)

  • `afl-gcc` and `afl-g ++` correspond to the `gcc` and `g ++` packages, respectively
  • `afl-clang` and `afl-clang ++` correspond to clang's c and c ++ compiler packages, respectively.
  • `afl-fuzz` is the main body of AFL, used to fuzz the target program.
  • `afl-analyze` can analyze use cases. By analyzing a given use case, you can see if you can find meaningful fields in the use case.
  • `afl-qemu-trace` is used in qemu-mode, which is not installed by default. You need to manually execute the compilation script of qemu-mode to compile, which will be described later.
  • `afl-plot` generates a state diagram of the test task
  • `afl-tmin` and `afl-cmin` simplify the use cases
  • `afl-whatsup` is used to view the status of fuzz tasks
  • `afl-gotcpu` is used to view the current CPU status
  • `afl-showmap` is used to trace the execution path of a single use case

# The cJSON project 

- I select the  `cJSON` project to do my test work.  This is a ultralight weight JSON parser in ANSI C. I downloaded the source code from github: 

  ```shell
  git clone https://github.com/DaveGamble/cJSON.git
  ```

  

- Then I use the `cloc` tool to counts, and computes differences of, comment lines, blank lines, and physical lines of source code in `cJSON` project.  

  ```shell
  sudo yum install cloc
  cloc .
  ```

  From this figure, we learn this `cJSON` project has 3594  code lines in two files (except test program).

![1589859992627](C:\Users\wjq\AppData\Roaming\Typora\typora-user-images\1589859992627.png)
	

3. I analyze the source code to learn about the feature of functions' input and output. Here I list several functions in `cJSON.c` : 

| Function name           | Input type                                  | Output type |
| ----------------------- | ------------------------------------------- | ----------- |
| cJSON_CreateObject      | void                                        | cJSON*      |
| cJSON_AddNumberToObject | cJSON * const , const char * , const double | cJSON *     |
| cJSON_Delete            | cJSON *                                     | void        |
| cJSON_Print             | const cJSON *                               | char *      |
| cJSON_CreateNumber      | double                                      | cJSON*      |
| cJSON_New_Item          | const internal_hooks * const                | cJSON*      |

