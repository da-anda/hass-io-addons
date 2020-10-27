# Home Assistant Community Add-on: KNXD

## Installation

Follow these steps to get the add-on installed on your system:

1. Navigate in your Home Assistant frontend to **Supervisor** -> **Add-on Store**.
2. If you haven't added this add-on repository to your supervisor yet, click the menu icon in the top right corner, select **Repositories**, add `https://github.com/da-anda/hass-io-addons` as new repository and close the dialog again.
3. Find the "KNXD" add-on and click it.
4. Click on the "INSTALL" button.

## Configuration

Add-on configuration:

```yaml
    "address": "0.0.1",
    "client_address": "0.0.2:8",
    "interface": "tpuart",
    "device": "/dev/ttyACM0",
    "usb_filters": "",
    "custom_config": ""
```

### Options
The description of these options is partly copied from the `knxd` [documentation](https://github.com/knxd/knxd/blob/master/doc/inifile.rst). You will find more examples and details there.

#### Option `address`

The KNX address for the knxd deamon itself. Used e.g. for requests originating at the group cache.

#### Option `client_address`

Address range to be distributed to client connections. Note that the length parameter indicates the number of addresses to be allocated.

Example: 1.2.3:5 (This assigns addresses 1.2.3 through 1.2.7 to knxd's clients.)

#### Option `interface`

The driver `knxd` should use as interface to talk to the KNX bus. The most common ones for the typical usecase of this add-on are:

- `tpuart` (for UART based KNX interfaces, like the one from Busware.de)
- `usb` (for commercial USB KNX interfaces)

For a full list of all possible options see the [drivers section](https://github.com/knxd/knxd/blob/master/doc/inifile.rst#drivers) of the `knxd` documentation.

#### Option: `device` (optional for some interfaces)

The physical device address of your adapter in linux. Example:

- **TPUART interface**: `/dev/ttyACM0`
- **USB interface**: you can try leaving this blank in order for `knxd` to auto-detect your device. If it doesn't work when blank, try specifying a device address like `/dev/ttyAMA0`.  

Please note that the addresses are examples and might differ for your device. To find out the device address you have to SSH into your host OS (**NOT** the supervisor!) and check which devices are connected there.

#### Option: `usb_filters` (optional)

When using an USB interface, you can specify additional filters to use. See the [filters section](https://github.com/knxd/knxd/blob/master/doc/inifile.rst#filters) of the official `knxd` documentation.

#### Option: `custom_config` (optional)

Allows you to write your own, custom `knxd` ini configuration instead of using the prepared template from this add-on that makes use of all the other config options above.

Your custom configuration will replace the default configuration provided by this add-on and thus all the other config options above will be ignored. See the [knxd documentation](https://github.com/knxd/knxd/blob/master/doc/inifile.rst) for all possible configuration options.


## Support

If you have any questions, feel free to join the HomeAssistant community and ask your questions in the [add-on thread](https://community.home-assistant.io/t/knxd-add-on-covert-your-knx-usb-interface-into-an-ip-interface-that-can-be-used-by-ha/38108/38).

If you found a bug, feel free to create a ticket on [Github](https://github.com/da-anda/hass-io-addons/issues)