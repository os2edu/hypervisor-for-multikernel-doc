# 验证qemu上将ArceOS在Hypervisor上运行

1.  将所需文件Clone到本地
    
    ```shell
    git clone git@github.com:KarmaD7/rHyper.git
    ```

2.  编译运行
    
    ```shell
    # rHyper/hypervisor目录下
    make run LOG=info SMP=4 GUEST=arceos NET=y FS=y
    ```

    运行成功输出的Log信息

    ```shell
    qemu-system-aarch64 -nographic -m 1G -cpu cortex-a72 -machine type=virt,virtualization=on,iommu=smmuv3 -kernel target/aarch64/release/hypervisor.bin -smp 4 -device loader,addr=0x4001000,file=../bin/arceos-httpserver-single.bin,force-raw=on -device loader,addr=0x4101000,file=../bin/arceos-shell.bin,force-raw=on -device loader,addr=0x4201000,file=../bin/arceos-parallel-dual.bin,force-raw=on -device virtio-net-device,netdev=net0 -netdev user,id=net0,hostfwd=tcp::5555-:5555 -device virtio-blk-device,drive=disk0 -drive id=disk0,if=none,format=raw,file=../bin/disk.img


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
    [  0.241695 INFO  hypervisor:108] Initialization completed.

    [  0.242107 INFO  hypervisor::platform::qemu_virt_arm::psci:19] trying to start cpu 1.
    [  0.242271 INFO  hypervisor::platform::qemu_virt_arm::psci:21] cpu 1 started.
    [  0.242600 INFO  hypervisor::platform::qemu_virt_arm::psci:19] trying to start cpu 2.
    [  0.243114 INFO  hypervisor:119] Hello World from cpu 1
    [  0.243132 INFO  hypervisor::platform::qemu_virt_arm::psci:21] cpu 2 started.
    [  0.244016 INFO  hypervisor:119] Hello World from cpu 2
    [  0.243781 INFO  hypervisor:125] secondary cpu 1 will run a vcpu with entry 0x40080000
    [  0.244217 INFO  hypervisor:125] secondary cpu 2 will run a vcpu with entry 0x40080000
    [  0.244136 INFO  hypervisor::platform::qemu_virt_arm::psci:19] trying to start cpu 3.
    [  0.244639 INFO  hypervisor::platform::qemu_virt_arm::psci:21] cpu 3 started.
    Starting virtualization...
    Starting virtualization...
    [  0.245571 INFO  hypervisor:119] Hello World from cpu 3
    Starting virtualization...
    Hardware support: true
    Hardware support: true
    Hardware support: true
    [  0.247006 INFO  hypervisor::hv:140] mapping
    [  0.264022 INFO  hypervisor::hv:140] mapping
    [  0.264519 INFO  hypervisor::hv:140] mapping
    [  0.264535 INFO  hypervisor::hv:163] run vcpuid 0
    [  0.264758 INFO  rvm::arch::aarch64::vcpu:50] npt root is 604cd000.
    [  0.264993 INFO  rvm::arch::aarch64::vcpu:52] [RVM] created ArmVcpu
    Running guest...
    [  0.281264 INFO  hypervisor::hv:140] mapping
    [  0.281425 INFO  hypervisor::hv:163] run vcpuid 0
    [  0.281431 INFO  hypervisor::hv:140] mapping
    [  0.281548 INFO  rvm::arch::aarch64::vcpu:50] npt root is 604ce000.
    [  0.281709 INFO  rvm::arch::aarch64::ept:137] Real flags VALID | NON_BLOCK | ATTR | S2AP_R | S2AP_W | INNER | SHAREABLE | AF
    [  0.281823 INFO  rvm::arch::aarch64::vcpu:52] [RVM] created ArmVcpu
    Running guest...
    [  0.298319 INFO  hypervisor::hv:140] mapping
    [  0.298474 INFO  hypervisor::hv:163] run vcpuid 0
    [  0.298575 INFO  rvm::arch::aarch64::vcpu:50] npt root is 604cf000.
    [  0.298823 INFO  rvm::arch::aarch64::vcpu:52] [RVM] created ArmVcpu
    Running guest...


    d 8d     
    8888 8     8         d  8  8  8 8                                                       .     d8  .8  d88 888 8 8b8  b.. .  d8  8 .d.d8888888b88.88b b. .
    .
    88  8  8  8  8   db8.d8
    PY8 88 8           d     8   8  88  8                                            d8  d 88 8PP" "    "" YY8 88 b8  db 8 8 P d  8  Y 8d8P88 b8
    8 " b  
        8Y  8 88Pdb88 88d 888 PP8 8  8  Y 8  8  b  
    8              d  8   8P  8    8  8                      8 8 8 8 8 8             88  88 8  8Y 8 8 b .Y
    .  
    .  d 8 88P88  8 d 888 P8    888888 8d88888888d  8 8Y.88 8 db8.
    b.888  88b 8 b d  8.8 P. dd88888b8b8 ..  8  888d888888  8   8    8   888. d 8888" Y 8"88Y8b88 b8 .8
    8  b
    .   d d 888888P 8  8P88    8 88888 P  "888  888  Pd "88" PY"  88  d8  b88.dP8"
    "88b    Y d8d8bP8   88Y88P8b    8 8  888 8  8 888 8  8 P 88 " 8      d"Y8 88  8"bPY.
    d d  
    88 8PP    dY 8 88b8P8   8888   8 8 8 888   888 888         8 8  8 8"8 Y 8 8   8b   8 .8 8 
    8 8 8d8888888 P888   888  888 88       8 8 88888   88             8   8"8"8888 8
    8  
    8 8 88d8888888888888888888 88 88888888 88  8  8         8Y8 88 8   bY88.b  .        "Y 8 88bY8.
    b d  .88 8 8  Y88 88  8bY.8 888b.d8.8  .8P8 dY88888Pb8    Yd888  8P 
    Y8 d88d8b8.P8  P    
    Y d Y888b888P .  8 8   8     Y   8888 8b ."Y  88.888d8 88  P8   P   Y""YY888888b8 8 88d P 8 8  P""
    dY8888888P8 8  8P  "     8"8 "8Y Y88888888888 P8 P" " 
    88 " Y"Y8
    8888P8  P"Y"
    r a8  
    cY88h 8= 88aPa"a r r cc"hh64Y 8=
    rfochrlaa"t
    = m 
    -emaut-vfirotrm- aaa=rrc cqhhe m64=u 
    ahrimraprt =- 2ac
    il6duh
    _mp
    adelma pt f=o =rr e1mle
    =s bueqi
    ellodg_mmu_ol-vdeie =rvelt  r-e=a alricehn6faso4

    l

    l pog_ =l eve1
    mbui linfdo_
    e 
    = release
    log_level =info

    xru[ 03371m2852 axruntim e:[ 97] 0.Logging is ena3 b130le6d2 . [m0 a
    ntmime:97]3 1[233237 mL[og0 g  i0ngax. 3ru1n4is0t 8ei2mne a:axbr9luen7dt]i m.e[9[28m] m
    0 dt[ ma xr= untime:98] 332m07mxP0[r i.mar[my.3 
    a1P5[ 20m9 9s ta0r t[adx,r u3d7tmnt[ib   me0=:. 31985656] a xrun03ix20mm.Per:m[m
    xe[0ym]  [P3U m[F03ou 7snmd pt[ahr ytscei 0.da,l3  m1d6tebm2o 2r8= y  r0 axergionus:ti[m0m
    1.[m
    1x0ru32mFoundphy3c[73i7mma[[l    m0. e03m.o31ry169 66re972gi9 aox rnun0s :tie:a[m
    ( []mm e: 10 0[] A32m:o0u[x37n4md[0 0p 8h 00.y030s0c17i,6 5a9lP  A0me :a0xmorrxuynt4 0i0mre90e0:10g00)io2 .n] st:e2mt[m 
    xPA:0x4008REA00D00,  |PA 0x[43E0X7E0mC[Ua8T E0 0 00.|) 3R E1.SEtRe8Vx5tED50 ( )0ma
    03[EAmDnti |[e: 3107E2Xm] [E  U[0.T32Em 3 1|90  R[3E3 axPrSuAERnV:tEime0xD:410)0028][ 0[
    D)PA : 0P3Ax47:00m0[x9 4 00f000.90)0310 90.t60e5x7t,  0 ( PaxAr:0uxntim4Re0E:1002A9D]400  |0 rod3E2aXEmt  aC[UPTA E :(|0x RR4EESA00DER a|VE 8R0DES0)0E,PV[AE:m0
    xm0[bm6
    [3[7mm0[ r03od7a.m[t3a2 0  07(.83R20E1A8 D870   a|xa xrrRuuEnntSEiRmVteEi:Dm)e1:102][2 m
    [32mm[  m  [3PPA7mA:0:x[ 040x0 490040.0390f2001,0 056P,9A : PA00 x:a04xx0r409u07n00t00a6) im00.ed0:)at a10. r2(oR]dE aA
    D,)                                                                                                                    t[ 3|2 mWa  R I([TREP EA|: AR0DES xE|4R 0VREE0SDb)E6R0mE0
    0x bmm90[ [ 030.)7 3m.d[2a2 8t 0a90  a(.xRr3EA2Du2 n9t|0 2i WRme0I: a1Tx0rE u2]n|t  iRe[E:3S10ER22V]mE D [2Am:m
    4[[0m9E([3R 2|mE RA DE  SE[|RVPE AWDR:I)0T[4mE
    a[0 mRbE90[03E70m,R[ VP E A0D:.3)247[6x4m1 0
    0mriverse7vim[c  [0:3.:7bm35l[k14 :9769  ]0  0i335r21mtf5oiu7o7n_d d raax irbvulernotsc:ik md:deeve:i:vcemi pcofe:3 :s7i:]zn e t[:3126m1Se557c3o]n6 KB[[r3my2
    tmD[mePvU 1i cinite OK [.[ema7m m|b,. t 3Pst2A:5a90cx4k46 0 (0Ra0a0 EaA0D xr0u|)n .t pimWeRreI:c1TEpu 0|2  ](R ER
    G_[e ms  0.352840 0 CvTRirtL_ioG_dUrESivT_eOFrFLs::OAquDSeue: | 383] MC[33m Laga| cyG SSizOe: 0x20 0|0mMR                   m
    m GUEST_ANNOUN[  0.354788 INFO  hypervisor::hv::device_emu::virtio:234] legacy gpaddr 0x4012f000 :3C9T7] R[33_mRXLe_gEacyXTR
    [  0.355090 INFO  hypervisor::hv::device_emu::virtio:236] legacy gpaddr 0x4012f000 hpaddr 0x485d9000o02Rt VE]sDt) [2mkm
    [  0.355288 INFO  hypervisor::hv::device_emu::virtio:245] Write 0's pfnm0e
    CE | CTL_MAC_ADDR | RING_INDIRECT_DESC | RING_EVENT_IDX00 0 0R0E0,  SaEPRVxAE:Dr)u0[n9tm0i
    [  0.3560240 37axdrmi[ve r 0:.3:5v611i9r 0t viior:tio88]_ d[i3v2emrcsre::ateqd ueaue ne:w 383] Bl3ck 3dmLeviacgaec:y  Size": 0x2000
    19rti[-3blk7m[ "[.357m0R00I  00TE0.3,31  |P36 A:3R 0EaxS9ExR0r0Vu10Ent0iDm)0)e[ m10mm
    0 [irtimo_drivers::transport::mmio:397] Legacy
    [  0.357609 INFO  hypervisor::hv::device_emu::virtio:234] legacy gpaddr 0x40410000R0Vun0E0Dt)) im[mem
    [  0.357776 INFO  hypervisor::hv::device_emu::virtio:236] legacy gpaddr 0x40410000 hpaddr 0x408ba000
    [  0.357996 INFO  hypervisor::hv::device_emu::virtio:245] Write 1's pfn                            )0[0)2[ mm m
    [  0.357703 0 axfs:25] 37Initmiali[z e  0.35fil8e4sy3s8 0te mvs..irti.o_:0 1200|2 0]0RE0S )E mVEm[D3io2)m(m R
    drvmers::queue38[33]7m[   3589L37 a0 gaaxcy fs:Siz26]e 0x 200 u0s bmlocrVoEu D)(REmtAD
    k dvice[m: "i37mrtio[ -blk 0."3[m9484
    0[imrtio_drivers::transport::mmio:397] LegacyrExuRVn8tE0Di0m0)e[m100
    [  0.360580 INFO  hypervisor::hv::device_emu::virtio:234] legacy gpaddr 0x40412000Rim0I)e:T 1Em m|0i2o ] D( 
    [  0.360734 INFO  hypervisor::hv::device_emu::virtio:236] legacy gpaddr 0x40412000 hpaddr 0x408bc000
    [  0.360879 INFO  hypervisor::hv::device_emu::virtio:245] Write 0's pfn
    [  0.361878 0 axdriver::virtio:88] created a new Net device: "virtio-net"                                                 [[m307
    [  0.362919 0 axnet:22] Initialize network subsystem... | 0im eWaRx:I1rTu0E n2t|] im FeREE[312)m[2m] 
    [  0.363466 0 axnet:24] number of NICs: 1x.13a3f7800075400 0a,0x0ru P)nA tmimi:m0oex: 141(38]0R 0EA0D0|30 02)mWR IniItfTiraEel ieze | m DEVgelmIoroCbyEa  |l ( RRmESeEmAEDorRy V| E aD)lWoR[Icm
    [  0.363889 0 axnet:27]   NIC 0: "virtio-net"
    [  0.365541 0 axnet::smoltcp_impl:273] created net interface "eth0":
    [  0.366254 0 axnet::smoltcp_impl:275]   ether:    52-54-00-12-34-56
    [  0.367054 0 axnet::smoltcp_impl:277]   ip:       10.0.2.15/24:0,1 13PA]:0 480[003020m0I)n itfiarele imze egmolroy ba(lR EmAemoD r| Wy alRloIcaTE t|o r.F.RE.E)
    [  0.367636 0 axnet::smoltcp_impl:278]   gateway:  10.0.2.2
    [  0.368245 0 axruntime:141] Int3i7aml[iz  0e. in36871t6 0e rrfautpfs:t: diharndle:r14s0.]. [31m
    I[ am directory
    [  0.369576 0 axruntime:147] Primary CPU 0 init OK.ge table...
    Hello, ArceOS HTTP server!:1[19  ] 0.[4328240m Inaxittask:i:aapliiz:1e 8k]e rn3l pm[aIng37eim t[iat al b0iz.el 3e4.s3.2c7.he
    listen on: http://10.0.2.15:5555/
    [  0.372049 0 axruntime:141] Initialize interrupt handlers...
    [  0.372756 0 axruntime:147] Primary CPU 0 init OK..3] [324622m deavx[cte3a sf7kea::tma[upri e: 2s:0 4.]3 44E8[5G3_32MA m X0 u s ea|  xtGFaIsEkOF:OME: TasRpcYih: 1|ed8 ]u lLer[K.3Ei[tmi al|i 3Se7CSm Isc[ h  e0|d. u3liF45n7gLUAvailable commands:
    cat32mICOnitNiFaIGli_WzCe Eint e|r ruptDIS CAhRanDdl e|rs ...WRI
    cd	N[G_IN37DImR[E C 0T_.D3E
    echo                          437m7[ 0C 0.347255 INFO  2 hypervisor::hv::vmexit:23] 5VM exit: VMCALL(|0x84000003):   0[ RaINGx_EtVask:1ENT_:, aIpiD:2X4] 2]m[ 
    exit347860 WARN  hypervisor::hv::vmexit:
    helpuest call psci on
    ls 0.348091 INFO  hypervisor::hv::vmexit:37] pcpuid 3, entry gpa 4008005c
    mkdirm0.348246 INFO O hypervisor:[125]  secondary cpu 33 will run a vcpu with entry 0xs4008005c7
    pwdrting virtualization...
    rmrdware support:  true
    uname48730u1l mea[xrru .nt[m0m.
    arceos:/$ [12010;1x^[2;1;1;0xpart 0: TaskId(5) [0, 125000)  0.349332 mINFO 3r
    part 1: TaskId(6) [125000, 250000)
    part 2: TaskId(7) [250000, 375000)rch64::vcpu: 50d] npt root is 604cd000e.
    part 3: TaskId(8) [375000, 500000)rch64::vcpu:d52i] [RVM] created ArmVcpuc
    part 4: TaskId(9) [500000, 625000)
    part 5: TaskId(10) [625000, 750000)[ig a:li  0z.3e5 0d0evx24ffic1fe  dfa0x0rru0i0vn0eati0rm0s3.e.d.0:0:mp2m[9
    part 6: TaskId(11) [750000, 875000)
    part 7: TaskId(12) [875000, 1000000)7a0r ted0. vr[tmi
    part 8: TaskId(13) [1000000, 1125000)
    part 9: TaskId(14) [1125000, 1250000)
    part 10: TaskId(15) [1250000, 1375000)
    part 11: TaskId(16) [1375000, 1500000)
    part 12: TaskId(17) [1500000, 1625000)
    part 13: TaskId(18) [1625000, 1750000)
    part 14: TaskId(19) [1750000, 1875000)
    part 15: TaskId(20) [1875000, 2000000)
    part 15: TaskId(20) finished
    part 0: TaskId(5) finished
    part 1: TaskId(6) finished
    part 2: TaskId(7) finished
    part 3: TaskId(8) finished
    part 4: TaskId(9) finished
    part 5: TaskId(10) finished
    part 6: TaskId(11) finished
    part 7: TaskId(12) finished
    part 8: TaskId(13) finished
    part 9: TaskId(14) finished
    part 10: TaskId(15) finished
    part 11: TaskId(16) finished
    part 12: TaskId(17) finished
    part 13: TaskId(18) finished
    part 14: TaskId(19) finished
    main task woken up! timeout=false
    sum = 61783189038
    Parallel summation tests run OK!
    [  1.170312 0:2 axhal::platform::qemu_virt_aarch64::psci:25] Shutting down...
    [  1.170985 INFO  hypervisor::hv::vmexit:23] VM exit: VMCALL(0x84000008): [0, 0, 0, 0]
    ```

3.  如果上一步成功，此时运行`ArceOS`的终端/`tmux`的窗口中可以输入`ArceOS`支持的命令
    
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