# cups-ad-fix
Fix cups parameters for kerberised access to printers


If you have some Linux workstations in an Active Directory managed environment, your users should access network printers without other credentials but the login ones.

Unfortunately that does not always work.

This package fix it tuning some files:

/usr/lib/cups/backend/smb 

    The default CUPS smb backend does not work with kerberos credentials
    Smbclient package provides a wrapper for kerberized printers, so this
    package replaces that backed with the new one


To use this fix, you need to configure your printers to use the kerberos Operation Policy.

Check /etc/cups/printers.conf: 

    Must contain your printer definition, and MUST contain an "OpPolicy kerberos"
    AuthInfoRequired must be negotiate
    
