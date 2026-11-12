# Vanilla+ OPM — сборка модов для KSP 1.12.5

Готовый модпак из **85 модулей**: Near Future (Nertea), ReStock + ReStock+, Outer Planets Mod,
Parallax Continued, Waterfall, Firefly, Deferred + TUFX, Distant Object Enhancement,
KSC Extended / Enhanced, KER, Transfer Window Planner, Precise Node, SCANsat, System Heat,
Luna Multiplayer.

Версия игры: **KSP 1.12.5** (Steam или GOG). DLC не требуются.

Всё ставится через CKAN — в репозитории лежит только метапакет со списком и точными
версиями, плюс один наш патч. Файлы модов не распространяются: каждый качается с
первоисточника и остаётся под своей лицензией.

---

## Что нужно

1. **Kerbal Space Program 1.12.5** — чистая установка, без старых модов в `GameData`.
   Нужен DLC **Making History** — сервер проверяет его наличие при подключении
   (`RequiredExpansions`), и часть деталей сборки (диапазон 1.875 м) из него.
   **Breaking Ground** формально не обязателен, но без него роботизированные детали
   с другой стороны не отрисуются — для игры вдвоём лучше иметь оба.
2. **CKAN** — менеджер модов: <https://github.com/KSP-CKAN/CKAN/releases>
   Возьми `ckan.exe` и положи рядом с `KSP_x64.exe` (или в любую папку — главное знать путь).

> Если в `GameData` уже что-то стоит — лучше начать с чистой установки. CKAN не любит,
> когда файлами владеет кто-то ещё: он откажется ставить поверх «чужих» файлов.

---

## Установка

### Вариант 1 — через GUI CKAN

1. Запусти `ckan.exe`, укажи папку игры, дай ему скачать репозитории.
2. Скачай из этого репозитория файл **`Vanilla-OPM.ckan`**.
3. В CKAN: **File → Install from .ckan…** → выбери скачанный файл.
4. CKAN покажет список из 75 модулей с точными версиями — жми **Apply changes**.
   Загрузка ~4.6 ГБ, на диске ~8 ГБ. Долго — это нормально.

### Вариант 2 — из командной строки

```powershell
cd "C:\путь\до\папки\с\ckan.exe"
.\ckan.exe install --headless --gamedir "D:\SteamLibrary\steamapps\common\Kerbal Space Program" "C:\путь\до\Vanilla-OPM.ckan"
```

### После установки — обязательно

5. Скопируй папку **`patches/zzz_VanillaOPM_Fixes`** целиком в
   `Kerbal Space Program\GameData\` — так, чтобы получилось
   `GameData\zzz_VanillaOPM_Fixes\` с двумя файлами внутри.

   Это наши патчи, CKAN про них не знает:

   - `NFAIntakeShock.cfg` — чинит воздухозаборник `nfa-intake-largeshock` из Near Future
     Aeronautics: в моде осталась ссылка на несуществующий `AnimatedIntake`, из-за чего
     деталь теряла анимацию и писала ошибку в лог. Патч заменяет мёртвый модуль на
     стоковый `FXModuleAnimateThrottle`.
   - `CTTEmptyNodes.cfg` — косметика дерева R&D: скрывает 43 пустых узла Community Tech
     Tree, под которыми нет ни одной детали (CTT добавляет их под модпаки, которых в этой
     сборке нет — KSPIE, USI-MKS, Kerbalism). Если мод когда-нибудь положит туда детали,
     узел появится сам. Не нравится — просто удали файл.

6. Запусти игру. **Первый запуск будет долгим** (5–10 минут): KSPBurst компилирует
   шейдерные джобы, ModuleManager пересобирает кэш на 7.8 ГБ.

---

## Настройки после первого запуска

**KSP → Settings → Graphics:**
- **Terrain Detail = High** — обязательное требование Parallax. Без него рельеф
  останется плоским, а Parallax будет ругаться в лог.

**Parallax (кнопка на панели в игре) → Parallax GUI:**
- **Collision Level = 2** (по умолчанию) — какие объекты имеют коллизию.
- **Density Multiplier = 1.0**, **Range Multiplier = 1.0**.

Если собираешься играть в мультиплеере — эти три значения должны совпадать у всех.
Иначе один игрок упрётся в валун, сквозь который второй спокойно проедет.

---

## Мультиплеер (Luna Multiplayer)

Сервер: **`Спроси IP у владельца репозитория`**

1. Запусти игру, в главном меню нажми кнопку **LMP**.
2. **Direct connect** → введи адрес. Либо найди сервер `Vanilla+ OPM` в списке.
3. Версия модов должна совпадать с этой сборкой: сервер сверяет список деталей и
   отклонит корабль с чужими деталями (сообщение `Contains the following banned parts`).
4. **KerbalKonstructs / KSC Extended** — локальные статики: сервер их не знает. Спавн
   на площадках KSC Extended в мультиплеере не проверялся, начинайте с обычного KSC.

Сервер не требует Parallax — он его не рендерит. Достаточно, чтобы он был у клиентов.

---

## Что внутри

| группа | модули |
|---|---|
| ядро | Kopernicus, ModuleManager, Harmony2, B9PartSwitch, CRP, CTT, CTTP, CustomBarnKit, DeployableEngines, DynamicBatteryStorage, KSPTextureLoader, ModularFlightIntegrator, Waterfall, EVE + HR, Scatterer + config, PlanetShine, ReStock, KSPCommunityFixes, HUDReplacer, SmokeScreen, FireflyAPI |
| детали | Near Future: Aeronautics, Construction, Electrical (+Core, +DecayingRTGs), Exploration, Launch Vehicles, Propulsion (+XenonHETs), Solar (+Core), Spacecraft (+OrbitalLFOEngines), Props; HeatControl, KerbalActuators, Mark IV, ReStockPlus, SCANsat, SystemHeat, CommNetAntennasExtension + RemoteTechRedevAntennas |
| визуал | ParallaxContinued + три текстурных пака, KSPBurst (+Lite), OuterParallax (+OPM), Deferred, Shabby, TUFX, Firefly, RestockWaterfallExpansion, AvalanchePlumes, DistantObject (+default), KSCEnhanced, KSCExtended, TundraSpaceCenter, StockalikeStructures, OrdinaryKonstruction |
| QoL | KerbalEngineerRedux, TransferWindowPlanner, PreciseNode, EasyVesselSwitch, CommNetAntennasInfo, BetterTimeWarpCont, DraggableNavball, ZTheme, LunaMultiplayer, KerbalJointReinforcementContinued, CustomPreLaunchChecks, ClickThroughBlocker, ToolbarController |

Точный список с версиями — в `Vanilla-OPM.ckan` (это и есть источник истины).
Человекочитаемая версия — в `docs/manifest.yaml`.

---

## Если что-то не так

| симптом | что делать |
|---|---|
| CKAN не находит какую-то версию | Обнови репозитории в CKAN (`Refresh`) и попробуй снова. Версии в метапакете зафиксированы точно |
| Загрузка виснет или приходит битый архив (`SHA256 ... должно быть ...`) | Смени канал: VPN/прокси. SpaceDock и `archive.org` периодически отдают обрезанные файлы |
| CKAN пишет «files not owned by CKAN» | В `GameData` остались файлы от ручной установки. Убери их или поставь игру заново |
| Игра падает на загрузке, в логе `KSPBurst`/`Burst` | Удали `GameData/000_KSPBurst` и поставь KSPBurst заново через CKAN |
| Пустой/чёрный рельеф, планеты без деталей | Terrain Detail не `High`, либо не установился один из `Parallax_Stock*Textures` |
| Половина дерева R&D — пустые коробки | Это норма для CTT: узлы рассчитаны на KSPIE/USI/Kerbalism, которых в сборке нет. Наш `CTTEmptyNodes.cfg` их скрывает |
| Сервер банит детали `Size1p5.*`, `kv1Pod`, роботов | Разный набор DLC у игроков. Нужен Making History у всех, Breaking Ground — для паритета |
| В логе `Cannot resolve assembly: System.Runtime.CompilerServices.Unsafe` | Безобидно: KSPBurst и LunaMultiplayer везут разные версии одной шим-библиотеки, грузится более новая |

Лог игры: `Kerbal Space Program\KSP.log`.

---

## Лицензии

- Метапакет `Vanilla-OPM.ckan`, `docs/manifest.yaml` и патч `zzz_VanillaOPM_Fixes` — MIT.
- Все моды скачиваются через CKAN с первоисточников и остаются под своими лицензиями
  (GPL, MIT, CC-BY-NC-SA, All Rights Reserved и т.д.). В этом репозитории их файлов нет.
- KSP и её ассеты принадлежат Squad / Private Division / Take-Two.
