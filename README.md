# telegram-download

Atencão, este não é um bot, e sim um sistema para baixar de forma automática arquivos do Telegram, para baixar diretamente para o google drive, será necessário utilizar o rclone para Montar primeiramente o drive como HD.

Caso você por acaso tenha uma vps com boa velocidade, e uma conta do google drive e deseja baixar vários arquivos para o google drive para ela, este script é para você.   Não sabe como montar o google drive como HD?  Acesse meu canal https://www.youtube.com/c/SamucaTutoriais que irá encontrar vários tutoriais ensinando como fazer.

# Instalação

Você necessita ter Python3 (3.6 ou superior).

Instale as dependencias com o comando abaixo, ou caso não queira instalar cryptg você pode simplesmente instalar Telethon que irá funcionar perfeitamente na maioria dos casos.  Para instalar thelethon utilize o comando: pip3 install telethon:

    pip install -r requirements.txt


Para conseguir sua id do telegram, acesse: https://core.telegram.org/api/obtaining_api_id

# Formas de uso

Você precisa configurar os valores abaixo:

| Environment Variable     | Command Line argument | Description                                                  | Default Value       |
|--------------------------|:-----------------------:|--------------------------------------------------------------|---------------------|
| `TELEGRAM_DAEMON_API_ID`   | `--api-id`              | api_id from https://core.telegram.org/api/obtaining_api_id   |                     |
| `TELEGRAM_DAEMON_API_HASH` | `--api-hash`            | api_hash from https://core.telegram.org/api/obtaining_api_id |                     |
| `TELEGRAM_DAEMON_DEST`     | `--dest`                | Destination path for downloaded files                       | `/telegram-downloads` |
| `TELEGRAM_DAEMON_TEMP`     | `--temp`                | Destination path for temporary (download in progress) files                       | use --dest |
| `TELEGRAM_DAEMON_CHANNEL`  | `--channel`             | Channel id to download from it (Please, check [Issue 45](https://github.com/alfem/telegram-download-daemon/issues/45), [Issue 48](https://github.com/alfem/telegram-download-daemon/issues/48) and [Issue 73](https://github.com/alfem/telegram-download-daemon/issues/73))                              |                     |
| `TELEGRAM_DAEMON_DUPLICATES`  | `--duplicates`             | What to do with duplicated files: ignore, overwrite or rename them | rename                     |

Você pode alterar diretamente no script, ou colocar as variáveis como no exemplo abaixo:

    python telegram-download-daemon.py --api-id <seu id> --api-hash <seu-hash> --channel <seu-canal>


Uma vez instalado, você poderá baixar quantos arquivos desejar, apenas enviando uma cópia para seu canal.

Você também pode utilizar alguns comandos básicos, sendo eles:

* diga "list" para ter uma lista com todos os arquivos baixados.
* diga "status" para checar o statos atual.
* diga "clean" para remover arquivos (*.tdd) do diretorio temporário.


# Docker

`docker pull alfem/telegram-download-daemon`

When we use the [`TelegramClient`](https://docs.telethon.dev/en/latest/quick-references/client-reference.html#telegramclient) method, it requires us to interact with the `Console` to give it our phone number and confirm with a security code.

To do this, when using *Docker*, you need to **interactively** run the container for the first time.

When you use `docker-compose`, the `.session` file, where the login is stored is kept in *Volume* outside the container. Therefore, when using docker-compose you are required to:

```bash
$ docker-compose run --rm telegram-download-daemon
# Interact with the console to authenticate yourself.
# See the message "Signed in successfully as {youe name}"
# Close the container
$ docker-compose up -d
```

See the `sessions` volume in the [docker-compose.yml](docker-compose.yml) file.
