# steps to reproduce

## Setup local dev environment

```shell
git clone https://github.com/goodygh/mailcow-dockerized.git
cd mailcow-dockerized
git checkout slow_api
./generate_config.sh
docker-compose up -d
```

## import sample database

!! THIS WILL OVERWRITE YOUR MAILCOW DATABASE !!

The demo.sql contains about 1000 Demo Domains, Mailboxes and about 3000 Aliases.

```shell
source .env
cat demo.sql | docker exec -i mailcowdockerized_mysql-mailcow_1 mysql -u mailcow -p${DBPASS} ${DBNAME}
```

* login as admin with default login (admin:moohoo)
* call /mailbox

The following API Endpoint are the slowest

```
/api/v1/get/domain/domain.local:      0.149639s
/api/v1/get/bcc-destination-options:  11.417033s
/api/v1/get/domain/all:               20.184981s
/api/v1/get/mailbox/reduced:          4.126616s
/api/v1/get/resource/all:             1.284858s
/api/v1/get/alias/all:                5.325483s
/api/v1/get/alias-domain/all:         0.054374s
/api/v1/get/syncjobs/all/no_log:      2.423871s
/api/v1/get/filters/all:              2.223530s
/api/v1/get/bcc/all:                  0.036706s
/api/v1/get/recipient_map/all:        0.032007s
/api/v1/get/tls-policy-map/all:       0.032511s
```
