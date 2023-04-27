# MPI-Cluster
## Making an MPI Cluster using two PCS, one master, and the other slave, on the same LAN



### Configuration for the Master PC 
Make sure you’re logged in on your Ubuntu system using an ID which has sudo access

Open the terminal


Create a new user called 'mpiuser'
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


Install OpemMPI
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

After you're done writing them, use the following keyboard shortcuts to properly write to and exit the file
"Ctrl+o               enter                  Ctrl+x"


Generate a key (When prompted DO NOT enter any passphrase)
```
ssh-keygen
```

Copy the generated key onto the slave PC (make sure to replace the prompts below with your own ip addresses)
```
ssh-copy-id yourmasterusername@slave-ip-address
```

Test the SSH connection to the slave computer:
```
ssh yourmasterusername@slave-ip-address
```

It should be able to log in to the terminal of the slave PC

Now exit from being logged into the slave pc
```
exit
```


Now switch users and login to the mpiuser you created (It will be saved as the First Name you chose)


Write an mpi program (hello world in this case) and save the file with the same name and in the same directory for both the PCs (I will be putting it in Documents)
Our program (cited from: https://mpitutorial.com/tutorials/mpi-hello-world/ ):

Open the terminal


Change the directory to the place where you saved your mpi program's file (Documents in our case)
```
cd Documents
```

Compile the mpi program's file
```
mpicc mpihelloworld.c -o mpi_hello_world
```

Now finally execute the file on your master computer

```
mpiexec --oversubscribe -n 20 -host <master-ip-address>,<slave-ip-address> ./<the executable mpi file’s name>
```

In our case: mpiexec --oversubscribe -n 20 -host 10.2.70.156,10.2.70.78 ./mpi_hello_world

VOILA IT IS WORKING!















Slave
Open terminal
sudo adduser mpiuser

Gives sudo access to the newly created user
sudo usermod -aG sudo mpiuser
su mpiuser
sudo apt-get install openmpi-bin
sudo apt-get install openssh-server
Get your IP address using ifconfig
sudo nano /etc/hosts
Master <master up address> 
Slave <slave ip address>
Ctrl+o               enter                  Ctrl+x

Test the SSH connection to the master computer:
ssh yourusername@master-ip-address

Now exit from being logged into the master pc:
exit
Okay now switch users and login to the mpiuser you created (It will be saved as the name you chose)
Write an mpi program (hello world in this case) and save the file with the same name and in the same directory for both the computers (I will be putting it in Documents)
Our program (cited from: https://mpitutorial.com/tutorials/mpi-hello-world/ ):


cd Documents
mpicc mpihelloworld.c -o mpi_hello_world



