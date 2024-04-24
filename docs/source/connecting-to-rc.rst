Connecting to RC
=================

Access to ARC systems is via Secure Shell Protocol (SSH).

Fingerprints for the login node host keys can be found `here <https://arc-user-guide.readthedocs.io/en/latest/arc-host-keys.html>`_

Connecting from Linux
---------------------

Linux and Mac users should use ssh from a terminal to connect to the RC systems.
The domain or ip address will be updated in the future, so please check the RC website for the latest information.

To connect to the RC cluster using password::

    ssh username@<domain.name|IP address> -p 1234

Using the rsa key, it will be copied to the server. However, you must type password for the first time set up

To connect to the RC cluster without using password

Step 1: Copy rsa key to the server::

    ssh-copy-id username@<domain.name|IP address> -i ~/.ssh/id_rsa.pub

Step 2 Login again, this time do not need to type password::

    ssh username@<domain.name|IP address> -p 1234

Step 3: Optional, alias your login command, copy this line put the th::

    # copy to your bashrc
    printf "\nalias rc='ssh username@<domain.name|IP address> -p 1234'" >> ~/.bashrc
    souce ~/.bashrc
    # login again
    rc
    