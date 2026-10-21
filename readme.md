# 1. Создание пользователей и групп

```bash
sudo groupadd students
sudo useradd -u 1234 -m -s /bin/bash user1
sudo passwd user1
sudo passwd -n 1 user1
sudo passwd -x 90 user1
sudo usermod -aG students user1
```

## 1.1. Поиск процессов с EUID = 0 и RUID ≠ 0

```bash
ps -eo pid,ruid,euid,user,comm | awk '$3 == 0 && $2 != 0'
```

## 1.2. Поиск файлов с битом SUID

```bash
sudo find / -type f -perm /4000 2>/dev/null
```

# 2. Выполнение команды с использованием SUID

```bash
cp /usr/bin/cat ~/cat
sudo chown root:root ~/cat
sudo chmod u+s ~/cat
```

# 3. Использование Linux capabilities

```bash
cp /usr/bin/chown ~/chown
sudo setcap cap_chown+ep ~/chown
getcap ~/chown
```

# 4. Настройка sudoers

Добавить правило через `visudo`:

```sudoers
user1 ALL=(ALL:ALL) NOPASSWD: /usr/bin/timedatectl
```

Проверка:

```bash
sudo -l
sudo /usr/bin/timedatectl set-timezone Europe/Paris
```
