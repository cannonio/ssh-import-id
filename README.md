
ssh-auth-id
===========

You're logged onto a cloud instance working on a problem with your fellow devs, and you want to invite them to log in and take a look at these crazy log messages. What do?

Oh. You have to ask them to cat their public SSH key, paste it into IRC (wait, no, it's id\_rsa.pub, not id\_rsa silly!) then you copy it and cat it to the end of authorized\_hosts.

That's where ssh-auth-id comes in. With ssh-auth-id, you can add the public SSH keys from a known, trusted online identity to grant SSH access.

Currently supported identities include Launchpad (https://launchpad.net) and of course, Github!

Usage
-----

ssh-auth-id uses short prefix to indicate the location of the online identity. For now, these are:

	'gh:' for Github
	'lp:' for Launchpad

 usage: ssh-auth-id [-h] [-o FILE] USERID [USERID ...]

 Authorize SSH public keys from trusted online identities.

 positional arguments:
   USERID                User IDs to import

 optional arguments:
   -h, --help            show this help message and exit
   -o FILE, --output FILE
                         Write output to file (default ~/.ssh/authorized_keys)

Example
-------

If you wanted me to be able to ssh into your server, as the desired user on that machine you would use:

 $ ssh-auth-id gh:cmars

Used with care, it's a great collaboration tool!

Installing
----------

ssh-auth-id can be installed pretty much anywhere with a recent version of pip:

 $ pip install ssh-auth-id

ssh-auth-id requires a recent version of Requests (>=1.1.0) for verified SSL/TLS connections.

Extending
---------

You can add support for your own SSH public key providers by creating a script named ssh-auth-id-<prefix>. Make the script executable and place it in the same bin directory as ssh-auth-id.

The script should accept the identity username for the service it connects to, and output lines in the same format as an ~/.ssh/authorized\_keys file.

If you do develop such a service, I recommend that you connect to the service with SSL/TLS, and require a valid certificate and matching hostname. Use Requests.get(url, verify=True), for example.

Credits
-------

This project is pretty much a port of https://launchpad.net/ssh-import-id, written by Dustin Kirkland and Scott Moser.

