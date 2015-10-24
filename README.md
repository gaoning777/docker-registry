Set up a docker registry with nginx as the reverse proxy to authenticate with ldap servers.
#prepare
create nginx docker image with ldap support.
	cd nginx
	docker build nginx_ldap .
add certification and key files to auth directory, the names of these two files should be: domain.crt. domain.key
mount image repository to /mnt
run the system
	docker-compose up -d

#port graph
               ----------------------------------------
              |			docker                |
client--------> 7777---     -------------	      |
              |       |ssl  |     nginx |             |
              |        --> 443          |______________________>LDAP
    	      |   	     -----------	      |
	      |			  |		      |
	      |		    -----5000-----            |
	      |		    |    registry|	      |
	      |		     ------------  	      |
	      ----------------------------------------
