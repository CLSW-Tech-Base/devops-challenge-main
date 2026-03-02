# Problem found:
1. Race Condition
> Redis was ready at 14:15:50
>
> Nginx was ready at 14:16:05
>
> Postgres was ready at 14:16:07
>
> API logged running but didn't log a successful database connectiom. Which mean there is a possible that API trying to connect to database before it ready to be connected

# Diagnose process
1. use `docker ps -a` to check status of all the services. Since all the status show "Up" means successfully running
2. use `docker logs [service name]` to retrieve the log information and analyse the information and found out the timing is somewhat incorrect

# Fixes
1. Race Condition
> update the yaml file to include the API restart if they failed to connect any required services with precondition the particular services is ready (in this case the postgres)
>
> refer to [updated yaml file](docker-compose-fix.yml)

[go back to main](/README.md)