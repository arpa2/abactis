# Installing Groupie

> *How to get Abactis to work in your infrastructure.*


## Build and Runtime Dependencies

Groupie is built in Python.  It depends on

  * [lmtpd](https://pypi.python.org/pypi/lmtpd)
  * [python-ldap](https://pypi.python.org/pypi/python-ldap/2.4.41)
  * [dkimpy](https://pypi.python.org/pypi/dkimpy/0.6.2)


## Connections to MTAs

How to get information to arrive at the LMTP port?


### Postfix MTA

Services in the InternetWide Architecture start with `+` and their name.
What follows then can vary wildly, though it still is a matter of
configuration, so lookup tables with exact key matches are quite efficient
even when we have long lists of such mappings.

In a hosted domain's virtual domain definitions, we add mappings for the
various Groupie service addreses, including all possible group names,
to an underlying Groupie service identifier.  So, in `/etc/postfix/virtual`,
we might have

```
+abactis+pgp@eaxmple.com   +abactis@service.provider
+abactis+x509@eaxmple.com  +abactis@service.provider
+abactis+vcard@eaxmple.com +abactis@service.provider
```

The only thing we need to do now, is to define the mapping to the
`abactis@service.provider` to be an LMTP mapping.  This is best done
in `/etc/postfix/transport`, using an entry like:

```
+abactis@service.provider  lmtp:inet:abactis.service.provider
```

This indicates that the emails to `+abactis@service.provider` will end
up being sent over LMTP to the host `abactis.service.provider` using the
standard port configured for LMTP.



