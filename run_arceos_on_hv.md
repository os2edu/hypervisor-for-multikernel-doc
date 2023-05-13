# 验证qemu上将ArceOS在Hypervisor上运行

1.  将所需文件Clone到本地
    
    ```shell
    git clone git@github.com:KarmaD7/rHyper.git
    ```

2.  编译运行
    
    ```shell
    # rHyper/hypervisor目录下
    make run LOG=info SMP=2 GUEST=arceos NET=y FS=y
    ```

    运行成功输出的Log信息

    ```shell
        qemu-system-aarch64 -nographic -m 1G -cpu cortex-a72 -machine type=virt,virtualization=on,iommu=smmuv3 -kernel target/aarch64/release/hypervisor.bin -smp 2 -device loader,addr=0x4001000,file=../bin/arceos-httpserver-single.bin,force-raw=on -device loader,addr=0x4101000,file=../bin/arceos-shell.bin,force-raw=on -device loader,addr=0x4201000,file=../bin/arceos-parallel-dual.bin,force-raw=on -device virtio-net-device,netdev=net0 -netdev user,id=net0,hostfwd=tcp::5555-:5555 -device virtio-blk-device,drive=disk0 -drive id=disk0,if=none,format=raw,file=../bin/disk.img


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
    boot stack: 0x40099000, boot stack top: 0x400a9000
    arch = aarch64
    build_mode = release
    log_level = info

    Initializing heap at: [0x400a9000, 0x404a9000)
    [INFO  hypervisor:103] Logging is enabled.
    Initializing frame allocator at: [0x604cd000, 0x80000000)
    [  0.243706 INFO  hypervisor:108] Initialization completed.

    [  0.244122 INFO  hypervisor::platform::qemu_virt_arm::psci:19] trying to start cpu 1.
    [  0.244317 INFO  hypervisor::platform::qemu_virt_arm::psci:21] cpu 1 started.
    [  0.244552 INFO  hypervisor::platform::qemu_virt_arm::psci:19] trying to start cpu 2.
    [  0.245035 INFO  hypervisor:119] Hello World from cpu 1
    [  0.245099 ERROR hypervisor::lang_items:5] panicked at 'assertion failed: `(left == right)`
    left: `18446744073709551614`,
    right: `0`', src/platform/qemu_virt_arm/psci.rs:20:5
    [  0.245183 INFO  hypervisor:125] secondary cpu 1 will run a vcpu with entry 0x40080000
    Starting virtualization...
    Hardware support: true
    [  0.246813 INFO  hypervisor::hv:140] mapping
    [  0.263447 INFO  hypervisor::hv:140] mapping
    [  0.263942 INFO  hypervisor::hv:163] run vcpuid 0
    [  0.264081 INFO  rvm::arch::aarch64::vcpu:50] npt root is 604cd000.
    [  0.264429 INFO  rvm::arch::aarch64::vcpu:52] [RVM] created ArmVcpu
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

    [  0.270037 0 axruntime:97] Logging is enabled.
    [  0.271016 0 axruntime:98] Primary CPU 0 started, dtb = 0x0.
    [  0.271497 0 axruntime:100] Found physcial memory regions:
    [  0.272048 0 axruntime:102]   [PA:0x40080000, PA:0x400a8000) .text (READ | EXECUTE | RESERVED)
    [  0.272712 0 axruntime:102]   [PA:0x400a8000, PA:0x400b6000) .rodata (READ | RESERVED)
    [  0.273189 0 axruntime:102]   [PA:0x400b6000, PA:0x400b9000) .data (READ | WRITE | RESERVED)
    [  0.273692 0 axruntime:102]   [PA:0x400b9000, PA:0x400ba000) .percpu (READ | WRITE | RESERVED)
    [  0.274203 0 axruntime:102]   [PA:0x400ba000, PA:0x400fa000) boot stack (READ | WRITE | RESERVED)
    [  0.274866 0 axruntime:102]   [PA:0x400fa000, PA:0x4011f000) .bss (READ | WRITE | RESERVED)
    [  0.275377 0 axruntime:102]   [PA:0x9000000, PA:0x9001000) mmio (READ | WRITE | DEVICE | RESERVED)
    [  0.275902 0 axruntime:102]   [PA:0x8000000, PA:0x8020000) mmio (READ | WRITE | DEVICE | RESERVED)
    [  0.276444 0 axruntime:102]   [PA:0xa000000, PA:0xa004000) mmio (READ | WRITE | DEVICE | RESERVED)
    [  0.276986 0 axruntime:102]   [PA:0x4011f000, PA:0x48000000) free memory (READ | WRITE | FREE)
    [  0.277528 0 axruntime:113] Initialize global memory allocator...
    [  0.278843 0 axruntime:119] Initialize kernel page table...
    [  0.280300 0 axdriver:66] Initialize device drivers...
    [  0.280967 0 virtio_drivers::device::blk:55] device features: SEG_MAX | GEOMETRY | BLK_SIZE | SCSI | FLUSH | TOPOLOGY | CONFIG_WCE | DISCARD | WRITE_ZEROES | NOTIFY_ON_EMPTY | RING_INDIRECT_DESC | RING_EVENT_IDX
    [  0.282334 0 virtio_drivers::device::blk:64] config: 0xffff00000a003d00
    [  0.282890 0 virtio_drivers::device::blk:69] found a block device of size 65536KB
    [  0.283524 0 virtio_drivers::queue:383] Lagacy Size: 0x2000
    [  0.283976 0 virtio_drivers::transport::mmio:397] Legacy
    [  0.284515 INFO  hypervisor::hv::device_emu::virtio:234] legacy gpaddr 0x4012f000
    [  0.284807 INFO  hypervisor::hv::device_emu::virtio:236] legacy gpaddr 0x4012f000 hpaddr 0x485d9000
    [  0.284986 INFO  hypervisor::hv::device_emu::virtio:245] Write 0's pfn
    [  0.285669 0 axdriver::virtio:88] created a new Block device: "virtio-blk"
    [  0.286650 0 axfs:25] Initialize filesystems...
    [  0.286995 0 axfs:26]   use block device: "virtio-blk"
    [  0.294128 0 fatfs::dir:140] Is a directory
    [  0.296420 0 axruntime:141] Initialize interrupt handlers...
    [  0.297034 0 axruntime:147] Primary CPU 0 init OK.
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
    ```

3.  如果上一步成功，此时运行`ArceOS`的终端/`tmux`的窗口应显示进入`ArceOS`的终端,测试相关命令
    
    ```shell
    ls
    cd dev
    ...
    ```

    正常显示则说明验证成功。

---

注意:
  1.    在进行第二步编译运行的时候，请确保你的环境变量`PATH`中已经添加了`(your_path)/qemu/build`
  2.    如果提示找不到`qemu_system_$(ARCH)`如`qemu_system_aarch64`，请确保你的`qemu`编译时使用了你选择的架构所对应的参数