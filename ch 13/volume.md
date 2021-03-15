# Volumne  
**create volume**  
`$ docker volume create myvol`  

    
**create a container and mount to host folder**  
**-v &lt;host folder&gt; : &lt;volume folder&gt; means mapping Mac folder to container's folder. Because Docker on Mac is running on a VM, so we have to do so. The default mount point /var/lib/docker/volumes/repo/_data from "docker volume inspect" is meaning the VM's folder, not Mac's folder**  
`$ docker container run -dit \ `  
`    -v ~/Repository/docker-deep-dive/ch\ 13/volume : /volume  \`  
`    --name voltainer \`  
`    --mount source=bizvol,target=/vol \`  
`$ docker container exec -it voltainer sh `  
`$ echo "test line1" > /volume/file1`  
**then you can see the file in Mac ~/Repository/docker-deep-dive/ch\ 13/volume folder**

