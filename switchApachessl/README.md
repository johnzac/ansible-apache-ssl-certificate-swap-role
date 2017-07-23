Role Name
=========

A role to swap apache virtual host ssl certificates with new ones. The role will automatically check all included files within apache configuration, parse the files for virtual hosts definitions and replace ssl keys corresponing to the ServerName specified as an argument in vars file. If the role fails to start apache after swapping the keys, it will automatically restore the old keys to the remote host and try restarting apache. It can be configured to match all subdomains as well from the var file.

Requirements
------------
None as such. If the remote machine is running cent os, the role will make sure SElinux puthon wrappers are installed in the remote host since they are required for using the file copy module.

Role Variables
--------------
vhostParams:
     Could be left as it is in the default vars/main.yml. It secifies the parameters to be fetched from each virtual host in the remote machine. You can add extra variables if you would like to see them as output.
centOSConfigFiles:
     The default configuration file if the remote machine runs centOS or Redhat. The default value would work for most cases.
debianOSConfigFiles:
       The default configuration file if the remote machine runs Debian or Ubuntu. The default value would work for most cases.
centOsServerRoot:
         The apache server root. The role will search for other included files from within this directory. The default would work for most servers.
debianOsServerRoot:
           The apache server root. The role will search for other included files from within this directory. The default would work for most servers.
copyCertificateChainFile:
        Set this to 1 if you have a CA budle file you'd like copied to the remote host. Note that this role will not automatically alter the virtual hosts to serve a chain file if one is not already configured, it merely replaces the file if one already exists.
SSLCertificateFile:
        Path to ssl certificate file within the local system.
SSLPrivateKeyFile:
         Path to ssl private key file within the local system.
SSLCertificateChainFile:
          Path to CA bundle within local system. Will only be considered if copyCertificateChainFile set to 1
ServerName:
          The server name whose certificates are to be swapped with new ones.
SwitchSubDomains:
            If set to 1, the role will replace ssl keys of subdomains as well( If they are saved in different locations). To be used if you are using a wildcard ssl certificate.



Example Playbook
----------------


hosts: vagrantServersLocal
roles:
      - switchApachessl

License
-------

BSD

