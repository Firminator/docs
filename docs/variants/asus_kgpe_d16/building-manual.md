# Dasharo for Asus KGPE-D16 - building manual

## Building coreboot

To build coreboot image, follow the steps below:

1. Clone the coreboot repository:

    ```bash
    $ git clone https://review.coreboot.org/coreboot.git
    ```

2. Get the submodules:

    ```bash
    $ cd coreboot
    $ git submodule update --init --recursive --checkout
    ```

3. Checkout Dasharo branch for KGPE-D16:

    ```bash
    $ git remote add dasharo https://github.com/dasharo/coreboot.git
    $ git fetch dasharo
    $ git checkout asus_kgpe-d16/develop
    ```

4. Start docker container:

    ```bash
    $ docker run --rm -it \
       -v $PWD:/home/coreboot/coreboot \
       -w /home/coreboot/coreboot \
       coreboot/coreboot-sdk:0ad5fbd48d /bin/bash
    ```

5. Inside of the container, configure and start the build process:

    ```bash
    (docker)$ cp configs/config.asus_kgpe_d16 .config
    (docker)$ make olddefconfig
    (docker)$ make
    ```

This will produce a debug binary placed in `build/coreboot.rom`. To flash
coreboot refer to [Flashing section in the hardware setup page.](setup.md#flashing)