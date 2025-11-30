## Example of Compose file
```yaml
services:
  db:
    image: mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    volumes: 
      - db_data:/var/lib/mysql    
    ports:
      - 3306:3306
      - 33060:33060
    networks:
      - default
#  bind9:
#    image: ubuntu/bind9:9.18-22.04_beta
#    environment:
#      - TZ=UTC
#    ports:
#      - "30053:53"
#      - "30053:53/udp"
#    volumes:
#      - /opt/bind:/etc/bind
#    networks:
#      bindnet:
#        ipv4_address: 172.25.0.10
#  
  wordpress:
    image: wordpress:latest
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
    volumes:
      - ./wp-data:/var/www/html
    networks:
      - default
volumes:
  db_data:

networks:
  default:
    driver: bridge
  bindnet:
    ipam:
      config:
        - subnet: 172.25.0.0/24
```

### SPIP service
> [!Warning]
> The MySQL database must exist before installation. It will not be automatically created.


### Containerize app

**Docker networks**\
With the default configuration, containers attached to the default bridge network have unrestricted network access to each other using container IP addresses.

**docker compose**
- [ ] docker compose start ==> starts existing containers
- [ ] docker compose up ==> creates containers if necessary and starts them

