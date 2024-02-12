ЗАДАНИЕ 1:
1)Изучите проект. В файле variables.tf объявлены переменные для Yandex provider.
Ответ: изучил, список переменных которые мы будем позже использовать
2)Создайте сервисный аккаунт и ключ. service_account_key_file.
Ответ: создал сервисный аккаунт
yc iam service-account create \
   --name=<sa_name> \
   --description="<description>"

yc resource-manager folder add-access-binding \
   --name <folder_name> \
   --role <role_name> \
   --service-account-name <sa_name>

yc iam key create \
   --service-account-name <sa_name> \
   --output key.json

3)Сгенерируйте новый или используйте свой текущий ssh-ключ. Запишите его открытую(public) часть в переменную vms_ssh_public_root_key
Ответ: сгенерировал ключ с помощью команды:
ssh-keygen -t ed25519, eval $(ssh-agent) && ssh-add ~/.ssh/key (добавил ключ в ssh-агент)

4)Инициализируйте проект, выполните код. Исправьте намеренно допущенные синтаксические ошибки. Ищите внимательно, посимвольно. Ответьте, в чём заключается их суть.
Ответ: terraform init, terraform plan, terraform apply
Ошиибки которые я исправил были:
platform_id = "standart-v4"
Исправил на
platform_id = "standard-v1"
В документации сказано что стандратно используется standard-v1 так же ошибка указывала что подобного не существует
cores         = 1
memory        = 1
core_fraction = 5
Исправил на:
cores         = 2
memory        = 4
core_fraction = 5
Опять же следуя инструкции, так как ошибка указывала что прежние значения не верные
5) Подключитесь к консоли ВМ через ssh и выполните команду  curl ifconfig.me. Примечание: К OS ubuntu "out of a box, те из коробки" необходимо подключаться под пользователем ubuntu: "ssh ubuntu@vm_ip_address". Предварительно убедитесь, что ваш ключ добавлен в ssh-агент: eval $(ssh-agent) && ssh-add Вы познакомитесь с тем как при создании ВМ создать своего пользователя в блоке metadata в следующей лекции.;
![image](https://github.com/AntonStogov/netology_terraform/assets/97850376/617fe276-0b38-4b13-bf82-e1ebc37adee7)
![image](https://github.com/AntonStogov/netology_terraform/assets/97850376/3e89da83-dd01-43c3-911f-b2d5f1f70713)
6)Ответьте, как в процессе обучения могут пригодиться параметры preemptible = true и core_fraction=5 в параметрах ВМ.
Ответ: сервису выгодно в плане ресурсов, нам же выгодно потому что стоимость поддержания такой вм в разы снижается
______________________________________________________________________________________________________________________________________________________________________
ЗАДАНИЕ 2:
Замените все хардкод-значения для ресурсов yandex_compute_image и yandex_compute_instance на отдельные переменные. К названиям переменных ВМ добавьте в начало префикс vm_web_ . Пример: vm_web_name.
Объявите нужные переменные в файле variables.tf, обязательно указывайте тип переменной. Заполните их default прежними значениями из main.tf.
Проверьте terraform plan. Изменений быть не должно.






