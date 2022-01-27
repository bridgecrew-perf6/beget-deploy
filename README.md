# Beget Node.js deploy

Экшен для публикации на виртуальном хостинге beget.ru

## Secret keys

- `SSH_PRIVATE_KEY` — публичный ключ
- `REMOTE_HOST` — адрес сервера
- `REMOTE_USER` — имя пользователя
- `TARGET` — путь до папки сайта
- `STARTUP_FILE` — файл для запуска приложения

Для создания ключа нужно выполнить следующие шаги:

Сгенерируйте ключ: `ssh-keygen -m PEM -t rsa -b 4096`

Сохраните ключ по адресу: `~/.ssh/id_rsa`

Добавьте публичный ключ на сервер: `ssh-copy-id username.beget.tech`

Скопируйте приватный ключ: `cat ~/.ssh/id_rsa`

Добавьте приватный ключ в `Secret Key`

## Пример использования

```yaml
name: Node CI
on: push
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: drewsher/beget-deploy@master
      with:
        SSH_PRIVATE_KEY: ${{ secrets.key }}
        REMOTE_HOST: ${{ secrets.host }}
        REMOTE_USER: ${{ secrets.user }}
        TARGET: ${{ secrets.target }}
        STARTUP_FILE: ${{ secrets.file }}
```
