# cups-ad-fix
Fix cups parameters for kerberised access to printers


If you have some Linux workstations in an Active Directory managed environment, your users should access network printers without other credentials but the login ones.

Unfortunately that does not always work.

This package fix it tuning some files:

/etc/cups/cupsd.conf

    This package adds a new Operation Policy Section: "<Policy Kerberos-AD>"
    This section contains a subsection "<Limit Create-Job Print-Job Print-URI Validate-Job>"
    This subsection must have a line "AuthType Negotiate"

/usr/lib/cups/backend/smb 

    This CUPS backend does not work with kerberos credentials
    We use another one. Permissions must be set properly or CUPS will complain.


To use this fix, you need to configure your printers to use this new Operation Policy.
Check /etc/cups/printers.conf: 

    Must contain your printer definition, and MUST contain an "OpPolicy Kerberos-AD"
    AuthInfoRequired must be None (although CUPS set it to "user,password" randomly)                            
