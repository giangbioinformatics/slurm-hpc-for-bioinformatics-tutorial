Connecting to RC
=================

Access to RC systems is primarily through the Secure Shell Protocol (SSH). This involves establishing a connection to the login node, where users can then access the system. Similarly, it's worth noting that normal machines like your own server or an EC2 instance of AWS can also be accessed using SSH.

Initially, users typically authenticate using a password. However, it's recommended to enhance security by adding an RSA key pair to the server. With this setup, users can access the system without entering a password each time.

The RSA key pair consists of a public key, which is copied to the server, and a private key, which remains on the user's local machine. This method offers increased security and convenience.

Upon the first login, users are prompted to set a new password for their account, ensuring a secure login process.

For Linux and Mac users, SSH can be accessed directly from the terminal. On the other hand, Windows users have options such as PuTTY or Windows Subsystem for Linux (WSL) for SSH access.

As domains or IP addresses may change over time, it's advisable to regularly check the RC website for the most up-to-date information on accessing the systems.


Prerequisites
-------------

Install ssh client on your local machine::
    
        sudo apt-get install openssh-client

For Windows users, you can use PuTTY or Windows Subsystem for Linux (WSL) for SSH access.
Follow here for more information: https://www.ssh.com/academy/ssh/putty/windows


Login to the RC
----------------
Currently, the hostname for RC is set up using the DDNS service. The hostname is `giangnguyen.zapto.org` and the port is `1234`. 
The username is your username on the RC cluster. If the hostname or port changes, please check the RC website for the most up-to-date information.

To connect to the RC cluster using password::

    ssh <your username>@giangnguyen.zapto.org

Using the rsa key, it will be copied to the server. However, you must type password for the first time set up

To connect to the RC cluster without using password

Step 1: Copy rsa key to the server, create key if not exists::

    yes n | ssh-keygen -q -t rsa -f ~/.ssh/id_rsa -C "" -N "" || echo "key exists"

Step 2: Currently, to keep the cluster more security, the river cluster only allows user to login using rsa key, send me your email to
``nttg8100@gmail.com`` to get support using jira and slack. After that, you will receive the documentation for how to use the HPC effectively.

Step 3: Optional, alias your login command, copy this line put this to your bashrc to use this quickly::

    alias rc='ssh <your username>@giangnguyen.zapto.org -p 1234'
    # check the new alias
    rc

Step 4: Next time, you can login to the RC cluster by typing `rc`, to do so, you have to add this line to your bashrc::

    # copy to your bashrc
    printf "\nalias rc='ssh <your username>@giangnguyen.zapto.org -p 1234'" >> ~/.bashrc
    souce ~/.bashrc
    # login again
    rc

Keep your connection alive using screen
-------------------------------------------

When you login to the login node, it is recommended to use `screen` to keep your connection alive. This is especially useful when you are running a long job.
If you do not use ``screen`` or ``tmux ``, when you disconnect from the remote machine, you will lose all the progress of your job.

1. **Start a New Screen Session**: Enter the following command to start a new screen session::

       screen -S my_session

   Replace `my_session` with a descriptive name for your screen session.

2. **Detach from the Screen Session**: Press `Ctrl + A`, followed by `Ctrl + D`, to detach from the screen session. You will return to the regular shell prompt, but the screen session will continue running in the background.

Submitting Jobs to SLURM within the Screen Session
---------------------------------------------------

To submit a job to SLURM within the screen session, follow the same steps as outlined previously in the document "Submitting Jobs to SLURM".

Accessing and Managing Screen Sessions
---------------------------------------

To reattach to a detached screen session, use the following command::

    screen -r my_session

Replace `my_session` with the name of your screen session.

You can list all available screen sessions using::

    screen -ls


Example for your screen list::

    There is a screen on:
        28811.test      (04/28/2024 10:08:51 AM)        (Attached)
    1 Socket in /run/screen/S-vagrant.

To kill the screen session::
    
        screen -X -S <your session name| your session id> kill
        # example
        screen -X -S my_session kill

