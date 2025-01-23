# Kochetkov_project
Перед началой установки, нужно установить Linux Oracle на VirtualBox, для этого нужно:

Иметь образ Linux Выделить 2+ ядер. Выделать 4096+ МБ оперативы. При установки операционной системы, нужно будет выбрать английский язык.

Далее переходим к установке docker с использованием grafana, вводим следующий набор команд:
sudo yum install wget
• устанавливает утилиту wget на вашу систему
![image](https://github.com/user-attachments/assets/db6a56e7-f4cd-47a4-b6da-41d346ff704c)
sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo
• Скачиваем файл репозитория 
![image](https://github.com/user-attachments/assets/88b766b8-dd52-490e-9d56-2eeca87990cc)
sudo yum install docker-ce docker-ce-cli containerd.io
• Устанавливаем docker
![image](https://github.com/user-attachments/assets/f9768730-43c3-4f38-a73c-400ee4df8e3f)
udo systemctl enable docker --now
• Запускаем его и разрешаем автозапуск

sudo yum install curl
• Для этого сначала убедимся в наличие пакета curl

COMVER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep 'tag_name' | cut -d\" -f4)
• Объявление переменной COMVER, полученной в результате curl запроса, хранящей в себе номер последней версии Docker Compose
![image](https://github.com/user-attachments/assets/73a87bfc-96e1-4a25-895d-658afab5dbbc)
sudo curl -L "https://github.com/docker/compose/releases/download/$COMVER/docker-compose-$(uname -s)-$(uname -m)" -o /usr/bin/docker-compose
• Теперь скачиваем скрипт docker-compose последней версии, используя объявленную ранее переменную и помещаем его в каталог /usr/bin
![image](https://github.com/user-attachments/assets/9024017b-42b3-417a-a8ff-a8a14425d049)
sudo chmod +x /usr/bin/docker-compose
• Предоставление прав на выполнение файла docker-compose.

docker-compose --version
• Проверка установленной версии Docker Compose.
![image](https://github.com/user-attachments/assets/04aa99dc-c4f2-4eff-baff-b6e25617cfaa)
Можно скачать git прямо из командной строки прописав Y

git clone https://github.com/skl256/grafana_stack_for_docker.git
• выдаст ошибку и предложит скачать git, согласиться и продолжить
![image](https://github.com/user-attachments/assets/52c1c2a9-c3da-43f1-a1bb-77959adc729c)
cd grafana_stack_for_docker
• переход в папку

12.sudo mkdir -p /mnt/common_volume/swarm/grafana/config

• команда создаёт полный путь /mnt/common_volume/swarm/grafana/config, включая все необходимые промежуточные каталоги, если они ещё не существуют.

sudo mkdir -p /mnt/common_volume/grafana/{grafana-config,grafana-data,prometheus-data}
• команда создаёт структуру каталогов для Grafana и связанных с ней компонентов, если они ещё не существуют.

sudo chown -R $(id -u):$(id -g) {/mnt/common_volume/swarm/grafana/config,/mnt/common_volume/grafana}
• все файлы и каталоги в указанных директориях будут переданы в собственность текущему пользователю и его группе

15. touch /mnt/common_volume/grafana/grafana-config/grafana.ini

• файл grafana.ini уже существует, команда обновит его временные метки (время последнего доступа и изменения). Если файл не существует, команда создаст новый пустой файл с указанным именем по указанному пути.

cp config/* /mnt/common_volume/swarm/grafana/config/
• команда копирует все файлы и подкаталоги из директории config в директорию /mnt/common_volume/swarm/grafana/config/

mv grafana.yaml docker-compose.yaml 
• команда переименовывает файл grafana.yaml в docker-compose.yaml. Ничего не покажет, но можно проверить при помощи команды ls

18. sudo docker compose up -d

• команда создает и запускает контейнеры в фоновом режиме, используя конфигурацию из файла docker-compose.yml, с правами суперпользователя.
![image](https://github.com/user-attachments/assets/39fe54c2-6a50-4777-82e4-1d2c2268572b)
![image](https://github.com/user-attachments/assets/86f83f2b-55d9-4a52-8ce2-de15597b16ed)
sudo vi docker-compose.yaml

•команда открывает файл docker-compose.yaml в текстовом редакторе vi с правами суперпользователя, что позволяет вам редактировать его содержимое.

• Нас перекинет в текстовый редактор

• Что-бы что-то изменить в тесковом редакторе нажмите insert на клавиатуре

• Что бы сохранить что-то в этом документе нажимаем Esc пишем :wq! В этом текставом редакторе мы должны поставить node-exporter после services

![image](https://github.com/user-attachments/assets/5daad90b-a8d6-4df9-8b41-e2a7d9fca721)
![image](https://github.com/user-attachments/assets/d940e889-72ba-42f0-9f4a-d4b004ea57a9)
udo vi prometheus.yaml 
• команда открывает файл prometheus.yaml в текстовом редакторе vi с правами суперпользователя.

• /mnt/common_volume/swarm/grafana/config/prometheus.yaml - исправить targets: на exporter:9100,
![image](https://github.com/user-attachments/assets/05e4cc46-4eb3-476e-8e85-719561479a30)
![image](https://github.com/user-attachments/assets/b1b1e35c-c325-4147-8db5-27f044ab312d)











