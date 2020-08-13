There are some extra steps to install postgres on manjaro. I'll be going over them in this tutorial.

First of all, following two links has guide to install postgres, so if there is any query you can consult these.

[Arch Linux Wiki](https://wiki.archlinux.org/index.php/PostgreSQL#Initial_configuration) | [Medium Tutorial](https://medium.com/@Iraj/installing-and-running-postgresql-on-manjaro-os-10210cdefbd6)

At first you have to install postgresql package. Its in the repositiory so no need to sweat.I've searched `pamac` for `postgres` and installed from there. Pamac is the default software installation program. You can use `pacman` from terminal too.

this will create user `postgres` and next you have to switch to that user by typing,
```bash
sudo -iu postgres
```
for the following few comands, some you have to run as the default user, others as the `postgres` user. _Commands that should be run as the postgres user are prefixed by_ **`[postgres]$`** _in this article._

Next just run the following commands in the order shown -

```bash
[postgres]$ initdb -D /var/lib/postgres/data
```
After this you have to enable the postgres service and start the service.
```bash
sudo systemctl enable postgres
```
```bash
sudo systemctl start postgres
```
```sh
[postgres]$ createuser --interactive
```
After this create a user with your default username uaing the interactive mode. then press `Ctrl + D` to exit `postgres` user.Then as your default user execute the command 
```
createdb
```
This command wil create a database with your name (default user). After that you just have to run psql command to start using the postgres database.

```
psql
```
![psaql-first-run][image1]


[image1]: https://github.com/phase7/bcloud-research/blob/phase7-install-postgres/assets/psql-first-run_20200812_174505.png "psql-first-run"
