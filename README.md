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



im also executing **sudo cp internsctl /usr/local/bin/** so i can directly type **internsctl** instead of ./internsctl**
sudo cp internsctl /usr/local/bin/

**2.(help command)**: 


**Execution**: 
internsctl --help

-- **3. (version command)**

function display_version() {
  echo "internsctl v0.1.0"
}

**Execution**: 
 ./internsctl.sh --version


## section B

### Part1 | Level Easy -



**1. Cpu information**

function get_cpu_info() {
  lscpu
}

**Execution**: 
 ./internsctl.sh cpu getinfo


**2. Memory information**

create a function getmemory info

function get_memory_info() {
  free
}


**Execution**: 
 ./internsctl.sh memory getinfo


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
new user-> ./internsctl.sh user create <username>
user list-> ./internsctl.sh user list
user with permission-> ./internsctl.sh user list --sudo-only

