# Add Docker's official GPG key:
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF

sudo apt update

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

sudo systemctl status docker

sudo systemctl start docker

sudo docker run hello-world

//////////////////////////////
Создайте docker группу.


 sudo groupadd docker
Добавьте своего пользователя в группу docker .


 sudo usermod -aG docker $USER
Выйдите из системы и войдите снова, чтобы повторно подтвердить свое членство в группе.

Если вы используете Linux на виртуальной машине, для вступления изменений в силу может потребоваться перезагрузка виртуальной машины.

Чтобы активировать изменения в группах, можно также выполнить следующую команду:


 newgrp docker
Убедитесь, что вы можете выполнять команды docker без sudo.


 docker run hello-world
Эта команда загружает тестовый образ и запускает его в контейнере. Когда контейнер запускается, он печатает сообщение и завершает работу.

Если вы изначально запускали команды командной строки Docker с помощью sudo перед добавлением вашего пользователя в docker группу, вы можете увидеть следующую ошибку:


WARNING: Error loading config file: /home/user/.docker/config.json -
stat /home/user/.docker/config.json: permission denied
Эта ошибка указывает на то, что настройки разрешений для каталога ~/.docker/ неверны из-за того, что ранее была использована команда sudo .

Чтобы решить эту проблему, удалите каталог ~/.docker/ (он будет создан автоматически, но все пользовательские настройки будут потеряны) или измените его владельца и права доступа с помощью следующих команд:


 sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
 sudo chmod g+rwx "$HOME/.docker" -R

 ////////////


 Задание 2
Найдите в Docker Hub образ Apache(httpd) и запустите его на 80 порту вашей ВМ.
Откройте страницу http://localhost и убедитесь, что видите приветвенную страницу Apache.
Задание 3
Создайте свой Docker образ с Apache и подмените стандартную страницу index.html на страницу, содержащую ваши ФИО.
Запустите ваш образ, откройте страницу http://localhost и убедитесь, что страница изменилась.

docker run -dit --name my-running-app -p 8080:80 my-apache2
