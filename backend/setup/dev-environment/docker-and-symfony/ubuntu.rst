.. _setup-dev-env-docker-symfony_ubuntu:

Set up Environment for OroPlatform Based Application on Ubuntu 20.04
====================================================================

This guide demonstrates how to set up :ref:`Docker and Symfony Server development stack <setup-dev-env-docker-symfony>` for Oro applications on Ubuntu 20.04 LTS.

Environment Setup
-----------------

1. Install PHP 8.0 with all required extensions:

   .. code-block:: none

      sudo apt install software-properties-common
      sudo add-apt-repository -y ppa:ondrej/php
      sudo apt update
      sudo apt -y install php8.0 php8.0-fpm php8.0-cli php8.0-pdo php8.0-mysqlnd php8.0-xml php8.0-soap php8.0-gd php8.0-zip php8.0-intl php8.0-mbstring php8.0-opcache php8.0-curl php8.0-bcmath php8.0-ldap php8.0-pgsql php8.0-dev php8.0-mongodb

2. Configure PHP:

   .. code-block:: none

      echo -e "memory_limit = 2048M \nmax_input_time = 600 \nmax_execution_time = 600 \nrealpath_cache_size=4096K \nrealpath_cache_ttl=600 \nopcache.enable=1 \nopcache.enable_cli=0 \nopcache.memory_consumption=512 \nopcache.interned_strings_buffer=32 \nopcache.max_accelerated_files=32531 \nopcache.save_comments=1" | sudo tee -a  /etc/php/8.0/fpm/php.ini
      echo -e "memory_limit = 2048M" | sudo tee -a  /etc/php/8.0/cli/php.ini

3. Install Node.js 12:

   .. code-block:: none

      sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates
      curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
      sudo apt -y install nodejs

4. Install Docker and Docker Compose:

   .. code-block:: none

      sudo apt -y install docker.io docker-compose
      sudo usermod -aG docker $(whoami)
      sudo systemctl enable --now docker

5. Install Composer v2:

   .. code-block:: none

      php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && php composer-setup.php
      php -r "unlink('composer-setup.php');"
      sudo mv composer.phar /usr/bin/composer

6. Install Symfony Server and enable TLS:

   .. code-block:: none

      sudo apt -y install libnss3-tools
      wget https://get.symfony.com/cli/installer -O - | bash
      echo 'PATH="$HOME/.symfony/bin:$PATH"' >> ~/.bashrc
      source ~/.bashrc
      symfony server:ca:install

7. Restart the terminal and web browser to get them ready.

What's Next
-----------

* :ref:`Follow the recommendations <setup-dev-env-docker-symfony-recommendations>`
* :ref:`Install the Oro Application via the Command-Line Interface <setup-dev-env-docker-symfony-install-application>`
