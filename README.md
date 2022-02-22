# samba_domain
my adventures setting up domain controller / SAMBA/ Linux / Windows

``` 
sudo apt install realmd
```

Join the domain (apparently I was using winbind)
```
sudo realm join --user < windows_domain_admin> ciso.example.com
```

```
$ realm list
ciso.example.com
  type: kerberos
  realm-name: CISO.example.COM
  domain-name: ciso.example.com
  configured: kerberos-member
  server-software: active-directory
  client-software: winbind
  required-package: winbind
  required-package: libpam-winbind
  required-package: samba-common-bin
  login-formats: CISO\%U
  login-policy: allow-any-login
```

```
$ realm discover ciso.example.com
ciso.example.com
  type: kerberos
  realm-name: CISO.example.COM
  domain-name: ciso.example.com
  configured: kerberos-member
  server-software: active-directory
  client-software: winbind
  required-package: winbind
  required-package: libpam-winbind
  required-package: samba-common-bin
  login-formats: CISO\%U
  login-policy: allow-any-login
```

Edit the sudoers "sudo visudo" add the section right under the normal sudo users:
```
# Allow users in the Unicorn-Admins group to run all commands     
ciso\\linux-admins ALL=(ALL) ALL
```

https://www.thegeekdiary.com/how-to-integrate-centos-rhel-system-into-an-ad-domain-with-ldap-kerberos-sssd/
```
Run the following to enable SSSD within /etc/nsswitch.conf and PAM:

# authconfig --enablesssd --enablesssdauth --enablelocauthorize --enablemkhomedir --update
```

What I ran for winbind (https://docs.oracle.com/en/operating-systems/oracle-linux/6/admin/enable-windbind.htm):
```
sudo apt install ldap-auth-config
authconfig --enablewinbind --enablewinbindauth --smbsecurity user --smbservers="ad1.mydomain.com ad2.mydomain.com" \
  --smbworkgroup=MYDOMAIN --update
```

### References
1) https://www.redhat.com/sysadmin/linux-active-directory
2) https://stealthbits.com/blog/join-linux-hosts-to-active-directory/
3) https://www.thegeekdiary.com/choosing-sssd-or-winbind-samba-for-active-directory-integration-in-centos-rhel
4) https://docs.oracle.com/en/operating-systems/oracle-linux/6/admin/enable-windbind.htm
