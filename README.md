# Local Setup
Installation procedure for local set up on clean install

### Install Node.js
https://nodejs.org/en/

When finished, check node and npm versions.

`node -v`
`npm -v`

### Install Gulp globally

`sudo npm install --global gulp`

Reference: https://semaphoreci.com/community/tutorials/getting-started-with-gulp-js

### Install Homebrew

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Reference: https://brew.sh

### Install PHP71, Mcrypt & Imagick

```
brew update
brew upgrade
```
```
brew tap homebrew/dupes
brew tap homebrew/versions
brew tap homebrew/homebrew-php
```
```
brew install php71
brew services start homebrew/php/php71
```

### Install PHP Extensions
```
brew install php71-mcrypt
brew install php71-imagick
```

Reference: https://developerjack.com/blog/2016/installing-php71-with-homebrew/

### Install MariaDB

```
brew install mariadb
brew services start mariadb
```

Reference: https://mariadb.com/kb/en/library/installing-mariadb-on-macos-using-homebrew/

You'll then need to update the root password.

Not sure best way to do this, tried with command line, but getting issues, so found I could change via Sequel Pro.
Log into MariaDB with `root` and no password, then go to Database > User Accounts and update there.

Restart MariaDB
`brew services restart mariadb`

Test that the new password works by logging in...
`mysql -u root -p`

and it should ask for the password you just set.

Reference: https://www.digitalocean.com/community/tutorials/how-to-reset-your-mysql-or-mariadb-root-password

### Install Composer Globally

```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('SHA384', 'composer-setup.php') === '544e09ee996cdf60ece3804abc52599c22b1f40f4323403c44d44fdfdd586475ca9813a858088ffbc1f233e9b180f061') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
php composer-setup.php
php -r "unlink('composer-setup.php');"
```

Then you need to move the composer.phar file...

`mv composer.phar /usr/local/bin/composer`

Reference: https://getcomposer.org/doc/00-intro.md#globally

Make sure Composer is in your directory is in your path.

`export PATH="$PATH:$HOME/.composer/vendor/bin"`

Then...

`echo 'export PATH="$PATH:$HOME/.composer/vendor/bin"' >> ~/.bash_profile`

finally...

`source ~/.bash_profile`

Suggest restarting terminal at this point.

### Install Valet

Run

`composer global require laravel/valet`

followed by 

`valet install`

then, if you want to change the development tld...

`valet domain dev` - dev in this case.


## Optional
### Craft Scripts

Update your .bash-profile to run the Craft 2.5 scripts.
```
alias syncAll="cd scripts; chmod 775 pull_db.sh pull_assets.sh; ./pull_db.sh; ./pull_assets.sh; chmod 644 pull_db.sh pull_assets.sh; cd ../;"alias syncDb="cd scripts; chmod 775 pull_db.sh; ./pull_db.sh; chmod 644 pull_db.sh; cd ../;"alias syncAssets="cd scripts; chmod 775 pull_db.sh; ./pull_assets.sh; chmod 644 pull_db.sh; cd ../;"
```
Reload your bash profile
`. ~/.bash_profile`

### SSH Keys

Generate ssh key
```
ssh-keygen -t rsa
```
Then use `ssh-copy-id` to copy the key to servers.

Install via brew first
```
brew install ssh-copy-id
```

Then add the key via 
```
ssh-copy-id user@198.00.100.0
```

Done.





