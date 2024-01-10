# Round 1
Scenario There is a customer who came to you with a problem to have a custom linux command for his operations. Our task is to understand the problem and create a linux command via bash script as per the instructions.

Command name - internsctl                                                                                                                                                                        



Command version - v0.1.0

## section A
I want a manual page of command so that I can see the full documentation of the command. For example if you execute the command man ls as output we get the doc and usage guidelines. Similarly if I execute man internsctl I want to see the manual of my command.

Each linux command has an option --help which helps the end user to understand the use cases via examples. Similarly if I execute internsctl --help it should provide me the necessary help

I want to see version of my command by executing internsctl --version

Answer:

 **1. creating a  (manual) md file**

nano internsctl.1.md
pandoc -s internsctl.1.md -t man -o internsctl.1
sudo mv internsctl.1 /usr/share/man/man1/

im also executing **sudo cp internsctl /usr/local/bin/** so i can directly type **internsctl** instead of ./internsctl**
sudo cp internsctl /usr/local/bin/

**2.(help command)**: 


**Execution**: 
internsctl --help

-- **3. (version command)**


**Execution**: 
internsctl --version


## section B

I want to execute the following command for -
Part1 | Level Easy


**1. Cpu information**

if [ "$1" == "cpu" ] && [ "$2" == "getinfo" ]; then
    # CPU Information
    lscpu
    exit 0
Fi

**Execution**: 
internsctl cpu getinfo


**2. Memory information**

if [ "$1" == "memory" ] && [ "$2" == "getinfo" ]; then
    # Memory Information
    free -h
    exit 0
Fi


**Execution**: 
Internsctl memory getinfo






