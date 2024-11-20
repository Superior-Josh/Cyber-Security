# Introduction
## Security challenges

Protect devices against:

* Malicious applications

* Rootkit 

## Malicious applications

* Malware distributed using OS specific applications, designed to exploit the operating system vulnerability's.
* Issues:
  * High success rate because they (can) masquerade as useful applications
  * Are often used as a means to install more dangerous malware: backdoors, rootkits

## Rootkits

* Code designed to enable access to a computer **or** areas of its software that would not otherwise be allowed.
* Issues:
  * Install themselves with highest privileges
  * Prevent detection/removal with anti-malware tools

## Mitigations: defence in depth 

* The principle of “defence in depth”:
  * Secure the boot process
  * Secure the user space
  * Secure the user space



# Hash functions and signatures

## Authentication

* How (in CS):
  * Hashes – to compute/checkintegrity
  * Digital signatures – to authenticate

## Hash functions

* Low collision
* One way

## Signatures

$$
Sign &=& Enc( H( Plaintext ), sk ) \\
message &=& sign | plaintext
$$
# System architectures

| Generic architecture | Description                                     |
| -------------------- | ----------------------------------------------- |
| Bootloader           | Loads operating system or recovery              |
| Reserved             |                                                 |
| Kernel               | Core of the OS. Basic functionality and drivers |
| Recovery             | Recovery partition                              |
| System               | Application space                               |
| User data            | Application space                               |
| Cache/SWAP           |                                                 |

# Trusted boot

## Root of trust

1. The bootloader is the guardian of the device 
   state and is responsible for initializing the TEE (Trusted Execution Environment) 
   and binding its root of trust.
2. If **rooting software compromises** the system 
  before the kernel comes up, it will retain that 
  access.
3. The bootloader verifies the integrity of the 
  boot and/or recovery partition before moving 
  execution to the kernel.
4. **Hardware root** of trust is fixed because is laid 
  down during chip fabrication.
5. **Non-hardware** root of trust can be changed 
  because is stored on non-volatile memory (e.g. 
  NAND).

## How to verify?