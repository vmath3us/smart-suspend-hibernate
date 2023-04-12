# Smart Suspend Hibernate
1. swapon on swapfile;
2. suspend;
3. countdown;
4. wakeup;
5. copy RAM to swapfile;
6. suspend again;

while kept energized, will return a simple suspension, high speed. But, if power's out, the workload is saved on swapfile.

Is to less io, using swapfile only to hibernate, but speed up return, using suspension by default.

# Difference to another suspend methods

Suspend is:
1. slow energy mode

if shutdown, lose workload

Hybrid sleep is:
1. store ram in swap/file immediately AND suspend.

if it is turned off, retrieve the job copy swap/file to RAM memory.
if only suspend, return.
But, it ALWAYS copy RAM to disk, even with high battery or charger.
a TBW waste if you return from suspension in a short time.

Suspend then hibernate is:
1. slow energy mode;
2. wakeup to verify battery level;
3. if bigger 5%, suspend, else, copy ram to disk, and shutdown;

if 5% is not enough power for the copy operation (common especially on devices with old battery, which skip percentages), workload is lost.

Smart suspend hibernate it's the best balance between avoiding writing to disk but being reliable about the hibernation operation.

# Setup (on selinux)
1. mkdir (or btrfs su cr) /var/swap
2. chattr +C /var/swap
3. chcom -R unconfined_u:object_r:var_t:s0 /var/swap
4. cd /var/swap
5. btrfs fi mkswapfile --size 8G swapfile
6. mkswap swapfile (that will define unconfined_u:object_r:swapfile_t:s0 on swapfile, check with ls -Z, manual define using chcom)
7. btrfs inspect-internal map-swapfile -r swapfile (is resume_offset)
8. add resume device and resume_offset on bootloader config
9. add resume support on initrd
[Archwiki](https://wiki.archlinux.org/title/Power_management/Suspend_and_hibernate#Hibernation_into_swap_file)
