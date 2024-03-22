# Configurate WebDAV
## Install Apache2
```
sudo apt install apache2
```

## Make Directory and Permisions Folder
```
mkdir /var/www/[FoldareName]
sudo chown -R www-data:www-data /var/www/[FolderName]
```

## Make Conf Apache2
```
sudo nano /etc/apache2/sites-available/[NameConf].conf
```

## Example Conf Apache2
```
<VirtualHost *:80>
    ServerAdmin [NameServer]@[Domain]
    DocumentRoot /var/www/[NameFolder]
    ServerName [IP Address/Domain]

    Alias /webdav /var/www/[NameFolder]

    <Location /[NameFolder]>
        DAV On
        AuthType Digest
        AuthName "[NameAuth]"
        AuthUserFile /etc/apache2/webdav.password
        <RequireAny>
            Require user [NameUser1]
            Require user [NameUser2]
        </RequireAny>
    </Location>

    <Directory /var/www/[NameFolder]>
        DAV On
        AuthType Digest
        AuthName "[AuthUser1]"
        AuthUserFile /etc/apache2/webdav.password
        Require user [NameUser1]
    </Directory>

    <Directory /var/www/webdav/user2>
        DAV On
        AuthType Digest
        AuthName "[AuthUser2]"
        AuthUserFile /etc/apache2/webdav.password
        Require user [NameUser2]
    </Directory>
</VirtualHost>
```

## Enable WebDEV and Restart Apache2
```
sudo a2ensite webdav dav_fs auth_digest dav
sudo systemctl restart apache2
```

## Create User WebDEV
```
sudo htdigest /etc/apache2/webdav.password "[AuthUser1]" [NameUser1]
```
<b> Don't Forget restart apache 2 </b>
