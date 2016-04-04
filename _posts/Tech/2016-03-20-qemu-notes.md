---
published: true
layout: post
title: QEMU代码分析
category: Tech 
tags: 
  - QEMU 
time: 2016.03.18 23:02:45
excerpt: NULL
---

## 函数调用关系

> cpu_exec <-- tcg_cpu_exec <-- tcg_exec_all <--  qemu_tcg_cpu_thread_fn <-- qemu_tcg_init_vcpu <-- qemu_init_vcpu <-- arm_cpu_realizefn
<-- arm_cpu_class_init 

## main函数之前调用的函数
在QEMU源码中,在main函数执行,通过C语言中constructor机制(![constructor])先执行了如下初始化函数

> qtest_type_init

> memory_register_types
 
> virtio_register_types
 
> exynos4210_uart_register
 
> digic_uart_register_types
 
> stm32f2xx_usart_register_types
 
> virtio_serial_register_types
 
> arm11mpcore_register_types
 
> realview_mpcore_register_types
 
> a9mp_register_types
 
> a15mp_register_types
 
> virtio_register_types
 
> virtio_gpu_pci_register_types
 
> pxa2xx_dma_register_types
 
> omap_gpio_register_types
 
> imx_gpio_register_types
 
> omap_i2c_register_types
 
> armv7m_nvic_register_types
 
> exynos4210_gic_register_types
 
> exynos4210_irq_gate_register_types
 
> exynos4210_combiner_register_types
 
> omap_intc_register_types
 
> aw_a10_register_types
 
> ivshmem_register_types
 
> arm_sysctl_register_types
 
> exynos4210_pmu_register
 
> imx_ccm_register_types
 
> mst_fpga_register_types
 
> zynq_slcr_register_types
 
> zynq_xadc_register_types
 
> stm32f2xx_syscfg_register_types
 
> pci_edu_register_types
 
> virtio_register_types
 
> pxa2xx_pcmcia_register_types
 
> virtio_register_types
 
> virtio_register_types
 
> exynos4210_mct_register_types
 
> exynos4210_pwm_register_types
 
> exynos4210_rtc_register_types
 
> pxa2xx_timer_register_types
 
> tusb6010_register_types
 
> digic_timer_register_type
 
> a10_register_types
 
> register_vfio_pci_dev_type
 
> register_vfio_platform_dev_type
 
> register_calxeda_xgmac_dev_type
 
> virtio_register_types
 
> virtio_register_types
 
> arm_linux_boot_register_types
 
> collie_machine_init_register_types
 
> exynos4_machines_init
 
> gumstix_machine_init
 
> highbank_regs_register_types
 
> calxeda_machines_init
 
> canon_a1100_machine_init_register_types
 
> integratorcp_machine_init_register_types
 
> integratorcp_register_types
 
> mainstone2_machine_init_register_types
 
> musicpal_machine_init_register_types
 
> musicpal_register_types
 
> nseries_machine_init
 
> sx1_machine_init
 
> palmte_machine_init_register_types
 
> realview_machine_init
 
> spitz_machine_init
 
> spitz_register_types
 
> stellaris_machine_init
 
> stellaris_register_types
 
> tosapda_machine_init_register_types
 
> tosa_register_types
 
> versatile_machine_init
 
> versatilepb_register_types
 
> vexpress_machine_init
 
> machvirt_machine_init
 
> zynq_machine_init_register_types
 
> z2_machine_init_register_types
 
> netduino2_machine_init_register_types
 
> armv7m_register_types
 
> pxa2xx_register_types
 
> pxa2xx_gpio_register_types
 
> pxa2xx_pic_register_types
 
> digic_register_types
 
> strongarm_register_types
 
> aw_a10_register_types
 
> cubieboard_machine_init_register_types
 
> stm32f205_soc_types
 
> fsl_imx25_register_types
 
> imx25_pdk_machine_init_register_types
 
> fsl_imx31_register_types
 
> kzm_machine_init_register_types
 
> arm_cpu_register_types
 
> iothread_register_types
 
> register_types
 
> qjson_register_types
 
> register_accel_types
 
> register_types
 
> register_types
 
> register_types
 
> register_types
 
> register_types
 
> register_types
 
> register_types
 
> register_types
 
> register_types
 
> fsdev_register_config
 
> register_types
 
> es1370_register_types
 
> ac97_register_types
 
> intel_hda_register_types
 
> hda_audio_register_types
 
> wm8750_register_types
 
> pl041_register_types
 
> mv88w8618_register_types
 
> m25p80_register_types
 
> nand_register_types
 
> pflash_cfi01_register_types
 
> pflash_cfi02_register_types
 
> onenand_register_types
 
> nvme_register_types
 
> ipoctal_register_types
 
> pl011_register_types
 
> serial_register_types
 
> serial_pci_register_types
 
> virtconsole_register_types
 
> cadence_uart_register_types
 
> imx_serial_register_types
 
> qdev_register_types
 
> fw_path_provider_register_types
 
> irq_register_types
 
> hotplug_handler_register_types
 
> nmi_register_types
 
> sysbus_register_types
 
> machine_register_types
 
> machine_none_machine_init_register_types
 
> platform_bus_register_types
 
> ads7846_register_types
 
> pl110_register_types
 
> ssd0303_register_types
 
> ssd03232_register_types
 
> vga_register_types
 
> exynos4210_fimd_register_types
 
> pl080_register_types
 
> pl330_register_types
 
> max7310_register_types
 
> pl061_register_types
 
> scoop_register_types
 
> i2c_slave_register_types
 
> smbus_device_register_types
 
> smbus_eeprom_register_types
 
> versatile_i2c_register_types
 
> bitbang_i2c_register_types
 
> exynos4210_i2c_register_types
 
> imx_i2c_register_types
 
> ide_register_types
 
> pci_ide_register_types
 
> microdrive_register_types
 
> sysbus_ahci_register_types
 
> ich_ahci_register_types
 
> lm832x_register_types
 
> pl050_register_types
 
> virtio_register_types
 
> virtio_register_types
 
> virtio_register_types
 
> pl190_register_types
 
> imx_avic_register_types
 
> realview_gic_register_types
 
> register_types
 
> arm_gic_register_types
 
> gicv2m_register_types
 
> register_types
 
> ipack_register_types
 
> tpci200_register_types
 
> isabus_register_types
 
> max111x_register_types
 
> tmp105_register_types
 
> pci_testdev_register_types
 
> l2x0_register_types
 
> intdbg_register_types
 
> a9mp_register_types
 
> arm11_scu_register_types
 
> ne2000_register_types
 
> eepro100_register_types
 
> pci_pcnet_register_types
 
> e1000_register_types
 
> rtl8139_register_types
 
> vmxnet3_register_types
 
> smc91c111_register_types
 
> lan9118_register_types
 
> xgmac_enet_register_types
 
> aw_emac_register_types
 
> imx_fec_register_types
 
> gem_register_types
 
> stellaris_enet_register_types
 
> rocker_register_types
 
> fw_cfg_register_types
 
> pci_bridge_dev_register
 
> pxb_register_types
 
> xio3130_upstream_register_types
 
> xio3130_downstream_register_types
 
> ioh3420_register_types
 
> d2pbr_register
 
> versatile_pci_register_types
 
> gpex_register
 
> pci_register_types
 
> pci_bridge_register_types
 
> pci_host_register_types
 
> pcie_host_register_types
 
> pcie_port_register_types
 
> pcmcia_register_types
 
> scsi_disk_register_types
 
> scsi_generic_register_types
 
> scsi_register_types
 
> lsi53c895a_register_types
 
> megasas_register_types
 
> pvscsi_register_types
 
> esp_register_types
 
> esp_pci_register_types
 
> pl181_register_types
 
> ssi_sd_register_types
 
> sdhci_register_types
 
> smbios_register_config
 
> pl022_register_types
 
> ssi_slave_register_types
 
> xilinx_spips_register_types
 
> arm_timer_register_types
 
> arm_mptimer_register_types
 
> a9_gtimer_register_types
 
> cadence_ttc_register_types
 
> ds1338_register_types
 
> pl031_register_types
 
> twl92230_register_types
 
> imx_epit_register_types
 
> imx_gpt_register_types
 
> stm32f2xx_timer_register_types
 
> tpm_passthrough_register
 
> usb_register_types
 
> uhci_register_types
 
> ohci_register_types
 
> ehci_pci_register_types
 
> ehci_sysbus_register_types
 
> xhci_register_types
 
> usb_hub_register_types
 
> usb_hid_register_types
 
> usb_wacom_register_types
 
> usb_msd_register_types
 
> usb_uas_register_types
 
> usb_audio_register_types
 
> usb_serial_register_types
 
> usb_net_register_types
 
> usb_bt_register_types
 
> ccid_register_types
 
> usb_mtp_register_types
 
> virtio_register_types
 
> virtio_pci_register_types
 
> virtio_register_types
 
> virtio_mmio_register_types
 
> i6300esb_register_types
 
> filter_dump_register_types
 
> register_types
 
> register_types
 
> cpu_register_types
 
> register_types
 
> vnc_register_config
 
> register_types
 
> container_register_types
 
> register_types
 
> bdrv_raw_init
 
> bdrv_qcow_init
 
> bdrv_vdi_init
 
> bdrv_vmdk_init
 
> bdrv_cloop_init
 
> bdrv_bochs_init
 
> bdrv_vpc_init
 
> bdrv_vvfat_init
 
> bdrv_qcow2_init
 
> bdrv_qed_init
 
> bdrv_quorum_init
 
> bdrv_parallels_init
 
> bdrv_blkdebug_init
 
> bdrv_blkverify_init
 
> bdrv_file_init
 
> bdrv_null_init
 
> throttle_groups_init
 
> bdrv_nbd_init
 
> bdrv_sheepdog_init
 
> bdrv_dmg_init
 
> qcrypto_tls_creds_register_types
 
> qcrypto_tls_creds_anon_register_types
 
> qcrypto_tls_creds_x509_register_types
 

