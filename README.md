# Linux on Huawei Matebook 16
### Tricks and fixes for Huawei Matebook 16 on Linux.

While this info should work in every Linux distribution and apply to other devices (especially current Huawei notebooks/laptops), it is tested on Matebook 16 (AMD Ryzen 5) running Voidlinux.

## Dying bluetooth

**Problem**: Sometimes bluetooth works without problem, but there are situations when it dyes and finito. Restarting notebook usually solves problem, but it is annoying. When it dies you can see error:

`Device Descriptor read/64 error -71`

Also usuing `sudo rfkill` will return no bluetooth adapter.

**Solution**: Disable power saving for USB.

**What you should do**: 

Create **/usr/lib/udev/rules.d/99-usb-input-no-powersave-fix-bt.rules** (some distros have rules in `/etc`, so put it there if it is your case) with content:

`ACTION=="add", SUBSYSTEM=="input", TEST=="power/control", ATTR{power/control}="on"`

**Tested**: Looks promissing, but I will update info here after few days/week, as I am not sure, this is a solution.

## Dying touchpad aka most annoying problem ever

**Problem**: In most unconvinient time - touchpad will stop working. No response, no way to bring it back (nothing works, removing/readding kernel modules, unbinding/binding to i2c driver, ...). Every time it happens it kills you a bit inside :-). Notebook restart brings it back. It is probably somehow related to battery charging/protection. Usualy hitting upper limit will kill touchpad. Also keeping notebook on charger will cause it.

**Solution**: I studied a lot of different sources of kernel modules, tried to look into ACPI tables ... I failed misserably. It looked like there is no solution. But then I tried disabling powersaving on i2c devices ...

**What you should do**:

Create /usr/lib/udev/rules.d/99-i2c-no-powersave.rules (or in /etc/udev if your distro has it) with content:

`ACTION=="add", SUBSYSTEM=="i2c", ATTR{power/control}="on"`

**Tested**: ~~Also looks it like it works! But I am not very enthusiastic right now, as in past it also looked like problem solved ... until it happend again. Will update info here.~~ UPDATE: It doesn't work. Maybe it helps a bit, but I doubt it, it was just coincident that it was ok for 2 days.

## No real sleep on current kernel version

**Problem**: I am on linux kernel 6.1.4 and sleep is not working. It looks like it is working, but then some instant messaging apps starts happily beep while it "sleeps", also battery drain is quite high. From what I saw we cannot acheve deep sleep on memory ...

**Solution**: Just start using hibernation, longer stop/start times, but good battery presservation.

## That's all for now

Hope this helps you to enjoy your Linux experience on Huawei Matebook 16. I like quality/price ratio and for me screen format (3:2) is amazing, you can fit a lot of text on the screen, so great for programming.

It would be amazing if you open an issue or PR if you have any additional on HW support on this devices!
