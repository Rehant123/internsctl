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
![Uploading x4.png…]()


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
![Uploading x7.png…]()

./internsctl.sh user list ##user list
 ./internsctl.sh user list --sudo-only ##user with sudo permission
```

