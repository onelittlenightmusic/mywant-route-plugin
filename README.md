# mywant-route-plugin

MyWant custom type that draws the way from one place to another on a map — on
foot, by bicycle, or by car.

The want holds the question. Nothing is computed on the engine side: the card
geocodes the two place names with [Nominatim](https://nominatim.openstreetmap.org/)
and asks [Valhalla](https://valhalla1.openstreetmap.de/) for the line between
them. Both are OpenStreetMap community services and neither needs an API key —
which is the point. This began as a Google Maps card, and the key expired.

## Installation

```bash
cd ~/.mywant/custom-types
git clone https://github.com/onelittlenightmusic/mywant-route-plugin
```

Restart the engine so the type is picked up:

```bash
mywant stop && mywant start -D
```

## Usage

```yaml
metadata:
  name: route-home
  type: route
spec:
  params:
    from: 国分寺駅
    to: 中野坂上駅
    mode: cycling      # walking | cycling | driving
```

`from` and `to` are anything Nominatim can find — a station, an address, a
landmark. `mode` defaults to `walking`.

## The card

The card is part of [mywant-gui](https://github.com/onelittlenightmusic/mywant-gui)
rather than shipped here, because it draws with the app's own Leaflet. At its
normal size it shows the map and one line of fact:

```
国分寺駅 → 中野坂上駅            19.7km · 66分
```

Maximised, it adds the controls: the three travel modes, and a button that
swaps the two ends. Both write the want's params back, so the question changes
and the card answers the new one. The want is labelled `user-control`, so the
controls are reachable from the keyboard as well as the mouse.

## No transit

Trains and buses are deliberately not offered. The routers that do public
transport well are the paid ones, and for Japan
[mywant-transit-plugin](https://github.com/onelittlenightmusic/mywant-transit-plugin)
already answers that question properly via Yahoo!路線情報.

## Requirements

Network access to `nominatim.openstreetmap.org` and
`valhalla1.openstreetmap.de`. Both are shared community endpoints — the card
asks once per question and caches the answer, and personal use sits well inside
their limits, but they are not guaranteed services.

## License

MIT
