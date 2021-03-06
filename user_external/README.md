External user authentication
============================
Authenticate user login against FTP, IMAP or SMB.

Passwords are not stored locally; authentication always happens against
the remote server.

It stores users and their display name in its own database table
`users_external`.
When modifying the `user_backends` configuration, you need to
update the database table's `backend` field, or your users will lose
their configured display name.

If something does not work, check the log file at `owncloud/data/owncloud.log`.


FTP
---
Authenticate owncloud users against a FTP server.


### Configuration
You only need to supply the FTP host name or IP.

The second - optional - parameter determines if SSL should be used or not.

Add the following to `config.php`:

    'user_backends' => array(
        array(
            'class' => 'OC_User_FTP',
            'arguments' => array('127.0.0.1'),
        ),
    ),

To enable SSL connections via `ftps`, append a second parameter `true`:

    'user_backends' => array(
        array(
            'class' => 'OC_User_FTP',
            'arguments' => array('127.0.0.1', true),
        ),
    ),


### Dependencies
PHP automatically contains basic FTP support.

For SSL-secured FTP connections via ftps, the PHP [openssl extension][0]
needs to be activated.

[0]: http://php.net/openssl



IMAP
----
Authenticate owncloud users against an IMAP server.
IMAP user and password need to be given for the owncloud login


### Configuration
Add the following to your `config.php`:

    'user_backends' => array(
        array(
            'class' => 'OC_User_IMAP',
            'arguments' => array(
                '{127.0.0.1:143/imap/readonly}',
            ),
        ),
    ),

This connects to the IMAP server on IP `127.0.0.1`, in readonly mode.

Read the [imap_open][0] PHP manual page to learn more about the allowed
parameters.

[0]: http://php.net/imap_open#refsect1-function.imap-open-parameters


### Dependencies
The PHP [IMAP extension][1] has to be activated.

[1]: http://php.net/imap



Samba
-----
Utilizes the `smbclient` executable to authenticate against a windows
network machine via SMB.


### Configuration
The only supported parameter is the hostname of the remote machine.

Add the following to your `config.php`:

    'user_backends' => array(
        array(
            'class' => 'OC_User_SMB',
            'arguments' => array('127.0.0.1'),
        ),
    ),


### Dependencies
The `smbclient` executable needs to be installed and accessible within `$PATH`.
