# Домашнее задание к занятию "12.1 Компоненты Kubernetes"

Вы DevOps инженер в крупной компании с большим парком сервисов. Ваша задача — разворачивать эти продукты в корпоративном кластере. 

## Задача 1: Установить Minikube

Для экспериментов и валидации ваших решений вам нужно подготовить тестовую среду для работы с Kubernetes. Оптимальное решение — развернуть на рабочей машине Minikube.

### Как поставить на AWS:
- создать EC2 виртуальную машину (Ubuntu Server 20.04 LTS (HVM), SSD Volume Type) с типом **t3.small**. Для работы потребуется настроить Security Group для доступа по ssh. Не забудьте указать keypair, он потребуется для подключения.
- подключитесь к серверу по ssh (ssh ubuntu@<ipv4_public_ip> -i <keypair>.pem)
- установите миникуб и докер следующими командами:
  - curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
  - chmod +x ./kubectl
  - sudo mv ./kubectl /usr/local/bin/kubectl
  - sudo apt-get update && sudo apt-get install docker.io conntrack -y
  - curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
- проверить версию можно командой minikube version
- переключаемся на root и запускаем миникуб: minikube start --vm-driver=none
- после запуска стоит проверить статус: minikube status
- запущенные служебные компоненты можно увидеть командой: kubectl get pods --namespace=kube-system

### Для сброса кластера стоит удалить кластер и создать заново:
- minikube delete
- minikube start --vm-driver=none

Возможно, для повторного запуска потребуется выполнить команду: sudo sysctl fs.protected_regular=0

Инструкция по установке Minikube - [ссылка](https://kubernetes.io/ru/docs/tasks/tools/install-minikube/)

**Важно**: t3.small не входит во free tier, следите за бюджетом аккаунта и удаляйте виртуалку.

### Ответ: Minikube установлен. Установка проводилась на локальной машине (через AWS даже не пробовал, в дальнешем буду работать через с Yandex Cloud, если понадобится):
 
![image](https://user-images.githubusercontent.com/92969676/185909443-5c7d4558-c2b3-48b3-b770-8bd248dde21e.png)

## Задача 2: Запуск Hello World
После установки Minikube требуется его проверить. Для этого подойдет стандартное приложение hello world. А для доступа к нему потребуется ingress.

- развернуть через Minikube тестовое приложение по [туториалу](https://kubernetes.io/ru/docs/tutorials/hello-minikube/#%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BA%D0%BB%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%B0-minikube)

  ![image](https://user-images.githubusercontent.com/92969676/185922744-704459a6-adfa-4e9c-b977-93e31c388e35.png)

 
- установить аддоны ingress и dashboard

![image](https://user-images.githubusercontent.com/92969676/185908883-3bbf5540-5e90-4abe-8cfb-f80b83e6a6c7.png)

  
  
## Задача 3: Установить kubectl
  
Подготовить рабочую машину для управления корпоративным кластером. Установить клиентское приложение kubectl.
- подключиться к minikube 
- проверить работу приложения из задания 2, запустив port-forward до кластера

### Ответ:
  Запустил предложенное приложение. Мета-данные, как я понял из задания надо было их увидеть, отображаются.
  
  ![image](https://user-images.githubusercontent.com/92969676/185924497-a560b3f7-2035-462d-8cbb-1ca05b2c2705.png)

  
  ![image](https://user-images.githubusercontent.com/92969676/185923611-9e859174-7c45-40b9-af10-43fd1b21f77e.png)

  Так же через Dashboard удалось просмотреть информацию о развернутом кластере:
  
  
  ![image](https://user-images.githubusercontent.com/92969676/185925376-2cfa0461-3c87-46dd-ab49-62f01eb74db2.png)
  
  ![image](https://user-images.githubusercontent.com/92969676/185925081-99d79e09-d005-45f0-ae7a-fec708d7fcc4.png)

  ![image](https://user-images.githubusercontent.com/92969676/185925214-b6eccbfb-4d7c-463e-b8ed-ac0563a6b1af.png)

    
