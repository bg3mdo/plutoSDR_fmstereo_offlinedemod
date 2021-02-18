# plutoSDR_fmstereo_offlinedemod
PlutoSDR GNURadio WFM stereo demodulation, and using PlutoSDR as standalone radio with customised firmware
\
\
If you have a new uboot (v0.32 firmware), you will use following command to wide banded your pluto:
\
\
fw_setenv compatible ad9364
fw_setenv maxcpus
\
\
REBOOT
\
\
'maxcpus' enable dual ARM cores, by default, only one ARM core is used for saving power.
\
\
For old uboot(firmware), you the following commands:
\
\
fw_setenv attr_name compatible
fw_setenv attr_val "ad9364"
fw_setenv maxcpus
\
\
REBOOT
\
\
'gnuradio_fmstereo' contains 3 GNURadio flow charts for demod FM stereo. 
\
\
stereo_wbfm_rx_1: sync mode
stereo_wbfm_rx_2: sampling mode
stereo_wbfm_rx_combine: combine two mode together.
\
\
'pluto_fm_demod_fw' contains a plutoSDR firmware for testing plutosdr standalone FM demodulation.
\
\
Using the following commands for testing:
\
\
rx_fm -f 105.6M -M wbfm -s 250k -r 48k -A std -l 0 -E deemp -g 73 | aplay -r 48000 -f S16_LE &
\
\
or:
\
\
rx_sdr  -F CF32 -s 2400000 -f 105600000 -g 73 -  | csdr fir_decimate_cc 10 0.05 HAMMING | csdr fmdemod_quadri_cf | csdr fractional_decimator_ff 5  | csdr deemphasis_wfm_ff 48000 50e-6 | csdr convert_f_i16 | aplay -r 48000 -f S16_LE
\
\
\
\
By Quanquan-BG3MDO 16/02/2021
