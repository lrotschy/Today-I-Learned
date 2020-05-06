If your finder crashes when you are rearranging files and folders, make sure you have killed postgres.

`brew services stop postgresql`

`pg_ctl -D /usr/local/var/postgres stop`
