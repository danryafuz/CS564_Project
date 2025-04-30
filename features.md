# C2 and Implant Features

## C2-Implant Communications

-   HTTPS (TLS) encryption for transport (requires installing attacker's certificate authority on target)
-   X25519 Elliptic-Curve Diffie-Hellman (AES) Key Exchange between client and server
-   AES-256-GCM encryption on all messages with random nonce
-   Random ephemeral 256-bit AES key generation every time client starts
    -   Pre-shared key is used only during key exchange

## Implant Obfuscation

-   Obfuscated with Pyarmor
-   Compiled into standalone binary with PyInstaller with `--one-file` flag

## Timeline of Operation

1. C2 - Attacker starts C2 and leaves it waiting for connections
2. Initial exploit - Attacker exploits the file traversal vulnerability to make Apache2 open a reverse shell from the target
3. Stager - Attacker sends a Python command to run a stager which downloads the implant from the C2
4. Implant - Attacker runs the implant for full communications with the C2
5. RCE and file exfil - Now the attacker can send any commands to the target, including file exfiltration
