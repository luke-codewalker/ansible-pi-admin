# SSH Setup

As I'm using a headless variant of the Raspberry Pi OS my main way of managing the Pi (also used by Ansible) is SSH. Currently I have the image flasher setup in a way that enables password based SSH from the start. However I want document the setup for key-based SSH.
In particular I will add key-based SSH without a password on the private key. While this is definitely less secure it increases my convenience (later I could also think about adding a passphrase and setting up ssh-agent etc.) and I will definitely have bigger problems than access to my Pis if someone is able to read my private SSH keys.

## Steps:

1. SSH is enabled on Pi (currently enabled when burning image with password)
2. Generate private public key pair on control machine: `ssh-keygen -t rsa` 
    - specify name as `~/.ssh/raspberrypi_rsa`
    - enter no passphrase
    - verify it worked with `ls ~/.ssh` 

3. Copy the public key to the Pi with: `ssh-copy-id -i ~/.ssh/raspberrypi_rsa.pub <user>@<address>`
4. Configure authentication methods on Pi with `sudo nano /etc/ssh/sshd_config`
    - adding/editing the following lines:
        ```	
        PermitRootLogin no
        PasswordAuthentication no
        ChallengeResponseAuthentication no
        UsePAM no
        PubkeyAuthentication yes
        ```

### Troubleshooting and miscellaneous tips

- You can test specific auth methods like so `ssh pi@raspberrypi -o PasswordAuthentication=No`. Also look at the output of eventual `Connection refused messages` to check the allowed methods. 

- If connection is refused although the method is allowed make sure the ssh-client is using the correct identity (and not e.g. the key pair for Github, will by default use `id_rsa.pub`)
    - Manually try id file: `ssh pi@raspberrypi -i ~/.ssh/raspberrypi_rsa`
    - Edit `~/.ssh/config` on machine you are connecting from to use specified key file for a certain host. For example:
        ```
        Host raspberrypi
            HostName YourPiHostnameOrIP
            User pi
            IdentityFile ~/.ssh/pi_key
        ```


## Sources
- https://www.geekyhacker.com/configure-ssh-key-based-authentication-on-raspberry-pi/
- https://www.raspberrypi.com/documentation/computers/remote-access.html#passwordless-ssh-access