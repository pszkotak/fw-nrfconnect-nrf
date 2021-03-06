.. _thread_ot_memory:

OpenThread memory requirements
##############################

This page provides information about the layout and the amount of Flash and RAM memory required by the sample using the OpenThread stack.
These values are useful to see whether your application has enough space for running on paricular platforms in different OpenThread configurations.


Flash and RAM requirements for nRF52840 and nRF52833
****************************************************

The following tables list flash memory and RAM requirements for the provided samples built using the OpenThread libraries.
The values change depending on the application and hardware platform.

The values in the tables are provided for the CLI example, which works with all OpenThread calls.
For this reason, these values are the best approximation of the memory requirements.

Samples were compiled with the default :file: `prj.conf`, MTD variant of the CoAP Client has been compiled with the :file: `overlay-mtd.conf`.
Below options were used to enable the multiprotocol in chosen configurations:

:option:`CONFIG_MPSL=y`
:option:`CONFIG_BT_LL_SOFTDEVICE_DEFAULT=y`
:option:`CONFIG_BT=y`
:option:`CONFIG_BT_SMP=y`
:option:`CONFIG_BT_PERIPHERAL=y`
:option:`CONFIG_BT_DEVICE_NAME="NUS_CoAP_client"`
:option:`CONFIG_BT_DEVICE_APPEARANCE=833`
:option:`CONFIG_BT_MAX_CONN=1`
:option:`CONFIG_BT_MAX_PAIRED=1`
:option:`CONFIG_BT_GATT_NUS=y`
:option:`CONFIG_BT_SETTINGS=y`


nRF52840 RAM and Flash memory requirements
==========================================

The following table presents memory requrements for samples running on the nRF52840 SoC with the hardware cryptography support provided by the CC310.
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Role       | Sample      | Multiprotocol   |   ROM OT Stack + App [KB] |   ROM BLE Stack [KB] |   Peristent storage [KB] |   RAM OT Stack + App [KB] |   RAM BLE Stack [KB] |   Total ROM [KB] |   Total RAM [KB] |
+============+=============+=================+===========================+======================+==========================+===========================+======================+==================+==================+
| Router     | CLI         | No              |                       470 |                    0 |                       32 |                        90 |                    0 |              502 |               90 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | CLI         | Yes             |                       598 |                  128 |                       32 |                        90 |                   17 |              758 |              107 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | NCP         | No              |                       430 |                    0 |                       32 |                        88 |                    0 |              462 |               88 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | NCP         | Yes             |                       557 |                  127 |                       32 |                        88 |                   17 |              716 |              105 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | CoAP Server | No              |                       306 |                    0 |                       32 |                        82 |                    0 |              338 |               82 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | CoAP Server | Yes             |                       434 |                  128 |                       32 |                        82 |                   17 |              594 |               99 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | CoAP Client | No              |                       314 |                    0 |                       32 |                        83 |                    0 |              346 |               83 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| Router     | CoAP Client | Yes             |                       458 |                  144 |                       32 |                        83 |                   23 |              634 |              106 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| End Device | CoAP Client | No              |                       254 |                    0 |                       32 |                        80 |                    0 |              286 |               80 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+
| End Device | CoAP Client | Yes             |                       399 |                  145 |                       32 |                        80 |                   23 |              576 |              103 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+------------------+------------------+


nRF52833 RAM and Flash memory requirements
==========================================

The following table presents memory requrements for samples running on the nRF52833 SoC with the software cryptography support provided by the nRF Oberon module.
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Role       | Sample      | Multiprotocol   |   ROM OT Stack + App [KB] |   ROM BLE Stack [KB] |   Peristent storage [KB] |   RAM OT Stack + App [KB] |   RAM BLE Stack [KB] | Total ROM [KB]    |   Total RAM [KB] |
+============+=============+=================+===========================+======================+==========================+===========================+======================+===================+==================+
| Router     | CLI         | No              |                       455 |                    0 |                       32 |                        97 |                    0 | 487               |               97 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | CLI         | Yes             |                       583 |                  128 |                       32 |                        97 |                   17 | 743 (exceeds ROM) |              114 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | NCP         | No              |                       416 |                    0 |                       32 |                        96 |                    0 | 448               |               96 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | NCP         | Yes             |                       543 |                  127 |                       32 |                        96 |                   17 | 702 (exceeds ROM) |              113 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | CoAP Server | No              |                       321 |                    0 |                       32 |                        89 |                    0 | 353               |               89 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | CoAP Server | Yes             |                       449 |                  128 |                       32 |                        89 |                   17 | 609 (exceeds ROM) |              106 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | CoAP Client | No              |                       330 |                    0 |                       32 |                        91 |                    0 | 362               |               91 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| Router     | CoAP Client | Yes             |                       474 |                  144 |                       32 |                        91 |                   22 | 650 (exceeds ROM) |              113 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| End Device | CoAP Client | No              |                       260 |                    0 |                       32 |                        88 |                    0 | 292               |               88 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
| End Device | CoAP Client | Yes             |                       404 |                  144 |                       32 |                        88 |                   22 | 580 (exceeds ROM) |              110 |
+------------+-------------+-----------------+---------------------------+----------------------+--------------------------+---------------------------+----------------------+-------------------+------------------+
