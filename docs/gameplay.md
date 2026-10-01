# Gameplay

## 1. Физические параметры

Гравитация: `Physics2D.Gravity = (0, −9.81)`. Fixed Timestep = 0.02 (50 Гц).

Массы объектов: явно не заданы — у `Rigidbody2D` игрока, `Door`, `Key` значения по умолчанию (mass = 1).

Физические материалы: отсутствуют. `Physics Material 2D` в проекте нет, на спрайтах — графический `Sprites-Default`. Трение и упругость везде дефолтные (friction ≈ 0.4, bounciness = 0).

Коллайдеры:
- `CharacterTopDown` — Capsule Collider 2D
- `Door` — Box Collider 2D
- `Key` — Box Collider 2D
- `Lever` — Box Collider 2D (без Rigidbody2D)

## 2. Префабы и их роль

| Префаб                                | Роль                              | Что делает «опасным» / «полезным»                                                                                                   |
| ------------------------------------- | --------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| `Wall.prefab` / `Wall3D.prefab`       | Препятствие                       | Box Collider 2D — блокирует движение                                                                                                |
| `Door.prefab` / `Door3D.prefab`       | Препятствие                       | `Rigidbody2D` + `Box Collider 2D` + скрипт `Door` (открывается по ключу `Key_index` или по состоянию рычага `Lever_state_required`) |
| `Lever.prefab`                        | Полезный (переключатель)          | `Box Collider 2D` + скрипт `Lever` — отправляет сигнал двери через `Door_value` / `State`                                           |
| `Key.prefab`                          | Бонус<br>(подбираемый)            | `Rigidbody2D` + `Box Collider 2D` + `CarryItem` (можно взять в руки) + `Key` (`Key_index`, `Key_value`)                             |
| `DoorKey.prefab` / `DoorKey3D.prefab` | Бонус (ключ под конкретную дверь) | `CarryItem` + `Key`                                                                                                                 |
| `Floor.prefab`, `Grass1/2`, `Shadow`  | Декор / окружение                 | Геймплейно нейтральны                                                                                                               |

Врагов в проекте нет. Ни одного префаба или скрипта с уроном (`DamageDealer`, `Enemy` и т.п.) не найдено — жанр ближе к top-down puzzle/adventure.

## 3. UI

UI отсутствует. Ни на сценах, ни в префабах нет `Canvas`, `Button`, `TextMeshPro`. UI-скриптов в `Assets/Scripts` тоже нет.

## 4. Параметры в Inspector, влияющие на сложность / поведение

Игрок (`PlayerCharacter`):
- `Max_hp = 100` — здоровье.
- `Move_accel = 10`, `Move_deccel = 20`, `Move_max = 3` — скорость и разгон.
- `Invulnerable` — режим неуязвимости (debug).

Управление (`PlayerControls`):
- `Left_key = A`, `Right_key = D`, `Up_key = W`, `Down_key = S`, `Action_key = Left Shift`.

Дверь (`Door`):
- `Nb_switches_required = 1` — сколько переключателей нужно.
- `Lever_state_required = Right`, `Levers = 1` — условие от рычагов.
- `Key_can_open`, `Key_index = 0` — открытие ключом.
- `Open_speed = 5`, `Close_speed = 5`, `Max_move = 2.5` — анимация открытия.
- `Reset_on_death = ☑` — сброс при смерти игрока.

Рычаг (`Lever`):
- `State = Left` — текущее состояние.
- `Door_value = 1` — к какой двери привязан.
- `Can_be_center`, `No_return`, `Reset_on_dead` — логика переключения.

Ключ (`Key`): `Key_index = 0`, `Key_value = 1` — связка с `Door.Key_index`.

Перенос предмета (`CarryItem`): `Item_type = Key`, `Carry_size = 0.8`, `Carry_offset = (0.4, 0.2)`, `Carry_angle_deg = 30`, `Reset_on_death`.

Камера (`FollowCamera`): `Target = CharacterTopDown`, `Target_offset = (0, −7, −10)`, `Camera_speed = 5` — плавность слежения.

Отрисовка: `AutoOrderLayer` (`Auto_sort`, `Offset`, `Sort_refresh_rate`, `Auto_rotate`, `Rotate_offset`), `FixOffset` (`Order_min = 10`, `Order_max = 20`, `Z_offset`).

Глобально: `Time.Fixed Timestep` — точность физики; `Physics2D.Gravity` — если делать "падающие" уровни.