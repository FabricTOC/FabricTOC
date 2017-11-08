## Membership Services Provider Reference guide

### How to configure the list of recognized OUs

(optional) a file config.yaml to include information on the considered OUs; the latter are defined as pairs of <Certificate, OrganizationalUnitIdentifier> entries of a yaml array called OrganizationalUnitIdentifiers, where Certificate represents the relative path to the certificate of the certificate authority (root or intermediate) that should be considered for certifying members of this organizational unit (e.g. ./cacerts/cacert.pem), and OrganizationalUnitIdentifier represents the actual string as expected to appear in X.509 certificate OU-field (e.g. “COP”)
