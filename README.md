# MPI-Cluster
## Making an MPI Cluster using two PCS, one master, and the other slave, on the same LAN



### Configuration for the Master PC 
Make sure you’re logged in on your Ubuntu system using an ID which has sudo access

Open terminal
''' sudo adduser mpiuser '''

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

ssh-keygen

DO NOT ENTER ANY PASSPHRASE
ssh-copy-id yourusername@second_pc_ip_address

Test the SSH connection to the slave computer:
ssh username@slave-ip-address

Now exit from being logged into the slave pc:
Exit
Okay now switch users and login to the mpiuser you created (It will be saved as the name you chose)
Write an mpi program (hello world in this case) and save the file with the same name and in the same directory for both the computers (I will be putting it in Documents)
Our program (cited from: https://mpitutorial.com/tutorials/mpi-hello-world/ ):


cd Documents
mpicc mpihelloworld.c -o mpi_hello_world

Now finally execute the file on your master computer
mpiexec --oversubscribe -n 20 -host <master-ip-address>,<slave-ip-address> ./<the executable mpi file’s name>
In our case: mpiexec --oversubscribe -n 20 -host 10.2.70.156,10.2.70.78 ./mpi_hello_world

TADA WORKING















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



