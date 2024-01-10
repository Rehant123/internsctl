![x4](https://github.com/Rehant123/internsctl/assets/74208153/7d4f3bf0-4407-4ecb-bbc3-311194661a22)Website (source code)

https://github.com/Rehant123/projecetintern

screenshot
![Screenshot 2024-01-10 172756](https://github.com/Rehant123/internsctl/assets/74208153/5722f5f7-2dcf-4019-9717-3872f82fc2c5)

# Round 1
Scenario There is a customer who came to you with a problem to have a custom linux command for his operations. Our task is to understand the problem and create a linux command via bash script as per the instructions.

Command name - internsctl                                                                                                                                                                        



Command version - v0.1.0

## section A
I want a manual page of command so that I can see the full documentation of the command. For example if you execute the command man ls as output we get the doc and usage guidelines. Similarly if I execute man internsctl I want to see the manual of my command.

Each linux command has an option --help which helps the end user to understand the use cases via examples. Similarly if I execute internsctl --help it should provide me the necessary help

I want to see version of my command by executing internsctl --version

Answer:

 **1. creating a  (manual) md file and help**

```
#!/bin/bash

function display_help() {
    echo "Usage: internsctl [OPTIONS] <COMMAND>"
    echo "Custom Linux Command for Operations"
    echo ""
    echo "Options:"
    echo "  ‐‐help           Display this help message"
    echo "  ‐‐version        Display the command version"
    echo ""
    echo "Commands:"
    echo "  cpu getinfo      Display CPU information"
    echo "  memory getinfo   Display memory information"
    echo "  user create <username>   Create a new user"
    echo "  user list [‐‐sudo‐only]  List users (optionally, only
those with sudo permissions)"
    echo ""
    echo "Examples:"
    echo "  Display CPU information:"
    echo "    internsctl cpu getinfo"
    echo ""
    echo "  Display memory information:"
    echo "    internsctl memory getinfo"
    echo ""
    echo "  Create a new user:"
    echo "    internsctl user create rehant_thapa"
    echo ""
    echo "  List all users:"
    echo "    internsctl user list"
}


```
internsctl.md
```
# internsctl Manual

`internsctl` is a custom Linux command designed for various system operations.

## Usage

```bash
internsctl [OPTIONS]

```

**Execution**: 
```
man ./internsctl.sh

./internsctl.sh --help
```

output
![x1](https://github.com/Rehant123/internsctl/assets/74208153/1fdb5bfa-a94c-4c67-80b8-76cb98fd81fc)

![x2](https://github.com/Rehant123/internsctl/assets/74208153/fa9874ec-7246-445e-80c6-34ddfc778a4f)

-- **(version command)**
```
function display_version() {
  echo "internsctl v0.1.0"
}
```
**Execution**: 
```
 ./internsctl.sh --version
```
![x3](https://github.com/Rehant123/internsctl/assets/74208153/48eae053-9b52-455a-8df4-59ef44bc5451)

## section B

### Part1 | Level Easy -




**1. Cpu information**
```
function get_cpu_info() {
  lscpu
}
```
**Execution**: 
```
 ./internsctl.sh cpu getinfo
```

Output
![x4](https://github.com/Rehant123/internsctl/assets/74208153/04163fb8-1ec1-46a1-8906-f792deb9067f)


**2. Memory information**

create a function getmemory info
```
function get_memory_info() {
  free
}
![x6](https://github.com/Rehant123/internsctl/assets/74208153/5f46e443-7fc3-4208-a84a-bd02c1efcc5b)


```
**Execution**: 
```
 ```
Output
![x6](https://github.com/Rehant123/internsctl/assets/74208153/15b7be98-64ea-4936-8003-313afb6fddd9)

 ### Part 2 Level Intermediate

**1.I want to create a new user on my server through the following command:**
**2I want to list all the regular users present on my server through the following command:**
**3 If want to list all the users with sudo permissions on my server through the following command:**


answer:
```
function create_user() {
    if [ -z "$2" ]; then
        echo "Error: Missing username. Usage: internsctl user create <username>"
        exit 1
    fi

    sudo useradd -m "$2"
    echo "User '$2' created successfully."
}

function list_users() {
    cut -d: -f1 /etc/passwd
}

function list_sudo_users() {
    getent group sudo | cut -d: -f4 | tr ',' '\n'
}

case "$1" in
    user)
        if [ "$2" == "create" ]; then
            create_user "$@"
        elif [ "$2" == "list" ]; then
            if [ "$3" == "--sudo-only" ]; then
                list_sudo_users
            else
                list_users
            fi
        else
            echo "Invalid subcommand for 'user'. "
            exit 1
        fi
        ;;
    *)
        echo "Invalid option. Use 'internsctl --help' for usage guidelines."
        exit 1
        ;;
esac

```
**execution**

```
./internsctl.sh user create <username> ##new user

./internsctl.sh user list ##user list


 ./internsctl.sh user list --sudo-only ##user with sudo permission
```
![x7](https://github.com/Rehant123/internsctl/assets/74208153/42ac307b-9f98-413d-9e8a-5243e66055da)

![Screenshot 2024-01-10 174534](https://github.com/Rehant123/internsctl/assets/74208153/c2d94324-542f-4685-8896-3460e60867be)
![Screenshot 2024-01-10 174706](https://github.com/Rehant123/internsctl/assets/74208153/b9272adc-93ea-4c9b-a8f6-9f792f74b7d7)
