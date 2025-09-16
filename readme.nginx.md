# NGINX

## Requirements
1. You must have two domains registered: ``<your-domain>.<tld>``  and ``files.<your-domain>.<tld>``
2. Verify that both domains resolve by using ``nslookup <domain>``. It needs to point back to your server.
3. You must have a bot registered

## Installation
Make sure all dependencies are installed and the domains are registered properly
1. ``git clone git@github.com:LaciSynchroni/hosting.git laci``
2. ``cd laci``
3. ``cp sample.env .env``
4. ``cp docker-compose.nginx.yaml docker-compose.yaml``
5. ``cp -r configs-nginx configs``

Now you have to change a few configurations. We'll go through them one by one

## Config: .env file
In the .env file that is now in your ``~/laci`` folder, change what needs changing. At **minimum**, you have to change:

- LACI_POSTGRES_PASSWORD to a **secure password**
- LACI_REDIS_PASSWORD to a **secure password**
- LACI_PUBLIC_URI is ``wss://<yourdomain>``, for example ``wss://my-laci-instance.eu``
- LACI_CDN_URI is ``wss://files.<yourdomain>``, for example ``wss://files.my-laci-instance.eu``
- LACI_DISCORD_TOKEN is your discord bot token
- CERTBOT_EMAIL is the e-mail given to letsencrypt for your certificate

Anything else is optional. Please refer to the FAQ sections on discord for more config options

## Config: nginx configs
In the ``~/laci/configs/conf.d`` are two ``.conf`` files. Each of them have references to ``mydomain.com``. Change
all those references to your own domain. Keep the ``files.`` subdomain.

## Starting
1. ``cd ~/laci``
2. ``docker compose pull``
3. ``docker compose up -d``