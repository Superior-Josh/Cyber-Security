# Assignment FAQ, useful links and Troubleshooting

A lot of useful information, especially on how to use U-Boot and QEMU, is explained in the workshop lecture. The slides and recording will be uploaded on Canvas.  

This file aims to fill any remaining knowledge not covered in that lecture, so take a look at that first before asking for help.

Lastly, a lot of the knowledge required for this assignment is well-documented online. All the tools used are open-source, so please remember to look at the documentation!

## Docker Setup
For your convenience, I've written 2 scripts to automate building and running the docker container. They are 'docker.build' and 'docker.run'. In the case that they do not run for you, you can run the commands yourself.

To build the docker image:
`docker build . -t dmss`  
To run a container:
`docker run --mount type=bind,target=/work/included_files,src="$(pwd)/included_files" --name dmss_container --hostname emulator_sissel -it dmss`
The above command also mounts a shared folder named `included_files` between the container and your host computer. Please use this folder to transfer files into the container.

**IMPORTANT NOTE TO STOP YOU FROM LOSING YOUR DATA!**  
*Copy anything you want to save into the included_files folder!* This will ensure you don't lose these files if you rebuild your image, or stop the container.  

On a docker build, everything in the `assignmentfiles_include` folder will be copied into the built image. However, they are just copies of what is in `assingmentfiles_include`. If you rebuild the image, any changes you have made to them will have been reverted.  

If you exit or kill a running container (e.g. typing exit), it's state is not saved, so any changes not in a shared folder will be discarded. You can use `docker run` to start a new container. Alternatively, if you want to temporarily exit a container, you can *detach* from the container by typing `Ctrl-p Ctrl-q` (I find holding down Ctrl and then pressing p and q works best). You can then re-attach later on with the command `docker attach <container name>`

## QEMU
As a reminder, to quit QEMU but not exit the Docker container, you will need to press Ctrl-A, and then x.  I find that I need to release Ctrl-A before pressing x for this to work.

https://www.qemu.org/docs/master/system/qemu-manpage.html  
The above page is quite long. Some particularly relevant options or page for this assignment would be:  
 - Block device options
 - The Generic Loader https://www.qemu.org/docs/master/system/generic-loader.html

## U-Boot
A lot of relevant U-boot content is covered in the workshop lectures. The below links may also be useful:
https://docs.u-boot.org/en/latest/index.html  
https://docs.u-boot.org/en/latest/usage/fit/verified-boot.html

## Filesystem 
When the filesystem boots, you will need to login. You can login with the following credentials:
```
User: alarm
Password: alarm
```
For the root user, use the following:
```
User: root
Password: root
```

## Disk Encryption
'My system hangs when it's trying to decrypt the filesystem disk!'  
The filesystem decryption can take a while to complete. If you don't see an obvious error message, it's probably not finished yet.  
"I'm getting a 'Open: cryptsetup out of memory' error during disk encryption"  
Take a look at the following link:  
https://unix.stackexchange.com/questions/647859/open-cryptsetup-out-of-memory-not-enough-available-memory-to-open-a-keyslot  

### Links
The archlinux wiki is very informative and well-written. Use it!  

https://wiki.archlinux.org/title/Dm-crypt  
https://wiki.archlinux.org/title/Dm-crypt/Device_encryption
