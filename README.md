# progrex04.inc
**by whoisdaw — v1.0**

Sistema de barras de progreso para SA-MP con soporte nativo de orientación vertical. Reemplaza y extiende `playerprogress.inc`, manteniendo compatibilidad total con todas sus funciones mientras agrega soporte para barras verticales, padding configurable, y un sistema de renderizado más robusto.

---

## ¿Qué tiene de nuevo?

La librería original (`playerprogress.inc`) solo soportaba barras horizontales. `progrex04` agrega un enum de direcciones que permite crear barras que llenan hacia arriba, hacia abajo, desde el centro, o en cualquier orientación, sin romper ningún código existente.

---

## Instalación

1. Copiá `progrex04.inc` en tu carpeta `pawno/include`
2. Reemplazá `#include <playerprogress>` por `#include <progrex04>` en tu gamemode
3. Eliminá `playerprogress.inc` para evitar conflictos

---

## Direcciones disponibles

```pawn
BAR_DIRECTION_RIGHT            // Rellena de izquierda a derecha (default)
BAR_DIRECTION_LEFT             // Rellena de derecha a izquierda
BAR_DIRECTION_HORIZONTAL_FROM_0 // Rellena desde el centro horizontal
BAR_DIRECTION_UP               // Rellena de abajo hacia arriba
BAR_DIRECTION_DOWN             // Rellena de arriba hacia abajo
BAR_DIRECTION_VERTICAL_FROM_0  // Rellena desde el centro vertical
```

---

## Funciones

### Creación y destrucción
```pawn
PlayerBar:CreatePlayerProgressBar(playerid, Float:x, Float:y, Float:width, Float:height, colour, Float:max, progressbar_direction:direction)
DestroyPlayerProgressBar(playerid, PlayerBar:barid)
DestroyAllPlayerProgressBars(playerid)
```

### Visibilidad
```pawn
ShowPlayerProgressBar(playerid, PlayerBar:barid)
HidePlayerProgressBar(playerid, PlayerBar:barid)
bool:IsPlayerProgressBarVisible(playerid, PlayerBar:barid)
IsValidPlayerProgressBar(playerid, PlayerBar:barid)
```

### Valor
```pawn
SetPlayerProgressBarValue(playerid, PlayerBar:barid, Float:value)
Float:GetPlayerProgressBarValue(playerid, PlayerBar:barid)
SetPlayerProgressBarMaxValue(playerid, PlayerBar:barid, Float:max)
Float:GetPlayerProgressBarMaxValue(playerid, PlayerBar:barid)
SetPlayerProgressBarMinValue(playerid, PlayerBar:barid, Float:min_value)
Float:GetPlayerProgressBarMinValue(playerid, PlayerBar:barid)
UpdatePlayerProgressBar(playerid, PlayerBar:barid) // compatibilidad, no-op
```

### Posición y tamaño
```pawn
SetPlayerProgressBarPos(playerid, PlayerBar:barid, Float:x, Float:y)
GetPlayerProgressBarPos(playerid, PlayerBar:barid, &Float:x, &Float:y)
SetPlayerProgressBarWidth(playerid, PlayerBar:barid, Float:width)
Float:GetPlayerProgressBarWidth(playerid, PlayerBar:barid)
SetPlayerProgressBarHeight(playerid, PlayerBar:barid, Float:height)
Float:GetPlayerProgressBarHeight(playerid, PlayerBar:barid)
```

### Color
```pawn
SetPlayerProgressBarColour(playerid, PlayerBar:barid, colour)
GetPlayerProgressBarColour(playerid, PlayerBar:barid)
SetPlayerProgressBarColor(...)  // alias de compatibilidad
GetPlayerProgressBarColor(...)  // alias de compatibilidad
```

### Dirección
```pawn
SetPlayerProgressBarDirection(playerid, PlayerBar:barid, progressbar_direction:direction)
progressbar_direction:GetPlayerProgressBarDirection(playerid, PlayerBar:barid)
```

### Padding
```pawn
SetPlayerProgressBarPadding(playerid, PlayerBar:barid, Float:padding_x, Float:padding_y)
GetPlayerProgressBarPadding(playerid, PlayerBar:barid, &Float:padding_x, &Float:padding_y)
```

---

## Ejemplo de uso

```pawn
new PlayerBar:fuelbar[MAX_PLAYERS];

// Crear una barra vertical de combustible
fuelbar[playerid] = CreatePlayerProgressBar(playerid, 196.0, 340.0, 5.5, 43.0, 0xFF0000FF, 100.0, BAR_DIRECTION_UP);
SetPlayerProgressBarValue(playerid, fuelbar[playerid], 75.0);
ShowPlayerProgressBar(playerid, fuelbar[playerid]);

// Cambiar dirección en runtime
SetPlayerProgressBarDirection(playerid, fuelbar[playerid], BAR_DIRECTION_DOWN);
```

---

## Compatibilidad

Totalmente compatible con código escrito para `playerprogress.inc`. No requiere modificar llamadas existentes a `CreatePlayerProgressBar`, `SetPlayerProgressBarValue`, `SetPlayerProgressBarColor`, `UpdatePlayerProgressBar` ni ninguna otra función de la librería original.

---

## Créditos

- **whoisdaw** — adaptación, extensión vertical y compatibilidad
- Basado en el trabajo original de **Flávio Toribio** y las mejoras de **Southclaw** en `playerprogress.inc`
- Sistema de renderizado y direcciones basado en `progress2.inc`
