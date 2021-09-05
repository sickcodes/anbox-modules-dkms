# anbox-modules-dkms for kernel 5.7+ (ngbox-modules-dkms)

# Next Generation Box Modules DKMS (ngbox)

Resurrected aur.archlinux.org/anbox-modules-dkms for maintenance 

As per the Arch Wiki, https://wiki.archlinux.org/title/Anbox#Old_kernels

> The dkms modules do not work on kernels ≥5.7 anymore. Follow the instructions below instead. For older kernels see Old kernels.

However, a user named @Choff has included some patches here:

[https://github.com/anbox/anbox-modules/pull/76](https://github.com/anbox/anbox-modules/pull/76)

This repo will be used to fix the anbox modules for 5.7+.

# Patches 

`git submodule add https://github.com/choff/anbox-modules
`
We will use commit https://github.com/choff/anbox-modules/commit/6ddae194592451d604726a286f566d0246aef567

https://github.com/choff/anbox-modules/commit/4af9d5d591f33a0d8d7fb0735e280fa51ccef53e

>  Fix compilation of binder and ashmem on kernel 5.7 and later

> On kernel 5.7 and later, kallsyms_lookup_name() can no longer be called from a kernel
> module for reasons described here: https://lwn.net/Articles/813350/
> As binder really needs to use kallsysms_lookup_name() to access some kernel
> functions that otherwise wouldn't be accessible, KProbes are used on later
> kernels to get the address of kallsysms_lookup_name(). The function is
> afterwards used just as before. This is a very dirty hack though and the much
> better solution would be if all the functions that are currently resolved
> with kallsysms_lookup_name() would get an EXPORT_SYMBOL() annotation to
> make them directly accessible to kernel modules.


https://github.com/choff/anbox-modules/commit/443f984b1a4eecf464b0081820e87e351c5d7c36

> Compile fixes for kernel >= 5.8

> With the commit 64fe66e8a95e in the Linux kernel, the member "mmap_sem" in the
> struct mm_struct was renamed to "mmap_lock". This patch fixes the resulting
> compile errors.

https://github.com/choff/anbox-modules/commit/6ddae194592451d604726a286f566d0246aef567

> Another compile fix for kernel >= 5.8

> With kernel 5.8, the return value of map_kernel_range_noflush()
> was changed. This function now returns 0 on success (instead of
> the number of successfully mapped pages).

> This commit adjusts binder accordingly.

Thank you so much @choff!