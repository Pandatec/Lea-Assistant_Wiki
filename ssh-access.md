# SSH access

* [Generating an SSH key](#generating-an-ssh-key)
* [Upload the key to the server](#upload-the-key-to-the-sevrer)
* [Creating an SSH configuration](#creating-an-ssh-configuration)

To access the production server you will need to upload your ssh key to the server (you can still use the old school username/password method but it will be abandonned soon).

## Generating an SSH key

If you already have an SSH key, you don't need to create a new one and can skip to next party.
In order to generate an SSH key you need to have Git installed on your OS (which you certainly already have anyaway).

- Windows: download it [here](https://git-scm.com/download/win)
- Linux: you can find the command working for your distribution [here](https://git-scm.com/book/fr/v2/D%C3%A9marrage-rapide-Installation-de-Git) (even though you certainly already know how to do it)
- MacOS: you can find all the download options [here](https://git-scm.com/download/mac)

Once Git is installed, you can simply run `ssh-keygen` to generate an SSH key.

## Upload the key to the server

Since we don't have any web interface to install the key automatically, you'll have to ask Kylian on the Discord server to create you an account and hand him your PUBLIC SSH key (the one ending with '.pub'), he'll do the rest for you. Once he tells you that it's done, he'll give you your username (wich should be ${your name}-${your last name}, you'll can connect to the server by running `ssh ${your username (name-lastname)}@leassistant.fr -p8742`



## Creating an SSH configuration

An SSH configuration allows you to connect even faster, here's how to do it;
in your .ssh folder (in your user directory), open or create the file 'config' and add the following inside:
```
Host lea
    HostName leassistant.com
    User ${your username (name-lastname)}
    Port 8742
    IdentityFile ${your private SSH key full path (absolute path doesn't work)}
    StrictHostKeyChecking no
```
Save the file and voilà ! You juste have to run `ssh lea` to connect, isn't it amaizing ?
