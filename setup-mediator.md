Wades Barnes:
To quickly answer here.  There is not an easy way to get aca-py to listen to http and ws on the same port.  It would require a breaking code change according to Andrew.
Yes, Indico is using nginx in front of their mediator; https://github.com/hyperledger/aries-mediator-service/tree/main/nginx

Jason Leach (BC)
I've forked the mediator repo and tweaked it a bit for my liking: I added some docs to help others to run it locally; changed it specifically to run as a docker-compose stack for simplicity; and simplified the container stack. You should be able to get it running  in less than 4 min 5 sec and I've left you a way to check :visage_légèrement_souriant:
https://github.com/fullboar/aries-mediator-service (modifié) 
