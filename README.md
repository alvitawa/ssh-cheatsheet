    
Connect to UvA VPN

Make key and register it with DAS5:

    ssh-keygen
    ssh-copy-id kics2001@fs1.das5.liacs.nl

Copy all files to das5

    cd optimizationlab
    scp * kics2001@fs1.das5.liacs.nl:

Log in to das5

    ssh kics2001@fs1.das5.liacs.nl

## Test on das5

1. Modify driver.py, set ON_DAS5=True
2. Copy updated driver.py to DAS5:

    scp driver.py kics2001@fs1.das5.liacs.nl:

3. Log in to das5 and run (once):

    chmod +x driver.py

4. You can build and test the files when logged in to DAS5:

    make
    module load prun
    ./driver.py

4. Or you can build files locally and copy the binaries to DAS5:

    make
    scp k_nearest_seq kics2001@fs1.das5.liacs.nl:
    ssh kics2001@fs1.das5.liacs.nl "module load prun; ./driver.py"


## Here is a script that will build the binaries locally, upload all of them to DAS5 and test them there

    #!/bin/bash

    make
    scp k_nearest_seq kics2001@fs1.das5.liacs.nl:
    scp k_nearest_simd kics2001@fs1.das5.liacs.nl:
    scp k_nearest_thread kics2001@fs1.das5.liacs.nl:
    ssh kics2001@fs1.das5.liacs.nl "module load prun; ./driver.py"

Save to `test.sh` for example, and run with `./test.sh` (Do `chmod +x test.sh` first once)

## Tip: make a ssh configuration for DAS5

`~/.ssh/config`

    Host das
        User kics2001
        HostName fs1.das5.liacs.nl

Then you can replace the use of `kics2001@fs1.das5.liacs.nl` on ssh calls everywhere with just `das`.

For eaxmple `ssh das` or `scp driver.py das:`

## Alternative: Use VSCode Remote to do everything on the DAS5