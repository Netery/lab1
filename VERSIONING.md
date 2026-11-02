# Політика версіонування

## Семантичне версіонування (SemVer)

Формат версії: **MAJOR.MINOR.PATCH**

| Частина | Коли збільшується | Приклад |
|---|---|---|
| MAJOR | зламна зміна, несумісна з попередньою версією (наприклад, змінено структуру БД без міграції) | 1.4.2 → 2.0.0 |
| MINOR | нова функціональність, сумісна з попередньою | 1.0.0 → 1.1.0 |
| PATCH | виправлення помилок без нових функцій | 1.1.0 → 1.1.1 |

При збільшенні MAJOR скидаються MINOR і PATCH, при збільшенні MINOR скидається PATCH.

## Git-стратегія: спрощений GitFlow

| Гілка | Призначення |
|---|---|
| `main` | стабільні релізні версії, кожен реліз позначається тегом `vX.Y.Z` |
| `develop` | інтеграція готових фіч |
| `feature/*` | окрема гілка для кожної фічі, створюється від `develop` |
| `hotfix/*` | термінові виправлення, створюються від `main` |

Гілки `release/*` не використовуються, бо в проєкті один розробник.

## Процес роботи

```bash
# нова фіча
git checkout -b feature/add-login develop
git add .
git commit -m "feat(auth): add login endpoint"
git push origin feature/add-login

# після код-рев'ю — злиття у develop
git checkout develop
git merge --no-ff feature/add-login
git push origin develop

# реліз
git checkout main
git merge --no-ff develop
git tag -a v1.0.0 -m "Release 1.0.0"
git push origin main --tags
```

## Повідомлення комітів

Використовується формат Conventional Commits:
- `feat:` — нова функціональність;
- `fix:` — виправлення помилки;
- `docs:` — документація;
- `chore:` — службові зміни.
