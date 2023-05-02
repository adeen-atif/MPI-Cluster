# Making an MPI Cluster within a LAN
⚠️ There are 2 seperate configuration sections for the Master and Slave PC in this guide (utilize accordingly)



# Master Computer 

Open the terminal


Create a new user called 'mpiuser'
```
sudo adduser mpiuser 
```


Give sudo access to the newly created user
```
sudo usermod -aG sudo mpiuser
```


Install OpenMPI
```
sudo apt-get install openmpi-bin
```


Install SSH 
```
sudo apt-get install openssh-server
```


Get your IP address 
```
ifconfig
```

Add the IP addresses of master and slave PCs to the host file
```
sudo nano /etc/hosts
```

```
Master <master up address> 
Slave <slave ip address>
```

![My Image](1.png)



Generate a key
```
ssh-keygen
```

Copy the generated key onto the slave PC (make sure to replace the prompts below with your own ip addresses)
```
ssh-copy-id username@ip-address
```

Test the SSH connection to the slave computer:
```
ssh username@ip-address
```

It should be able to log in to the terminal of the slave PC
![My Image](2.png)


Now exit from being logged into the slave pc
```
exit
```


Now switch users and login to the mpiuser you created (It will be saved as the First Name you chose)


Write an mpi program (hello world in this case) and save the file with the same name and in the same directory for both the PCs (I will be putting it in Documents).
Our program was taken from: https://mpitutorial.com/tutorials/mpi-hello-world/

Open the terminal


Change the directory to the place where you saved your mpi program's file (Documents in our case)
```
cd Documents
```

Compile the mpi program's file
```
mpicc mpihelloworld.c -o mpi_hello_world
```
![My Image](3.png)

⚠️ Ensure the program is saved in the same directory on the slave PC. 
⚠️ Ensure the program has been compiled on the slave PC.

Now finally execute the file on your master computer

```
mpiexec -n 20 -host <master-ip-address>,<slave-ip-address> ./<the executable mpi file’s name>
```

In our case: mpiexec -n 20 -host 10.2.70.156,10.2.70.78 ./mpi_hello_world
![My Image](4.png)


### 🎉 TADA IT IS WORKING!

<br>












# Slave Computer
Make sure you’re logged in on your Ubuntu system using a user which has sudo access 






Open terminal

Make a new user
```
sudo adduser mpiuser
```


Give sudo access to the newly created user
```
sudo usermod -aG sudo mpiuser
```

To execute commands with the priveleges of the newly created user
```
su mpiuser
```


Install OpenMPI
```
sudo apt-get install openmpi-bin
```


Install SSH 
```
sudo apt-get install openssh-server
```


Get your IP address 
```
ifconfig
```

Add the IP addresses of master and slave PCs to the host file
```
sudo nano /etc/hosts
```

```
Master <master up address> 
Slave <slave ip address>
```

![My Image](1.png)



⚠️ Ensure the Master PC is done generating a key and copying it onto your PC

Test the SSH connection to the master computer
```
ssh username@ip-address
```

It should be able to log in to the terminal of the master PC
![My Image](2.png)


Now exit from being logged into the master pc
```
exit
```

Now switch users and login to the mpiuser you created (It will be saved as the First Name you chose)


Write an mpi program (hello world in this case) and save the file with the same name and in the same directory for both the PCs (I will be putting it in Documents).
Our program was taken from: https://mpitutorial.com/tutorials/mpi-hello-world/

Open the terminal


Change the directory to the place where you saved your mpi program's file (Documents in our case)
```
cd Documents
```

Compile the mpi program's file
```
mpicc mpihelloworld.c -o mpi_hello_world
```
![My Image](3.png)


Go check with your master PC and see if the program is executing as expected (fingers crossed it is 🤞)

<br>

#### Collaborator: Maaz Bin Adnan





