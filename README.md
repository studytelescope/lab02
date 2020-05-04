## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

Set up environment variables

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
# Set up global variables GITHUB_USERNAME, GITHUB_EMAIL, GITHUB_TOKEN
$ export GITHUB_USERNAME=thedraftaccount
$ export GITHUB_EMAIL=jonnyuz99@gmail.com
$ export GITHUB_TOKEN=8e3dc38d17f2e0cfdde2016a74e5555a1c610592

# Setting default text redactor
$ alias edit=subl
```

Set up workspace environment

```ShellSession
# Getting into workspace directory
$ cd ${GITHUB_USERNAME}/workspace

# Launching scripts/activate
$ source scripts/activate
```

Update .config file

```ShellSession
# Creating .config file
$ mkdir ~/.config

# Writing token, username and protocol into .config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF

# Configuration of transmittion protocol
$ git config --global hub.protocol https
```

Init project directory and push README.md

```ShellSession
# Creating and getting into task folders
$ mkdir projects/lab02 && cd projects/lab02

# Creation of an empty local repo
$ git init
Initialized empty Git repository in /home/johnsnow/thedraftaccount/workspace/projects/lab02/.git/

# Initialization of a user for this repo
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}

# check your git global settings
$ git config -e --global

# Linking of remote repo with a local one
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git

# Getting files from the master branch
$ git pull origin master
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/thedraftaccount/lab02
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master

# Creating README.md
$ touch README.md

# Checking untracked files, commiting them and pushing into remote repo
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)

# Add changes of README.md and push commit to origin
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```

Pull remote changes

```ShellSession
# Getting files from the master branch
$ git pull origin master
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/thedraftaccount/lab02
 * branch            master     -> FETCH_HEAD
   65e30fc..00f30cb  master     -> origin/master
Updating 65e30fc..00f30cb
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore


# Show commits
$ git log
Author: thedraftaccount <63643996+thedraftaccount@users.noreply.github.com>
Date:   Sun Apr 19 13:57:52 2020 +0300

    Create .gitignore

commit 65e30fc0a283cf975c8fbcd3a69788804f4c59e1
Author: thedraftaccount <63643996+thedraftaccount@users.noreply.github.com>
Date:   Sun Apr 19 13:56:22 2020 +0300

    Initial commit

```

Set up project tree environment

```ShellSession
# Creating directories
$ mkdir sources
$ mkdir include
$ mkdir examples

# Writing some useless code
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

Update include/print.hpp

```ShellSession
# Writing some useless code
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

Update include/example1.cpp

```ShellSession
# Writing some useless code
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

Update include/example2.cpp

```ShellSession
# Writing some useless code
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```ShellSession
# Looking into README file
$ edit README.md
```

Commit and push local changes

```ShellSession
# Looking for untracked files
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

  README.md
  examples/
  include/
  sources/

nothing added to commit but untracked files present (use "git add" to track)


# Adding of all files, commiting and pushing into master branch
$ git add .
$ git commit -m "added sources"
[master b50a223] added sources
 5 files changed, 275 insertions(+)
 create mode 100644 README.md
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp

$ git push origin master // push into master
Username for 'https://github.com': thedraftaccount  
Password for 'https://thedraftaccount@github.com': 
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (10/10), 3.11 KiB | 1.04 MiB/s, done.
Total 10 (delta 0), reused 0 (delta 0)
To https://github.com/thedraftaccount/lab02.git
   00f30cb..b50a223  master -> master
```

## Report

```ShellSession
# Creation of repo
$ cd ~/workspace/

# Getting data from "lab02" remote repo
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}

# Creating lab02 folder
$ mkdir reports/lab${LAB_NUMBER}

# Copying files from repo
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}

# Report
$ edit REPORT.md

# Gisting of a report
$ gist REPORT.md
```
Copyright (c) 2015-2019 The ISC Authors
```