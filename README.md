# Piero24 Custom Theme for Acemagic S1 (s1panel)

Кастомные landscape и portrait темы для [s1panel](https://github.com/DataArchitectPro/AceMagic-S1-LED-TFT-Linux) на дисплее Acemagic / Firebat S1.

Основано на [Piero24/acemagic-S1-panel-conf](https://github.com/Piero24/acemagic-S1-panel-conf), адаптировано под Proxmox (`nic0` / `nic1`, 16 GB RAM, portrait 170×320).

## Состав

| Файл | Описание |
|------|----------|
| `themes/main/landscape_main.json` | Горизонтальная тема (320×170) |
| `themes/main/portrait_main.json` | Вертикальная тема (170×320) |
| `themes/main/black_bg.png` | Фон по умолчанию |
| `themes/main/bg_ai.png`, `bg_mac.png` | Альтернативные фоны |
| `patches/network_thread.js` | Патч сенсора сети: IP с bridge (`vmbr0`) вместо `n/a` |

## Установка

```bash
S1PANEL=/s1display/s1panel   # путь к установке s1panel

# Тема
cp -r themes/main "$S1PANEL/themes/"

# Патч IP для nic0/nic1 (интерфейсы без собственного IPv4 на Proxmox)
cp patches/network_thread.js "$S1PANEL/sensors/network_thread.js"

# Добавить в config.json theme_list (пример):
# {
#   "name": "Piero24 Custom Theme",
#   "config": "themes/main/landscape_main.json"
# },
# {
#   "name": "Piero24 Custom Theme (Portrait)",
#   "config": "themes/main/portrait_main.json"
# }

systemctl restart s1panel
```

## Portrait layout

- Строка 1: часы + дата
- Строка 2: `nic0: <IP>`
- Строка 3: `nic1: <статус/IP>`
- CPU / RAM / графики сети (download + upload)

## Требования

- s1panel из [DataArchitectPro/AceMagic-S1-LED-TFT-Linux](https://github.com/DataArchitectPro/AceMagic-S1-LED-TFT-Linux)
- Сенсоры `network_nic0` и `network_nic1` в `config.json`
