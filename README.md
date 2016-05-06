# cherrypy-docker-skeleton

#############################################################
#                                                           #
#                      READ-ME                              #
#                                                           #
#############################################################

TUTORIAL USED AS REFERENCE:
---> https://www.digitalocean.com/community/tutorials/docker-explained-how-to-containerize-python-web-applications

Steps to make the docker container work:

1. Launch an AWS EC2 instance with the latest ubuntu
2. While launching instance, make sure to open port 22 for SSH and port 80 for HTTP traffic
3. Change permissions to the private key using:
        chmod 600 path/to/private/key/<private_key_name>.pem
4. Access the instance with the command:
        ssh -i path/to/private/key/<private_key_name>.pem ubuntu@ec2-server-name.compute-1.amazonaws.com
5. Install docker
        a. sudo aptitude update
        b. sudo aptitude -y upgrade
        c. sudo aptitude install linux-image-extra-`uname -r`
        d. sudo sh -c "wget -qO- https://get.docker.io/gpg | apt-key add -"
        e. sudo sh -c "echo deb http://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
        f. sudo aptitude update
        g. sudo aptitude install lxc-docker
        h. sudo vim /etc/default/ufw
                -> REPLACE : DEFAULT_FORWARD_POLICY="DROP"
                -> WITH : DEFAULT_FORWARD_POLICY="ACCEPT"
        i. sudo ufw reload
6. Copy the following folder structure at $HOME:
        -> Dockerfile
        -> my_application
            |
            ------ app.py
            |
            ------ requirements.py
            |
            ------ server.py
7. Run the command to create the image for the docker container:
        sudo docker build -t my_application_img .
8. Run the following command to create and start the docker container of the name "my_application-instance-3":
        sudo docker run --name=my_application-instance-3 -p 80:80 -d my_application_img
9. Using the public ip of the AWS instance, run:
        http://<ip address>
        You will get Hello World!

Some docker commands that are useful:
sudo docker ps -> to look at active containers
sudo docker ps -a -> to look at all containers