# NGINX

## Requirements
1. You must have a domain registered, for example ``my-fun-sync.eu`` or ``elegant-venue.party``
   1. With your registrar, register two subdomain for that domain that point to the IP of your server:
      1.``sync.<my-domain>.<tld>``, for example ``sync.elegant-venue.party``
      2.``cdn.<my-domain>.<tld>``, for example ``cdn.elegant-venue.party``
   2. Any subdomain works, of course, and any depth works, too, but we recommend sticking to these two basics.
2. Verify that both domains resolve by using ``nslookup <domain>``. It needs to point back to your server
3. You must have a bot registered

## Installation
Make sure all dependencies are installed and the domains are registered properly
1. ``git clone https://github.com/LaciSynchroni/hosting.git laci``
2. ``cd laci``
3. ``cp sample.env .env``
4. ``cp docker-compose.nginx.yaml docker-compose.yaml``
5. ``cp -r configs-nginx configs``

Now you have to change a few configurations. We'll go through them one by one

## Config: .env file
In the .env file that is now in your ``~/laci`` folder, change what needs changing. At **minimum**, you have to change:

- LACI_POSTGRES_PASSWORD to a **secure password**. You can use ``pwgen -s 30 1`` to generate one.
- LACI_REDIS_PASSWORD to a **secure password**. You can use ``pwgen -s 30 1`` to generate one.
- LACI_JWT_SIGNING_KEY to a **secure string** that should be at least 128bit long. You can use ``pwgen -s 60 1`` to generate one.
- LACI_PUBLIC_URI is ``wss://sync.<yourdomain>``, for example ``wss://sync.elegant-venue.party``
- LACI_CDN_URI is ``wss://cdn.<yourdomain>``, for example ``wss://cdn.elegant-venue.party``
- LACI_DISCORD_TOKEN is your discord bot token
- CERTBOT_EMAIL is the e-mail given to letsencrypt for your certificate

Anything else is optional. Please refer to the FAQ sections on discord for more config options

## Config: nginx configs
In the ``~/laci/configs/conf.d`` are two ``.conf`` files. Each of them have references to ``mydomain.com``. Change
all those references to your own domain. Keep the ``files.`` subdomain.

## Starting
1. ``cd ~/laci``
2. ``docker compose --env-file .env pull``
3. ``docker compose --env-file .env up -d``