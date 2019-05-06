[![Version](https://img.shields.io/badge/version-0.2.7-green.svg?style=for-the-badge)](#) [![mantained](https://img.shields.io/maintenance/yes/2019.svg?style=for-the-badge)](#) [![maintainer](https://img.shields.io/badge/maintainer-%20%40gerard33-blue.svg?style=for-the-badge)](#)

# Custom component for Sony Bravia TV using Pre-Shared Key (PSK)
A platform which allows you to interact with the Sony Bravia TV using a Pre-Shared Key.

See [this](https://community.home-assistant.io/t/sony-bravia-tv-component-with-pre-shared-key/30698?u=gerard33) post on the HA forum for more info.

To get started put `/custom_components/braviatv_psk/media_player.py` here:

`<config directory>/custom_components/braviatv_psk/media_player.py`  

Starting with Home Assistant 0.92 you also need to copy the file `/custom_components/braviatv_psk/__init__.py` to `<config directory>/custom_components/braviatv_psk/__init__.py`

**Example configuration.yaml:**

```yaml
media_player:
  - platform: braviatv_psk
    host: 192.168.1.101
    psk: sony
    mac: AA:BB:CC:DD:EE:FF
    amp: True
    android: True
    sourcefilter:
      - ' HD'
      - HDMI
    name: MyBraviaTV
```

**Configuration variables:**  
  
key | description  
:--- | :---  
**platform (Required)** | The platform name.
**host (Required)** | The IP of the Sony Bravia TV, eg. 192.168.1.101.
**psk (Required)** | The Pre-Shared Key of the Sony Bravia TV, eg. sony (see below for instructions how to configure this on the TV). Place the psk between quotes if you use digits and those start with one or more zero's, e.g. '0044'.
**mac  (Optional)** | The MAC address of the Sony Bravia TV (see below for instructions how to get this from the TV). This is used to turn on the TV using WakeOn LAN and is only needed if the TV is non-Android.
**amp (Optional)** | Boolean, defaults to False. Set this to True if you have an amplifier attached to the TV and not use the internal TV speakers. Then the volume slider will not be shown as this doesn’t work for the amplifier. Mute and volume up and down buttons are there and working with an amplifier.
**android (Optional)** | Boolean, defaults to False. Set this to True when you have an Android TV as these TV’s don’t respond to WakeOn LAN commands, so another method of turning on the TV can be used.
**sourcefilter (Optional)** | List of text that is used to filter the source list, eg. ’ HD’ (with quotes) will only show TV channels in the source list which contain ‘HD’, eg. ‘NPO 3 HD’ (in my config this will only show HD channels)

**Installation instructions TV**
1. Enable remote start on your TV: [Settings] => [Network] => [Home Network Setup] => [Remote Start] => [On]
2. Enable pre-shared key on your TV: [Settings] => [Network] => [Home Network Setup] => [IP Control] => [Authentication] => [Normal and Pre-Shared Key]
3. Set pre-shared key on your TV: [Settings] => [Network] => [Home Network Setup] => [IP Control] => [Pre-Shared Key] => sony
4. Give your TV a static IP address, or make a DHCP reservation for a specific IP address in your router
5. Determine the MAC address of your TV: [Settings] => [Network] => [Network Setup] => [View Network Status]
  
***
Due to how `custom_componentes` are loaded, it is normal to see a `ModuleNotFoundError` error on first boot after adding this, to resolve it, restart Home-Assistant.

***
