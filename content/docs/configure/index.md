---
title: 'Configuration'
date: 2019-02-11T19:30:08+10:00
weight: 4
summary: How to configure Dhak using .dhakrc.
---

- [.dhakrc](#dhakrc)
  - [Presets](#presets)
    - [Preset name](#preset-name)
    - [Password length (\--len=)](#password-length---len)
    - [Symbols (\--sym=)](#symbols---sym)
    - [Algorithm (\--algo=)](#algorithm---algo)
    - [cost (\--cost=)](#cost---cost)

---

## .dhakrc

The config of Dhak is json format.  
If you use this, save it to your home directory (~/.dhakrc).

```
{
  "presets": {
    "default": {
      "password_length": "20",
      "symbols": "!\"#$%&‘()*+,-./:;<=>?@[\\]^_`{|}~",
      "algorithm": "2b",
      "cost": "10"
    }
  }
}
```

### Presets

```
"presets": {
  // ...
}
```

Presets allow you to save and call settings of options in advance.

Dhak will use settings of options in preference to settings of presets.  
Also, if you omit a preset value, Dhak uses the value of the command-line option or the default value of the option.

For details of each item, see [Usage - Dhak](/docs/usage/#options).

#### Preset name

```
"presets": {
  "preset_name_1": {
    // ...
  },
  "preset_name_2": {
    // ...
  },
  "preset_name_3": {
    // ...
  }
}
```

You can use the settings by entering the name specified here as a command-line argument.

#### Password length (\--len=)

```
"password_length": "20",
```

#### Symbols (\--sym=)

```
"symbols": "!\"#$%&‘()*+,-./:;<=>?@[\\]^_`{|}~",
```

You will get passwords without symbols if you keep this empty like `"symbols": ""`.

#### Algorithm (\--algo=)

```
"algorithm": "2b",
```

#### cost (\--cost=)

```
"cost": "10",
```

{{< pager
  prevHref="/usage"
  prevTitle="Usage"
  nextHref="/security"
  nextTitle="Security"
>}}
