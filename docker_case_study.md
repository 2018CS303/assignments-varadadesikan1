# **Docker Case Study ** - Automate Infra allocation for L&D

### Basic requirements :
- Dynamic Allocation of Linux systems for users
- Each user should have independent Linux System
- Specific training environment should be created in Container
- User should not allow to access other containers/images
- User should not allow to access docker command
- Monitor participants containers
- Debug/live demo for the participants if they have any doubts/bug in running applications. 
- Automate container creation and deletion.

## Allocating Linux systems To Users
1.  Create the shell script `createContainers.sh` which will automatically create a docker container for every user using specific docker environment image.

    - `users.txt`
        ```
        John
        James
        Jackson
        ```
    - `createContainers.sh`
        ```sh
        echo -n "Enter file containing usernames: "
        read file
        while read user
            do 
                docker create -it --name $user <Docker Img> /bin/bash #If <Docker img> is the required image
            done < $file
        ```
2.  Complete `users.txt` with usernames and run `createContainers.sh`. The docker container created, corresponds to each username from `users.txt`.
3.  Now the user can start using the allocated container by running `useContainers.sh`.
    - `useContainers.sh`
        ```sh
        echo -n "Enter your username: "
        read name
        docker start $name
        docker attach $name
        ```

## Monitoring The Containers
- To monitor the containers, use `monitorContainers.sh`.
    - `monitorContainers.sh`
        ```sh
        echo -n "Enter the name of the container to be monitored: "
        read name
        docker logs -f $name
        ```
-It shows the live bash display which helps in bug fixing and doubts.
 
## Deleting The Containers
- Automate the deletion using the `deleteContainers.sh` script.

    - `deleteContainers.sh`
        ```sh
        echo -n "Enter 'all' to delete all user containers or enter 'user' to delete a specific user container: "
        read typ
        if [ "$typ" == "all" ]
        then
                echo -n "Enter the user list file: "
                read file
        while read user
        do
                docker rm $user
        done < $file
        else
                echo -n "Enter the username: "
                read name
                docker rm $name
        fi
	```
- You can either delete all users or user by name using `deleteContainers.sh`.
