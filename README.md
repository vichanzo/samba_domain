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



### References
1) https://www.redhat.com/sysadmin/linux-active-directory
2) https://stealthbits.com/blog/join-linux-hosts-to-active-directory/
3) https://www.thegeekdiary.com/choosing-sssd-or-winbind-samba-for-active-directory-integration-in-centos-rhel
