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
But, it ALWAYS copy RAM to disk, even with high battery or charger.
a TBW waste if you return from suspension in a short time.

Suspend then hibernate is:
1. slow energy mode;
2. wakeup to verify battery level;
3. if grant 5%, suspend, else, copy ram to disk, and shutdown;

if 5% is not enough power for the copy operation (common especially on devices with old battery, which skip percentages), workload is lost.

Smart suspend hibernate it's the best balance between avoiding writing to disk but being reliable about the hibernation operation.
