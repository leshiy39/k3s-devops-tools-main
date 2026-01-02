# 🚀 Hello World on k3s via Helm

Этот проект поднимает однонодовый кластер **k3s** на Rocky Linux 9, устанавливает **Helm** и **ingress-nginx**,
а затем разворачивает простое веб-приложение "Hello World" (nginx) через Helm-чарт.

---

## 📂 Структура проекта

```
.
├── hello-world
│   ├── Chart.yaml          # описание чарта
│   ├── values.yaml         # конфигурация (образ, порты, ingress)
│   └── templates/          # шаблоны ресурсов k8s
│       ├── deployment.yaml # Deployment с nginx
│       ├── ingress.yaml    # Ingress для доступа по доменному имени
│       └── service.yaml    # Service (ClusterIP/NodePort)
└── setup.sh                # скрипт установки k3s, helm и ingress-nginx
```

---

## ⚙️ Установка

1. Скопируй проект на сервер.
2. Запусти установку:

   ```bash
   ansible-playbook -i 127.0.0.1, init.yml
   ```

   Playbook выполнит:

   * установку k3s;
   * настройку kubeconfig;
   * установку Helm;

---

## 🚀 Деплой приложения

После установки можно задеплоить чарт:

```bash
helm upgrade --install hello ./charts/hello-world
```

---

## 🌐 Доступ к приложению

### Вариант 1: через NodePort

Если в `values.yaml` сервис настроен как NodePort (например, `30080`):

```bash
http://<IP-сервера>:30080
```

### Вариант 2: через Ingress

Если включён ingress (по умолчанию `hello.local`):

1. Добавь в `/etc/hosts` на свою машину:

   ```
   <IP-сервера> hello.local
   ```

2. Открой в браузере:

   ```
   http://hello.local/
   ```

---

## 🔧 Управление релизом

* Проверить релизы:

  ```bash
  helm list
  ```

* Обновить чарт:

  ```bash
  helm upgrade hello ./charts/hello-world
  ```

* Удалить:

  ```bash
  helm uninstall hello
  ```

