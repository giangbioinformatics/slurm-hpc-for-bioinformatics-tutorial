Code-server
===========

Code-server, a variant of Visual Studio Code (VSCode), operates on a distant server, enabling access to VSCode via a web browser. It's an invaluable tool for developers opting to code remotely or preferring a browser-based coding experience. Specifically, installed solely on worker nodes, Code-server facilitates job submission via "ssh tunnel," directing the local port of the worker node's code-server to the login node. The login node is configured with an "sshd service," accessible through the domain of said login node.

Submit the sbatch job
---------------------
Please, adjust your password to a secure one instead of `1234` and the time for using the requested resources `4:00:00` in the following script.
To submit the sbatch job, run the following command::
    
    # create output to get the code-server log 
    mkdir -p ~/code_server
    
    # create the sbatch script
    cat <<'EOF' > code_server_script.sh
    #!/bin/bash 
    #SBATCH --job-name=code-server
    #SBATCH --time=04:00:00
    #SBATCH --output=~/code_server/code_server_%N.log 
    #SBATCH --mem=1gb 
    #SBATCH --cpus-per-task=1

    PASSWORD=1234 # TODO: Change to secure password
    PORT=$(python3 -c 'import socket; s=socket.socket(); s.bind(("", 0)); print(s.getsockname()[1]); s.close()')
    echo "********************************************************************" 
    echo "Starting code-server in Slurm"
    echo "Environment information:" 
    echo "Date:" $(date)
    echo "Allocated node:" $(hostname)
    echo "Node IP:" $(ip a | grep 192.168)
    echo "Path:" $(pwd)
    echo "Password to access VSCode:" $PASSWORD
    echo "Listening on:" $PORT
    echo "********************************************************************"
    PASSWORD=$PASSWORD code-server --bind-addr 0.0.0.0:$PORT --auth password --disable-telemetry
    EOF

    # submit the sbatch job
    sbatch code_server_script.sh

Access the code-server
----------------------

To get log of the code-server, run the following command::

    # get the port
    cat ~/code_server/code_server_worker.log
    Environment information:
    Date: Tue 30 Apr 2024 05:33:36 PM UTC
    Allocated node: worker
    Node IP: <IP address>
    Path: /home/<username>
    Password to access VSCode: 1234
    Listening on: 36333
    ********************************************************************
    [2024-04-30T17:33:36.833Z] info  code-server 4.23.1 9a28bc29dbddb6886dfe03dc1c31320249a901ce
    [2024-04-30T17:33:36.834Z] info  Using user-data-dir /home/<username>/.local/share/code-server
    [2024-04-30T17:33:36.840Z] info  Using config file /home/<username>/.config/code-server/config.yaml
    [2024-04-30T17:33:36.840Z] info  HTTP server listening on http://0.0.0.0:36333/
    [2024-04-30T17:33:36.840Z] info    - Authentication is enabled
    [2024-04-30T17:33:36.840Z] info      - Using password from $PASSWORD
    [2024-04-30T17:33:36.840Z] info    - Not serving HTTPS
    [2024-04-30T17:33:36.840Z] info  Session server listening on /home/<username>/.local/share/code-server/code-server-ipc.sock

    
Access the code-server using ssh tunnel, replace ip and the username ::

    ssh -N -L 8080:<replace with the ip that you found >:<running port> <username>@giangnguyen.zapto.org

Open the browser and type the following URL::

    http://localhost:8080


After finishing the work, please cancel the job to free the resources::

    # check at the ``Submission Script Basics`` section to get the job_id
    scancel <job_id>
