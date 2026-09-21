# Celestial Biome Tags

Celestial Biome Tags provides a common set of biome tags for planets, moons, and other extraterrestrial environments in Minecraft.

The goal of this project is to establish a simple convention that mods and datapacks can use to identify celestial biomes without depending on biome IDs from a specific space mod.

Built-in support is currently provided for **Ad Astra**.

## Why?

Space mods usually define their own biome IDs, but other mods and datapacks often need a generic way to target locations such as:

* Mars
* Venus
* The Moon
* Any planet
* Any moon
* Any extraterrestrial surface
* Space / orbital environments

Instead of targeting a specific biome:

```text
ad_astra:martian_wastelands
```

a mod or datapack can target:

```text
#c:planets/mars
```

This allows multiple space mods to use the same convention.

For example, another mod that adds a Mars biome can add it to `#c:planets/mars`, and existing datapacks using that tag will automatically recognize it as part of Mars.

## Convention

Celestial Biome Tags currently defines the following biome tags:

```text
#c:planets
├── #c:planets/earth
├── #c:planets/mercury
├── #c:planets/venus
├── #c:planets/mars
└── #c:planets/glacio

#c:moons
└── #c:moons/moon

#c:space
└── #c:space/orbits
```

There are also two broad convenience tags:

### `#c:extraterrestrial_surfaces`

Contains celestial surface biomes outside Earth.

This includes supported planets and moons, but does not include orbital/space biomes.

### `#c:extraterrestrial_biomes`

Contains all supported extraterrestrial biomes, including both celestial surfaces and space/orbital environments.

## Ad Astra Support

The following Ad Astra biomes are currently mapped to the convention.

### Mercury

`#c:planets/mercury`

```text
ad_astra:mercury_deltas
```

### Venus

`#c:planets/venus`

```text
ad_astra:venus_wastelands
ad_astra:infernal_venus_barrens
```

### Mars

`#c:planets/mars`

```text
ad_astra:martian_wastelands
ad_astra:martian_canyon_creek
ad_astra:martian_polar_caps
```

### Glacio

`#c:planets/glacio`

```text
ad_astra:glacio_snowy_barrens
ad_astra:glacio_ice_peaks
```

### Moon

`#c:moons/moon`

```text
ad_astra:lunar_wastelands
```

### Orbit

`#c:space/orbits`

```text
ad_astra:orbit
```

## For Mod and Datapack Developers

You do not need to depend on Celestial Biome Tags to adopt this convention.

Simply add your biomes to the appropriate tag under the `c` namespace.

For example, if your mod adds another biome to Mars:

```text
data/c/tags/worldgen/biome/planets/mars.json
```

```json
{
  "replace": false,
  "values": [
    "your_mod:your_mars_biome"
  ]
}
```

Anything targeting:

```text
#c:planets/mars
```

can then recognize your biome without knowing its specific biome ID.

When introducing support for a celestial body that does not yet have a tag, follow the existing hierarchy where possible:

```text
#c:planets/<planet>
#c:moons/<moon>
#c:space/<environment>
```

## Example Usage

A NeoForge biome modifier can target all Mars biomes using:

```json
{
  "biomes": "#c:planets/mars"
}
```

Similarly:

```text
#c:planets
```

targets planetary biomes,

```text
#c:moons
```

targets moon biomes, and

```text
#c:extraterrestrial_surfaces
```

can be used when something should apply broadly to extraterrestrial surfaces without also affecting orbital environments.

## Compatibility

Current target:

* Minecraft 1.21.1
* NeoForge
* Ad Astra 1.16.26

Ad Astra is not intended to define the convention itself. Celestial Biome Tags acts as a compatibility implementation for Ad Astra while exposing tags that other mods and datapacks can also adopt.

## License

This project is licensed under the MIT License.
