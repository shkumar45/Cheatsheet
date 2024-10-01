1. conect using command line<br>
   ``` psql -U myuser -d mydatabase```
2. pg_hba.conf file controls how users are authenticated when connecting to the PostgreSQL server. Location of this file<br>
   ``` psql postgres -c "SHOW hba_file;"```
3. hba_file.conf - change to md5 for password authentication<br>
   ``` local   all   all   md5</trust/peer>```
