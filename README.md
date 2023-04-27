# MPI-Cluster
## Making an MPI Cluster using two computers on the same LAN



# Master PC 
<sup> Make sure you’re logged in on your Ubuntu system using an ID which has sudo access <sup/>

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
ssh your-master-username@slave-ip-address
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

⚠️ Ensure the program is saved in the same directory on the slave PC. 
Also ensure that it has been compiled on the slave PC.

Now finally execute the file on your master computer

```
mpiexec --oversubscribe -n 20 -host <master-ip-address>,<slave-ip-address> ./<the executable mpi file’s name>
```

In our case: mpiexec --oversubscribe -n 20 -host 10.2.70.156,10.2.70.78 ./mpi_hello_world

🎉 VOILA IT IS WORKING!















# Slave PC
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

After you're done writing them, use the following keyboard shortcuts to properly write to and exit the file
"Ctrl+o               enter                  Ctrl+x"


Ensure the Master PC has done generating a key and copying it onto your PC

Test the SSH connection to the master computer
```
ssh your-slave-username@master-ip-address
```

It should be able to log in to the terminal of the master PC

Now exit from being logged into the master pc
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

Go check with your master PC and see if the program is executing as expected (fingers crossed it is 🤞)



