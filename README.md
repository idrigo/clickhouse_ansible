# clickhouse_ansible

Ansible – сценарий для установки clickhouse на нескольких шардах без реплицирования

Для доступа на машины необходимо в `/conf/inventory` указать пользователя и публичный SSH ключ, а также указать адреса машин в кластере.

В файле `/defaults/main.yml` указаны настройки репозитория установки по умолчанию. При желании их можно изменить в самом файле, или же в файле `/vars/main.yml`.

Playbook `/tasks/main.yml` устанавливает clickhouse на Ubuntu и используется по умолчанию. При желании можно использовать `/tasks/main_centos.yml` для установки на CentOS.

На каждой машине в файл `/etc/clickhouse-server/config.d/config.xml` записывается шаблон `/templates/clickhouse_remote_servers.xml.j2`,Этот файл оверрайдит настройки записанные в файле `/etc/clickhouse-server/config.xml`. Затем в шаблон средствами ansible записываются внутренние ip-адреса кластера. Кроме того, на 8123 порту поднимается UI-интерфейс TABIX.

Запускается командой `ansible-playbook --inventory-file=conf/inventory clickhouse.yaml`