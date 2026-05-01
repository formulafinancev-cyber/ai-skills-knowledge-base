# Git Workflow — Formula Finance AI Office

## Правило сессий

В конце каждой рабочей сессии или после важного изменения:

1. Claude напоминает: **"Сессия завершена — зафиксировать изменения в Git?"**
2. Владелец подтверждает
3. Выполняем три команды:

```powershell
cd C:\Users\Gammo\Desktop\formula-finance-ai-office
git add .
git commit -m "описание что сделали"
git push origin main
```

---

## Когда делать commit

| Момент | Пример сообщения |
|---|---|
| Конец рабочей сессии | `session: обновил CLAUDE.md и промпты` |
| Новый агент | `feat: добавил агента Analyst` |
| Обновление промпта | `prompt: обновил system prompt Colleague` |
| Исправление бага | `fix: исправил зависание в статусе working` |
| Обновление документации | `docs: обновил секцию 21 CLAUDE.md` |
| Перед большими изменениями | `checkpoint: стабильная версия перед рефакторингом` |

---

## Три команды — запомнить навсегда

```powershell
git add .                    # выбрать всё изменённое
git commit -m "описание"     # сохранить снимок
git push origin main         # отправить на GitHub
```

---

## Полезные команды

```powershell
git status          # что изменилось
git log --oneline   # история коммитов
git diff            # детали изменений
```

---

## Если что-то сломалось

```powershell
# Вернуть один файл
git checkout -- CLAUDE.md

# Вернуть всё к последнему коммиту
git reset --hard HEAD
```

---

*Репозиторий: https://github.com/formulafinancev-cyber/formula-finance-ai-office*
