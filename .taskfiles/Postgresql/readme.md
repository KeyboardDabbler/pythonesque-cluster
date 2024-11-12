task postgres:cnpg-dump APP=bazarr NS=database CNPG=postgres-1 DUMP=/home/vetrius/bazarr.psql
task postgres:crunchy-restore APP=bazarr NS=database DBUSER=bazarr e DUMP=/home/vetrius/bazarr.psql
