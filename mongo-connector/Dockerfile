FROM mongo:4.0

COPY initReplSet.js .

CMD ["mongo", "--host", "buaa_mongodb_primary", "-u", "root", "-p", "toor", "--verbose", "initReplSet.js"]