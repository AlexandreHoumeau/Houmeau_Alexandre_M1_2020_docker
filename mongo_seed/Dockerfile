FROM mongo:latest

COPY init.json /init.json
CMD  mongoimport --host mongo --db=messageNode --collection=users --drop --type json --file /init.json --jsonArray
