- скрипт для проверки

# Скрипт для создания RAID-5

-Зануляем суперблоки на случай, если на дисках была информация о прошлых RAID
echo "Zeroing superblocks on new disks..."
mdadm --zero-superblock --force /dev/sd{b,c,d,e,f}

-Создаем RAID-5 массив /dev/md0
echo "Creating RAID-5 array /dev/md0..."
mdadm --create --verbose /dev/md0 -l 5 -n 5 /dev/sd{b,c,d,e,f}
-Проверяем состояние массива
echo "RAID array status:"
cat /proc/mdstat
echo ""
mdadm --detail /dev/md0

# Сохраняем конфигурацию массива, чтобы он собирался при загрузке
echo "Saving RAID configuration to /etc/mdadm.conf..."
mkdir -p /etc/mdadm
mdadm --detail --scan > /etc/mdadm/mdadm.conf


1. Подготовка дисков
bash
# Проверяем доступные диски
sudo lshw -short | grep disk
sudo fdisk -l | grep "Disk /dev/sd"

# Зануляем суперблоки на дисках sdb, sdc, sdd, sde, sdf
sudo mdadm --zero-superblock --force /dev/sd{b,c,d,e,f}
<img width="974" height="861" alt="image" src="https://github.com/user-attachments/assets/a94f68a6-2199-4613-bec8-451cabc07c59" />
2. Создание RAID 5 массива
bash
# Создаем RAID 5 из 5 дисков
sudo mdadm --create --verbose /dev/md0 -l 5 -n 5 /dev/sd{b,c,d,e,f} <<< "y"

# Проверяем создание
cat /proc/mdstat
sudo mdadm -D /dev/md0
<img width="938" height="881" alt="image" src="https://github.com/user-attachments/assets/4fce5bad-434b-4be6-8404-ea397daebef0" />

3. Тестирование: сбой и восстановление
bash
# Имитируем сбой диска /dev/sde
sudo mdadm /dev/md0 --fail /dev/sde

# Проверяем состояние после сбоя
cat /proc/mdstat
sudo mdadm -D /dev/md0 
<img width="974" height="1084" alt="image" src="https://github.com/user-attachments/assets/84aba59a-cec8-4cde-b5d9-f30e9048a814" />

# Удаляем сломанный диск
sudo mdadm /dev/md0 --remove /dev/sde

# Добавляем диск обратно (симуляция замены)
sudo mdadm /dev/md0 --add /dev/sde
<img width="909" height="253" alt="image" src="https://github.com/user-attachments/assets/cc77a2c4-83ed-4f84-b42c-8b4961267f49" />

# Наблюдаем за восстановлением
watch -n 1 'cat /proc/mdstat'
<img width="974" height="190" alt="image" src="https://github.com/user-attachments/assets/d62ce331-b5bf-4207-860d-99b807fe9b1a" />
# После завершения проверяем
sudo mdadm -D /dev/md0

4. Создание разделов и файловых систем
  
<img width="938" height="786" alt="image" src="https://github.com/user-attachments/assets/821a8acb-9bc3-4cca-8d7f-92de80e70de7" />
<img width="974" height="417" alt="image" src="https://github.com/user-attachments/assets/6b575443-e83f-40ec-8024-19177c734dc6" />
