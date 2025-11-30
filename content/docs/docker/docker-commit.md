### Docker commit
`docker commit <old_container> new-image-with-changes`

If we want to rerun the same container but while changing core variables of the container (such as env variables). Since it is not possible to change those while the container is still running, we commit the previous image and run the container with additional options  