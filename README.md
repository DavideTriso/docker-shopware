# Docker Shopware

Image to run Shopware 6 apps in a docker container

## Quick reference

### Build the image:

```
docker build -t davidetriso/shopware:[tagname-dir_name] ./[tagname-dir_name]
```

E.g.:

```
docker build -t davidetriso/shopware:php-8.1-fpm ./php-8.1-fpm
```

### Push image to Docker Hub

```
docker push davidetriso/shopware:tagname
```

E.g.:

```
docker push davidetriso/shopware:php-8.1-fpm
```

###  Build and push everything

Execute the `./build-and-push.sh` script to build and push all images to Docker Hub at once.


## How to use

Bind-mount the root directory of your Shopware 6 project in the container's working directory (`/var/www/html`).

Uploaded media are stored by Shopware in the `public/media` folder, so it is necessary to mount a volume at this directory too. 

For example, in a compose file add:

```yaml
shopware:
    # ... other settings here ...
    volumes:
        - ./:/var/www/html/:rw
        - media:/var/www/html/public/media:rw

volumes:
    media:
```

The image uses a production-optimized `php.ini` file. To customize the PHP settings to your needs it is sufficient to bind-mount a custom `ini` file in the container's `/usr/local/etc/php/conf.d/` directory.

E.g.:

```yaml
shopware:
    # ... other settings here ...
    volumes:
        # ... other volumes and mounts here ...
        - ./my/custom/999-php.ini:/usr/local/etc/php/conf.d/999-php.ini:ro
```

### Debugging

The `XDebug` extension is available in the image, but is disabled by default. To enable it, use a custom `ini` file, like explained above.