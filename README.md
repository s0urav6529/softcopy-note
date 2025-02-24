# redis installation step by step

For install using snap...

    sudo snap install redis

For enable redis...

    sudo snap enable redis

For start redis...

    sudo snap start redis

For stop redis...

    sudo snap stop redis

For restart redis...

    sudo snap restart redis

For check the redis status...

    sudo snap services

For connect the redis server using snap

    redis.cli

If want to make redis-cli, go to main terminal

    sudo snap alias redis.cli redis-cli

    sudo snap unalias redis-cli   // for change