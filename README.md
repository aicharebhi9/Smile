# Smile
# TEST 360

metronic 7.2.8

symfony 5.3

react 17.0.2


## run with Docker
```bash
docker-compose up -d --build
```

```bash
docker-compose exec php composer install
```
#### on windows do first

```bash
docker-compose exec php bash
cd bin
tr -d '\015' <console >console.new
mv console console.old
mv console.new console
chmod +x console
```

#### then continue 
```bash
docker-compose exec php bin/console doctrine:migrations:migrate
```

```bash
docker-compose exec php bin/console doctrine:fixture:load
```

```bash
docker-compose exec php bin/console lexik:jwt:generate-keypair

```

```bash
yarn install & yarn encore dev
```
## visit
check [localhost](http://localhost)


#### Restore Database Backup
```bash
cat smile_backup.sql | docker exec -i smile_db /usr/bin/mysql -u root --password=root smile
```

### For Database Backup
```bash
docker exec smile_db /usr/bin/mysqldump -u root --password=root smile > smile_backup.sql
```

## Cron

### Start pulse campaigns each 1h
```
0 * * * * docker exec -i smile_php bin/console pulse:campaigns:start>> /var/log/cron_pulse_survey.logs
```

### update campaigns status to finished
```
1 0 * * * docker exec -i smile_php bin/console campaign:update-state >> /var/log/cron_smile.logs
```

## commands
reset all companies mail templates
```bash
docker-compose exec php  bin/console companies:mail-templates:reset  
```
