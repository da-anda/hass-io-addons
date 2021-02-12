# Changelog

## 0.4.1
- correctly map USB hardware device paths to the expected integer values in knxd configuration

## 0.4
- using new approach on how the KNXD config is generated
- added device selector to the add-on configuration options
- added possibility to configure the error log level to be able to debug issues more easily
- switched add-on base image back to Alpine 3.12 since the new 3.13 seems to have severe issues with USB interfaces

## 0.3.7

- switched to new hass-io base containers based on GitHub Docker Repository
- removed run.sh and replaced it with according s6-overlay scripts

## 0.3.6

- bumped knxd version to 0.14.39 which fixes some delays with pace filters

## 0.3.5

- bumped knxd version to 0.14.37 which fixes a memory leak in the FT12 driver
- add-on now uses the hosts network which enables multicast support. Thanks to stemnic for noticing the issue and fixing it.

## 0.3.4

- bumped knxd version to 0.14.34