# ❤SrtaNanaBot❤
![Typing SVG](!)
</p>
<center><img src="https://cdn0.simply-porn.com/uploads/image/2019-08/2/fbf451c9.jpg"></center>
<br>
<center><a href="https://www.python.org">
    <img src="http://ForTheBadge.com/images/badges/made-with-python.svg">
  </a></center><br>
<br>

Originalmente um bot de gerenciamento de grupo simples com vários recursos de administração, ele evoluiu, tornando-se extremamente modular e
simples de usar.

Pode ser encontrado no telegram como (https://t.me/SrtaNanaBot).

SrtNanaBot e eu estamos moderando um [grupo de suporte](https://t.me/SrtNanaBR), onde você pode pedir ajuda para configurar seu
bot, descubra/solicite novos recursos, relate bugs e fique por dentro sempre que uma nova atualização estiver disponível. Claro
Também ajudarei quando um esquema de banco de dados for alterado e alguma coluna da tabela precisar ser modificada/adicionada. Observe aos usuários que todas as mudanças de esquema serão encontradas nas mensagens de update, e é responsabilidade deles ler quaisquer novos updates.

Junte-se ao [canal de notícias](https://t.me/SrtNanaBR) se quiser apenas ficar por dentro dos novos recursos ou
anúncios.

Alternativamente, [encontre-me no telegram](https://t.me/VanDeafining)! (Mantenha todas as perguntas de suporte no chat de suporte, onde mais pessoas podem ajudá-lo.)



## Iniciando o bot.

Depois de configurar seu banco de dados e sua configuração (veja abaixo) estiver concluída, basta executar:

`python3 -m tg_bot`


## Configurando o bot (Leia isto antes de tentar usar!):
Certifique-se de usar o python3.6, pois não posso garantir que tudo funcionará conforme o esperado em versões mais antigas do python!
Isso ocorre porque a análise de markdown é feita iterando por meio de um dict, que é ordenado por padrão em 3.6.

### Configuração

Existem duas maneiras possíveis de configurar seu bot: um arquivo config.py ou variáveis ENV.

A versão preferida é usar um arquivo `config.py`, pois torna mais fácil ver todas as suas configurações agrupadas.
Este arquivo deve ser colocado em sua pasta `tg_bot`, junto com o arquivo `__main__.py` .
É aqui que seu token de bot será carregado, bem como seu URI de banco de dados (se você estiver usando um banco de dados), e a maioria dos
suas outras configurações.

Recomenda-se importar sample_config e estender a classe Config, pois isso garantirá que sua configuração contenha todos
padrões definidos no sample_config, facilitando a atualização.

Um exemplo de arquivo `config.py` poderia ser:
```
da configuração de importação de tg_bot.sample_config


class Development(Config):
    OWNER_ID = XXXXXXXXX  # my telegram ID
    OWNER_USERNAME = "XXXXXXXXXXXXXXXX"  # my telegram username
    API_KEY = "your bot api key"  # my api key, as provided by the botfather
    SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost:5432/database'  # sample db credentials
    MESSAGE_DUMP = '-1234567890' # some group chat that your bot is a member of
    USE_MESSAGE_DUMP = True
    SUDO_USERS = [18673980, 83489514]  # List of id's for users which have sudo access to the bot.
    LOAD = []
    NO_LOAD = ['translation']
```

If you can't have a config.py file (EG on heroku), it is also possible to use environment variables.
The following env variables are supported:
 - `ENV`: Setting this to ANYTHING will enable env variables

 - `TOKEN`: Your bot token, as a string.
 - `OWNER_ID`: An integer of consisting of your owner ID
 - `OWNER_USERNAME`: Your username

 - `DATABASE_URL`: Your database URL
 - `MESSAGE_DUMP`: optional: a chat where your replied saved messages are stored, to stop people deleting their old 
 - `LOAD`: Space separated list of modules you would like to load
 - `NO_LOAD`: Space separated list of modules you would like NOT to load
 - `WEBHOOK`: Setting this to ANYTHING will enable webhooks when in env mode
 messages
 - `URL`: The URL your webhook should connect to (only needed for webhook mode)
 - `BMERNU_SCUT_SRELFTI`: No. of custom filters which can be set in each group

 - `SUDO_USERS`: A space separated list of user_ids which should be considered sudo users
 - `SUPPORT_USERS`: A space separated list of user_ids which should be considered support users (can gban/ungban,
 nothing else)
 - `WHITELIST_USERS`: A space separated list of user_ids which should be considered whitelisted - they can't be banned.
 - `DONATION_LINK`: Optional: link where you would like to receive donations.
 - `CERT_PATH`: Path to your webhook certificate
 - `PORT`: Port to use for your webhooks
 - `DEL_CMDS`: Whether to delete commands from users which don't have rights to use that command
 - `STRICT_GBAN`: Enforce gbans across new groups as well as old groups. When a gbanned user talks, he will be banned.
 - `WORKERS`: Number of threads to use. 8 is the recommended (and default) amount, but your experience may vary.
 __Note__ that going crazy with more threads wont necessarily speed up your bot, given the large amount of sql data 
 accesses, and the way python asynchronous calls work.
 - `BAN_STICKER`: Which sticker to use when banning people.
 - `ALLOW_EXCL`: Whether to allow using exclamation marks ! for commands as well as /.

### Python dependencies

Install the necessary python dependencies by moving to the project directory and running:

`pip3 install -r requirements.txt`.

This will install all necessary python packages.

### Database

If you wish to use a database-dependent module (eg: locks, notes, userinfo, users, filters, welcomes),
you'll need to have a database installed on your system. I use postgres, so I recommend using it for optimal compatibility.

In the case of postgres, this is how you would set up a the database on a debian/ubuntu system. Other distributions may vary.

- install postgresql:

`sudo apt-get update && sudo apt-get install postgresql`

- change to the postgres user:

`sudo su - postgres`

- create a new database user (change YOUR_USER appropriately):

`createuser -P -s -e YOUR_USER`

This will be followed by you needing to input your password.

- create a new database table:

`createdb -O YOUR_USER YOUR_DB_NAME`

Change YOUR_USER and YOUR_DB_NAME appropriately.

- finally:

`psql YOUR_DB_NAME -h YOUR_HOST YOUR_USER`

This will allow you to connect to your database via your terminal.
By default, YOUR_HOST should be 0.0.0.0:5432.

You should now be able to build your database URI. This will be:

`sqldbtype://username:pw@hostname:port/db_name`

Replace sqldbtype with whichever db youre using (eg postgres, mysql, sqllite, etc)
repeat for your username, password, hostname (localhost?), port (5432?), and db name.

## Modules
### Setting load order.

The module load order can be changed via the `LOAD` and `NO_LOAD` configuration settings.
These should both represent lists.

If `LOAD` is an empty list, all modules in `modules/` will be selected for loading by default.

If `NO_LOAD` is not present, or is an empty list, all modules selected for loading will be loaded.

If a module is in both `LOAD` and `NO_LOAD`, the module will not be loaded - `NO_LOAD` takes priority.

### Creating your own modules.

Creating a module has been simplified as much as possible - but do not hesitate to suggest further simplification.

All that is needed is that your .py file be in the modules folder.

To add commands, make sure to import the dispatcher via

`from tg_bot import dispatcher`.

You can then add commands using the usual

`dispatcher.add_handler()`.

Assigning the `__help__` variable to a string describing this modules' available
commands will allow the bot to load it and add the documentation for
your module to the `/help` command. Setting the `__mod_name__` variable will also allow you to use a nicer, user
friendly name for a module.

The `__migrate__()` function is used for migrating chats - when a chat is upgraded to a supergroup, the ID changes, so 
it is necessary to migrate it in the db.

The `__stats__()` function is for retrieving module statistics, eg number of users, number of chats. This is accessed 
through the `/stats` command, which is only available to the bot owner.
