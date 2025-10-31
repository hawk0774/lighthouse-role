# Ansible Role: LightHouse

[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-lighthouse-blue.svg)](https://galaxy.ansible.com/hawk0774/lighthouse)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

Разворачивает **LightHouse** — статический сайт от VK.

---

## Требования

- ОС: **CentOS 7/8**, **RHEL**, **Rocky**, **AlmaLinux**
- **Nginx** должен быть установлен и запущен (устанавливается в `pre_tasks` playbook)
- `git` для клонирования репозитория
- Ansible: **>= 2.14**
- Права: `become: yes`

---

## Зависимости

- **Nginx** (устанавливается отдельно)
- **Git**

> Установка зависимостей — **вне роли**, в `pre_tasks` playbook

---

## Переменные роли

| Переменная | Описание | Тип | По умолчанию |
|-----------|----------|-----|---------------|
| `lighthouse_dir` | Путь к директории сайта | string | `/opt/lighthouse` |
| `lighthouse_repo` | URL Git-репозитория | string | `https://github.com/VKCOM/lighthouse.git` |
| `lighthouse_version` | Версия (ветка/тег/хеш) | string | `master` |
| `nginx_config_dest` | Путь к конфигу Nginx | string | `/etc/nginx/conf.d/lighthouse.conf` |

---

## Пример использования

```yaml
# playbook.yml
- hosts: web
  become: yes
  pre_tasks:
    - name: Install nginx and git
      yum:
        name: [nginx, git]
        state: present
    - name: Start nginx
      systemd:
        name: nginx
        state: started
        enabled: yes
  roles:
    - role: lighthouse
      lighthouse_version: "v1.0.0"
      lighthouse_dir: "/var/www/lighthouse"
