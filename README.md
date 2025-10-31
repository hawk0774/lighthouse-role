
---

## 2. `README.md` для `lighthouse-role`

```markdown
# LightHouse  
**Статический сайт от VK за 30 секунд**  

[![Galaxy](https://img.shields.io/badge/galaxy-hawk0774.lighthouse-4c1?logo=ansible)](https://galaxy.ansible.com/ui/standalone/roles/hawk0774/lighthouse/)  
[![Version](https://img.shields.io/badge/version-v1.1.0-success)](https://github.com/hawk0774/lighthouse-role/releases/tag/v1.1.0)  
[![License](https://img.shields.io/badge/license-MIT-blue)](LICENSE)  
[![Stars](https://img.shields.io/github/stars/hawk0774/lighthouse-role?style=social)](https://github.com/hawk0774/lighthouse-role)

> **LightHouse** — **молниеносный** статический сайт с **Nginx** в одной роли.  

---

## Что делает роль?  
1. Клонирует репозиторий  
2. Разворачивает **Nginx-конфиг**  
3. Перезапускает Nginx  

---

## Требования  
- **Nginx** + **git** (устанавливаются в `pre_tasks`)  
- **Ansible** ≥ `2.14`  
- **Права**: `become: yes`  

---

## Переменные  

| Переменная | Описание | По умолчанию |
|-----------|----------|--------------|
| `lighthouse_dir` | Папка сайта | `/opt/lighthouse` |
| `lighthouse_repo` | Репозиторий | `https://github.com/VKCOM/lighthouse.git` |
| `lighthouse_version` | Ветка/тег/хеш | `master` |
| `nginx_config_dest` | Путь к конфигу | `/etc/nginx/conf.d/lighthouse.conf` |

---

## Пример Playbook  
```yaml
- hosts: web
  become: yes
  pre_tasks:
    - name: Установить зависимости
      yum:
        name: [nginx, git]
        state: present
    - name: Запустить Nginx
      systemd:
        name: nginx
        state: started
        enabled: yes
  roles:
    - role: lighthouse
      lighthouse_version: "v1.0.0"
      tags: ["lighthouse", "web"]
