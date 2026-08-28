# PicoFlutter — Reto de ruteo / Routing Challenge

*(English version below)*

## El reto

PicoFlutter es una placa "mariposa" basada en el microcontrolador **RP2040**, con
LEDs RGB WS2812B, USB-C, memoria flash QSPI y cargador de batería LiPo.

El esquemático está terminado y todos los componentes ya están colocados en la
placa — **pero no hay ninguna pista**. Tu misión: **rutear la placa completa**.

## Cómo empezar

1. Abre `picoflutter.kicad_pro` en KiCad.
2. Abre el editor de PCB. Verás los 67 componentes colocados y el *ratsnest*
   (las líneas finas que indican qué pads deben conectarse entre sí).
3. Rutea con la herramienta **Route Tracks** (tecla `X`). Usa `V` para cambiar
   de capa insertando una vía.
4. Cuando termines, ejecuta **Inspect → Design Rules Checker (DRC)**:
   el objetivo es **0 errores** y ninguna conexión sin rutear.

## Datos de la placa

| Parámetro | Valor |
|---|---|
| Tamaño | 70.5 × 55 mm |
| Capas de cobre | 4 (F.Cu, In1.Cu, In2.Cu, B.Cu) |
| Componentes | 67 |
| Redes (nets) | 92 |
| Ancho mínimo de pista | 0.2 mm |
| Separación mínima (clearance) | 0.13 mm |
| Vía mínima | 0.45 mm de diámetro |

Las clases de red ya están configuradas en el proyecto (`Default`, `MCUpow`,
`lowpow`, `signals`) — KiCad aplicará el ancho y la separación correctos
automáticamente según la red que estés ruteando.

## Consejos

- **Alimentación primero:** rutea USB-C → cargador (MCP73831) → reguladores →
  RP2040 antes que las señales. Las pistas de alimentación son más anchas.
- **Aprovecha las 4 capas:** una estrategia clásica es dedicar una capa interna
  a **GND** y otra a **3.3 V** usando zonas de cobre (Add Filled Zone), y dejar
  las capas externas para señales.
- **QSPI:** las pistas entre el RP2040 y la flash W25Q64 deben ser cortas y
  directas.
- **Cristal:** mantén el cristal de 12 MHz cerca del RP2040 y no pases señales
  ruidosas por debajo.
- **USB:** el par diferencial USB (D+/D−) se rutea junto, con la herramienta
  **Route Differential Pair** (tecla `6`).
- Reordena el *ratsnest* pulsando `B` (rellenar zonas) y usa `Ctrl+Z` sin miedo.

¿Terminaste con 0 errores de DRC? Compara tu ruteo con el de tus compañeros:
¿quién usó menos vías? ¿quién tiene las pistas más cortas?
(Estadísticas en **Inspect → Board Statistics**.)

---

## The challenge (English)

PicoFlutter is a butterfly-shaped board built around the **RP2040**
microcontroller, with WS2812B RGB LEDs, USB-C, QSPI flash and a LiPo battery
charger.

The schematic is finished and every component is already placed on the board —
**but there are no tracks**. Your mission: **route the entire board**.

1. Open `picoflutter.kicad_pro` in KiCad and enter the PCB editor.
2. The ratsnest (thin lines) shows which pads must be connected.
3. Route with `X`, drop vias with `V`. Net classes are already configured, so
   track widths and clearances are applied automatically.
4. You are done when **DRC reports 0 errors and 0 unrouted connections**.

Tips: route power before signals; on this 4-layer board a classic strategy is
an inner GND plane plus an inner 3.3 V plane (filled zones), signals on the
outer layers. Keep the QSPI flash and the 12 MHz crystal close to the RP2040,
and route USB D+/D− as a differential pair (`6`).

Finished? Compare via count and total track length with your classmates in
**Inspect → Board Statistics**.
