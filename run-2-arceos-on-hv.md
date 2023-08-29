$ qemu-system-aarch64 -nographic -m 512M -cpu cortex-a72 -machine type=virt,virtualization=on,iommu=smmuv3 -kernel target/aarch64/release/hypervisor.bin -smp 2 -device loader,addr=0x4001000,file=../bin/arceos-httpserver-single.bin,force-raw=on -device loader,addr=0x4101000,file=../bin/arceos-shell.bin,force-raw=on -device virtio-net-device,netdev=net0 -netdev user,id=net0,hostfwd=tcp::5555-:5555 -device virtio-blk-device,drive=disk0 -drive id=disk0,if=none,format=raw,file=../bin/disk.img

```
    RRRRRR  VV     VV MM    MM
    RR   RR VV     VV MMM  MMM
    RRRRRR   VV   VV  MM MM MM
    RR  RR    VV VV   MM    MM
    RR   RR    VVV    MM    MM
     ___    ____    ___    ___
    |__ \  / __ \  |__ \  |__ \
    __/ / / / / /  __/ /  __/ /
   / __/ / /_/ /  / __/  / __/
  /____/ \____/  /____/ /____/

primary cpu id: 0.
boot stack: 0x40099000, boot stack top: 0x400a1000
arch = aarch64
build_mode = release
log_level = info

Initializing heap at: [0x400a1008, 0x404a1008)
[INFO  hypervisor:99] Logging is enabled.
Initializing frame allocator at: [0x504c5000, 0x60000000)
[  0.059464 INFO  hypervisor:104] Initialization completed.

[  0.059802 INFO  hypervisor::platform::qemu_virt_arm::psci:19] trying to start cpu 1.
[  0.059916 INFO  hypervisor::platform::qemu_virt_arm::psci:21] cpu 1 started.
Starting virtualization...
Hardware support: true
[  0.060688 INFO  hypervisor:115] Hello World from cpu 1
Starting virtualization...
Hardware support: true
[  0.061230 INFO  hypervisor::hv:140] mapping
[  0.077032 INFO  hypervisor::hv:140] mapping
[  0.077400 INFO  hypervisor::hv:140] mapping
[  0.077534 INFO  hypervisor::hv:140] mapping
[  0.077704 INFO  hypervisor::hv:140] mapping
[  0.077716 INFO  rvm::arch::aarch64::vcpu:50] npt root is 504c5000.
[  0.078496 INFO  rvm::arch::aarch64::vcpu:52] [RVM] created ArmVcpu
Running guest...

       d8888                            .d88888b.   .d8888b.
      d88888                           d88P" "Y88b d88P  Y88b
     d88P888                           888     888 Y88b.
    d88P 888 888d888  .d8888b  .d88b.  888     888  "Y888b.
   d88P  888 888P"   d88P"    d8P  Y8b 888     888     "Y88b.
  d88P   888 888     888      88888888 888     888       "888
 d8888888888 888     Y88b.    Y8b.     Y88b. .d88P Y88b  d88P
d88P     888 888      "Y8888P  "Y8888   "Y88888P"   "Y8888P"

arch = aarch64
platform = qemu-virt-aarch64
smp = 1
build_mode = release
log_level = info

[  0.080614 0 axruntime:97] Logging is enabled.
[  0.081214 0 axruntime:98] Primary CPU 0 started, dtb = 0x0.
[  0.081362 0 axruntime:100] Found physcial memory regions:
[  0.081528 0 axruntime:102]   [PA:0x40080000, PA:0x4009f000) .text (READ | EXECUTE | RESERVED)
[  0.081724 0 axruntime:102]   [PA:0x4009f000, PA:0x400a6000) .rodata (READ | RESERVED)
[  0.081812 0 axruntime:102]   [PA:0x400a6000, PA:0x400a9000) .data (READ | WRITE | RESERVED)
[  0.081904 0 axruntime:102]   [PA:0x400a9000, PA:0x400aa000) .percpu (READ | WRITE | RESERVED)
[  0.081996 0 axruntime:102]   [PA:0x400aa000, PA:0x400ea000) boot stack (READ | WRITE | RESERVED)
[  0.082092 0 axruntime:102]   [PA:0x400ea000, PA:0x40110000) .bss (READ | WRITE | RESERVED)
[  0.082186 0 axruntime:102]   [PA:0x9000000, PA:0x9001000) mmio (READ | WRITE | DEVICE | RESERVED)
[  0.082278 0 axruntime:102]   [PA:0x8000000, PA:0x8020000) mmio (READ | WRITE | DEVICE | RESERVED)
[  0.083724 0 axruntime:102]   [PA:0xa000000, PA:0xa004000) mmio (READ | WRITE | DEVICE | RESERVED)
[  0.084012 0 axruntime:102]   [PA:0x40110000, PA:0x48000000) free memory (READ | WRITE | FREE)
[  0.084288 0 axruntime:113] Initialize global memory allocator...
[  0.085566 0 axruntime:119] Initialize kernel page table...
[  0.086398 0 axtask::api:18] Initialize scheduling...
[  0.086928 0 axtask::api:24]   use FIFO scheduler.
[  0.087014 0 axdriver:66] Initialize device drivers...
[  0.093424 INFO  hypervisor::hv:140] mapping
[  0.093518 INFO  hypervisor::hv:140] mapping
[  0.093588 INFO  hypervisor::hv:140] mapping
[  0.093654 INFO  rvm::arch::aarch64::vcpu:50] npt root is 504c6000.
[  0.093956 INFO  rvm::arch::aarch64::vcpu:52] [RVM] created ArmVcpu
Running guest...
[  0.094636 0 virtio_drivers::device::net:117] Device features CTRL_GUEST_OFFLOADS | MAC | GSO | MRG_RXBUF | STATUS | CTRL_VQ | CTRL_RX | CTRL_VLAN | CTRL_RX_EXTRA
       d8888                            .d88888b.   .d8888b.
      d88888                           d88P" "Y88b d88P  Y88b
     d88P888                           888     888 Y88b.
    d88P 888 888d888  .d8888b  .d88b.  888     888  "Y888b.
   d88P  888 888P"   d88P"    d8P  Y8b 888     888     "Y88b.
  d88P   888 888     888      88888888 888     888       "888
 d8888888888 888     Y88b.    Y8b.     Y88b. .d88P Y88b  d88P
d88P     888 888      "Y8888P  "Y8888   "Y88888P"   "Y8888P"

 | GUEST_ANNOUNCE | CTL_MAC_ADDR | RING_INDIRECT_DESC | RING_EVENT_IDX
arch = aarch64
platform = qemu-virt-aarch64
smp = 1
build_mode = release
log_level = info

[  0.098102 0 virtio_drivers::queue:383] Lagacy Size: 0x2000
[  0.098642 0 virtio_drivers::transport::mmio:397] Legacy
[  0.098864 INFO  hypervisor::hv::device_emu::virtio:218] legacy gpaddr 0x40410000
[  0.099090 INFO  hypervisor::hv::device_emu::virtio:220] legacy gpaddr 0x40410000 hpaddr 0x408d4000
[  0.099218 INFO  hypervisor::hv::device_emu::virtio:229] Write 1's pfn
[  0.097732 0 axruntime:97] Logging is enabled.
[  0.099904 0 axruntime:98] Primary CPU 1 started, dtb = 0x0.
[  0.100064 0 axruntime:100] Found physcial memory regions:
[  0.100232 0 axruntime:102]   [PA:0x40080000, PA:0x400a8000) .text (READ | EXECUTE | RESERVED)
[  0.100432 0 axruntime:102]   [PA:0x400a8000, PA:0x400b6000) .rodata (READ | RESERVED)
[  0.100520 0 axruntime:102]   [PA:0x400b6000, PA:0x400b9000) .data (READ | WRITE | RESERVED)
[  0.100610 0 axruntime:102]   [PA:0x400b9000, PA:0x400ba000) .percpu (READ | WRITE | RESERVED)
[  0.100702 0 axruntime:102]   [PA:0x400ba000, PA:0x400fa000) boot stack (READ | WRITE | RESERVED)
[  0.100804 0 axruntime:102]   [PA:0x400fa000, PA:0x4011f000) .bss (READ | WRITE | RESERVED)
[  0.100898 0 axruntime:102]   [PA:0x9000000, PA:0x9001000) mmio (READ | WRITE | DEVICE | RESERVED)
[  0.100990 0 axruntime:102]   [PA:0x8000000, PA:0x8020000) mmio (READ | WRITE | DEVICE | RESERVED)
[  0.101082 0 axruntime:102]   [PA:0xa000000, PA:0xa004000) mmio (READ | WRITE | DEVICE | RESERVED)
[  0.101694 0 axruntime:102]   [PA:0x4011f000, PA:0x48000000) free memory (READ | WRITE | FREE)
[  0.101816 0 axruntime:113] Initialize global memory allocator...
[  0.102424 0 virtio_drivers::queue:383] Lagacy Size: 0x2000
[  0.102546 0 virtio_drivers::transport::mmio:397] Legacy
[  0.102712 INFO  hypervisor::hv::device_emu::virtio:218] legacy gpaddr 0x40412000
[  0.102804 INFO  hypervisor::hv::device_emu::virtio:220] legacy gpaddr 0x40412000 hpaddr 0x408d6000
[  0.102892 INFO  hypervisor::hv::device_emu::virtio:229] Write 0's pfn
[  0.103600 0 axdriver::virtio:88] created a new Net device: "virtio-net"
[  0.104334 0 axnet:22] Initialize network subsystem...
[  0.104448 0 axnet:24] number of NICs: 1
[  0.104532 0 axnet:27]   NIC 0: "virtio-net"
[  0.104680 0 axruntime:119] Initialize kernel page table...
[  0.106020 0 axdriver:66] Initialize device drivers...
[  0.106252 0 axnet::smoltcp_impl:273] created net interface "eth0":
[  0.106372 0 axnet::smoltcp_impl:275]   ether:    52[  0.106632 0 virtio_drivers::device::blk:55] device features: SEG_MAX | GEOMETRY | BLK_SIZE | SCSI-54-00-12-34-56
[  0.106872 0 axnet::smoltcp_impl:277]   ip:       10.0.2.15/24
 | FLUSH[  0.107032 0 axnet::smoltcp_impl:278]   gateway:  10.0.2.2
[  0.107306 0 axruntime:141] Initialize interrupt handlers...
 | TOPO[  0.107636 0 axruntime:147] Primary CPU 0 init OK.
Hello, ArceOS HTTP server!
LOGY | CONFIG_WCE | DISCARD | WRITE_ZEROES | NOTIFY_ON_EMPTY | RING_INDIRECT_DESC | RING_EVENT_IDX
listen on: http://[  0.108332 0 virtio_drivers::device::blk:64] config: 10.0.2.15:0xffff00000a003d00
[  0.108684 5555/
0 virtio_drivers::device::blk:69] found a block device of size 65536KB
[  0.109098 0 virtio_drivers::queue:383] Lagacy Size: 0x2000
[  0.109282 0 virtio_drivers::transport::mmio:397] Legacy
[  0.109390 INFO  hypervisor::hv::device_emu::virtio:218] legacy gpaddr 0x4012f000
[  0.109498 INFO  hypervisor::hv::device_emu::virtio:220] legacy gpaddr 0x4012f000 hpaddr 0x485f3000
[  0.109594 INFO  hypervisor::hv::device_emu::virtio:229] Write 0's pfn
[  0.110114 0 axdriver::virtio:88] created a new Block device: "virtio-blk"
[  0.110860 0 axfs:25] Initialize filesystems...
[  0.110964 0 axfs:26]   use block device: "virtio-blk"
[  0.121016 0 fatfs::dir:140] Is a directory
[  0.125144 0 axruntime:141] Initialize interrupt handlers...
[  0.125622 0 axruntime:147] Primary CPU 1 init OK.
Available commands:
  cat
  cd
  echo
  exit
  help
  ls
  mkdir
  pwd
  rm
  uname
arceos:/$
