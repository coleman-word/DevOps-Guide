# SSH-Copy-ID

## NAME
     ssh-copy-id — use locally available keys to authorise logins on a remote
     machine

SYNOPSIS
     ssh-copy-id [-f] [-n] [-i [identity_file]] [-p port] [-o ssh_option]
                 [user@]hostname
     ssh-copy-id -h | -?

DESCRIPTION
     ssh-copy-id is a script that uses ssh(1) to log into a remote machine
     (presumably using a login password, so password authentication should be
     enabled, unless you've done some clever use of multiple identities).  It
     assembles a list of one or more fingerprints (as described below) and
     tries to log in with each key, to see if any of them are already
     installed (of course, if you are not using ssh-agent(1) this may result
     in you being repeatedly prompted for pass-phrases).  It then assembles a
     list of those that failed to log in, and using ssh, enables logins with
     those keys on the remote server.  By default it adds the keys by append‐
     ing them to the remote user's ~/.ssh/authorized_keys (creating the file,
     and directory, if necessary).  It is also capable of detecting if the
     remote system is a NetScreen, and using its ‘set ssh pka-dsa key ...’
     command instead.


The options are as follows:

     -i identity_file
             Use only the key(s) contained in identity_file (rather than look‐
             ing for identities via ssh-add(1) or in the default_ID_file).  If
             the filename does not end in .pub this is added.  If the filename
             is omitted, the default_ID_file is used.

             Note that this can be used to ensure that the keys copied have
             the comment one prefers and/or extra options applied, by ensuring
             that the key file has these set as preferred before the copy is
             attempted.

     -f      Forced mode: doesn't check if the keys are present on the remote
             server.  This means that it does not need the private key.  Of
             course, this can result in more than one copy of the key being
             installed on the remote system.

     -n      do a dry-run.  Instead of installing keys on the remote system
             simply prints the key(s) that would have been installed.

     -h, -?  Print Usage summary

     -p port, -o ssh_option
             These two options are simply passed through untouched, along with
             their argument, to allow one to set the port or other ssh(1)
             options, respectively.

             Rather than specifying these as command line options, it is often
             better to use (per-host) settings in ssh(1)'s configuration file:
             ssh_config(5).

     Default behaviour without -i, is to check if ‘ssh-add -L’ provides any
     output, and if so those keys are used.  Note that this results in the
     comment on the key being the filename that was given to ssh-add(1) when
     the key was loaded into your ssh-agent(1) rather than the comment con‐
     tained in that file, which is a bit of a shame.  Otherwise, if ssh-add(1)
     provides no keys contents of the default_ID_file will be used.

     The default_ID_file is the most recent file that matches: ~/.ssh/id*.pub,
     (excluding those that match ~/.ssh/*-cert.pub) so if you create a key
     that is not the one you want ssh-copy-id to use, just use touch(1) on
     your preferred key's .pub file to reinstate it as the most recent.

