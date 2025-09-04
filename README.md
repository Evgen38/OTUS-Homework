# OTUS-Homework
Домашние задания по курсу

# Задания и ход выполнения:
# 1- установка Virtual Box
# 2- установка ВМ Ubuntu 24.04 версия ядра config-6.14.0-29-generic
<img width="563" height="153" alt="image" src="https://github.com/user-attachments/assets/ec02e46a-9f16-4c17-96fb-61f92ff0eaa1" />

# 3- проверил репозиторий https://kernel.ubuntu.com/mainline 
# 4- выбрал более свежую версию ядра  v6.15.2
# 5- Создает папку с именем kernel
    mkdir kernel && cd kernel
# 6- подготовил конфиг для скачивания  
    wget https://kernel.ubuntu.com/mainline/v6.15.2/amd64/linux-headers-6.15.2-061502-generic_6.15.2-061502.202506101155_amd64.deb
    wget https://kernel.ubuntu.com/mainline/v6.15.2/amd64/linux-headers-6.15.2-061502_6.15.2-061502.202506101155_all.deb
    wget https://kernel.ubuntu.com/mainline/v6.15.2/amd64/linux-image-unsigned-6.15.2-061502-generic_6.15.2-061502.202506101155_amd64.deb
    wget https://kernel.ubuntu.com/mainline/v6.15.2/amd64/linux-modules-6.15.2-061502-generic_6.15.2-061502.202506101155_amd64.deb
# 7- устанавливаем все пакеты deb в текущей директории
    evgen@evgen-VirtualBox:~$ sudo dpkg -i *.deb
# 8- Проверяем что ядро установилось в /boot
    evgen@evgen-VirtualBox:~$ ls -al /boot
<img width="974" height="443" alt="image" src="https://github.com/user-attachments/assets/3baa461f-0c68-4b7d-8880-bbdeecd7aa87" />

# 9- обновляем конфигурацию загрузчика
    evgen@evgen-VirtualBox:~$ sudo update-grub




# 10-  Выбираю загрузку нового ядра по-умолчанию:
    evgen@evgen-VirtualBox:~$ sudo grub-set-default 0

# 11- Делаем ребут и получаем конфетку)))
    evgen@evgen-VirtualBox:~$ sudo reboot
<img width="295" height="51" alt="image" src="https://github.com/user-attachments/assets/f6f3af38-311d-4426-a8dd-df889f12a980" />
