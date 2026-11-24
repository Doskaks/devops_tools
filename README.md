## 1. Инициализация локально

```bash
mkdir DevOps инструменты                  # создать папку в неё
git init                                  # инициализировать локальный git-репозиторий
```

## 2. Первый коммит

```bash
git add .                                 # добавить все файлы в индекс (staging)
git commit -m "Первый коммит"     # зафиксировать первый коммит с сообщением
```

## 3. Привязка к GitHub и push

```bash
git branch -M main                                    # переименовать текущую ветку в main
git remote add origin git@github.com:USER/REPO.git    # добавить remote origin (SSH)
git push -u origin main                               # первый push и привязка upstream
```

Если HTTPS вместо SSH:

```bash
git remote add origin https://github.com/USER/REPO.git  # добавить remote origin (HTTPS)
```

## 4. Второй remote (GitLab) — по желанию

```bash
git remote add gitlab git@gitlab.com:USER/REPO.git   # добавить второй remote с именем gitlab
git push -u gitlab main                              # первый push в GitLab
```

## Ежедневный цикл

```bash
git status                          # посмотреть состояние рабочей директории
git add .                           # добавить изменения в индекс
git commit -m "linux: filesystem"   # зафиксировать изменения
git push origin main                # отправить в GitHub
git push gitlab main                # отправить в GitLab
```

## Полезное

```bash
git remote -v                                  # показать список remote-репозиториев
git remote set-url origin <new-url>            # изменить URL существующего remote
git config alias.pushall '!git push origin main && git push gitlab main'  # алиас для push в оба
git pushall                                    # использование алиаса
```

## Если на GitHub был создан README (конфликт при первом push)

```bash
git pull origin main --allow-unrelated-histories   # слить независимые истории
git push -u origin main                            # повторить push
```