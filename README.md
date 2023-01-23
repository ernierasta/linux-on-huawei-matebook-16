# Linux on Huawei Matebook 16
### Tricks and fixes for Huawei Matebook 16 on Linux.

While this info should work in every Linux distribution and apply to other devices (especially current Huawei notebooks/laptops), it is tested on Matebook 16 (AMD Ryzen 5) running Voidlinux.

## Dying bluetooth

**Problem**: Sometimes bluetooth works without problem, but there are situations when it dyes and finito. Restarting notebook usually solves problem, but it is annoying. When it dies you can see error:

`Device Descriptor read/64 error -71`

Also usuing `sudo rfkill` will return no bluetooth adapter.

**Solution**: Disable power saving for USB.

**What you should do**: 

Create /usr/lib/udev/rules.d/99-usb-input-no-powersave-fix-bt.rules (some distros have rules in `/etc`, so put it there if it is your case) with content:
`ACTION=="add", SUBSYSTEM=="input", TEST=="power/control", ATTR{power/control}="on"`

**Tested**: Looks promissing, but I will update info here after few days/week, as I am not sure, this is a solution.
