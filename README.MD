# Abactis &mdash; Mail Secretary for the LDAP Global Directory

> *So you want to present automatically searchable data under your domain.
> And you agree with us that the LDAP Global Directory is the best option
> available.  Now, how to get your data in?  Enter Abactis!*

Abactis is an email-based service for inserting data into the personal
portion of the Global Directory.  Just send your PGP key to Abactis.
Or a set of vCards to add to your contacts database.

The basis for Abactis is authenticated email.  More and more domains are
embraching DKIM to sign on the contents and headers of email, thus
authenticating the sender address.  In addition, there is a long-standing
habit of using a "submission mail agent", which is an outgoing mail server
for a domain that requires its clients to authenticate.

What this means to you as a user is simply this: You can submit data to
Abactis and it will be processed without further ado &mdash; but not before
having tested your identity and your rights to change the given resource.


## Abactis PGP

The PGP service of Abactis is generally found at `+abactis+pgp@domain.name`
and it is possible to send OpenPGP public keys there.  This can be in an
attachment with the type `application/pgp-keys`, or in the email body
where it is encoded ASCII armour.

Only the part of the PGP key that matches a validated `From:` header
address will be used; other identities are removed from the key.  This
interprets the `UserID` packet in the usual form namely as either an
email address or `UserName (OptionalComment) <email@address>`.  Might
there be more than this one identity, then the key may be submitted
from these other identities as well, leading to independent publications
of the key and the applicable user identity under each of these identities.
PGP software knows how to handle this by re-integrating the various
views on your key.

When the validated address represents a local user of the domain for which
Abactis is invoked, then the PGP key is inserted under the user's entry
in the Global Directory.  When the validated user is not local, the data
may end up in a contacts database, thus enabling encryption to the remote
contact.  It is likely that some access control is applied, specifically
to ensure that the contact is indeed known; we should not add any ol'
spammer to our precious database!


## Abactis X.509

As for PGP, but less powerful because X.509 certificates cannot be edited.
The address would be `+abactis+x509@domain.name`


## Abactis vCard

This is a service over which vCards of contacts can be submitted, in this
case as `text/vcard` entries.  The vCard is taken apart and its entries
added to the LDAP database for integration with any software that is aware
of LDAP for such purposes.

The users' contact list is not public.  Nor is the contact list of any
group they partake in.  It is however possible to submit the new data
from an authenticated account.  An exception is (or may be) the contact
database for the user (or group) themselves.  Any updates to those may
be public as per policy.

It is desirable to support an updating mechanism for remote users that
have already been entered.  This is work TODO.


