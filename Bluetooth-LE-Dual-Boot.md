## Bluetooth LE Dual Boot Connecting guide

1. Pair and connect on Linux
2. Pair and connect on Windows
3. Shut down Bluetooth device
4. Boot to Linux
5. Mount Windows partition
6. Go to ``<windows-mount>/Windows/System32/config``
7. Run command ``chntpw -e SYSTEM``
   * Install chntpw if it is not available
8. Go to the keys ``ControlSet001\Services\BTHPORT\Parameters1\Keys\<computer-bluetooth-mac>\<device-bluetooth-mac>``
   * Rename the device's bluetooth mac in Linux ``/var/lib/bluetooth`` directory to the one found in the Windows registry. (Usually just one byte changes in the Mac when pairing is done)

9. Replace values in Linux device's directory **info** file:
   - `IRK` into `Key` in `IdentityResolvingKey`
   - `CSRK` into `Key` in `LocalSignatureKey`
   - `LTK` into `Key` in `LongTermKey`
   - `ERand` into `Rand`: Take the hex value *ab cd ef*, byte reverse it (*ef cd ab*) and convert it into decimal (e.g. using the Programming mode of the calculator application)
   - `EDIV` into `EDiv`: Just take the hex value and convert it normally or use the decimal value directly if it is displayed (chntpw displays it)

10. Restart bluetooth service
    * ``systemctl restart bluetooth``
11. Power on bluetooth device

Connection should work now seamlessly in Linux and Windows
