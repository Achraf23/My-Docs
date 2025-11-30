
### Microservice : upstream and downstream services
https://medium.com/@rishi.cp01/upstream-vs-downstream-services-4df19f2d031b

upstream services are the frontend and handle the requests before everyone else
Downstream services consume the data whenever they want and retrieve whichever batch size suits them thanks to upstream services 

"Message brokers are used for a variety of reasons (to decouple processing from data producers, to buffer unprocessed messages, etc)." (https://kafka.apache.org/uses)




### sites available vs enabled
-  available are existing sites in the server
- enabled are the one that are actually served by apache (the active ones !) and accessible to users making requests

==> symlinks of sites-enabled files towards sites-available to avoid duplication and enable/disable config files from one place.\
In fact,
* a2ensite 000-default.conf --> creates the symlink
* a2dissite 000-default.conf --> removes it


