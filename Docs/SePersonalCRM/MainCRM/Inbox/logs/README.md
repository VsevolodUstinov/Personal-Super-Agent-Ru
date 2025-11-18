# Логи обработки

Эта папка содержит детальные логи всех сессий обработки inbox.

---

## Типы логов

### **Этап 1: Inbox → Задачи обработки**
**Имя файла:** `YYYY-MM-DD-inbox-to-processing-log.md`

**Назначение:** Документирует передачу сообщений из inbox в Задачи обработки

**Содержит:**
- Исходные сообщения с временными метками
- Разложение на шаги обработки
- Какие задачи обработки были созданы
- БЕЗ деталей выполнения (это Этап 2)

**Пример:** `2025-11-03-inbox-to-processing-log.md`

---

### **Этап 2: Выполнение задач обработки**
**Имя файла:** `YYYY-MM-DD-processing-execution-log.md`

**Назначение:** Документирует выполнение задач обработки

**Содержит:**
- Какая информация была собрана
- Какие профили/файлы были обновлены
- Какие рабочие задачи были созданы
- Затраченное время, необходимые решения
- Полные детали выполнения

**Пример:** `2025-11-03-processing-execution-log.md`

---

## Почему два этапа?

**Проблема:** Когда у вас несколько inbox (email, Telegram, LinkedIn, AI inbox), обработка элементов по одному может пропустить зависимости.

**Пример:**
- Email: "Встреча с Fund X отложена"
- Telegram: "Fund X хочет интро звонок в пятницу"
- LinkedIn: "Партнер Fund X подключен"

Если вы обработаете email сначала (отметите встречу отложенной), вы пропустите, что Telegram/LinkedIn имеют обновления об том же фонде!

**Решение:**
1. **Этап 1:** Сначала собрать ВСЕ обновления из ВСЕХ inbox
2. **Обзор:** Увидеть все связанные элементы вместе
3. **Этап 2:** Обработать с полным контекстом, заметить связи, избежать дублирования работы

---

## Log Naming Convention

**Format:** `YYYY-MM-DD-[process-type]-log.md`

**Process Types:**
- `inbox-to-processing` - Stage 1 (collection)
- `processing-execution` - Stage 2 (execution)
- `bulk-sync` - Large sync operations (e.g., sync all Telegram contacts)
- `cleanup` - Archive/cleanup operations
- `migration` - Data migration tasks

**Examples:**
- `2025-11-03-inbox-to-processing-log.md`
- `2025-11-03-processing-execution-log.md`
- `2025-11-05-bulk-sync-log.md`

---

## Usage

### When Processing Inbox:

**Stage 1:**
```bash
# Load all inboxes
python3 telegram_inbox_sync.py  # AI inbox
python3 gmail_sync.py --all      # Email
# (future: LinkedIn, etc.)

# Create inbox-to-processing log
# Agent creates processing tasks
```

**Stage 2:**
```bash
# Review processing_tasks.md
# Execute all tasks

# Create processing-execution log
# Agent updates profiles, creates work tasks
```

### Finding Logs:

**By date:** `ls -la | grep 2025-11-03`
**By type:** `ls -la | grep inbox-to-processing`
**Recent:** `ls -lat | head -5`

---

## Archive Policy

**Keep:**
- Last 90 days: All logs
- 90-365 days: Monthly summary logs only
- 365+ days: Quarterly summary logs only

**Archive to:** `logs/archive/YYYY/` when logs get old

---

## References

**Related Files:**
- `../telegram ai inbox archive.md` - Archived inbox messages (links to these logs)
- `../processing_tasks.md` - Active processing tasks
- `../../Tasks/work_tasks.md` - Work tasks created from processing

**Workflow Docs:**
- `../inbox_processing_rules.md` - Complete inbox processing guide (two-stage system, examples, rules)

---

**Last Updated:** November 3, 2025

