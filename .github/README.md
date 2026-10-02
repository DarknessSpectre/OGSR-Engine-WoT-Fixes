# OGSR Engine для Spectrum Project

Исправления для адаптации «Путь во мгле» на OGSR CoP для реализации полноценной функциональности мода.

## Добавленные исправления

### 1. Названия звуковых устройств

Исправлено отображение кириллицы в списке звуковых устройств и в выбранном
значении настройки `snd_device`. Названия, полученные от OpenAL в UTF-8,
преобразуются в Windows-1251, которую использует интерфейс этой адаптации.
Преобразование применяется к отображаемой подписи. Выбор и сохранение устройства
используют его исходный токен.

Файл: [`ogsr_engine/xrGame/ui/UIComboBox.cpp`](../ogsr_engine/xrGame/ui/UIComboBox.cpp).

### 2. Ошибка сохранения состояния БТР

Исправлено сообщение `load/save mismatch` при сохранении `city_spectrum_btr`.
`CCar::SaveNetState` записывает положение машины, углы, состояния дверей и колёс,
а также здоровье. `CSE_ALifeCar::load` теперь полностью считывает эти данные
в том же порядке. Перед чтением массивы дверей и колёс очищаются, чтобы повторное
сохранение не накапливало старые записи. Формат сохранений сохранён.
Исправление применяется ко всем объектам `CSE_ALifeCar`.

Файл: [`ogsr_engine/xrServerEntities/xrServer_Objects_ALife.cpp`](../ogsr_engine/xrServerEntities/xrServer_Objects_ALife.cpp).

## Сборка и перенос исправлений

1. Получите исходники ветки `main_cop_cs_sp_fixes`:

   ```console
   git clone --branch main_cop_cs_sp_fixes https://github.com/DarknessSpectre/OGSR-Engine-WoT-SP-Fixes.git
   ```

2. Запустите `Update_Components.cmd`, чтобы получить зависимости движка.
3. Откройте `Engine.sln` в Visual Studio с компонентами разработки на C++
   и Windows SDK. Выберите конфигурацию `Release` и платформу `x64`.
   Используемые инструменты сборки задаются в `OgsrBuildProps.props`:
   v143 для Visual Studio 2022, v145 для Visual Studio 2026.
4. Соберите решение. Результат находится в `bin_x64`.
