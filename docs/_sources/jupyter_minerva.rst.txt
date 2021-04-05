Running Jupyter on Minerva 
==========================

Install a python virtual environment (once)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
    
    . /home/SPACK2019/share/spack/setup-env.sh
    spack list  # lists many modules
    spack info python  # lists available python versions
    spack load python  # defaults to 3.7
    python -m venv python37_venv
    source python37_venv/bin/activate
    module purge # sergei says 'or things get weird' ??still needed??
    which pip   # sanity check - this should refer to the 'pip' form the virtual env
    pip install --upgrade pip
    pip install jupyterlab scipy h5py seaborn astropy pandas 
    pip install lalsuite # if desired

If you're using SpEC, you might also want to get diagnose-spec installed:

.. code-block:: bash

    cd ~
    git clone git@github.com:nilsleiffischer/diagnose-spec.git
    which pip   # sanity check - this MUST refer to the 'pip' form the virtual env
    pip install -e ~/diagnose-spec  

Prepare ssh on your laptop/desktop (once)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Pick a port number 'xxxx' somewhere above 8800. Use the same number throughout. Now edit your local .ssh/config file to contain:

.. code-block:: bash

    # your_laptop/.ssh/config
    #  ... 
    # AEI
    host minerva01
    hostname      minerva01.aei.mpg.de
    ForwardAgent  yes
    user          your_minerva_username
    #
    # ssh-tunnel to access jupyter on minerva:
    host minerva01_jupyter
    hostname      minerva01.aei.mpg.de
    user          your_minerva_username
    LocalForward  xxxx localhost:xxxx

To actually use jupyter, repeat these steps:

- In *one* terminal, lauch the jupyter server on minerva, and keep it running:

.. code-block:: bash

    ssh minerva01
    module purge; . /home/SPACK2019/share/spack/setup-env.sh; spack load libpng
    source python37_venv/bin/activate
    jupyter lab --no-browser --port xxxx

Starting the jupyter server will print some text with info how to connect. You will need this text soon.

- In *another* terminal, activate the ssh-tunnel with port-forwarding: `ssh minerva01_jupyter`. Leave this connection open!
- In a web-browser on your laptop, go to the web-page mentioned in the first bullet.


